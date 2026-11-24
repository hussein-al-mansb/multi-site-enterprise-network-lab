# Addressing and VLANs

The following details come from the recorded project design and previously displayed CLI outputs. **Confirm the running configuration in Packet Tracer before treating them as the final authoritative inventory.**

## Jeddah headquarters

| VLAN | Name | Expected subnet | HSRP virtual gateway |
|---:|---|---|---|
| 10 | ADMIN | `10.10.10.0/24` | `10.10.10.1` |
| 20 | SALES | `10.10.20.0/24` | `10.10.20.1` |
| 40 | GUEST | `10.10.40.0/24` | `10.10.40.1` |
| 50 | SERVERS | `10.10.50.0/24` | `10.10.50.1` |
| 60 | DMZ | `10.10.60.0/24` | `10.10.60.1` |
| 99 | MGMT | `10.10.99.0/24` | `10.10.99.1` |

Previous HSRP evidence showed CORE-01 at `.2` and CORE-02 at `.3` in those VLAN subnets, with primary/standby roles split across the pair.

### Recorded servers

| Host | Recorded IP |
|---|---|
| `JED-INFRA-SRV` | `10.10.50.10` |
| `JED-INVENTORY-SRV` | `10.10.50.20` |
| `JED-WEB-SRV` | `10.10.60.10` |

## Observed branch routes

In the OSPF route screenshots, Jazan networks appear with `10.20.20.0`, `10.20.30.0`, `10.20.40.0`, and `10.20.99.0` prefixes. Abha networks appear with `10.30.20.0`, `10.30.30.0`, `10.30.40.0`, and `10.30.99.0` prefixes. These are route observations, **not a confirmed complete interface/gateway inventory**.

## Branch network segmentation

| Site | Recorded VLAN names |
|---|---|
| Jazan | 20 SALES, 30 WAREHOUSE, 40 GUEST, 99 MGMT |
| Abha | 20 SALES, 30 WAREHOUSE, 40 GUEST, 99 MGMT |

**Branch subnet and gateway tables:** Not independently reconfirmed from the submitted file. Fill these in after running `show ip interface brief` on the branch routers and checking PC gateway addresses. This intentionally avoids inventing unverified values.
