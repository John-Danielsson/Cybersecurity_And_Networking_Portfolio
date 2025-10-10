# Measure Performance with iPerf

## Objective: Use iPerf to test throughput and jitter across your network, gaining insight into real-time performance.

**🛠 Tools Needed:**
iPerf3 (free, open-source)
Two devices on the same network (e.g., PC + laptop or phone)
Wi-Fi connection (2.4 GHz or 5 GHz)

**Step 1: Install and Set Up iPerf3**
Download iPerf3 on both devices (PC as server, laptop/phone as client).
No admin rights needed—just extract and run via terminal or Command Prompt.
Ensure both devices are connected to the same Wi-Fi network.

**Step 2: Run Initial Test**
On the server (e.g., PC), open terminal and run: iperf3 -s
On the client (e.g., laptop), run: iperf3 -c [server IP] (e.g., iperf3 -c 192.168.1.100)
Review output for throughput and jitter (e.g., “40 Mbps, 2 ms jitter”).
Log: “Baseline test: 40 Mbps, 2 ms jitter on 2.4 GHz.”

```
johndanielsson@JDs-MacBook-Air ~ % iperf3 -s                              
-----------------------------------------------------------
Server listening on 5201 (test #1)
-----------------------------------------------------------
Accepted connection from 10.0.0.115, port 53756
[  5] local 10.0.0.249 port 5201 connected to 10.0.0.115 port 53757
[ ID] Interval           Transfer     Bitrate
[  5]   0.00-1.00   sec  7.75 MBytes  64.8 Mbits/sec                  
[  5]   1.00-2.01   sec  14.9 MBytes   124 Mbits/sec                  
[  5]   2.01-3.01   sec  16.4 MBytes   137 Mbits/sec                  
[  5]   3.01-4.01   sec  15.4 MBytes   129 Mbits/sec                  
[  5]   4.01-5.00   sec  15.4 MBytes   129 Mbits/sec                  
[  5]   5.00-6.00   sec  18.4 MBytes   154 Mbits/sec                  
[  5]   6.00-7.01   sec  18.2 MBytes   152 Mbits/sec                  
[  5]   7.01-8.00   sec  16.9 MBytes   142 Mbits/sec                  
[  5]   8.00-9.01   sec  20.5 MBytes   171 Mbits/sec                  
[  5]   9.01-10.00  sec  18.9 MBytes   159 Mbits/sec                  
[  5]  10.00-10.14  sec  2.12 MBytes   131 Mbits/sec                  
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate
[  5]   0.00-10.14  sec   165 MBytes   136 Mbits/sec                  receiver
-----------------------------------------------------------
```

**Step 3: Simulate Load**
While running the test again, stream a video or download a large file on the client device.
Rerun the iPerf test. Are speeds down? Jitter up?
Switch to 5 GHz if available—most modern routers and devices support this.
Run test again on 5 GHz. Look for improvement (e.g., “45 Mbps, 1 ms jitter”).
Note: “Video load reduced performance. 5 GHz improved speed and reduced jitter.”

```
johndanielsson@JDs-MacBook-Air ~ % iperf3 -s
-----------------------------------------------------------
Server listening on 5201 (test #1)
-----------------------------------------------------------
Accepted connection from 10.0.0.115, port 53765
[  5] local 10.0.0.249 port 5201 connected to 10.0.0.115 port 53766
[ ID] Interval           Transfer     Bitrate
[  5]   0.00-1.01   sec  36.5 MBytes   305 Mbits/sec                  
[  5]   1.01-2.01   sec  38.1 MBytes   320 Mbits/sec                  
[  5]   2.01-3.01   sec  37.9 MBytes   318 Mbits/sec                  
[  5]   3.01-4.00   sec  34.6 MBytes   291 Mbits/sec                  
[  5]   4.00-5.01   sec  38.4 MBytes   321 Mbits/sec                  
[  5]   5.01-6.01   sec  39.0 MBytes   327 Mbits/sec                  
[  5]   6.01-7.01   sec  40.0 MBytes   336 Mbits/sec                  
[  5]   7.01-8.00   sec  38.5 MBytes   324 Mbits/sec                  
[  5]   8.00-9.00   sec  38.4 MBytes   321 Mbits/sec                  
[  5]   9.00-10.01  sec  39.1 MBytes   328 Mbits/sec                  
[  5]  10.01-10.07  sec  2.62 MBytes   357 Mbits/sec                  
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate
[  5]   0.00-10.07  sec   383 MBytes   319 Mbits/sec                  receiver
-----------------------------------------------------------
```

**Step 4: Reflect**
Write a brief reflection: What affected your performance? What conditions helped throughput improve? What did iPerf reveal about your network?
