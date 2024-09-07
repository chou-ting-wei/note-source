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

### Reset the Switch

Revert a Juniper EX2300 switch to its factory-default configuration using the Factory Reset/Mode button.

1. Press the Factory Reset/Mode button for 10 seconds
   > The switch transitions into factory-default configuration, the console displays committing factory default configuration, and the Link/Activity LED on the RJ-45 network ports and the uplink ports is lit steadily in green color.
2. Press the Factory Reset/Mode button for 10 more seconds
   > The switch transitions into initial setup mode, the console displays committing ezsetup config, and the Link/Activity LED on the RJ-45 network ports and the uplink ports blink in green color.
