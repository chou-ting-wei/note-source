---
title: GRE Configuration
type: docs
---

# GRE Configuration

## Define the Tunnel Interface

```txt
Router(config)# interface Tunnel<tunnel_id>
Router(config-if)# ip address <ip_address> <subnet_mask>
```

## Set the Source and Destination

```txt
Router(config-if)# tunnel source <interface>
Router(config-if)# tunnel destination <ip_address>
```

## Specify the Tunnel Mode

```txt
Router(config-if)# tunnel mode gre ip
```

## Verify the Tunnel Configuration

```txt
Router# show interface Tunnel<tunnel_id>
```
