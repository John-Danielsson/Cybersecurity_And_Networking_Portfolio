# Set Up an IPv6 Virtual Network in Azure (Beginner)

## Objective: Create a Virtual Network (VNet) that includes IPv6, add an IPv6 subnet, and understand where IPv6 ranges live in the Azure Portal. No CLI, no VMs—just the portal and screenshots.

Estimated time: 15–20 minutes

**🛠 What You Need**
An Azure account (free tier is fine)
Access to the Azure Portal
Finished Day 21 (you can reuse the same resource group)

**Step 1 — Open Your Resource Group**

In the Portal, search Resource groups → open HL-Networking-RG (or create it if you skipped Day 21).

**Step 2 — Create a Dual-Stack VNet (IPv4 + IPv6)**

Create a resource → search Virtual Network → Create.
Resource group: HL-Networking-RG
Name: HL-IPv6-VNet
Region: same as your RG.
Go to the IP addresses tab:
IPv4 address space: 10.22.0.0/16
IPv6: set to Enabled
IPv6 address space: use a documentation range like 2001:db8:22::/48 (good for screenshots/learning)
Continue to Review + create → Create.

**Step 3 — Add an IPv6 Subnet**

Open HL-IPv6-VNet → left menu Subnets → + Subnet.
Subnet name: IPv6Subnet
IPv4 subnet address range (optional): you can leave blank if you want a pure IPv6 subnet for this exercise.
IPv6 subnet → set to Enabled → Address range (IPv6): 2001:db8:22:1::/64
Add to save.

**Step 4 — Explore What You Built**

On the VNet Overview, confirm you see both:
IPv4: 10.22.0.0/16
IPv6: 2001:db8:22::/48
Open Subnets → select IPv6Subnet → confirm the IPv6 range 2001:db8:22:1::/64.
Concept check: IPv6 hosts typically use a /64 subnet so they can do SLAAC (auto-addressing).

**Step 5 — (Optional, Easy) Add One IPv6 Security Rule**

If you’re comfortable, attach a simple NSG with a single allow rule—purely for learning/visuals. (No VMs are required.)

1. Create a resource → Network security group → Name: HL-IPv6-NSG → same RG/Region → Create.
2. Open the NSG → Inbound security rules → Add:
Name: Allow-HTTPS | Priority: 100 | Protocol: TCP | Port: 443 | Action: Allow.
3. Associate it to your subnet: NSG → Subnets → Associate → VNet HL-IPv6-VNet → Subnet IPv6Subnet.
4. Concept: NSGs are dual-stack—they apply to both IPv4 and IPv6 traffic.

**✅ Deliverables**

Screenshot: HL-IPv6-VNet Overview with both IPv4 and IPv6 address spaces visible.

<img width="999" height="688" alt="Screenshot 2025-10-16 at 11 26 56" src="https://github.com/user-attachments/assets/162e31f2-692a-4c0e-951f-b63ab057e8a8" />

Screenshot: Subnets blade showing IPv6Subnet and its /64 range.

<img width="1466" height="684" alt="Screenshot 2025-10-16 at 11 27 44" src="https://github.com/user-attachments/assets/87b650f9-ed2f-4ffe-836a-0323e7f4e3a9" />

(Optional) Screenshot: HL-IPv6-NSG inbound rules table showing Allow-HTTPS (priority 100).

<img width="1470" height="671" alt="Screenshot 2025-10-16 at 11 28 21" src="https://github.com/user-attachments/assets/c855bc74-f7ba-4a83-b6c0-5f1ffb8bc47f" />

1–2 sentences: “Why do many IPv6 subnets use /64?”

Answer: /64 is the default subnet size for IPv6 LANs.

**🎯 Stretch (Only if you feel good)**

Add a second IPv6 subnet 2001:db8:22:2::/64 named IPv6Private. Explain one reason you’d keep it separate from IPv6Subnet.

<img width="1470" height="480" alt="Screenshot 2025-10-16 at 11 30 39" src="https://github.com/user-attachments/assets/3032651a-302f-427d-83f0-9c5193eb46d6" />

Create (but don’t deploy) a Public IP (IPv6) resource in the portal to see where you’d attach it to a VM/NIC later.

Write a pretend DNS note: “AAAA record points www.example.test → 2001:db8:22:1::10.” (AAAA = IPv6, A = IPv4.)

**🧠 Quick Ref**

IPv6 address space on the VNet = the big range (e.g., /48).
IPv6 subnet = a slice inside the VNet (commonly /64 for hosts/SLAAC).
AAAA DNS record = “IPv6 address for a hostname.”
Tip: 2001:db8::/32 is a documentation-only range—great for screenshots and learning.

**🧹 Clean Up (recommended)**

If you’re done, delete to avoid clutter:

Open Resource groups → HL-Networking-RG → Delete resource group → confirm name.
Lab Summary: You created a dual-stack VNet, added an IPv6 /64 subnet, and (optionally) attached an NSG rule—all in the Azure Portal. You now know where IPv6 lives in Azure and what a /48 vs /64 means at a beginner level.
