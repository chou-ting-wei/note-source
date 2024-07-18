---
title: 1. Basic Operations
type: docs
---

# Basic Operations

## Navigate Between IOS Modes

1. Move between User EXEC mode and Privileged EXEC mode
   ```txt
   Switch> enable
   Switch# disable
   Switch>
   ```
2. Move between Privileged EXEC mode and Global Configuration mode
   ```txt
   Switch# configure terminal
   Switch(config)# exit
   Switch#
   ```
3. Move from any sub-configuration mode to Privileged EXEC mode
   ```txt
   Switch(config-line)# end
   Switch#
   % or
   Switch(config-line)# Ctrl+Z
   Switch#
   ```

## Commands Shortening

Commands and keywords can be shortened to the minimum number of characters that identify a unique selection.

```txt
Switch# conf t
Switch(config)#
```

```txt
Switch# con t
% Ambiguous command: “con t”
```

## Keyboard Shortcuts

| Shortcut              | Description                                            |
| :-------------------- | :----------------------------------------------------- |
| ?                     | List available commands.                               |
| Tab                   | Autocomplete & check if the current command is viable. |
| Ctrl + Z              | Return to Privileged EXEC Mode.                        |
| Ctrl + Shift + 6      | Cancel Cisco IOS process.                              |
| Up Arrow / Down Arrow | Scroll through previously entered commands.            |

## Save the Running Configuration File

To save the running configuration to the startup configuration, use one of the following commands.

```txt
Switch# copy running-config startup-config
% or
Switch# write memory
```

## Configure Hostname

```txt
Switch# configure terminal
Switch(config)# hostname <hostname>
<hostname>(config)#
```

## Configure Password

1. Console Access password

   ```txt
   Switch(config)# line console 0
   Switch(config-line)# password <password>
   Switch(config-line)# login
   Switch(config-line)# exit
   Switch(config)#
   ```

2. Privileged EXEC Access password

   ```txt
   Switch(config)# enable password <password>
   ```

## Configure Users and their Secrets

1. Console Access secret

   ```txt
   Switch(config)# username <user> secret <password>
   Switch(config)# line console 0
   Switch(config-line)# login local
   Switch(config-line)# exit
   Switch(config)#
   ```

2. Privileged EXEC Access secret

   ```txt
   Switch(config)# enable secret <password>
   ```

## Banner Message Configuration

The delimiter can be any character, being used to mark the start and end of message.

```txt
Switch(config)# banner motd !
<message>
!
Switch(config)#
```

## Verify and Monitor Cisco Device

```txt
Switch# show running-config
Switch# show startup-config
Switch# show interfaces
Switch# show arp
Switch# show version
```

## Cisco Discovery Protocol

1. Show all CDP neighbors

   ```txt
   Switch# show cdp neighbors
   ```

2. Show details of one neighbor

   ```txt
   Switch# show cdp entry <device_id>
   ```

3. Disable CDP globally

   ```txt
   Switch(config)# no cdp run
   ```

4. Disable CDP for an interface

   ```txt
   Switch(config)# interface <interface>
   Switch(config-if)# no cdp enable
   ```

## Link Layer Discovery Protocol

1. Enable LLDP globally

   ```txt
   Switch(config)# lldp run
   ```

2. Enable LLDP for an interface

   ```txt
   Switch(config)# interface <interface>
   Switch(config-if)# lldp receive
   Switch(config-if)# lldp transmit
   ```

3. Show all LLDP neighbors

   ```txt
   Switch# show lldp neighbors
   ```

## SSH Configuration

1. Configure hostname and domain name

   ```txt
   Switch(config)# hostname <hostname>
   Switch(config)# ip domain-name <domain_name>
   ```

2. Configure RSA key pair

   ```txt
   Switch(config)# crypto key generate rsa
   ! Choose modulus length = 1024
   ```

3. Choose SSH version

   ```txt
   Switch(config)# ip ssh version 2
   ```

4. Allow users to login by SSH
   ```txt
   Switch(config)# line vty 0 15
   Switch(config-line)# transport input ssh
   Switch(config-line)# login local
   ```

## Force Other Users to Logout

1. Check current connections

   ```txt
   Switch# show users
   ```

   ```
      Line    User   Host(s)  Idle      Location
   * 0 con 0         idle     00:00:00
     2 vty 0  user2  idle     00:00:45
     3 vty 1  user3  idle     00:00:23
   ```

2. Disconnect a user session by clearing a VTY line

   ```txt
   Switch# clear line vty <line_num>
   ```

## Password Recovery

1. Initialize the flash file system

   ```
   The system has been interrupted ...
   ```

   ```txt
   switch: flash_init
   ```

2. Display the contents of the flash memory

   ```txt
   switch: dir flash:
   ```

   ```
   Directory of flash:/
     13  drwx  192   Mar 01 1993 22:30:48  c2960-lanbase-mz.122-25.FX
     11  -rwx  5825  Mar 01 1993 22:31:59  config.text
     18  -rwx  720   Mar 01 1993 02:21:30  vlan.dat
   ```

3. Rename `config.text`

   ```txt
   switch: rename flash:config.text flash:config.bak
   ```

4. Boot the system

   ```txt
   switch: boot
   ```

5. Skip the initial configuration dialog

   ```
   In order to access the device manager, ...
   [...]
   Would you like to enter the initial configuration dialog?
   ```

   ```txt
   [yes/no]: no
   ```

6. Restore the configuration file and running-config

   ```txt
   Switch> enable
   Switch# copy running-config startup-config
   Switch# copy flash:config.bak flash:config.text
   Switch# copy startup-config running-config
   ```

7. Update the console password

   ```txt
   Switch(config)# line console 0
   Switch(config-line)# password passwd
   Switch(config-line)# login
   ```

8. Save the configuration to startup-config

   ```txt
   Switch# copy running-config startup-config
   ```

## Reset the Switch

1. Initialize the flash file system

   ```
   The system has been interrupted ...
   ```

   ```txt
   switch: flash_init
   ```

2. Display the contents of the flash memory

   ```txt
   switch: dir flash:
   ```

   ```
   Directory of flash:/
     13  drwx  192   Mar 01 1993 22:30:48  c2960-lanbase-mz.122-25.FX
     11  -rwx  5825  Mar 01 1993 22:31:59  config.text
     18  -rwx  720   Mar 01 1993 02:21:30  vlan.dat
   ```

3. Delete `config.text` and `vlan.dat`
   ```txt
   switch: delete flash:config.text
   switch: delete flash:vlan.dat
   ```
4. Boot the system

   ```txt
   switch: boot
   ```

5. Skip the initial configuration dialog

   ```
   In order to access the device manager, ...
   [...]
   Would you like to enter the initial configuration dialog?
   ```

   ```txt
   [yes/no]: no
   ```
