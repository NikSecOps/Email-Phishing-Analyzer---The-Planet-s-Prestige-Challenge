# Email-Phishing-Analyzer-The-Planet's-Prestige-Challenge
This repository contains the work done on the "The Planet's Prestige" challenge from Blue Team Labs.

<div align="center">
  <img src="screenshots/logo.png" width="180" alt="logo" />
  <h1>🧩 PuzzleToCoCanDa</h1>
  <h3>A Blue Team Labs Online CTF • Phishing Investigation Challenge</h3>
</div>

---

## 📜 Overview

> 💌 One strange email.  
> 📎 A fake PDF that’s actually a ZIP.  
> 🤖 Bots, CooCoins, and a missing President's daughter?!  
> 🎯 Welcome to the interplanetary madness that is **PuzzleToCoCanDa**, a phishing-themed CTF from Blue Team Labs Online.

This challenge blends phishing analysis, header forensics, metadata extraction, and a sprinkle of alien storytelling. I tackled it using OSINT tools, CyberChef, and some good ol' DFIR skills.

---

## 🧠 Objective

Analyze a spoofed email and its attachments to extract:

- The **email service** used by the attacker
- The **spoofed identity**
- The **command & control domain**
- The **location of the attacker**
- And of course… the **villain behind it all**

---

## 📬 Email Header Analysis

🕵️ Spoofed as `billjobs@microapple.com`, this suspicious email was sent from:

| 🔍 Field        | 🔎 Value                                |
|----------------|-----------------------------------------|
| SPF Result     | ❌ Fail – Not a permitted sender         |
| Source IP      | `93.99.104.210`                         |
| Return-Path    | `billjobs@microapple.com`              |
| Real Service   | `emkei.cz` – a spoofing email service  |
| Reply-To       | `negeja3921@pashter.com`               |

> **Conclusion:** The attacker used `emkei.cz`, a known email spoofing tool, to forge the sender address.

---

## 🗃️ Attachment Forensics

The attached file was sneakily named `PuzzleToCoCanDa.pdf`. But after using `file` on it:

```bash
file PuzzleToCoCanDa.pdf
# → Zip archive data...

🪄 Renamed it to .zip → Extracted into:

📁 DaughtersCrown.jpeg
📁 GoodiesMajor.pdf
📁 Money.xlsx
📁 $-Money.xlsx

📄 Metadata Hunt

Used exiftool on GoodiesMajor.pdf:

exiftool GoodiesMajor.pdf

🔍 Metadata Field	💬 Value
Author	Pestero Negeja
Title	Good luck, Major!

    💡 Villain identified: Pestero Negeja

🧪 Payload Decoding (CyberChef)

Decoded the hidden base64 message from Money.xlsx using CyberChef:

🧾 Result:

The Martian Colony, Beside Interplanetary Spaceport.
Send 1 Billion CooCoins 💰 in cash 🤑 with a spaceship 🚀

    Location of the attacker: 🪐 The Martian Colony

🕸️ Command & Control Domain

The email’s Reply-To was negeja3921@pashter.com.

    Probable C2 Domain: 🔗 pashter.com

🛠️ Tools Used
🧰 Tool	🧪 Purpose
📄 Notepad++	Inspecting raw email headers
📦 CyberChef	Decoding base64 and extracting strings
🔍 ExifTool	PDF metadata analysis
🧠 emldump.py	Email attachment extraction
🧪 VirusTotal	File scanning and IOC validation
📊 OLETools	(Optional) Analyzing Excel macros
📌 TL;DR Answers
🔎 Question	🧠 Answer
Email service used by attacker	emkei.cz
“Reply-To” address	negeja3921@pashter.com
Malicious attachment disguise	.zip file spoofed as .pdf
Attacker’s identity	Pestero Negeja
Attacker’s "location"	The Martian Colony
Probable C2 domain	pashter.com
🎉 Challenge Complete!

    “Don’t trust your eyes,” they said…
    But with base64 decoding, metadata snooping, and some DFIR grit – the Major solved the puzzle. 🧩

✍️ Author

Made with 💻 and ☕ by YourNameHere
