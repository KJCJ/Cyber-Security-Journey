# OSINT Investigation: Unmasking an Impersonation Account

**Date:** October 2, 2026
**Analyst:** Julian Jarrett (KJCJ)

## Overview

This write-up documents a practical Open-Source Intelligence (OSINT) investigation into a suspicious social media account (`gaialove55551`) that was attempting to impersonate a real individual. The goal was to determine if the account was legitimate, identify any linked accounts, and uncover the truth behind the persona.

The investigation used a combination of automated username enumeration tools and manual verification to successfully identify the account as a scam and locate the real person being impersonated.

## Tools Used

- **Kali Linux**: The operating system used for the investigation.
- **Sherlock**: A command-line tool for hunting down usernames across more than 400 social networks.
- **Maigret**: A more advanced OSINT tool that collects a dossier on a person by username from over 3,000 sites, extracting detailed profile information and finding linked accounts.

## Methodology & Commands

The investigation followed a standard OSINT workflow: automated discovery, manual filtering, and verification.

### 1. Username Enumeration with Sherlock

The first step was to see where the username `gaialove55551` was registered.

**Installation (on Kali Linux):**
```bash
sudo apt install sherlock
```

**Execution:**
```bash
sherlock gaialove55551 --print-found
```

**Key Findings:**
Sherlock returned 45 results. However, many were false positives (e.g., Reddit and 7Cups explicitly showed "user not found"). The most significant result was a profile on TikTok.

### 2. Deeper Analysis with Maigret

To get more detailed information and find linked accounts, Maigret was used.

**Installation (using pipx is recommended):**
```bash
pipx install maigret
```

**Execution:**
```bash
maigret gaialove55551 --html
```

**Key Findings:**
Maigret's output was far more precise. It confirmed the TikTok account and extracted its public metadata, which was the critical piece of evidence.

- **TikTok Profile:** `https://www.tiktok.com/@gaialove55551`
- **Bio:** "Come with me on my vow of Nunhood until I buy myself my first home (1st goal). Painter, Palm Reader, Witch, Spiritual Reading and offer Spiritual Cleansing"
- **Following:** 2,542
- **Followers:** 251
- **Likes:** 165
- **Verified:** No

This data revealed a heavily unbalanced follower-to-following ratio, a common indicator of a bot or spam account.

### 3. Manual Verification & Discovery

The final and most crucial step was manually visiting the identified profile. Upon further investigation, the real person was identified as **Queen Nefertiti 👑** on Instagram (username: `@gaialove5555`), who has a significantly larger and more legitimate following (7,759 followers and 29K likes). 

She had already posted warnings to her audience about the impersonator on her original profile. 

**The Evidence:**
The pinned video on the **original** profile stated: *"Hello guys Pls don't fall a victim of this account they are trying to impersonate me... Kindly report and block this account immediately they message you."* The fake account does not have this warning; it only contains stolen content.

<img width="590" height="1278" alt="20261002_001648466_iOS" src="https://github.com/user-attachments/assets/ccb8a827-3cf2-4d40-85a0-e6a2cf119073" />

<img width="590" height="1278" alt="IMG_5448" src="https://github.com/user-attachments/assets/1cffcc6b-5012-4666-8e99-e9defda8aa89" />

## Conclusion

The OSINT investigation was successful. The `gaialove55551` account was definitively identified as an impersonation scam. The combination of automated tools (Sherlock, Maigret) and manual verification (checking profile pages and pinned videos) provided clear, irrefutable evidence.

### Key Takeaways

- **Automated tools are a starting point, not a conclusion.** Tools like Sherlock and Maigret are excellent for discovery, but their results must be manually verified to filter out false positives.
- **Maigret provides more context** than Sherlock, as it can extract specific profile details and metadata that are crucial for assessment.
- **Behavioral red flags are critical.** An unbalanced follower ratio, stolen content, and a warning from the real person are definitive signs of an impersonation account.
- **Documentation is key.** Recording every step, command, and finding creates a reproducible and valuable educational resource.

## Disclaimer

This investigation was conducted purely for educational purposes using publicly available information. All data was accessed and analyzed ethically, with no attempts to access private information or harass the individuals involved. Always respect platform terms of service and privacy laws.
