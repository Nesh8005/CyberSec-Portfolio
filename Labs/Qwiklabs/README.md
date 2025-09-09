# Lab 1: Install Software in a Linux Distribution

## Overview
In this lab, I used the **Advanced Package Tool (APT)** and `sudo` to install, uninstall, and reinstall applications in a Linux Bash shell. The applications demonstrated were **Suricata** (a network intrusion detection tool) and **tcpdump** (a packet capture tool).  

This lab helped me gain hands-on practice with application management in a Debian-based Linux environment.

---

## Scenario
As a security analyst, I needed to ensure that both **Suricata** and **tcpdump** were installed on my Linux system. The tasks involved:  

1. Confirming APT is installed  
2. Installing and uninstalling Suricata  
3. Installing tcpdump  
4. Listing installed applications  
5. Reinstalling Suricata  

---

## Tasks and Commands

### Task 1: Ensure APT is installed
```bash
apt
```
Expected output: version info and usage details of APT.

### Task 2: Install and Uninstall Suricata
```bash
# Install Suricata
sudo apt install suricata

# Verify installation
suricata

# Uninstall Suricata
sudo apt remove suricata

# Verify uninstallation
suricata
```
### Expected error after uninstall:
```
-bash: /usr/bin/suricata: No such file or directory
```

### Task 3: Install tcpdump
```
sudo apt install tcpdump
```
### Task 4: List Installed Applications
```
apt list --installed
```

Look for:
```
tcpdump/oldstable,now 4.9.3-1~deb10u2 amd64 [installed]
```
### Task 5: Reinstall Suricata
```
sudo apt install suricata
apt list --installed
```

Look for both applications:
```
suricata/... [installed]
tcpdump/... [installed]
```
### Key Learnings

1. Confirming the availability of package managers like APT.

2. Installing applications with dependencies.

3. Uninstalling and verifying removal of applications.

4. Checking installed packages and their versions.

5. Reinforcing best practices with sudo for system-level changes.

### Conclusion

This lab demonstrated how to effectively manage Linux applications using APT. As a security analyst, these skills are critical when deploying and verifying security tools such as Suricata and tcpdump.
