---
title: RIP Configuration
type: docs
---

# RIP Configuration

## Enable RIP

```txt
Router(config)# router rip
Router(config-router)#
```

## Start RIP routing

```txt
Router(config-router)# network <subnet>
```

## Propagate Default Static Route

```txt
Router(config)# ip route 0.0.0.0 0.0.0.0 {ip-address | exit-intf}
Router(config)# router rip
Router(config-router)# default-information originate
```

## Enable RIPv2

Make RIP a classless routing protocol.

```txt
Router(config-router)# version 2
```

## Disable Auto Summarization

When automatic summarization has been disabled, RIPv2 no longer summarizes networks to their classful address at boundary routers.

```txt
Router(config-router)# no auto-summary
```

## Configure Passive Interface

Passive interface is a feature used by routing protocol to stop sending updates on the particular interface.

1. Passive by default

   ```txt
   Router(config-router)# passive-interface default
   Router(config-router)# no passive-interface <interface>
   ```

2. Specific passive interface

   ```txt
   Router(config-router)# passive-interface <interface>
   ```
