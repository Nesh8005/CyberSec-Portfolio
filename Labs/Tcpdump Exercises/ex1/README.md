## 🧠 EXERCISE 1 — Identify Network Interfaces
### 📘 Description

#### This exercise identifies the available network interfaces that can be used for packet capture using tcpdump.

### 🧩 Command Used
```bash
sudo tcpdump -D
```
### ✅ Expected Output

You’ll see a list of available interfaces:
```bash
1.enp0s3
2.lo
3.any
```
#### enp0s3 — typically the main Ethernet adapter
#### lo — the local loopback interface
#### any — captures traffic from all interfaces

The interface any can be used to capture packets from all interfaces.

### 🖼️ Screenshot

<img width="1291" height="775" alt="2025-10-07 (1)" src="https://github.com/user-attachments/assets/910a0388-044b-454b-9227-e0134fafca61" />


### 🧠 Notes

The sudo prefix is required for permission to view interfaces.

Using any is useful when you’re not sure which interface your network traffic is using.
