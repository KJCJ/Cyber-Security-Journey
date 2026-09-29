# Home Lab

This folder documents my home lab: the hardware, the network layout, the tools I run, and how I keep it safe. It's where I practise against deliberately vulnerable targets.

## Purpose

- Build a repeatable environment for web, network and (later) cloud security practice
- Get hands-on with Linux, Docker, networking and common security tooling
- Document what I build and what I learn along the way

## Hardware and machines

| Device | Role | Notes |
|---|---|---|
| Laptop (host) | Runs VirtualBox and Kali | Windows |
| Kali VM | Attacker machine | Kali Linux, 8 GB RAM, 80 GB disk, IP 192.168.56.102 |
| Ubuntu VM | Target machine | Ubuntu Server 24.04, 2 GB RAM, 20 GB disk, IP 192.168.56.101 |
| Raspberry Pi 4 | Production — runs my app | Hands-off, not part of the lab |

## Network layout

The lab runs on an **isolated network** so nothing vulnerable is ever exposed to my home LAN or the internet.

- **Host-only adapter** — the isolated lab network (192.168.56.0/24)
- **NAT (Kali only)** — internet access for Kali updates, not the target

### Verified

- Kali (192.168.56.102) can reach Ubuntu (192.168.56.101) on the isolated network
- Ubuntu target has no internet route — no exposure
- Confirmed with `ping` and `ip route` from both machines

## Software and tooling

- **Kali VM:** Burp Suite, Nmap, Wireshark, Metasploit, sqlmap
- **Ubuntu target:** Ubuntu Server 24.04 LTS, OpenSSH server installed
- **Local AI assistant:** Ollama running Dolphin-Mistral for offline analysis of code and security concepts (no data leaves the machine)

## Why isolation matters

The target VM is deliberately vulnerable. If it could reach the internet, it would be exposed. If it could reach my home network, it would be a foothold inside my house. Isolation ensures the only traffic it sees is from my attacker VM.

## How I isolate the lab

- Target sits on the host-only adapter with no route out
- Host firewall blocks the lab subnet from reaching my home network
- Snapshots are taken before each exercise so I can roll back
- Only systems I own or that are designed for training are targeted

## What I'm practising

- Web vulnerabilities: IDOR, SQL injection, XSS, CSRF (OWASP Top 10)
- Network scanning and enumeration with Nmap and Wireshark
- Linux hardening and log review
- Writing up findings in a clear, reproducible way

## What I've learned so far

- Setting up isolated VMs in VirtualBox
- Using host-only networking to separate attacker and target from the internet
- Verifying isolation with `ping` and `ip route`
- Documenting findings so someone else can reproduce them

## Next steps

- Add a vulnerable web app target (DVWA or OWASP Juice Shop)
- Add cloud security practice (AWS free tier)
- Add a SIEM (Wazuh or Elastic) for blue team practice
- Automate lab setup with Docker Compose

## Write-ups from this lab

- [Finding and fixing an IDOR in my own app](../writeups/idor.md)
