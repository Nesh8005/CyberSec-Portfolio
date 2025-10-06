#  Wireshark Lab 1 — Packet Analysis

**Date:** October 6, 2025  
**Tool:** Wireshark  
**Course Module:** Introduction to Network Analysis  
**Objective:** Learn to explore, filter, and interpret captured network traffic using Wireshark.

---

##  Overview
In this lab, I acted as a security analyst investigating network traffic from a captured `.pcap` file.  
The goal was to understand how to read packets, identify key protocols (DNS, TCP, HTTP), and apply filters to isolate suspicious or relevant data.

---

##  Tools Used
- **Wireshark:** Network protocol analyzer  
- **.pcap file:** Pre-recorded network capture sample  

---

##  Learning Objectives
- Understand Wireshark’s packet list, details, and bytes panes  
- Learn how to apply filters to find specific traffic  
- Inspect DNS and TCP packets  
- Reconstruct communication using “Follow TCP Stream”  

---

##  Tasks Summary

### 1️⃣ Explore Data
- Opened `sample.pcap` in Wireshark  
- Reviewed captured packets and their metadata (No., Time, Source, Destination, Protocol, Info)  
- Noted various network protocols (ARP, DNS, TCP, HTTP)

### 2️⃣ Apply Filters
Used display filters to isolate specific packet types:
ip.addr == 192.168.1.5
dns
tcp.port == 80


### 3️⃣ Inspect DNS Queries
- Identified DNS requests made by the host machine  
- Mapped queried domains to resolved IP addresses  

### 4️⃣ Follow TCP Stream
- Reconstructed an HTTP session between client and server  
- Observed GET and POST requests  
- Learned how Wireshark can reassemble full conversation data  

---

##  Key Takeaways
- Each packet captured represents a snapshot of communication between devices.  
- Filters make it easier to identify suspicious or relevant traffic.  
- Following TCP streams helps analysts see entire conversations.  
- DNS is a valuable starting point for detecting abnormal activity.

---

##  Example Filters
| Purpose | Wireshark Filter |
|----------|------------------|
| Show DNS traffic | `dns` |
| Show HTTP traffic | `http` |
| Show packets from a specific IP | `ip.addr == 192.168.1.10` |
| Show TCP traffic on port 443 | `tcp.port == 443` |

---


---

##  Reflection
This lab helped reinforce my understanding of how network communication works behind the scenes.  
It also showed how Wireshark can be used for real-world incident response and forensic investigations.



