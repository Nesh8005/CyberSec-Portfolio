## 🔍 EXERCISE 5 — Disable Name Resolution
### 📘 Description

By default, tcpdump tries to resolve IP addresses and port numbers into domain names and service names, which can make the output messy or slower.
In this exercise, I disabled name resolution in Kali Linux to display only numeric IP addresses and ports.

### 🧩 Command Used
```bash
sudo tcpdump -r testcapture.pcap -n
```

or
```bash
sudo tcpdump -r testcapture.pcap -nn
```

### ✅ Output (Kali Linux)
reading from file testcapture.pcap, link-type LINUX_SLL2 (Linux cooked v2), snapshot length 262144
Warning: interface names might be incorrect
14:47:58.789407 eth0  B   ARP, Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:48:00.222603 eth0  B   ARP, Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:48:00.795262 eth0  B   ARP, Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:48:01.790709 eth0  B   ARP, Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:48:07.765811 eth0  B   ARP, Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:48:08.295027 eth0  B   ARP, Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:48:09.301011 eth0  B   ARP, Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:48:10.782619 eth0  B   ARP, Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:48:11.290718 eth0  B   ARP, Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:48:12.301113 eth0  B   ARP, Request who-has 192.168.11.2 tell 192.168.11.1, length 46


Notice that no hostnames or service names (like google.com or https) appear — only raw IPs and ports.

### 🖼️ Screenshot

(Add your screenshot below — for example:)

<img width="2582" height="1550" alt="image" src="https://github.com/user-attachments/assets/ef86320c-904a-4ebb-aef3-26ec43791cee" />


### 🧠 Notes

-n → Disables DNS resolution (no domain names).

-nn → Disables both DNS and port name resolution (no domain or service names).

Disabling name resolution speeds up the display and keeps output clean.

This is especially useful when analyzing raw network captures.
