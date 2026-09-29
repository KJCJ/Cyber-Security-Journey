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
| Kali VM | Attacker machine | Kali Linux, 8 GB RAM, 80 GB disk |
| Ubuntu VM | Target machine | Ubuntu Server (building next) |
| Raspberry Pi 4 | Production — runs my app | Hands-off, not part of the lab |

## Network layout

The lab runs on an **isolated network** so nothing vulnerable is ever exposed to my home LAN or the internet.

- **Host-only adapter** — the isolated lab network
- **NAT (Kali only)** — internet access for Kali updates, not the target
