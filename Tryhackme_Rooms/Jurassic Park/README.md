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
```
| Port | Service |
| ---- | ------- |
| 22   | SSH     |
| 80   | HTTP    |

🌐 Web Enumeration

Since a web server was available, the website became the main target.

Vulnerable Endpoint

item.php?id=2

