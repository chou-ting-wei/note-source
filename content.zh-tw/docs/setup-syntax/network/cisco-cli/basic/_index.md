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
   ```
   ```txt
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
```

```txt
switch# write memory
```

## Configure Hostnames

```txt
switch# configure terminal
switch(config)# hostname SW-EC1f
SW-EC1f(config)#
```

## Configure Passwords

### Console Access password

```txt
SW-EC1f(config)# line console 0
SW-EC1f(config-line)# password passwd1
SW-EC1f(config-line)# login
SW-EC1f(config-line)# exit
SW-EC1f(config)#
```

### Privileged EXEC Access password

```txt
SW-EC1f(config)# enable password passwd2
```
