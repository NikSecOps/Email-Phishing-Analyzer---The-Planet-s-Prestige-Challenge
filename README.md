# 🧩 PuzzleToCoCanDa – BTLO CTF Write-up

> A phishing email, spoofed headers, Base64-encoded alien ransom, and a villain named Pestero Negeja?  
> This Blue Team Labs Online challenge was out of this world! 🛸

---

## 📌 Challenge Summary

We received a **suspicious phishing email** with:

- A forged sender address
- Disguised attachment pretending to be a PDF
- Hidden messages inside files

🎯 **Goal:** Find out who sent the email, what service they used, and what secrets the attachments were hiding.

---

## 📬 Step 1: Email Header Analysis

Here’s what I found in the header:

| Field             | Value                          |
|------------------|---------------------------------|
| From             | `billjobs@microapple.com` (spoofed) |
| Return-Path      | `billjobs@microapple.com`       |
| SPF Check        | ❌ Failed (unauthorized sender) |
| Source IP        | `93.99.104.210`                |
| Email Service    | `emkei.cz` (spoofing site)     |
| Reply-To         | `negeja3921@pashter.com`       |

🕵️ **Conclusion:** The attacker used [emkei.cz](https://emkei.cz/) to spoof the email sender.

---

## 📦 Step 2: Unpacking the Attachment

The file was named `PuzzleToCoCanDa.pdf`, but when I checked it:

```bash
file PuzzleToCoCanDa.pdf
# Output: Zip archive data...

It was actually a ZIP file! After renaming and extracting:

Contents:

    DaughtersCrown.jpeg

    GoodiesMajor.pdf

    Money.xlsx

    $-Money.xlsx

🔍 Step 3: Identifying the Attacker

Ran exiftool on GoodiesMajor.pdf:

exiftool GoodiesMajor.pdf

Metadata:

    Author: Pestero Negeja

🎯 Attacker Identified: Pestero Negeja
🔓 Step 4: Decoding the Hidden Message

Opened Money.xlsx and found Base64-encoded text.
Used CyberChef to decode it.

📜 Decoded Message:

The Martian Colony, Beside Interplanetary Spaceport.
Send me 1 Billion CooCoins 💰 in cash 🤑 with a spaceship 🚀

🪐 Attacker's Location: The Martian Colony 😄
🌐 Step 5: Finding the Command & Control Domain

From the email’s "Reply-To" address:
📧 negeja3921@pashter.com

The domain pashter.com is likely being used as the C2 server.
✅ Final Answers (Quick Summary)
❓ Question	✅ Answer
Email service used by attacker	emkei.cz
Reply-To email address	negeja3921@pashter.com
What was the attachment really?	A ZIP file disguised as a PDF
Attacker’s name	Pestero Negeja
Attacker's location	The Martian Colony
C2 domain	pashter.com
🛠️ Tools I Used
Tool	Purpose
Notepad++	Read email headers
file	Check actual file types
CyberChef	Decode Base64 messages
ExifTool	View metadata of PDF/Office files
VirusTotal	Scan attachments for threats
emldump.py	(optional) Extract .eml file parts
