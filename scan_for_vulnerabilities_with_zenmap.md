# Scan for Vulnerabilities with Nmap

## Objective: Use Nmap to scan your system for open ports and identify active services—an essential step in understanding network security risks.

## 🛠 Tools Needed:
Nmap (free)
Windows, Linux, or Mac PC
Internet access

**Step 1: Install Nmap**
Download and install Nmap from nmap.org.
Windows users: Zenmap GUI is included (optional).
Mac/Linux users: Use the terminal for CLI scans.

Despite what the instructions say, I have Zenmap GUI on my MacBook.

**Step 2: Scan Your Own Device**
Find your IP address using ipconfig (Windows) or ifconfig (Linux/macOS).
In Zenmap, set Target to your IP address (e.g., 192.168.1.100).
Select the “Quick Scan” profile and start the scan.
Example Output: Port 80 (HTTP), Port 443 (HTTPS), Port 53 (DNS) open.
Note: “Found open ports: 80, 443, 53—web and DNS services running.”

Here's what ```ifconfig``` says is my MacBook's IP address: ```10.0.0.241```.

With that, this is the output I get with a quick scan on Zenmap with my IP address above as the target:

<img width="427" height="113" alt="Screenshot 2025-10-07 at 19 14 02" src="https://github.com/user-attachments/assets/2f0c1b1b-dadd-49dd-9136-cd32ebfecbdd" />


**Step 3: Analyze the Results**
Review each open port and what service it represents.
Is HTTP (port 80) open but HTTPS (443) missing? That could be a security concern.
Unexpected services like Telnet (port 23) or FTP (port 21)? Those should be disabled unless needed.
Tip: Compare your results to the expected ports from Day 14 (DHCP, NTP, DNS).
Record something like: “Port 443 and 53 expected, port 23 open—potential Telnet risk.”

There is only 1 port open: 5000 TCP running the "UPNP" service. I have no idea what that is, so I will look it up.

Apparently UPnP is Universal Plug n Play. From the perspective of devices scanning my laptop, port 5000 is open for external connections.
UPnP allows devices to discover each other and establish network services for sharing data, media streaming, and device management.

All the other common ports (e.g. 443 for HTTPS) are either closed or protected by a firewall.

**Step 4: Reflect**
Write a short paragraph: What risks did Nmap reveal? How do open ports translate to real-world vulnerabilities?

Nmap revealed that I may have a security risk on port 5000, in the sense that someone may be able to establish an unauthorized connection with my computer.
Therefore, I will block that port. It helps that I don't ever use AirPlay, which uses port 5000.
