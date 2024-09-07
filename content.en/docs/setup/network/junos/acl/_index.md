---
title: ACL Configuration
type: docs
---

# ACL Configuration

## Create Firewall Filter

```txt
user@hostname# set firewall family inet filter <filter_name> term 1 from source-address <allowed-ip-address>
user@hostname# set firewall family inet filter <filter_name> term 1 from protocol tcp
user@hostname# set firewall family inet filter <filter_name> term 1 from destination-port ssh
user@hostname# set firewall family inet filter <filter_name> term 1 then accept
user@hostname# set firewall family inet filter <filter_name> term 2 from protocol tcp
user@hostname# set firewall family inet filter <filter_name> term 2 from destination-port ssh
user@hostname# set firewall family inet filter <filter_name> term 2 then reject
user@hostname# set firewall family inet filter <filter_name> term 3 then accept
```

## Apply to Loopback Interface

```txt
user@hostname# set interfaces lo0 unit 0 family inet filter input <filter_name>
```
