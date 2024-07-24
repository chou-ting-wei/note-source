---
title: Basic Operations
type: docs
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
   root@>  ?
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
   ---(more ...%)--- Ctrl+C
   ```

### Navigate Between OS Modes

1. When you log in to the device and type the `cli` command and press Enter, you are automatically in operational mode
   ```txt
   ---JUNOS 17.2B1.8 built 2018-05-09 23:41:29 UTC
   % cli
   user@host>
   ```
2. To enter configuration mode, type the `configure` command or the `edit` command in CLI operational mode

   ```txt
   user@host> configure
   Entering configuration mode

   [edit]
   user@host#
   ```

3. You can exit configuration mode and return to operational mode in one of the following ways

   ```txt
   [edit]
   user@host# commit and-quit
   % or
   [edit]
   user@host# exit
   ```

4. To display the output of an operational mode command such as `show` while in configuration mode, issue the `run` configuration mode command
   ```txt
   [edit]
   user@host# run operational-mode-command
   ```

## Device Configuration

### Configure Hostname

```txt
[edit]
root# set system host-name <new_hostname>

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
   % or
   [edit]
   user@hostname# edit interfaces ge-0/0/[<start>-<end>]
   [edit interfaces ge-0/0/[<start>-<end>]]
   user@hostname# set disable
   ```

### Reset the Switch

Revert a Juniper EX2300 switch to its factory-default configuration using the Factory Reset/Mode button.

1. Press the Factory Reset/Mode button for 10 seconds
   > The switch transitions into factory-default configuration, the console displays committing factory default configuration, and the Link/Activity LED on the RJ-45 network ports and the uplink ports is lit steadily in green color.
2. Press the Factory Reset/Mode button for 10 more seconds
   > The switch transitions into initial setup mode, the console displays committing ezsetup config, and the Link/Activity LED on the RJ-45 network ports and the uplink ports blink in green color.
