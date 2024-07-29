---
title: ACL Configuration
type: docs
---

# ACL Configuration

Access Control Entries (ACEs) in an Access Control List (ACL) consist of ordered permit or deny statements. Each ACL ends with an implicit `deny all` for unmatched traffic.

## Standard ACL

Standard ACLs, which filter traffic solely based on source IP addresses, are ideally placed close to the destination, given their inability to specify destination addresses.

1. Numbered ACL

   ```txt
   Router(config)# access-list <list_number> {deny | permit} <src_ip> [wildcard_mask]
   Router(config)# access-list <list_number> remark <description>
   ```

   > list-number should be 1-99, 1300-1999 (for Cisco IOS).

2. Named ACL

   ```txt
   Router(config)# ip access-list standard <list_name>
   Router(config-std-nacl)# {permit | deny} <src_ip> [wildcard_mask]
   Router(config-std-nacl)#remark <description>
   ```

3. Configuration Example
   ```txt
   Router(config)# ip access-list standard test-acl
   Router(config-std-nacl)# permit 192.168.2.2
   Router(config-std-nacl)# permit 192.168.2.3
   ```

## Extended ACL

Extended ACLs, which filter traffic based on source IP, source port, destination IP, destination port, and protocol, are strategically placed close to the source to effectively filter undesirable traffic.

1. Numbered ACL

   ```txt
   Router(config)# access-list <list_number> {permit | deny} <protocol> <src_ip> <src_wildcard> <dst_ip> <dst_wildcard>
   ```

   > list-number should be 100-199 or 2000-2699 (for Cisco IOS).

2. Named ACL

   ```txt
   Router(config)# ip access-list extended <list_name>
   Router(config-ext-nacl)# {permit | deny} <protocol> <src_ip> <src_wildcard> <dst_ip> <dst_wildcard>
   ```

3. Configuration Example
   ```txt
   Router(config)# ip access-list extended PC-1-to-2
   Router(config-ext-nacl)# permit ip host 192.168.1.2 host 192.168.2.2
   Router(config-ext-nacl)# permit tcp host 192.168.1.171 any eq 22
   Router(config-ext-nacl)# deny tcp any any eq 22
   ```

## Configure ACL on Interface

1. Apply to interface

   ```txt
   Router(config-if)# ip access-group {<list_number> | <list_name>} {in | out}
   ```

2. Apply to line (e.g. console, vty)

   ```txt
   Router(config-line)# access-class {<list_number> | <list_name>} {in | out}
   ```

## Verify ACL Configuration

```txt
Router# show ip access-lists
Router# show access-list <list_number>
Router# show ip access-list <list_name>
```
