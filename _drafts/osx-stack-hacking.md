---
layout: post
title: "Full-Stack Window Management in OS X"
permalink: /stack-hacking
---

### Outline

Concepts:
  - Context-less keybinds
    - No context-switching, no overhead. No matter where you are, no
      matter which workspace, you can do what you're trying to do.
    - It's a thick stack of apps, so have a concept of the division of
      functions for each "layer". Otherwise, you end up with a stack
      that's hard to maintain.
    - Configuration for entire stack should be version-controlled through
      dotfiles, allowing us to easily deploy the stack across machines
        - TODO: Track Maestro/Karabiner/Seil, if possible.
        - TODO: Write a script to easily deploy config automatically. Use
          short-stack?

Stack layers:
  - Karabiner/Seil (low-level keyboard -> OS functionality)
    - Caps = hyper when held (NOT ctrl), esc when tapped
    - Super-duper mode (use x+c instead of s+d. s+d conflicts with words
      like 'sounds')
      - vim bindings everywhere, including navigate by-word, begin/end of
        line, +space for selection
        - Navigate by tab with i/o
        - Navigate by or end/begin of tab list with u/p
        - copy/paste (I don't really use this)
    - Change key repeat rate/delay
    - Double-tap shift for caps (mirrors behavior of mobile kbs)

  - Hammerspoon (window-management)
    - Use hyper+right hand keys to navigate to specific apps 
    - Use hyper-hjkl to navigate between windows in a workspace
    - Keep windows in a single layer. Don't have overlap
    - ctrl-r for drawing complex window arrangements (completely
      configurable)
    - (to-do) Save window arrangements/workspaces depending on whether
      you're plugged into a monitor / which monitor
      - (to-do) throw app to another monitor (see Matt's dotfiles)

  - Keyboard Maestro (adding app-specific bindings, helps in achieving
    context-less binds)
    - Slack-like command-k navigation in messages.app
    - Tab-switching behavior in iMessage / Slack (navigate by unread
      channel / organization)
    - Disable problem bindings that conflict with your contextless scheme
      - Sometimes I would hit command-k when I think Slack is active, but
        Textual was actually selected, and this binding would clear chat
        history in the current channel. I don't want this, so I disabled
        with maestro.
    - Chrome-like tab-switching in tmux for super-duper mode (command+num
      / super-duper i/o)
  - Alfred? General functionality.
  - Misc
    - Vimium / vimari (which sucks)
