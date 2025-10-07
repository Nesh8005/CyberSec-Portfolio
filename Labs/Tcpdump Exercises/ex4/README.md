## 📖 EXERCISE 4 — Read the Saved Capture File
### 📘 Description

In this exercise, I used tcpdump on Kali Linux to read and inspect the contents of a previously saved packet capture file (testcapture.pcap).
This allows reviewing network traffic without doing a live capture.

### 🧩 Command Used
```bash
sudo tcpdump -r testcapture.pcap
```
### ✅ Output (Kali Linux)
Reading from file testcapture.pcap, link-type LINUX_SLL2 (Linux cooked v2), snapshot length 262144
Warning: interface names might be incorrect
14:47:58.789407 eth0  B   ARP, Ethernet (len 6), IPv4 (len 4), Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:48:00.222603 eth0  B   ARP, Ethernet (len 6), IPv4 (len 4), Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:48:00.795262 eth0  B   ARP, Ethernet (len 6), IPv4 (len 4), Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:48:01.790709 eth0  B   ARP, Ethernet (len 6), IPv4 (len 4), Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:48:07.765811 eth0  B   ARP, Ethernet (len 6), IPv4 (len 4), Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:48:08.295027 eth0  B   ARP, Ethernet (len 6), IPv4 (len 4), Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:48:09.301011 eth0  B   ARP, Ethernet (len 6), IPv4 (len 4), Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:48:10.782619 eth0  B   ARP, Ethernet (len 6), IPv4 (len 4), Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:48:11.290718 eth0  B   ARP, Ethernet (len 6), IPv4 (len 4), Request who-has 192.168.11.2 tell 192.168.11.1, length 46
14:48:12.301113 eth0  B   ARP, Ethernet (len 6), IPv4 (len 4), Request who-has 192.168.11.2 tell 192.168.11.1, length 46


The file is read and printed to the terminal with timestamped packet details.

### 🧩 Optional (Verbose Output)

To display more detailed protocol information:
```bash
sudo tcpdump -r testcapture.pcap -vv
```
### 🖼️ Screenshot

<img width="2582" height="1550" alt="image" src="https://github.com/user-attachments/assets/ea6bb57a-9592-4a72-9356-21d8342bfc17" />


### 🧠 Notes

The -r flag reads from a .pcap file instead of capturing live traffic.

Use -v, -vv, or -vvv for increasing levels of verbosity.

Great for offline traffic analysis after a capture session.
