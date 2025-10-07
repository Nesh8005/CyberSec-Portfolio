# 📶 EXERCISE 2 — Capture a Few Packets
## 📘 Description

#### In this exercise, I captured a small number of live network packets using tcpdump on Kali Linux.
#### This helps visualize how data travels between IP addresses in real time.

### 🧩 Command Used
```bash
sudo tcpdump -i any -c 5
```

### ✅ Output (Kali Linux)
tcpdump: WARNING: any: That device doesn't support promiscuous mode
(Promiscuous mode not supported on the "any" device)
tcpdump: verbose output suppressed, use -v[v]... for full protocol decode
listening on any, link-type LINUX_SLL2 (Linux cooked v2), snapshot length 262144 bytes
14:43:58.795072 eth0  B   ARP, Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:43:58.801129 eth0  Out IP 192.168.11.131.35235 > 192.168.11.2.domain: 24125+ PTR? 2.11.168.192.in-addr.arpa. (43)
14:43:58.812838 eth0  In  IP 192.168.11.2.domain > 192.168.11.131.35235: 24125 NXDomain 0/0/0 (43)
14:43:58.813304 eth0  Out IP 192.168.11.131.36997 > 192.168.11.2.domain: 52467+ PTR? 1.11.168.192.in-addr.arpa. (43)
14:43:58.824238 eth0  In  IP 192.168.11.2.domain > 192.168.11.131.36997: 52467 NXDomain 0/0/0 (43)
5 packets captured
7 packets received by filter
0 packets dropped by kernel



#### Each line shows a captured packet with timestamps, IPs, and protocol info.

### 🖼️ Screenshot

<img width="1291" height="775" alt="2025-10-07 (9)" src="https://github.com/user-attachments/assets/dce79fca-2647-4505-ba84-f983ba3bdc30" />


### 🧠 Notes

The -i any flag captures packets across all interfaces.

The -c 5 flag limits capture to 5 packets only.

Use Ctrl + C to stop capturing early.

This command is great for testing your tcpdump setup before deeper analysis.
