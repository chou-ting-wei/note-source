---
title: OpenSSH Server
type: docs
---

# OpenSSH Server

1. Install the OpenSSH server
   ```sh
   sudo apt update
   sudo apt install openssh-server
   ```
2. Start and enable the SSH service
   ```sh
   sudo systemctl start ssh
   sudo systemctl enable ssh
   sudo systemctl status ssh
   ```
3. SSH configuration
   ```sh
   sudo vi /etc/ssh/sshd_config
   sudo systemctl restart ssh
   ```
