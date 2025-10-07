# Network Services and Applications in Action

## Objective: Explore common network services like DHCP, DNS, and NTP using built-in tools, and build familiarity with how your computer communicates on the network.

🔓 Explore Services with Command Prompt

🛠 Tools Needed:
Computer
Command Prompt
Internet access

**Step 1: Check DHCP**
Open Terminal.
Type ```ipconfig getpacket en0```

Here's my DHCP server IP address: ```server_identifier (ip): 10.0.0.1```

**Step 2: Test DNS**
Type ```dig google.com``` — it should return an IP and show your DNS server.
Try ```dig facebook.com``` for comparison.

```dig google.com``` on MacOS gets me the IP address for Google: ```142.250.217.110```
```dig facebook.com``` on MacOS gets me the IP address for Facebook: ```57.144.216.1```

However, to find my DNS server I have to use the command ```ipconfig getpacket en0``` and look for the field ```domain_name_server (ip_mult):```, which gets me ```{75.75.75.75, 75.75.76.76}```


**Step 3: Check NTP**
Type ```sudo systemsetup -getnetworktimeserver```

Source: ```time.apple.com```

Type ```sntp time.apple.com```

Output: ```+0.000480 +/- 0.029337 time.apple.com 2620:149:a00:3000::1f2```

Explanation:

```+0.000480``` = my computer is ahead of the Apple NTP server by 0.000480 seconds.

```+/- 0.029337``` = my computer's time has a margin of error equal to +/- 0.029337 seconds.

```2620:149:a00:3000::1f2``` = IPv6 address of Apple NTP server.

In other words, my computer is very closely synchronized to the Apple NTP server.

**Step 4: Reflect**
Write a short paragraph: How do DHCP, DNS, and NTP each keep your network running smoothly?

DHCP automatically assigns IP addresses and other network parameters like DNS server, subnet mask, and gateway to hosts on a network,
negating the need to manually configure each device on the network.

DNS resolves domain names to IP addresses and vice versa, making web browsing much easier for humans.
DNS makes it so that you don't have to type in the IP address of the website you want to visit!

NTP ensures that your computer and all other computers you communicate agree on what time it is.
This is critical for coordinating networked systems (among other things), because if devices communicating with each other
don't agree on the time of day, this can trip up time-dependent processes like authentication, logging, and packet TTL.
