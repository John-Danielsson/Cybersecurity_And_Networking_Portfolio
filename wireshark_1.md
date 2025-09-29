# Tracing and Analyzing Packets with WireShark

## Objective: Use tracert/traceroute and Wireshark to visualize packet flow through routers and strengthen Network+ troubleshooting skills.

Tools Needed:

- Command Prompt (Windows) or Terminal (Linux/macOS)
- Wireshark (free, open-source packet analyzer)

### Step 1: Trace Your Router’s Path

Windows: Open Command Prompt → ```tracert google.com```
Linux: Open Terminal → ```traceroute google.com``` (Install with sudo apt install traceroute if needed)

Here is my Terminal's (I'm on macOS) 1st line of output for ```traceroute google.com```:

```
(base) JDs-MacBook-Pro-work:~ JohnDanielsson$ traceroute google.com

traceroute to google.com (142.250.217.110), 64 hops max, 52 byte packets

 1  10.0.0.1 (10.0.0.1)  3.251 ms  1.358 ms  1.433 ms
```



### Step 2: Capture Router Traffic

Open Wireshark and select your active network interface (Wi-Fi or Ethernet).

Click the green shark fin icon to start capturing.

In CMD/Terminal, run: ```ping google.com```

Let it run ~10 pings, then stop the capture (red square icon).

### Step 3: Analyze with Wireshark

In the filter bar, type icmp and press Enter to isolate ping traffic.
Look for echo requests and replies.
Note IP addresses: your router (e.g., 192.168.1.1) and Google (e.g., 142.250.190.78).
Optional: Run arp -a (Windows) or ip neigh (Linux) to find MAC addresses.
Example observation: “Router at 192.168.1.1 forwarded ICMP echo requests to Google.”

### Step 4: Reflect

**How did tracert/traceroute reveal the router’s role?**

I saw how many hops were required for the packets from my computer to travel to ```google.com```. That showed me how the router helps me access information from the wider Internet and also delivers information to me in the form of packets.

**What did Wireshark add to your understanding?**

Even just letting WireShark run for 30 seconds resulted in hundreds of packets.
I didn't have any good real-time visual for just how much information is flying around the Internet, even in my small home Wi-Fi network.
WireShark also gave me a better sense of different protocols are used for different purposes across the Internet.
For example, my ```ping``` requests used the ICMP protocol instead of something like UDP, which makes sense since ICMP is used by network devices to send operational information to each other.

**How did Wireshark help you understand the role of ports in communication? What did you learn about protocol-port relationships?**

I got a visual representation of how ports designate what type of service or protocol is being executed. It helped me understand that port numbers guide traffic to the correct service. An analogy would be that packets are letters, port numbers are mail slots, and protocols are the language that the letter is written in.
