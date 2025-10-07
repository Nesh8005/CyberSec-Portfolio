## 🎯 EXERCISE 6 — Filter Specific Packets
### 📘 Description

In this exercise, I learned how to filter specific packets in Kali Linux using tcpdump.
Filtering helps narrow down traffic by protocol, port, or IP address, making packet analysis more focused and efficient.

### 🧩 Command Used

To capture only HTTP (port 80) traffic:

sudo tcpdump -i any port 80


You can also filter by protocol, IP, or a combination:

sudo tcpdump -i any tcp
sudo tcpdump -i any host 192.168.56.101
sudo tcpdump -i any port 443

### ✅ Output (Kali Linux Example)
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on any, link-type LINUX_SLL (Linux cooked), capture size 262144 bytes
10:52:45.987654 IP 192.168.56.101.49212 > 172.217.194.138.80: Flags [S], seq 12345, win 64240, length 0
10:52:46.001234 IP 172.217.194.138.80 > 192.168.56.101.49212: Flags [S.], seq 67890, ack 12346, win 65535, length 0
10:52:46.003456 IP 192.168.56.101.49212 > 172.217.194.138.80: Flags [.], ack 67891, win 64240, length 0


The capture now shows only packets on port 80 (HTTP) — filtering out all unrelated traffic.

### 🖼️ Screenshot

<img width="2582" height="1550" alt="image" src="https://github.com/user-attachments/assets/6f3c3b39-ed81-483e-a934-7fb846a034ce" />


### 🧠 Notes

port 80 → captures only HTTP traffic

port 443 → captures only HTTPS traffic

host <IP> → captures traffic to or from a specific IP

tcp / udp → filters by protocol type

Combine multiple filters using logical operators:

sudo tcpdump -i any 'tcp and port 80'
sudo tcpdump -i any 'ip and host 8.8.8.8'


Filtering makes captures faster and the output easier to analyze.
