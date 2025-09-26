# Subnetting Basics

## Objective: Break down a /24 network into four /26 subnets by hand, then verify with a subnet calculator.

### Calculating By Hand

Here is a /24 network mask in decimal format: 255.255.255.0

To convert the /24 mask into /26, I need to borrow 2 bits from the host portion of the IP address.

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
| 1 | 192.168.1.0 - 192.168.1.63 | 192.168.1.0 | 192.168.1.63 | 192.168.1.1 - 192.168.1.62 |
| 2 | 192.168.1.64 - 192.168.1.127 | 192.168.1.64 | 192.168.1.127 | 192.168.1.65 - 192.168.1.126 |
| 3 | 192.168.1.128 - 192.168.1.191 | 192.168.1.128 | 192.168.1.191 | 192.168.1.129 - 192.168.1.190 |
| 4 | 192.168.1.192 - 192.168.1.255 | 192.168.1.192 | 192.168.1.255 | 192.168.1.193 - 192.168.1.254 |

### Questions For Reflection

**What does “borrowing bits” mean?**

Using up bits that would normally be in the host portion of the IP address for designating the subnet that the IP address belongs to.

**How do the network and broadcast addresses define the usable range?**

The usable range is the range of addresses that can be assigned to hosts within a given subnet. The network address is the first address of the subnet and the broadcast address is the last address of the subnet. In more general terms: The host portion of the IP address starts with a multiple of the block size. In this case, it would be .0, .64, .128, and so on. The broadcast address is the network address plus the block size minus 1. That would be .63, .127, and .191 for the preceding network addresses, respectively.

### Bonus

[CIDR Visualization](https://drive.google.com/file/d/1dzxVR1wFQAB7k2pFL8Mz9WPAXTTv-u0_/view?usp=sharing)
