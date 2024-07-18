---
title: 5. OSPF Configuration
type: docs
---

<!--
Check this post:
1. Fix each title to make it looks more professionally
2. All variables(not included in {} part, e.g. {ip-address | exit-intf} should not be modified) should be enclosed in <> replaced with placeholders using underscores and all lowercase, with the common used variables, like <network_address>, <subnet_mask>, <interface_type>, <interface_number>...
3. Check if exist any error in all command
4. Make all the cisco commands to start with Switch or Router, such as Switch#, Router(config)#
5. Generate in txt code block
-->

# OSPF Configuration

## Single Area OSPF Configuration

### Configure Loopback Interface

An always-up interface which you can assign an IP address (Layer 3).

```txt
Router(config)# interface loopback 0
Router(config-if)# ip address <network_address> <subnet_mask>
```

### Enable OSPF

```txt
Router(config)# router ospf <process_id>
Router(config-router)#
```

### Check the Router ID

```txt
Router# show ip protocols
```

### Advertising Networks

1. Global configuration

   ```txt
   Router(config)# router ospf <process_id>
   Router(config-router)# network <network_address> <wildcard> area 0
   ```

2. Per-interface configuration

   ```txt
   Router(config)# interface <interface_type> <interface_number>
   Router(config-if)# ip ospf <process_id> area 0
   ```

### Verify OSPF Neighbor

```txt
Router# show ip ospf neighbor
```

### Reload OSPF Process

```txt
Router# clear ip ospf process
```

### Set interface priority

```txt
Router(config)# interface <interface_type> <interface_number>
Router(config-if)# ip ospf priority 255
Router(config-if)# end
```

### Propagate Default Route

```txt
Router(config)# ip route 0.0.0.0 0.0.0.0 <interface_type> <interface_number>
Router(config)# router ospf <process_id>
Router(config-router)# default-information originate
```

### Configure Passive Interfaces

1. Passive by default

   ```txt
   Router(config-router)# passive-interface default
   Router(config-router)# no passive-interface <interface_type> <interface_number>
   ```

2. Specific passive interface

   ```txt
   Router(config-router)# passive-interface <interface_type> <interface_number>
   ```

### Adjust Reference Bandwidth

OSPF uses a reference bandwidth of 100 Mbps for any links.

```txt
Router(config)# router ospf <process_id>
Router(config-router)# auto-cost reference-bandwidth 10000 (Bandwidth in Mbps)
```

### Adjust Interface Bandwidth

All interfaces have default bandwidth values assigned to them.

```txt
Router(config)# interface <interface_type> <interface_number>
Router(config-if)# bandwidth 100000 (Bandwidth in Kbps)
```

### Manually Setting OSPF Costs

Administrators can also manually modify the cost of each interface.

```txt
Router(config)# interface <interface_type> <interface_number>
Router(config-if)# ip ospf cost 100
```

### Show OSPF Accumulates Costs

The cost of an OSPF route is the accumulated value from one router to the destination network.

```txt
Router# show ip route <network_address>
```

## Multi Area OSPF

### Integrate with RIPv2

```txt
Router(config)# router ospf <process_id>
Router(config-router)# redistribute rip subnets
```

### Convert to Stub Area

It must be configured consistently across all routers within the area, which eliminates Type 4 and Type 5 LSA.

```txt
Router(config)# router ospf <process_id>
Router(config-router)# area 10 stub
```

### Convert to Totally Stubby Area

Eliminates Type 3, 4, and 5 LSA and must be configured consistently across all routers within the area.

```txt
Router(config)# router ospf <process_id>
Router(config-router)# area 10 stub no-summary
```

### Convert to Not-So-Stubby Area

Use the `nssa` keyword instead of `stub` to prevent Type 5 AS External LSA flooding in a Not-So-Stubby Area.

```txt
Router(config)# router ospf <process_id>
Router(config-router)# area 20 nssa
```

### Convert to Totally NSSA

Further reduce the table by eliminating Type 3, 4, 5 LSA.

```txt
Router(config)# router ospf <process_id>
Router(config-router)# area 20 nssa no-summary
```

### Stub Area Comparison

| Area Type           | External Routes (Type 4, 5 LSA) | Inter-Area Routes (Type 3 LSA) |
| :------------------ | :------------------------------ | :----------------------------- |
| Normal Area         | Yes                             | Yes                            |
| Stub Area           | No                              | Yes                            |
| Totally Stubby Area | No                              | No                             |
| Not-So-Stubby Area  | Yes (as Type 7 LSA)             | Yes                            |
| Totally NSSA        | Yes (as Type 7 LSA)             | No                             |

| Area Type                 | Area Restriction                                                                                           |
| :------------------------ | :--------------------------------------------------------------------------------------------------------- |
| Normal Area               | None                                                                                                       |
| Stub Area                 | No Type 4 and Type 5 LSA allowed.                                                                          |
| Totally Stubby Area       | No Type 3, 4, 5 LSA allowed, except for the default summary route.                                         |
| Not-So-Stubby Area (NSSA) | No Type 4 and Type 5 LSA allowed. Utilize Type 7 LSA for external routes.                                  |
| Totally NSSA              | No Type 3, 4, 5 LSA allowed, except for the default summary route. Utilize Type 7 LSA for external routes. |

## LSA Types and Information

LSAs provide OSPF network details like a database record.

| Name                     | Sender | Receiver                           | Information                           |
| :----------------------- | :----- | :--------------------------------- | :------------------------------------ |
| Type 1 Router LSA        | Router | All other routers in the same area | Link / Network information            |
| Type 2 Network LSA       | DR     | All other routers in the same area | List of routers that DR connects with |
| Type 3 Summary LSA       | ABR    | All routers in the different area  | Network information of other areas    |
| Type 4 Summary ASBR LSA  | ABR    | All routers in OSPF routing domain | Information of ASBR                   |
| Type 5 AS External LSA   | ASBR   | All routers in OSPF routing domain | External network                      |
| Type 7 NSSA External LSA | ASBR   | All the routers in the NSSA        | External network                      |

### Type 1 Router LSA

All routers advertise their directly connected OSPF-enabled links and forward their network information to OSPF neighbors.

```txt
Router# show ip ospf <process_id> database router
```

```
OSPF Router with ID (140.113.0.1) (Process ID 42)
Router Link States (Area 0)
LS Type: Router Links
Link State ID: 140.113.0.1
Advertising Router: 140.113.0.1
[...]
Number of Links: 1
```

### Type 2 Network LSA

Contains the Router ID and IP address of Designated Router.

```txt
Router# show ip ospf <process_id> database network
```

```
OSPF Router with ID (140.113.0.1) (Process ID 42)
Net Link States (Area 0)
LS Type: Network Links
Link State ID: 10.113.0.2 (address of Designated Router)
Advertising Router: 140.113.0.2
Network Mask: /24
Attached Router: 140.113.0.1
Attached Router: 140.113.0.2
[...]
```

### Type 3 Summary LSA

Generated by Area Border Router to advertise networks from other areas.

```txt
Router# show ip ospf <process_id> database summary
```

```
OSPF Router with ID (140.113.0.15) (Process ID 42)
Summary Net Link States (Area 10)
LS Type: Summary Links(Network)
Link State ID: 140.113.0.0 (summary Network Number)
Advertising Router: 140.113.0.10
Network Mask: /24
Link State ID: 10.0.2.0 (summary Network Number)
Advertising Router: 140.113.0.10
Link State ID: 140.113.20.0 (summary Network Number)
Advertising Router: 140.113.0.10
```

### Type 4 Summary ASBR LSA

Type 3 LSA describes routes to networks, while Type 4 LSA, though similar in format, specifically details routes to AS boundary routers.

```txt
Router# show ip ospf <process_id> database asbr-summary
```

```
OSPF Router with ID (140.113.0.15) (Process ID 42)
Summary ASB Link States (Area 10)
LS Type: Summary Links(AS Boundary Router)
Link State ID: 140.113.0.1 (AS Boundary Router address)
Advertising Router: 140.113.0.10
Network Mask: /0
```

### Type 5 AS External LSA

Advertise routes to external destinations of the OSPF routing domain.

```txt
Router# show ip ospf <process_id> database external
```

```
OSPF Router with ID (140.113.0.15) (Process ID 42)
Type-5 AS External Link States
Routing Bit Set on this LSA
LS Type: AS External Link
Link State ID: 0.0.0.0 (External Network Number)
Advertising Router: 140.113.0.1
Network Mask: /0
```

#### Metric Types for Type 5 LSA

1. Type 1 Metric  
   The total (internal + external) cost is used when calculating the routing table.
2. Type 2 Metric  
   The external cost dominates the total path cost, internal cost is considered only if multiple paths have the same external cost.

### Summary LSA Comparison

| LSA Type                     | Purpose                                                                       | Contents                            | Usage                                                                                                        |
| :--------------------------- | :---------------------------------------------------------------------------- | :---------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| Type 3 Network Summary LSA   | Advertises routes between OSPF areas (inter-area)                             | Network address, subnet mask, cost  | Used by ABR to share routes between areas, helping OSPF routers determine routes to networks in other areas. |
| Type 4 ASBR Summary LSA      | Advertises the location of an ASBR to other areas                             | Router ID of the ASBR, cost to ASBR | Enables routers in other areas to locate the ASBR and use it for routing to external destinations.           |
| Type 3 Default Summary Route | Advertises a default route to areas that do not have full routing information | Default route (0.0.0.0/0), cost     | Used in stub areas to provide a path to external networks without needing specific external routes.          |
