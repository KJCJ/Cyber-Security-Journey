# OSINT Investigation: Unmasking an Impersonation Account

**Date:** October 2, 2026

## Overview

This write-up documents a practical Open-Source Intelligence (OSINT) investigation into a suspicious social media account (`gaialove55551`) that was attempting to impersonate a real individual. The goal was to determine if the account was legitimate, identify any linked accounts, and uncover the truth behind the persona.

The investigation used a combination of automated username enumeration tools and manual verification to successfully identify the account as a scam and locate the real person being impersonated.

## Tools Used

- **Sherlock**: A command-line tool for hunting down usernames across more than 400 social networks.
- **Maigret**: A more advanced OSINT tool that collects a dossier on a person by username from over 3,000 sites, extracting detailed profile information and finding linked accounts.

## Methodology & Commands

The investigation followed a standard OSINT workflow: automated discovery, manual filtering, and verification.

### 1. Username Enumeration with Sherlock

The first step was to see where the username `gaialove55551` was registered.

**Installation (on Kali Linux):**
```bash
sudo apt install sherlock
