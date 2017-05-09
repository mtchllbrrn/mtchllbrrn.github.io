---
layout: post
title: "Gratuitous macOS Stack-Hacking"
permalink: /stack-hacking-core
---

*To my coworkers and friends who have expressed interest in this article:
I'm sorry it's taken so long!*

# Introduction

Like most developers, I customize my environment for the sake of
productivity, fluency, and pure enjoyment.  At its best, working in my
environment feels like playing an instrument: My thoughts flow directly
through my fingers, never pausing to think of *how*, only *what*.  It's
something like achieving a state of constant musical improvisation.

Vim enthusiasts can relate.  Proficiency with The One True Editor is
a constantly empowering experience.  Unfortunately, this empowerment ends
at the editor, leaving the developer hobbled everywhere else; especially
when s/he is forced to reach for a trackpad or mouse. I started
stack-hacking because I wanted to achieve vim-like fluency in *all* layers
of my development environment.

What I've come to is a somewhat monstrous, layered set of customizations,
due in part to the limitations Apple places on its OS.  In addition, it
changes constantly depending on my needs and new discoveries.  Despite all
of this, it has made me significantly more productive.

This article will cover only what I consider the "core" of my stack. These
apps offer functionality that is so useful that I would recommend it to
*any* dev, regardless of their particular needs: simple
app-switching/launching, window resizing, and universal vim-like text
navigation. 

Many of my configurations are based on existing work from other
developers.  I'll link to relevant articles for installation instructions,
rather than re-hash the individual steps myself.

## Disclaimer

I don't believe you should read this article with the intention of copying
my configuration wholesale.  Instead, I suggest reading it as a source of
ideas and as a recommendation for tools that I find useful.  If these
ideas sound interesting, I suggest implementing them one-by-one, slowly,
so as to come to grips with each before moving on to the next.

I call my configuration "gratuitous" for a reason.  If you're not careful,
it's easy to fall off the deep end.

# Core Concepts

## Contextless Bindings

Our most common tasks should be invoked with a single keystroke that works
regardless of our current context.  For instance, if we're switching
between iTerm and Slack, we shouldn't have to command-tab, visually find
the desired app, and tab over `n` times.  Instead, we prefer a single
keystroke each for invoking iTerm & Slack that works regardless of which
app we currently have focused, even if the app isn't open.  This concept
applies to everything from app focusing, text navigation, window
splitting, etc.

## Home Row is Home

Home row is where we are most comfortable, and our environment should
reflect this.  The corollary is, "STAY ON THE KEYBOARD."  Each
configuration should keep us there, and our choice of keystrokes should be
informed both by how frequently we invoke that operation and by its
location on the keyboard: Frequent operations should already be under your
fingers, not across the keyboard.

## Division of Labor & Maintainability

As we configure our environment, we continually integrate additional
apps/tools, and for any given feature, it might be possible to implement
it in multiple tools. As such, we run the risk of creating the stack
equivalent of spaghetti code:  "My system-wide vim bindings aren't
working, but I can't remember which tool implements them!" It becomes
important to devise a mental model for the division of labor among these
tools, allowing maintainability even as our stack grows.

In addition, we should prefer to use tools that allow for
version-controlled configuration.  I keep all of them in my [dotfiles
repo](https://github.com/mtchllbrrn/dotfiles), making it easy to reverse
changes, configure new machines, and distribute as needed.

# Layer 1: Low-Level Rebinding with Karabiner

**NOTE**: *macOS Sierra has broken some of Karabiner/Seil's functionality.
Karabiner's devs are working hard on porting to Sierra with
[Karabiner-Elements](https://github.com/tekezo/Karabiner-Elements), and it
already replicates most of the functionality. For what it's worth, I won't
be updating to Sierra until I'm confident all of my configuration will
carry over. Caveat emptor!*

[Karabiner](https://pqrs.org/osx/karabiner/) and
[Seil](https://pqrs.org/osx/karabiner/seil.html.en) form the backbone of
my stack.  Karabiner offers a lot of low-level keyboard rebinding
functionality that can't be achieved with other macOS tools.  Seil is
effectively an extension for Karabiner that allows us to rebind the Caps
Lock key.

## Our Own Modifier: Hyper

The most important feature of Karabiner is its ability to implement
a so-called Hyper key, inspired by the classic [Space Cadet
keyboards](https://en.wikipedia.org/wiki/Space-cadet_keyboard) of
yesteryear. On the standard macOS keyboard, and at the OS-level, you'll
find four modifiers: Shift, Control, Option, Command (fn doesn't count
because it's recognized *only* at the hardware level). Hyper is
a conceptual fifth modifier, giving us a clean "namespace" for all of our
new bindings.  This namespace is free from existing OS- or app-level
bindings, so we never have to worry about conflicting with existing
functionality.  This is perfect for our goal of contextless bindings.

Under the hood, Karabiner achieves this by binding a key of your choice to
*all four* of the existing modifiers. Have you ever seen a keyboard
shortcut that uses Shift + Control + Alt + Command? They don't exist, so
it's the perfect way to emulate our fifth modifier.

Check out [this
article](http://www.tenshu.net/p/fake-hyper-key-for-osx.html) for details
on configuring your Hyper key with Karabiner and Seil.  The article
describes mapping Hyper to Caps Lock, which is an excellent choice, but
I have decided that Control is the best Hyper for me.  Most of my time is
spent in a terminal, so I like having Control's functionality on Caps
Lock, close to my pinky, instead (more on this below).  Note that I still
bind Caps Lock to F19, as discussed in the article, to allow for easy
rebinding.

## Super-Duper Mode

Super-Duper mode is chock-full of functionality right on the home row.
Check out [Jason Randolph's
repo](https://github.com/jasonrudolph/keyboard) for the original idea.
Super-Duper mode can be invoked by pressing and holding S and D. Once
you're there, here's some of the functionality you get:

* H/J/K/L are mapped to Left/Down/Up/Right, giving us easy vim bindings
  system-wide.
* F is bound to Command, meaning we can navigate to the beginning/end of
  a line with F+H or F+L.
* A is bound to option, which allows similar navigation by-word.
* O and I are Ctrl+Tab and Ctrl+Shift+Tab, respectively, giving us easy
  tab navigation in most apps.
* U and P are bound similarly for navigating to the first or last tab.
  These tab-navigating bindings don't work in every app, but I'll show you
  a way to fix that in a future article.

To add this feature to Karabiner, copy  [this
snippet](https://gist.github.com/mtchllbrrn/d9c03cb82d266e2fb082b06d0e68f69c)
to Karabiner's `private.xml` file. It lives in `~/Application
Support/Karabiner`, by default.  From there, just check the appropriate
box in Karabiner's list of configurations.

Now that that's out of the way, I have a confession:  I invoke Super-Duper
with X+C, not S+D, and I use Z and V for Option and Command, respectively.
This prevents accidental Super-Duper invocations when typing words with
juxtaposed S's and D's, like "sounds."  You can achieve the same thing by
taking a look at the XML snippet and editing accordingly (I don't want to
make this too easy :P).

## Additional Karabiner Configuration

#### Remap Caps Lock to Control on hold and Escape on tap

As I mentioned above, I like having Control within easy reach for terminal
operations. A lot of devs achieve this with native macOS functionality
(via keyboard settings), but I use Karabiner because it also allows me to
invoke Escape with a single tap of Caps Lock.  This is surprisingly useful
in a whole lot of apps, and it's much easier than reaching for Escape
(Home Row is Home).

[Here's the
snippet](https://gist.github.com/mtchllbrrn/19984257d82ec27576f20080676b3e58),
just copy it into Karabiner's `private.xml` and check its box in
Karabiner. Remember that you must have configured Caps Lock to send F19
with Seil, as detailed in the Hyper article above.

#### Remap Right-Command to Delete

Delete is one of your most-used keys, yet it takes a massive reach with
your weakest finger to press it.  Right-Command is a better spot, and
I never used the key anyway.

This feature comes with Karabiner out of the box, no need to edit your
`private.xml`.

#### Remap Right-Shift + Left-Shift to Caps Lock toggle

I rebound Caps Lock to Control/Escape, but sometimes I still want to
invoke Caps Lock. To do so, I simply tap both shifts at the same time to
toggle Caps Lock.  It feels extra-authoritative for those all-caps
moments.

This feature also comes with Karabiner out of the box.

# Layer 2: Window Management with Hammerspoon

[Hammerspoon](http://www.hammerspoon.org) offers a powerful scripting
environment for automating a variety of OS tasks.  It's particularly
suited to window management, but it features a robust set of modules for
scripting everything from system volume, notifications, mouse position,
battery information, etc.  If there's a single stack-hacking tool that's
worth learning from the inside out, this is it.

Out of the box, Hammerspoon doesn't do anything: It's a blank slate
waiting for your configuration in `~/.hammerspoon/init.lua`. [This simple
configuration](https://gist.github.com/mtchllbrrn/efb5baabbafb8742fd52c826269dbdf0)
implements the essential window-management functionality:

* Hyper + Up/Down/Left/Right will resize the active window to half of the
  screen.  Hyper + F will fullscreen the window.
* Hyper + H/J/K/L will navigate directionally between apps in a single
  workspace, much in the same way you might navigate between panes in
  tmux.
* Hyper + U/I/O/P/L/etc will focus or launch the the specified app, no
  matter which workspace or app is currently active.

Notice that we're starting to lean heavily on Hyper, and all of our binds
are invoked with a single keystroke.  We're also minimizing fatigue by
preferring two-handed bindings for our most common functionality.  This
makes invocation very fast and avoids contortion.

In particular, I recommend getting used to the app shortcuts.  Switching
between apps is a common operation, so having the ability to go directly
to your desired app with a single keystroke is especially helpful.
I suggest taking a look at the sample configuration and editing it to
reflect your most-used apps.

Once the initial configuration is out of the way, you're free to explore
all of Hammerspoon's additional functionality.  Despite its versatility,
the devs have done an excellent job of writing a sensible,
[well-documented API](http://www.hammerspoon.org/docs/).
[Here's](https://github.com/Hammerspoon/hammerspoon/wiki/Sample-Configurations)
a great list of others' configurations, which serves as a great source of
inspiration.

# Conclusion

The addition of Karabiner & Hammerspoon to your workflow, with the right
configuration, will get you 90% of the way towards a Gratuitously
Stack-Hacked Environment™. They are easily the biggest steps you can take.
In future articles, I'll discuss how other tools can be incorporated to
extend your capabilities, cover various corner-cases, and achieve the
final 10%.

Above all, it's important that you take ownership of every change you
make.  The only way for us to reap the benefits of gratuity without
drowning in the complexity is to understand each tool and each
customization.  Off-the-shelf solutions lead to sub-optimal results and
complacency because they are not *your* solutions.

If you have any questions about what you see here, feel free to reach out.

We've come a long way on our gratuitous journey, but our work has only
just begun.
