---
title: Oracle VM VirtualBox
type: docs
---

# Oracle VM VirtualBox

## Guest Additions

1.  Update and upgrade packages

    ```sh
    sudo apt update
    sudo apt upgrade
    ```

2.  Install essential build tools

    ```sh
    sudo apt install build-essential dkms linux-headers-$(uname -r)
    ```

3.  Install VirtualBox Guest Additions

    ```sh
    sudo apt-get install virtualbox-guest-x11
    sudo reboot
    ```
