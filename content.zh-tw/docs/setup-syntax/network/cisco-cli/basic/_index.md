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

## Configure Hostnames

```txt
Switch# configure terminal
Switch(config)# hostname <hostname>
<hostname>(config)#
```

## Configure Passwords

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

## Banner Messages

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
   Switch(config)# interface <interface_type> <interface_number>
   Switch(config-if)# no cdp enable
   ```

## Link Layer Discovery Protocol

1. Enable LLDP globally

   ```txt
   Switch(config)# lldp run
   ```

2. Enable LLDP for an interface

   ```txt
   Switch(config)# interface <interface_type> <interface_number>
   Switch(config-if)# lldp receive
   Switch(config-if)# lldp transmit
   ```

3. Show all LLDP neighbors

   ```txt
   Switch# show lldp neighbors
   ```
