# Looking at DNS and DHCP with CLI on MacOS

## Objective: Use MacOS Terminal to explore how DNS resolves domain names and how DHCP assigns your IP address — connecting these protocols to your daily internet use.

I was supposed to use Windows for this lab but I have a MacBook. Here goes.

### DHCP

I need to find the following:

1. IPv4 Address
2. DHCP Server
3. DHCP Enabled

1. I use ```ipconfig getifaddr en0``` and get ```10.0.0.115```.
2. I use ```ipconfig getpacket en0```, look for ```server_identifier (ip)``` in the output and get ```10.0.0.1```.
3. Using the command above, I look to see if the lease time is present. It is, which means that DHCP is enabled.

### DNS

Now I'll look see what the IP addresses of ```google.com``` and ```facebook.com``` are.

```dig google.com``` = ```142.251.33.78```

```dig facebook.com``` = ```57.144.216.1```

### Question for Reflection

**How does DHCP simplify network setup?**

DHCP automatically hands out IP addresses, leases, subnets, gaateways, and DNS information to hosts on its network. This means that you don't have to manually configure each device on the network. Huge time saver!
