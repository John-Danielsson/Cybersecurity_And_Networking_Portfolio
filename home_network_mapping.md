# Map Your Home Network Devices

## Objective: Identify and diagram your home network devices to understand their roles, aligning with Network+ Infrastructure skills.

Tools Needed: Pen and paper or a free diagramming tool (e.g., draw.io).

LINK TO DIAGRAM: [https://drive.google.com/file/d/13hwuU4w1GG0Siy39Pv6QBeX77mV6ixbG/view?usp=sharing](https://drive.google.com/file/d/13hwuU4w1GG0Siy39Pv6QBeX77mV6ixbG/view?usp=sharing)

**Step 1: Identify Your Devices**
Walk around or think through your home network setup.
Spot your router (likely a Wi-Fi combo unit), any switches (home office?), or WAPs (Wi-Fi extenders).
Check your router’s label—does it mention firewall features?
Write down each device and its role (e.g., Router: connects to ISP, WAP: Wi-Fi for phone).

**Step 2: Diagram Your Network**
Draw a simple diagram of your setup:
Place the router in the center. Label it with its IP address (e.g., 192.168.1.1).
Connect other devices: PCs, phones, switches, printers, etc.
Mark the firewall inside the router with a shield icon if applicable.
Example: Router → Switch → PC, Printer; Router → WAP → Phone

**Step 3: Test Connectivity**
On your PC, open a browser and visit a site (e.g., google.com).
Reflect: What devices helped make that request succeed?

The devices that helped this happen are the router, the WAP, and my laptop.

**Step 4: Reflect**
Write a short paragraph answering:

**How do your devices work together?**

My home router combines a router, firewall, and WAP, but it does not have a traditional layer 2 switch.

**What’s the difference between a router, a switch, and a firewall?**

Router: directs traffic between computer networks and uses IP addresses to make forwarding decisions. Operates at OSI layer 3.

Switch: Forwards frames based on their MAC addresses to the destination port. Operates at OSI layer 2.

Firewall: permits or denies access to network traffic based on things like source IP address, protocol, or port number.
Operates at OSI layers 3 and 4 primarily, but modern firewalls can inspect traffic up to layer 7.
