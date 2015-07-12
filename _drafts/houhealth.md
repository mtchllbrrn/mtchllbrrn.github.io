---
layout: post
title: "Dev Rundown: HouHealth"
---
###Intro
[HouHealth](http://houhealth.com) makes it easy to browse Houston's restaurants' health code violations. The site was built with Rails and deployed to a Digital Ocean droplet via Docker. This post assumes some basic knowledge of Rails, and focuses on the bits that make the development of this app unique.

I happened upon this data on [Houston's Open Data Portal](http://data.ohouston.org) during a local civic hackathon. As a Houstonite, there's an unspoken law that I dig good food, so I was excited to check out the health code compliance of my favorite restaurants. However, the experience of browsing this ginormous .xlsx was painful (~100,000 records!), to say the least. Google Drive could hardly load the entire thing. I created HouHealth as a more accessible interface to this data for the everyday user.

###Overview
The brunt of the work behind HouHealth involves massaging the datasets into appropriate Rails models. The .xlsx is presented in a per-violation manner: Each row of the .xlsx represents a distinct violation. Each violation includes the restaurant's account number, name, inspection date, and a description of the violation (plus a few other fields that aren't as relevant to our needs). In Rails terms, it makes the most sense to organize this data into a Restaurants model and a Violations model. That is, each Restaurant `has_many` Violations, and each Violation `belongs_to` a Restaurant. This allows us to easily search for a restaurant of interest and to retrieve all of the violations associated with that restaurant.

The first step of the process is to convert the .xlsx into a more friendly format. CSV to the rescue! It's plain text, perfect for parsing into something more useful. I used a combination of [Zamzar](http://www.zamzar.com/convert/xlsx-to-csv/) and [Guerilla Mail](http://guerillamail.com) to convert the dataset without giving up any email information. That might seem roundabout, but I prefer not to download one-off programs (like a file converter) if I can help it.

###Populating the Models
Once we've created our Restaurant model, we need to populate it with the appropriate entries from the dataset. A Rake task is the perfect candidate for the job:

```ruby
require 'csv'
task :generate_restaurant_entries_fy14 => :environment do
  csv_text = File.read('db/data/by-violation/fy14-violations.csv')
  csv = CSV.parse(csv_text, :headers => true)
  csv.each do |row|
    account_number = row[0]
    if !(Restaurant.exists? account_number: account_number)
      Restaurant.create(account_number: row[0],
                        facility_name: row[1],
                        facility_type: row[3],
                        address: row[7],
                        number_of_employees: row[14])
    end
  end
end
```

Remember, we're attempting to create the entries for our Restaurant model, but each entry in the dataset is a single violation. The solution is simple enough: For each violation entry in the dataset, check to see if its Restaurant exists in our model. If it doesn't, create it. Running the above task with `rake generate_restaurant_entries_fy14` populates our Restaurant model with all of the appropriate entries.

Next up is the Violation model. This is a more natural model to populate, seeing as the dataset maps one-to-one with the model. Here's the Rake task:

```ruby
require 'csv'
task :generate_violation_entries_fy14 => :environment do
  csv_text = File.open('db/data/by-violation/fy14-violations.csv', "r:ISO-8859-1")
  csv = CSV.parse(csv_text, :headers => true)
  csv.each do |row|
    Violation.create(restaurant_id: row[0],
                     risk: row[2],
                     date: DateTime.strptime(row[4], '%m/%d/%Y'),
                     inspector: row[5],
                     site_name: row[6],
                     code: row[8],
                     weight: row[9],
                     comment: row[10],
                     correct_by: row[11],
                     score: row[12])
  end
end
```

###Display
With our models created and their entries populated, all that's left is to display them on the site. The only remaining bit of trickery is to group the violations on each restaurant's page in some meaningful way. Each restaurant is inspected a couple times each year, and each inspection generates multiple violations. It makes sense to group the violations according to their inspection date:

```erb
<dl class="dl-horizontal">
  <% @restaurant.violations.group_by(&:date).each do |date, violations| %>
    <div class="well">
      <h5><%= date.strftime("%B %e, %Y") %></h5>
      <% violations.each do |v| %>
        <dt><%= v.code %></dt>
        <dd><%= v.comment %></dd>
      <% end %>
    </div>
  <% end %>
</dl>
```

###Deployment
