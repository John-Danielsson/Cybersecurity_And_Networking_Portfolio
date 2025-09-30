# Map Your Network with Command-Line Tools

## Objective: Use common command-line tools to map local and internet connections, identify devices on your network, and view how data travels from your device to external destinations.

Tools Needed: Command Prompt (Windows) or Terminal (macOS/Linux).

I am on macOS for this exercise.

**Part 1: Local Network**

```ipconfig``` / ```ifconfig```

Windows: ```ipconfig``` | macOS/Linux: ```ifconfig```
Look for IPv4 address, subnet mask, default gateway.
Example: IPv4: ```192.168.1.10```, Subnet: ```255.255.255.0```, Gateway: ```192.168.1.1```.
ping (local)

IPv4 address: ```10.0.0.115```

Subnet mask: ```0xffffff00``` (/24)

Gateway: ```10.0.0.1```

Run: ```ping [your gateway]``` (e.g., ```ping 192.168.1.1```)

Check reply time and TTL.

Example: Reply from ```192.168.1.1```: time=1ms TTL=64 → Router is up, quick response.

Here is my output:

```
(base) JDs-MacBook-Pro-work:~ JohnDanielsson$ ping -c 1 10.0.0.1

PING 10.0.0.1 (10.0.0.1): 56 data bytes

64 bytes from 10.0.0.1: icmp_seq=0 ttl=64 time=5.800 ms
```

```arp -a```

Run: ```arp -a```
Review IP-to-MAC address mappings for local devices.
Example: ```192.168.1.1 00-14-22-01-23-45``` → Router’s MAC address.

My output:

```
(base) JDs-MacBook-Pro-work:~ JohnDanielsson$ arp -a
? (10.0.0.1) at 80:da:c2:87:65:27 on en0 ifscope [ethernet]
? (10.0.0.8) at 96:fe:b3:90:21:1a on en0 ifscope [ethernet]
? (10.0.0.30) at 30:24:a9:e5:19:59 on en0 ifscope [ethernet]
? (10.0.0.37) at d6:60:e:71:49:13 on en0 ifscope [ethernet]
? (10.0.0.49) at 16:53:ec:e4:74:a2 on en0 ifscope [ethernet]
? (10.0.0.113) at 3e:1f:af:f7:f1:27 on en0 ifscope [ethernet]
? (10.0.0.115) at ac:bc:32:ab:f9:39 on en0 ifscope permanent [ethernet]
? (10.0.0.132) at d4:57:63:bf:eb:12 on en0 ifscope [ethernet]
? (10.0.0.150) at 90:56:82:42:cf:9 on en0 ifscope [ethernet]
? (10.0.0.160) at 8e:9c:43:f4:d3:ae on en0 ifscope [ethernet]
? (10.0.0.161) at 0:9:a7:81:29:2d on en0 ifscope [ethernet]
? (10.0.0.187) at 6c:b1:33:a2:85:c6 on en0 ifscope [ethernet]
? (10.0.0.249) at 62:14:22:48:a3:ba on en0 ifscope [ethernet]
? (10.0.0.255) at ff:ff:ff:ff:ff:ff on en0 ifscope [ethernet]
mdns.mcast.net (224.0.0.251) at 1:0:5e:0:0:fb on en0 ifscope permanent [ethernet]
? (239.255.255.250) at 1:0:5e:7f:ff:fa on en0 ifscope permanent [ethernet]
```

```netstat -an```

Run: ```netstat -an```
View active TCP/UDP connections.
Example: ```TCP 192.168.1.10:49152 142.250.190.78:443 ESTABLISHED``` → Active HTTPS connection.

My output was very large, so I will just paste part of the 1st row:

```
Proto Recv-Q Send-Q  Local Address          Foreign Address        (state)    
tcp6       0      0  2601:600:c902:d9.51026 2001:558:fd02:24.443   ESTABLISHED
```


**Part 2: Internet Path**

```ping``` (public)

Run: ```ping 8.8.8.8```
Check response time and stability.
Example: ```Reply from 8.8.8.8: time=20ms TTL=117``` → Google DNS reachable.

My output:

```
^X(base) JDs-MacBook-Pro-work:~ JohnDanielsson$ ping 8.8.8.8 -c 1
PING 8.8.8.8 (8.8.8.8): 56 data bytes
64 bytes from 8.8.8.8: icmp_seq=0 ttl=115 time=16.707 ms

--- 8.8.8.8 ping statistics ---
1 packets transmitted, 1 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 16.707/16.707/16.707/0.000 ms
```

```tracert / traceroute```

Windows: ```tracert 8.8.8.8``` | macOS/Linux: ```traceroute 8.8.8.8```
View the hops from your device to the destination.
Example: Hop 1: ```192.168.1.1```, Hop 2: ISP gateway, Hop 3: upstream router, etc.
nslookup

My output:

```
(base) JDs-MacBook-Pro-work:~ JohnDanielsson$ traceroute 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 64 hops max, 52 byte packets
 1  10.0.0.1 (10.0.0.1)  5.390 ms  1.427 ms  1.297 ms
 2  10.22.111.2 (10.22.111.2)  10.701 ms
    10.22.111.3 (10.22.111.3)  9.988 ms
    10.22.111.2 (10.22.111.2)  12.060 ms
 3  po-305-316-rur02.bremerton.wa.seattle.comcast.net (68.87.160.73)  11.017 ms
    po-305-315-rur01.bremerton.wa.seattle.comcast.net (68.87.160.65)  9.461 ms
    po-305-316-rur02.bremerton.wa.seattle.comcast.net (68.87.160.73)  12.087 ms
 4  po-2-rur02.bremerton.wa.seattle.comcast.net (69.139.163.130)  12.229 ms
    po-100-xar02.bremerton.wa.seattle.comcast.net (96.216.66.145)  10.551 ms
    po-2-rur02.bremerton.wa.seattle.comcast.net (69.139.163.130)  12.588 ms
 5  be-310-arsc1.seattle.wa.seattle.comcast.net (96.216.66.133)  14.202 ms
    po-100-xar02.bremerton.wa.seattle.comcast.net (96.216.66.145)  10.473 ms
    be-310-arsc1.seattle.wa.seattle.comcast.net (96.216.66.133)  13.249 ms
 6  be-310-arsc1.seattle.wa.seattle.comcast.net (96.216.66.133)  15.010 ms
    be-36141-cs04.seattle.wa.ibone.comcast.net (68.86.93.13)  15.954 ms
    be-310-arsc1.seattle.wa.seattle.comcast.net (96.216.66.133)  27.794 ms
 7  be-2411-pe11.seattle.wa.ibone.comcast.net (96.110.32.238)  14.671 ms
    be-36141-cs04.seattle.wa.ibone.comcast.net (68.86.93.13)  13.632 ms
    be-2311-pe11.seattle.wa.ibone.comcast.net (96.110.32.234)  15.157 ms
 8  be-2111-pe11.seattle.wa.ibone.comcast.net (96.110.32.226)  16.171 ms * *
 9  * * *
10  192.178.105.41 (192.178.105.41)  17.013 ms
    209.85.243.97 (209.85.243.97)  13.350 ms
    192.178.105.141 (192.178.105.141)  15.004 ms
11  dns.google (8.8.8.8)  13.115 ms  12.368 ms  13.321 ms
```

Run: ```dig google.com```

View resolved IP addresses for the domain.

Example: Name: ```google.com```, Address: ```142.250.190.78```

My output:

```
(base) JDs-MacBook-Pro-work:~ JohnDanielsson$ dig google.com

; <<>> DiG 9.10.6 <<>> google.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 34076
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 512
;; QUESTION SECTION:
;google.com.			IN	A

;; ANSWER SECTION:
google.com.		106	IN	A	142.251.215.238

;; Query time: 15 msec
;; SERVER: 2001:558:feed::1#53(2001:558:feed::1)
;; WHEN: Mon Sep 29 19:57:52 PDT 2025
;; MSG SIZE  rcvd: 55
```


**Part 3: Routing**

```route print``` / ```netstat -r```

Windows: ```route print``` | macOS/Linux: ```netstat -r```
Check your default gateway and routing table entries.
Example: ```0.0.0.0 0.0.0.0``` ```192.168.1.1``` → All traffic goes through your router.

My output:

```
(base) JDs-MacBook-Pro-work:~ JohnDanielsson$ netstat -r
Routing tables

Internet:
Destination        Gateway            Flags           Netif Expire
default            10.0.0.1           UGScg             en0       
10/24              link#4             UCS               en0      !
10.0.0.1/32        link#4             UCS               en0      !
10.0.0.1           80:da:c2:87:65:27  UHLWIir           en0   1141
10.0.0.8           96:fe:b3:90:21:1a  UHLWI             en0   1065
10.0.0.30          link#4             UHLWIi            en0      !
10.0.0.37          d6:60:e:71:49:13   UHLWI             en0      !
10.0.0.49          16:53:ec:e4:74:a2  UHLWI             en0   1185
10.0.0.113         3e:1f:af:f7:f1:27  UHLWI             en0    717
10.0.0.115/32      link#4             UCS               en0      !
10.0.0.115         ac:bc:32:ab:f9:39  UHLWI             lo0       
10.0.0.132         d4:57:63:bf:eb:12  UHLWI             en0    785
10.0.0.160         8e:9c:43:f4:d3:ae  UHLWI             en0    783
10.0.0.187         6c:b1:33:a2:85:c6  UHLWI             en0    844
10.0.0.249         62:14:22:48:a3:ba  UHLWI             en0    975
10.0.0.255         ff:ff:ff:ff:ff:ff  UHLWbI            en0      !
127                localhost          UCS               lo0       
localhost          localhost          UH                lo0       
169.254            link#4             UCS               en0      !
224.0.0/4          link#4             UmCS              en0      !
mdns.mcast.net     1:0:5e:0:0:fb      UHmLWI            en0       
239.255.255.250    1:0:5e:7f:ff:fa    UHmLWI            en0       
255.255.255.255/32 link#4             UCS               en0      !
```

**Step 4: Wrap-Up**

**Write one interesting finding (e.g., your tracert output).**

I thought my ARP table would have way fewer entries, but when I consider the amount of Internet-connected devices in my house, it makes sense.

**How many devices appeared in your arp -a output?**

16

**What’s your average ping time to Google?**

15.005ms

### Quick Quiz

**What does ifconfig tell you?**

The command tells me the configuration of all the interfaces on my computer.

**Why use tracert instead of ping?**

To see each hop that a packet takes on the route to its destination.

**What’s one thing netstat -an shows?**

The listening ports on your computer. The command ```netstat -an``` displays all active network connections and listening ports on a computer.

The ```a``` flag means all connections and the ```n``` flag displays the connections and ports numerically.

