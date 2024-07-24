---
title: AAA Configuration
type: docs
---

# AAA Configuration

AAA is a network security framework for

- Authentication: Verifying user identities
- Authorization: Defining user privileges
- Accounting: Logging user activities and durations

## Enable AAA on Device

This step involves activating the AAA model on Cisco routers or Cisco Catalyst 2960 switches.

```txt
Router/Switch(config)# aaa new-model
```

## Configure RADIUS Server

1. For routers
   ```txt
   Router(config)# radius server <server_name>
   Router(config-radius-server)# address ipv4 <server_ip>
   Router(config-radius-server)# key <password>
   ```
2. For switches
   ```txt
   Switch(config)# radius-server host <server_ip> key <password>
   ```

## Authentication Method List

```txt
Router/Switch(config)# aaa authentication login <list_name> <auth_list>
```

## Apply Authentication Method

Apply the authentication method list to VTY, console, or AUX lines to enforce specific access rules.

```txt
Router/Switch(config-line)# login authentication <list_name>
```

## Configuration Example

```txt
Router(config)# aaa new-model
Router(config)# radius server radius
Router(config-radius-server)# address ipv4 192.168.1.1
Router(config-radius-server)# key radiuskey

Router(config)# aaa authentication login ccna group radius local
Router(config)# line vty 0 15
Router(config-line)# login authentication ccna
```
