---
title: Fish
type: docs
---

# Fish

## config.fish

```sh
# ~/.config/fish/config.fish
if status is-interactive
    # Commands to run in interactive sessions can go here
    set -gx PATH /opt/homebrew/bin $PATH
end

set -g fish_greeting ""
```