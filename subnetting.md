# Subnetting Basics

Objective: Break down a /24 network into four /26 subnets by hand, then verify with a subnet calculator.

Here is a /24 network mask in decimal format: 255.255.255.0

To convert the /24 mask into /26, I need to add 2 bits to the last octet.

256 - 2 ^ (8 - 2) = 256 - 64 = 192

Therefore, the /26 mask is:

255.255.255.192

The block size is calculated by substracting 2 from 8, then raising 2 to that power.

2 ^ (8 - 2) = 2 ^ 6 = 64

This also means 62 usable host addresses per subnet.

Here is the example IP Address I will use for this exercise: 192.168.1.0

Since there are 4 /26 subnets, the address ranges are as follows:

| Subnet | IP Address Range | Network | Broadcast | Usable |
|---|---|---|---|---|
| 0 | 192.168.1.0 - 192.168.1.63 | 192.168.1.0 | 192.168.1.63 | 192.168.1.1 - 192.168.1.62 |
| 1 | 192.168.1.64 - 192.168.1.127 | 192.168.1.64 | 192.168.1.127 | 192.168.1.65 - 192.168.1.126 |
| 0 | 192.168.1.128 - 192.168.1.191 | 192.168.1.128 | 192.168.1.191 | 192.168.1.129 - 192.168.1.190 |
| 0 | 192.168.1.192 - 192.168.1.255 | 192.168.1.192 | 192.168.1.255 | 192.168.1.193 - 192.168.1.254 |
