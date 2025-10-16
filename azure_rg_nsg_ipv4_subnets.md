# Azure Virtual Network (Beginner)

## Objective: Create a single Virtual Network (VNet) with one subnet in the Azure Portal—no CLI, no VMs. You’ll see where IP ranges live in the portal and take a couple of screenshots for your notes.

Estimated time: 15–20 minutes

**🛠 What You Need**
- An Azure account (free tier is fine)
- Access to the Azure Portal

**Step 1 — Create a Resource Group**

In the Portal, search for Resource groups → click Create.
Resource group: HL-Networking-RG
Region: pick the closest to you (e.g., East US).
Click Review + create → Create.

**Step 2 — Create a VNet with One Subnet**

Click Create a resource → search Virtual Network → Create.
Resource group: HL-Networking-RG
Name: HL-VNet
Region: same region as your RG.
IPv4 address space: 10.0.0.0/16 (leave IPv6 off).
Go to the IP addresses tab:
Edit the default subnet to:
Subnet name: PublicSubnet
Subnet address range: 10.0.1.0/24
Review + create → Create (wait ~1 minute).

**Step 3 — Explore What You Built**

Open HL-VNet → on the Overview page, note the Address space 10.0.0.0/16.
Click Subnets → confirm PublicSubnet uses 10.0.1.0/24.
Concept check: /16 is the big private network; your /24 is a smaller slice inside it.

**Step 4 — (Optional, Easy) Add a Simple Security Rule**

If you’re comfortable, create a single “allow HTTPS” rule with a Network Security Group (NSG). If not, skip this step.

Create resource → Network security group → Name: HL-Web-NSG → same RG/Region → Create.
Open HL-Web-NSG → Inbound security rules → Add:
Name: Allow-HTTPS | Priority: 100 | Protocol: TCP | Port: 443 | Action: Allow.
Associate it to your subnet: NSG → Subnets → Associate → VNet HL-VNet → Subnet PublicSubnet.

**✅ Deliverables**

Screenshot of HL-VNet Overview with the Address space visible.

<img width="732" height="640" alt="hl_vnet" src="https://github.com/user-attachments/assets/55b75724-dad3-45d7-87e0-ba4fa23f9347" />

Screenshot of the Subnets blade showing PublicSubnet and 10.0.1.0/24 and PrivateSubnet and 10.0.2.0/24.

<img width="1461" height="641" alt="subnets" src="https://github.com/user-attachments/assets/43641f68-0a57-4afa-b96a-753fd113d50e" />

(Optional) Screenshot of HL-Web-NSG inbound rules table (showing Allow-HTTPS priority 100).

<img width="1466" height="520" alt="Screenshot 2025-10-16 at 10 23 09" src="https://github.com/user-attachments/assets/cacc990a-b986-4bb1-9f82-f4b0030af67c" />

1–2 sentences: “What’s the difference between the VNet address space and a subnet range?”

The VNet address range is much larger than the subnet ranges. The subnets are slices of the VNet address range so by definition they have to be smaller than the VNet address range.

**🎯 Stretch**

Add a second subnet PrivateSubnet at 10.0.2.0/24 and explain one reason you’d keep it separate from PublicSubnet.
Rename things clearly (resource group, VNet, subnets) so screenshots tell a story for your portfolio.

My answer: if I were running a company, I would want a private subnet for my employees' use only and a public subnet for guests' use. This setup would make sense in a very large restaurant or mixed use building. See the above screenshots.

**🧠 Quick Ref**

VNet = your private network in Azure (big range, e.g., 10.0.0.0/16).
Subnet = a smaller slice inside the VNet (e.g., 10.0.1.0/24).
NSG = simple firewall you can attach to a subnet to allow/deny traffic.
