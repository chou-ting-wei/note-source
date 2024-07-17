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

| Shortcut              | Description                                           |
| :-------------------- | :---------------------------------------------------- |
| ?                     | List available commands                               |
| Tab                   | Autocomplete & check if the current command is viable |
| Ctrl + Z              | Return to Privileged EXEC Mode                        |
| Ctrl + Shift + 6      | Cancel Cisco IOS process                              |
| Up Arrow / Down Arrow | Scroll through previously entered commands            |

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
switch(config)# hostname SW-EC1f
SW-EC1f(config)#
```

## Configure Passwords

1. Console Access password

   ```txt
   SW-EC1f(config)# line console 0
   SW-EC1f(config-line)# password passwd1
   SW-EC1f(config-line)# login
   SW-EC1f(config-line)# exit
   SW-EC1f(config)#
   ```

2. Privileged EXEC Access password

   ```txt
   SW-EC1f(config)# enable password passwd2
   ```

## Configure Users and their Secrets

1. Console Access secret

   ```txt
   SW-EC1f(config)# username user secret passwd3
   SW-EC1f(config)# line console 0
   SW-EC1f(config-line)# login local
   SW-EC1f(config-line)# exit
   SW-EC1f(config)#
   ```

2. Privileged EXEC Access secret

   ```txt
   SW-EC1f(config)# enable secret passwd4
   ```

## Banner Messages

The delimiter can be any character, being used to mark the start and end of message.

```txt
SW-EC1f(config)# banner motd !
helloworld hellloflvksdflsdk!
SW-EC1f(config)#
```

## Verify and Monitor Cisco Device

```txt
SW-EC1f# show running-config
SW-EC1f# show startup-config
SW-EC1f# show interfaces
SW-EC1f# show arp
SW-EC1f# show version
```

## Cisco Discovery Protocol

1. Show all CDP neighbors

   ```txt
   Sw-Lab1# show cdp neighbors
   ```

2. Show details of one neighbor

   ```txt
   Sw-Lab1# show cdp entry Device-ID
   ```

3. Disable CDP globally

   ```txt
   Sw-Lab1(config)# no cdp run
   ```

4. Disable CDP for an interface

   ```txt
   Sw-Lab1(config)# interface fastEthernet 0/1
   Sw-Lab1(config-if)# no cdp enable
   ```

## Link Layer Discovery Protocol

1. Enable LLDP globally

```txt
Sw-Lab1(config)# lldp run
```

2. Enable LLDP for an interface

```txt
Sw-Lab1(config)# interface fastEthernet 0/1
Sw-Lab1(config-if)# lldp receive
Sw-Lab1(config-if)# lldp transmit
```

3. Show all LLDP neighbors

```txt
Sw-Lab1# show lldp neighbors
```
