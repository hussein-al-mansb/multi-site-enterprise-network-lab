# Verification notes and scope boundaries

## Verified by screenshot from the lab session

- JAZ-R01 and ABH-R01 OSPF adjacency with two `FULL/BDR` neighbors each.
- Both Jazan and Abha sales hosts successfully pinged `10.10.50.10` with four replies and 0% loss.
- JED-EDGE-01 PAT: `10.10.10.100` translated to `203.0.113.2`, 6 dynamic ICMP translations and hits visible.
- JED-ACCESS: three DHCP Snooping entries; Fa0/1 and Fa0/2 in `Secure-up`, sticky MAC, max 1, no violations in the final captured evidence.
- HSRP baseline on JED-CORE-01 / JED-CORE-02 with complementary Active/Standby roles for VLANs 10/20/40/50/60/99.
- HQ core VLAN tables and a Core-01 trunk table showing VLANs 10/20/40/50/60/99. Images may not cover the complete interface address inventory.
- SSH administrative access limited via VTY access-class in the shown router configuration.

## Not fully verified

- **HSRP failover:** baseline is documented, but controlled shutdown/failover and service continuity under failure are **not** shown. Do not claim a passed failover test.
- **Guest ACL enforcement:** `JED-GUEST-IN` rules are present and guest-to-private ICMP was unreachable in the screenshot, but `show ip interface vlan 40` showed `Inbound access list is not set` during the troubleshooting session. Do not attribute the block specifically to an operational ACL without additional proof. SSH VTY ACL is confirmed separately.
- **Full branch addressing table:** partial subnets are visible in routing tables, but exact per-VLAN branch gateway IPs were not all established. Complete them only from real device output.
- **Independent `.pkt` simulation:** supplied file is packaged, not executed and retested by the documentation tooling.

## Optional follow-up commands (no need to rerun for first publication)

```text
show standby brief
show ip ospf neighbor
show ip route ospf
show ip nat translations
show ip nat statistics
show ip dhcp snooping binding
show port-security interface fa0/1
show vlan brief
show interfaces trunk
show ip interface brief
show ip interface vlan 40
```

If later performing failover tests, do so on a saved **copy** of the `.pkt` file.
