# Map Your Network with Command-Line Tools

## Objective: Use common command-line tools to map local and internet connections, identify devices on your network, and view how data travels from your device to external destinations.

Tools Needed: Command Prompt (Windows) or Terminal (macOS/Linux).

**Part 1: Local Network**

```ipconfig``` / ```ifconfig```

Windows: ```ipconfig``` | macOS/Linux: ```ifconfig```
Look for IPv4 address, subnet mask, default gateway.
Example: IPv4: ```192.168.1.10```, Subnet: ```255.255.255.0```, Gateway: ```192.168.1.1```.
ping (local)

Run: ```ping [your gateway]``` (e.g., ```ping 192.168.1.1```)

Check reply time and TTL.

Example: Reply from ```192.168.1.1```: time=1ms TTL=64 → Router is up, quick response.

```arp -a```

Run: ```arp -a```
Review IP-to-MAC address mappings for local devices.
Example: ```192.168.1.1 00-14-22-01-23-45``` → Router’s MAC address.

```netstat -an```

Run: ```netstat -an```
View active TCP/UDP connections.
Example: ```TCP 192.168.1.10:49152 142.250.190.78:443 ESTABLISHED``` → Active HTTPS connection.


**Part 2: Internet Path**

```ping``` (public)

Run: ```ping 8.8.8.8```
Check response time and stability.
Example: ```Reply from 8.8.8.8: time=20ms TTL=117``` → Google DNS reachable.

```tracert / traceroute```

Windows: ```tracert 8.8.8.8``` | macOS/Linux: ```traceroute 8.8.8.8```
View the hops from your device to the destination.
Example: Hop 1: ```192.168.1.1```, Hop 2: ISP gateway, Hop 3: upstream router, etc.
nslookup

Run: ```nslookup google.com```

View resolved IP addresses for the domain.

Example: Name: ```google.com```, Address: ```142.250.190.78```



**Part 3: Routing**

```route print``` / ```netstat -r```

Windows: ```route print``` | macOS/Linux: ```netstat -r```
Check your default gateway and routing table entries.
Example: ```0.0.0.0 0.0.0.0``` ```192.168.1.1``` → All traffic goes through your router.

**Step 4: Wrap-Up**

Share: Post one interesting finding (e.g., your tracert output) in the challenge group or forum.

Reflect: How many devices appeared in your arp -a output? What’s your average ping time to Google?

### Quick Quiz

**What does ipconfig tell you?**



**Why use tracert instead of ping?**



**What’s one thing netstat -an shows?**


