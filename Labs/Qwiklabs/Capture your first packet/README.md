# 🧠 Lab: Capture Your First Packet

**Duration:** 1 hour  
**Level:** Introductory  
**Cost:** Free  
**Platform:** Linux (Qwiklabs environment)  
**Tools Used:** `tcpdump`, `ifconfig`, `curl`

---

## 🧩 Overview

As a **security analyst**, understanding how to capture and filter network traffic is a crucial skill.  
In this lab, I learned how to use **tcpdump** to capture, filter, and inspect live network traffic in a Linux environment.

The lab focused on:
- Identifying network interfaces
- Capturing live packets using `tcpdump`
- Saving packet captures to a `.pcap` file
- Filtering and analyzing captured packets

---

## 🧪 Scenario

I acted as a **network analyst** tasked with capturing and analyzing live traffic from a Linux virtual machine.  
The goal was to monitor packets flowing through the `eth0` network interface and save them for further analysis.

---

## ⚙️ Tasks & Commands

### **Task 1: Identify Network Interfaces**

List available interfaces using:
```bash
sudo ifconfig
```
Alternatively, identify interfaces available for packet capture:
```bash
sudo tcpdump -D
```
✅ Outcome: Identified eth0 as the main network interface for capturing traffic.

--- 

### **Task 2: Inspect Network Traffic with tcpdump**
Capture and display 5 live packets with verbose output:

```bash
sudo tcpdump -i eth0 -v -c5
```
### 📘 Options explained:

-i eth0: Capture from eth0 interface

-v: Verbose mode (more detailed packet info)

-c5: Stop after capturing 5 packets

✅ Outcome: Observed live packet data including timestamps, protocols, source/destination IPs, and TCP flags.

---

### **Task 3: Capture Network Traffic into a File**
Save captured HTTP (port 80) packets into a file:

```bash
sudo tcpdump -i eth0 -nn -c9 port 80 -w capture.pcap &
```
Generate traffic to capture:

```bash
curl opensource.google.com
``` 
Verify the file was created:

``` bash
ls -l capture.pcap
```
📘 Options explained:

-nn: Disable hostname and port resolution

-c9: Capture 9 packets

port 80: Filter only HTTP traffic

-w capture.pcap: Write packets to file

✅ Outcome: Successfully created capture.pcap file containing 9 HTTP packets.

---

### **Task 4: Filter the Captured Packet Data**
View packet headers from the saved capture:

```bash
sudo tcpdump -nn -r capture.pcap -v
```
View packet data in hexadecimal and ASCII:

```bash
sudo tcpdump -nn -r capture.pcap -X
```
#### 📘 Options explained:

-r: Read from saved capture file

-X: Display both hex and ASCII output

-v: Verbose output for detailed packet info

#### ✅ Outcome: Analyzed captured packets and viewed raw hex/ASCII data to identify patterns.

---

### 🧠 Key Learnings
1. Learned how to identify active network interfaces on Linux.

2. Understood how tcpdump captures live traffic and filters packets.

3. Gained experience saving and inspecting .pcap files.

4. Practiced reading and interpreting raw packet data.

Reinforced the importance of filtering for efficiency and security.

---
### 🧩 Commands Summary
Purpose	Command
#### List interfaces	sudo ifconfig / sudo tcpdump -D
#### Capture 5 live packets	sudo tcpdump -i eth0 -v -c5
#### Capture HTTP packets to file	sudo tcpdump -i eth0 -nn -c9 port 80 -w capture.pcap &
#### Generate HTTP traffic	curl opensource.google.com
#### Read from capture file	sudo tcpdump -nn -r capture.pcap -v
#### View capture in Hex/ASCII	sudo tcpdump -nn -r capture.pcap -X
---
### 🏁 Conclusion
Successfully completed all tasks and verified:

Network interfaces identified

Live traffic captured

Packets saved, read, and filtered

Data analyzed using verbose and hex views

This lab provided a solid foundation in packet capturing and basic network analysis using tcpdump.


<img width="1280" height="764" alt="2025-10-08" src="https://github.com/user-attachments/assets/a6834478-6daa-4070-965a-5adfbb0eae23" />
<img width="1280" height="764" alt="2025-10-08 (1)" src="https://github.com/user-attachments/assets/5321ac8b-003a-4bac-b7e0-b107516710ec" />
<img width="1280" height="764" alt="2025-10-08 (2)" src="https://github.com/user-attachments/assets/d3cd5e60-b9e9-441f-9601-da0ee46217fe" />
