---
title: Basic Operations
type: docs
weight: 10
---

# Basic Operations

## Navigation and User Interface

### Start the Junos OS CLI

1. Log in as `root`
2. Start the CLI

   ```txt
   root# cli
   root@>
   ```

   > The > command prompt shows that you are in operational mode. Later, when you enter configuration mode, the prompt will change to #.

3. Type ? to show the top-level commands available in operational mode
   ```txt
   root@> ?
   ```
   ```
   Possible completions:
       clear           Clear information in the system
       configure       Manipulate software configuration information
       diagnose        Invoke diagnose script
       file            Perform file operations
       [...]
   ```
4. Methods to exit the paginated output
   ```txt
   ---(more ...%)--- q
   % or
   ---(more ...%)--- <Ctrl+C>
   ```

### Navigate Between OS Modes

1. When you log in to the device and type the `cli` command and press Enter, you are automatically in operational mode
   ```txt
   ---JUNOS 17.2B1.8 built 2018-05-09 23:41:29 UTC
   % cli
   user@hostname>
   ```
2. To enter configuration mode, type the `configure` command or the `edit` command in CLI operational mode

   ```txt
   user@hostname> configure
   Entering configuration mode

   [edit]
   user@hostname#
   ```

3. You can exit configuration mode and return to operational mode in one of the following ways

   ```txt
   [edit]
   user@hostname# commit and-quit
   % or
   [edit]
   user@hostname# exit
   ```

4. Use the `run` command to run operational mode commands whlie in configuration mode
   ```txt
   [edit]
   user@hostname# run <operational_mode_command>
   ```

## Device Configuration

### Configure Hostname

```txt
[edit]
root# set system host-name <hostname>

```

### Configure Root Password

```txt
[edit]
root# set system root-authentication plain-text-password
New password: **********
Retype new password: **********
```

### Configure User Account

1. Create the local user account

   ```txt
   [edit]
   root# set system login user <user> class super-user
   ```

2. Set the encrypted password

   ```txt
   [edit]
   root# set system login user <user> authentication plain-text-password
   New password: **********
   Retype new password: **********
   ```

### Configure a Range of Interfaces

```txt
user@hostname# wildcard range set interfaces ge-0/0/[<start>-<end>]
```

### Delete Specific Configuration

```txt
[edit]
user@hostname# delete <configuration_command>
```

### SSH Configuration

1. Configure hostname and domain name

```txt
user@hostname# set system host-name <hostname>
user@hostname# set system domain-name <domain_name>
```

2. Configure AES key pair

   ```txt
   set system services ssh ciphers aes256-ctr
   set system services ssh ciphers aes256-cbc
   set system services ssh ciphers aes192-ctr
   set system services ssh ciphers aes192-cbc
   set system services ssh ciphers aes128-ctr
   set system services ssh ciphers aes128-cbc
   ```

3. Allow users to login by SSH

   ```txt
   user@hostname# set system services ssh protocol-version v2
   ```

4. Choose SSH version

   ```txt
   user@hostname# set system services ssh
   ```

### Verify and Monitor Juniper Device

```txt
user@hostname> show configuration
user@hostname> show system commit
user@hostname> show interfaces
user@hostname> show arp
user@hostname> show version
```

## Network Discovery

### Link Layer Discovery Protocol

1. Enable LLDP globally

   ```txt
   [edit]
   user@hostname# set protocols lldp interface all
   ```

2. Enable LLDP for an interface

   ```txt
   [edit]
   user@hostname# set protocols lldp interface <interface>
   ```

3. Show all LLDP neighbors

   ```txt
   user@hostname> show lldp neighbors
   ```

## Device Management and Security

### Shut Down Unused Ports

1. Identify unused ports

   ```txt
   user@hostname> show interfaces terse
   ```

2. Shut down unused ports

   ```txt
   [edit]
   user@hostname# set interfaces <interface> disable
   ```

### Upgrade the Switch

1. Download the latest Junos OS image from [Support - Juniper Networks](https://support.juniper.net/support/)
2. List the disks connected to your system

   ```sh
   diskutil list
   ```

   ```
   /dev/disk0 (internal, physical):
      #:                       TYPE NAME                    SIZE       IDENTIFIER
      0:      GUID_partition_scheme                        *500.3 GB   disk0
      1:             Apple_APFS_ISC Container disk1         524.3 MB   disk0s1
      2:                 Apple_APFS Container disk3         494.4 GB   disk0s2
      3:        Apple_APFS_Recovery Container disk2         5.4 GB     disk0s3

   /dev/disk3 (synthesized):
      #:                       TYPE NAME                    SIZE       IDENTIFIER
      0:      APFS Container Scheme -                      +494.4 GB   disk3
                                    Physical Store disk0s2
      1:                APFS Volume Macintosh HD            10.7 GB    disk3s1
      2:              APFS Snapshot com.apple.os.update-... 10.7 GB    disk3s1s1
      3:                APFS Volume Preboot                 6.6 GB     disk3s2
      4:                APFS Volume Recovery                966.2 MB   disk3s3
      5:                APFS Volume Data                    141.3 GB   disk3s5
      6:                APFS Volume VM                      1.1 GB     disk3s6

   /dev/disk4 (external, physical):
      #:                       TYPE NAME                    SIZE       IDENTIFIER
      0:     FDisk_partition_scheme                        *8.1 GB     disk4
      1:               Windows_NTFS Untitled                8.1 GB     disk4s1
   ```

3. Unmount the USB drive

   ```sh
   diskutil unmountDisk /dev/disk4
   ```

4. Write the Junos image to the USB drive

   ```sh
   sudo dd if=junos-install-media-usb-ex-arm-32-21.4R3-S9.5.img of=/dev/rdisk4 bs=1m
   ```

   > Make sure to replace `junos-install-media-usb-ex-arm-32-21.4R3-S9.5.img` with the correct file path for your Junos image. Use `/dev/rdisk4` instead of `/dev/disk4` for faster write speeds on macOS.

5. Display the current configuration

   ```sh
   cscc@twchou_J2300> show configuration | display set
   ```

6. Boot and install from USB

   ```
   Boot Menu

   1. Boot [P]revious installed Junos packages
   2. Boot Junos in [S]ingle user mode
   3. Boot from [R]ecovery snapshot
   4. Boot from [U]SB
   5. Boot to [O]AM shell
   6. Snapshot [B]oot menu
   7. [M]ain menu
   ```

7. Verify the installed version

   ```sh
   --- JUNOS 21.4R3-S9.5 Kernel 32-bit  JNPR-12.1-20240304.935bb4f_buil
   root@:RE:0% cli
   {master:0}
   root> show version
   ```

8. Configure additional settings

   ```sh
   {master:0}
   root> configure
   Entering configuration mode

   {master:0}[edit]
   root# delete chassis auto-image-upgrade

   {master:0}[edit]
   root# set system root-authentication plain-text-password
   New password:
   Retype new password:

   {master:0}[edit]
   root# commit
   ```

### Reset the Switch

Revert a Juniper EX2300 switch to its factory-default configuration using the Factory Reset/Mode button.

1. Press the Factory Reset/Mode button for 10 seconds
   > The switch transitions into factory-default configuration, the console displays committing factory default configuration, and the Link/Activity LED on the RJ-45 network ports and the uplink ports is lit steadily in green color.
2. Press the Factory Reset/Mode button for 10 more seconds
   > The switch transitions into initial setup mode, the console displays committing ezsetup config, and the Link/Activity LED on the RJ-45 network ports and the uplink ports blink in green color.
