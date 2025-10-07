## 💾 EXERCISE 3 — Save Captured Packets to a File
### 📘 Description

In this exercise, I used tcpdump on Kali Linux to capture live network packets and save them into a .pcap file.
This allows me to analyze the traffic later using tools like Wireshark.

### 🧩 Command Used
sudo tcpdump -i any -c 10 -w testcapture.pcap

### ✅ Output (Kali Linux)
tcpdump: WARNING: any: That device doesn't support promiscuous mode
(Promiscuous mode not supported on the "any" device)
tcpdump: listening on any, link-type LINUX_SLL2 (Linux cooked v2), snapshot length 262144 bytes
10 packets captured
10 packets received by filter
0 packets dropped by kernel


The capture file testcapture.pcap is now saved in the current directory.

### 🖼️ Screenshot

<img width="2582" height="1550" alt="image" src="https://github.com/user-attachments/assets/e2e6a7eb-6deb-448b-ae68-a8d602fdff78" />


### 🧠 Notes

The -w flag writes the output to a file instead of displaying it on the screen.

You can later read this file using:
```bash
sudo tcpdump -r testcapture.pcap
```

.pcap files can be opened in Wireshark for a detailed GUI analysis.

Always confirm that the file has been created using:
```bash
ls -l testcapture.pcap
```
