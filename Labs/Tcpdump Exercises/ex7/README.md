## 🧩 EXERCISE 7 — Combine Everything
### 📘 Description

In this final exercise, I combined all the previous concepts — capturing live packets, applying filters, limiting capture count, and saving results into a .pcap file.
This command captures both HTTP (port 80) and HTTPS (port 443) traffic and stores them for analysis.

### 🧩 Command Used
```bash
sudo tcpdump -i any -c 20 -w webtraffic.pcap 'ip and (port 80 or port 443)'
```

### ✅ Output (Kali Linux)
tcpdump: WARNING: any: That device doesn't support promiscuous mode
(Promiscuous mode not supported on the "any" device)
tcpdump: listening on any, link-type LINUX_SLL2 (Linux cooked v2), snapshot length 262144 bytes
20 packets captured
33 packets received by filter
0 packets dropped by kernel


The output confirms that 20 packets were successfully captured and saved in webtraffic.pcap.

### 🖼️ Screenshot

<img width="2582" height="1550" alt="image" src="https://github.com/user-attachments/assets/03b071f4-a3e6-4e45-a849-9aa7f6c121ff" />


### 🧠 Notes

-i any → captures traffic from all interfaces.

-c 20 → limits the capture to 20 packets.

-w webtraffic.pcap → writes packets to a file instead of displaying them.

'ip and (port 80 or port 443)' → filters only HTTP and HTTPS packets.

You can later read the file using:

sudo tcpdump -r webtraffic.pcap -nn


This command is a practical example of combining interface selection, filtering, capture limits, and saving output — the core of packet analysis with tcpdump.
