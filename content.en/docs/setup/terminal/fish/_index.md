---
title: Fish
type: docs
---

# Fish

## Installing Fish Shell

1. Install fish on Linux
   ```sh
   sudo apt update
   sudo apt install fish
   ```
2. Set fish as default shell

   ```sh
   chsh -s /usr/bin/fish
   ```

3. Verify Installation
   ```sh
   fish --version
   ```

## Changing Fish Shell Configuration

1. Open the Fish configuration file

   ```sh
   vim ~/.config/fish/config.fish
   ```

2. Add or modify configurations

   ```sh
   if status is-interactive
       # Commands to run in interactive sessions can go here
   end
   set -U fish_greeting
   ```

3. Apply the changes
   ```sh
   source ~/.config/fish/config.fish
   ```
