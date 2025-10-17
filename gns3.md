# Simulate Routing & Infrastructure with GNS3

## Objective: Build a tiny routed network in GNS3 with two routers and two PCs, enable dynamic routing (OSPF), verify end-to-end connectivity, and practice basic failure testing.

**🛠 What You Need**
GNS3 installed (local is fine)
Routers: Choose one
VyOS (recommended, free/open-source), or
Cisco IOS/vIOS (licensed & provided by you)
Two VPCS nodes (built into GNS3)

**Step 1 — Topology & IP Plan**

Drag into the workspace: R1, R2, PC1 (VPCS), PC2 (VPCS). Cable like this:
```
PC1 ── R1 ── R2 ── PC2

R1 LAN  (to PC1): 192.168.1.0/24   R1 LAN IP: 192.168.1.1
R2 LAN  (to PC2): 192.168.2.0/24   R2 LAN IP: 192.168.2.1
R1↔R2 link        : 10.0.0.0/30     R1: 10.0.0.1, R2: 10.0.0.2

PC1 IP: 192.168.1.10/24  GW 192.168.1.1
PC2 IP: 192.168.2.10/24  GW 192.168.2.1
```
**Step 2 — Configure the PCs (VPCS)**
```
# On PC1 console
ip 192.168.1.10/24 192.168.1.1

# On PC2 console
ip 192.168.2.10/24 192.168.2.1
```
**Step 3 — Configure the Routers**
Pick the set that matches your router image.

A) Cisco IOS / vIOS
```
! R1 (interfaces may be Gi0/0, Gi0/1, etc. Adjust to your device)
enable
conf t
interface g0/0
 ip address 192.168.1.1 255.255.255.0
 no shutdown
interface g0/1
 ip address 10.0.0.1 255.255.255.252
 no shutdown
router ospf 1
 network 192.168.1.0 0.0.0.255 area 0
 network 10.0.0.0 0.0.0.3 area 0
end
wr

! R2
enable
conf t
interface g0/0
 ip address 10.0.0.2 255.255.255.252
 no shutdown
interface g0/1
 ip address 192.168.2.1 255.255.255.0
 no shutdown
router ospf 1
 network 10.0.0.0 0.0.0.3 area 0
 network 192.168.2.0 0.0.0.255 area 0
end
wr
```
B) VyOS (free)
```
# R1
configure
set interfaces ethernet eth0 address 192.168.1.1/24
set interfaces ethernet eth1 address 10.0.0.1/30
set protocols ospf area 0 network 192.168.1.0/24
set protocols ospf area 0 network 10.0.0.0/30
commit; save; exit

# R2
configure
set interfaces ethernet eth0 address 10.0.0.2/30
set interfaces ethernet eth1 address 192.168.2.1/24
set protocols ospf area 0 network 10.0.0.0/30
set protocols ospf area 0 network 192.168.2.0/24
commit; save; exit
```
**Step 4 — Verify OSPF & Connectivity**

OSPF neighbors come up
IOS: show ip ospf neighbor
VyOS: show ip ospf neighbor

Routes are learned
IOS: show ip route ospf
VyOS: show ip route (look for OSPF routes)

End-to-end ping
From PC1: ping 192.168.2.10 (should succeed)
From PC2: ping 192.168.1.10

**Step 5 — Quick Failure Test**

In GNS3, shut down the R1↔R2 link (right-click interface → Disable) or bring one router down.
Try the ping again from PC1 to PC2 (it should fail).
Re-enable the link; pings should recover once OSPF adjacencies reconverge.

**✅ Deliverables**

Screenshot of topology with node labels and interface links.
Screenshot of show ip ospf neighbor (or VyOS equivalent) showing FULL adjacency.
Screenshot of a successful ping from PC1 to PC2.

**🎯 Stretch (Optional)**

Add an ACL/firewall rule on R2 to block ICMP from 192.168.1.0/24 and observe how it affects pings.
Change OSPF hello/dead timers on the R1↔R2 link and measure convergence.
Add a second link between R1 & R2 and enable OSPF cost changes to prefer one path.

**🧠 Reflect**

Why do we advertise both the LAN and the inter-router link into OSPF?

What did the failure test tell you about dynamic routing vs static routing?

Where would segmentation or ACLs live in this tiny design, and why?
