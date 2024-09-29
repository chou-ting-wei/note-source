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
    # Example: Aliases or functions can be placed here
end

# Set the universal PATH and make sure /usr/local/bin comes first
set -U PATH /usr/local/bin $PATH

# Disable Fish Shell greeting message
set -U fish_greeting ""
```