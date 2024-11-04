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

3. Verify installation
   ```sh
   fish --version
   ```

4. Launch fish configuration interface
   ```sh
   fish_config
   ```

## Oh-My-Fish

1. Install Oh-My-Fish

   ```sh
   curl -L https://get.oh-my.fish | fish
   ```

2. Install the `agnoster` theme
   ```sh
   omf install agnoster
   omf theme agnoster
   ```
