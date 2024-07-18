---
title: 1. Basic Operations
type: docs
---

# Basic Operations

## Navigate Between IOS Modes

1. Move between User EXEC mode and Privileged EXEC mode
   ```txt
   switch> enable
   switch# disable
   switch>
   ```
2. Move between Privileged EXEC mode and Global Configuration mode
   ```txt
   switch# configure terminal
   switch(config)# exit
   switch#
   ```
3. Move from any sub-configuration mode to Privileged EXEC mode
   ```txt
   switch(config-line)# end
   switch#
   % or
   switch(config-line)# Ctrl+Z
   switch#
   ```

## Commands Shortening

Commands and keywords can be shortened to the minimum number of characters that identify a unique selection.

```txt
switch# conf t
switch(config)#
```

```txt
switch# con t
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
switch# copy running-config startup-config
% or
switch# write memory
```

## Configure Hostnames

```txt
switch# configure terminal
switch(config)# hostname <hostname>
<hostname>(config)#
```

## Configure Passwords

1. Console Access password

   ```txt
   switch(config)# line console 0
   switch(config-line)# password <password>
   switch(config-line)# login
   switch(config-line)# exit
   switch(config)#
   ```

2. Privileged EXEC Access password

   ```txt
   switch(config)# enable password <password>
   ```

## Configure Users and their Secrets

1. Console Access secret

   ```txt
   switch(config)# username <user> secret <password>
   switch(config)# line console 0
   switch(config-line)# login local
   switch(config-line)# exit
   switch(config)#
   ```

2. Privileged EXEC Access secret

   ```txt
   switch(config)# enable secret <password>
   ```

## Banner Messages

The delimiter can be any character, being used to mark the start and end of message.

```txt
switch(config)# banner motd !
<message>
!
switch(config)#
```

## Verify and Monitor Cisco Device

```txt
switch# show running-config
switch# show startup-config
switch# show interfaces
switch# show arp
switch# show version
```

## Cisco Discovery Protocol

1. Show all CDP neighbors

   ```txt
   switch# show cdp neighbors
   ```

2. Show details of one neighbor

   ```txt
   switch# show cdp entry <device_id>
   ```

3. Disable CDP globally

   ```txt
   switch(config)# no cdp run
   ```

4. Disable CDP for an interface

   ```txt
   switch(config)# interface <interface_type> <interface_number>
   switch(config-if)# no cdp enable
   ```

## Link Layer Discovery Protocol

1. Enable LLDP globally

```txt
switch(config)# lldp run
```

2. Enable LLDP for an interface

```txt
switch(config)# interface <interface_type> <interface_number>
switch(config-if)# lldp receive
switch(config-if)# lldp transmit
```

3. Show all LLDP neighbors

```txt
switch# show lldp neighbors
```
