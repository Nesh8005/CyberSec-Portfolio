# 🧠 Suricata Lab: Examine Alerts, Logs, and Rules

## 📘 Overview
This lab demonstrates how to **analyze alerts, logs, and rules using Suricata**, an open-source **Intrusion Detection and Prevention System (IDS/IPS)** and **network analysis tool**.  

You’ll explore how Suricata detects suspicious network activity, creates alerts based on custom rules, and logs data for analysis.

---

## 🎯 Objectives
By completing this lab, you will learn to:
- Create and examine **custom Suricata rules (signatures)**  
- Use **packet capture (PCAP)** files to simulate network traffic  
- Trigger custom Suricata alerts  
- Examine log outputs in **`fast.log`** and **`eve.json`**  
- Analyze event data using **`jq`** for JSON filtering

---

## 🧩 Scenario
You are a **Security Analyst** monitoring your organization’s network for suspicious activity.  
Your tasks:
1. Configure and examine Suricata rules  
2. Trigger alerts using provided packet capture traffic  
3. Investigate log outputs to understand alert behavior  

You’ll use two files provided in your environment:
- `sample.pcap` → Simulated network traffic  
- `custom.rules` → Contains Suricata detection rules  

---

## ⚙️ Files in Use

| File | Description |
|------|--------------|
| `sample.pcap` | Contains example network traffic data for testing |
| `custom.rules` | Custom Suricata rule definitions |
| `/var/log/suricata/fast.log` | Quick alert log (deprecated but useful for QA) |
| `/var/log/suricata/eve.json` | Main JSON log containing detailed event data |

---

## 🧠 Task Breakdown

### 🧩 Task 1 – Examine a Custom Rule
Display the rule:
```bash
cat custom.rules
Example rule:
```
```bash
alert http $HOME_NET any -> $EXTERNAL_NET any (msg:"GET on wire"; flow:established,to_server; content:"GET"; http_method; sid:12345; rev:3;)
```

## Rule Components:

Action: alert – generate an alert when conditions are met

Header: defines protocol, IPs, ports, and traffic direction

## Options: specific conditions and identifiers for alerts

msg: alert message

flow: packet direction

content: keyword to match in traffic

sid: signature ID

rev: rule revision number

## 🟩 Summary: Triggers an alert when Suricata detects an HTTP GET request from $HOME_NET to $EXTERNAL_NET.

# 🧩 Task 2 – Trigger a Custom Rule
### List Suricata log directory:

```bash
ls -l /var/log/suricata
```
Run Suricata using custom rule and sample PCAP:

```bash
sudo suricata -r sample.pcap -S custom.rules -k none
```

### Command breakdown:

-r sample.pcap → process packets from the PCAP file

-S custom.rules → use custom rule set

-k none → skip checksum validation

### View alerts:

```bash
cat /var/log/suricata/fast.log
```
### Example Output:

```less
11/23/2022-12:38:34.624866 [**] [1:12345:3] GET on wire [**] {TCP} 172.21.224.2:49652 -> 142.250.1.139:80
11/23/2022-12:38:58.958203 [**] [1:12345:3] GET on wire [**] {TCP} 172.21.224.2:58494 -> 142.250.1.139:80
```
🟩 Result: Suricata detected and logged two HTTP GET alerts.

## 🧩 Task 3 – Examine eve.json Output
### Display contents:

```bash
cat /var/log/suricata/eve.json
```
Format for better readability:

```bash
jq . /var/log/suricata/eve.json | less
```
Sample Output:

```json
{
  "timestamp": "2022-11-23T12:38:34.624866+0000",
  "flow_id": 14500150016149,
  "alert": {
    "signature": "GET on wire",
    "severity": 3
  },
  "proto": "TCP",
  "dest_ip": "142.250.1.139"
}
```
🟩 Key Observations:

severity: 3

alert.signature: "GET on wire"

dest_ip: 142.250.1.139

Extract specific fields:

```bash
jq -c "[.timestamp,.flow_id,.alert.signature,.proto,.dest_ip]" /var/log/suricata/eve.json
```
Example output:

```css
["2022-11-23T12:38:34.624866+0000",14500150016149,"GET on wire","TCP","142.250.1.139"]
["2022-11-23T12:38:58.958203+0000",1647223379236084,"GET on wire","TCP","142.250.1.102"]
```
Display logs for a specific flow:

```bash
jq "select(.flow_id==14500150016149)" /var/log/suricata/eve.json
```

### 🧾 Key Takeaways
✅ Rule Creation: Defines how Suricata identifies suspicious activity
✅ Alert Triggering: Simulates traffic via PCAP to test detection
✅ Log Analysis: fast.log gives quick alerts; eve.json provides detailed JSON-based telemetry
✅ Practical Skill: Understand IDS workflows and Suricata’s real-world applications

### 🧰 Tools Used
Suricata

jq (JSON processor)

Linux Bash Shell

### 🏁 Conclusion
You have successfully:

Created and examined Suricata custom rules

Triggered alerts using simulated network data

Analyzed Suricata logs (fast.log and eve.json)

Extracted and filtered event data with jq

This hands-on exercise builds a foundational understanding of network intrusion detection and alert analysis — essential skills for any cybersecurity analyst.
