🧩 PuzzleToCoCanDa – BTLO CTF Write-up

Welcome to my simple and fun walkthrough of the PuzzleToCoCanDa challenge on Blue Team Labs Online (BTLO)! In this challenge, I investigated a suspicious phishing email and found some hidden surprises – including an alien criminal demanding CooCoins 😅

📅 Challenge Summary

We received a strange email with:

A fake sender

A suspicious attachment

A hidden message

Goal: Find out who sent the email, what service they used, and what was hidden inside the attachments.

📧 Step 1: Email Header Analysis

What I found:

Field

Value

From

billjobs@microapple.com (spoofed)

Return-Path

Same

SPF Check

❌ Failed (unauthorized sender)

Source IP

93.99.104.210

Email Service Used

emkei.cz (spoofing site)

Reply-To

negeja3921@pashter.com

🔎 The attacker used emkei.cz to spoof the email.

📁 Step 2: Unpacking the Attachment

The file looked like a PDF: PuzzleToCoCanDa.pdfBut when I ran the file command:

file PuzzleToCoCanDa.pdf
# Output: Zip archive data...

So I renamed it to .zip and extracted it.

Files inside:

DaughtersCrown.jpeg

GoodiesMajor.pdf

Money.xlsx

$-Money.xlsx

🔍 Step 3: Finding the Attacker

I ran exiftool on GoodiesMajor.pdf:

exiftool GoodiesMajor.pdf

Author: Pestero Negeja✅ That's our attacker!

🤮 Step 4: Decoding the Message

I opened Money.xlsx and found some Base64-encoded text.

Used CyberChef to decode it.

Result:

The Martian Colony, Beside Interplanetary Spaceport.
Send me 1 Billion CooCoins 💰 in cash 🤑 with a spaceship 🚀

👽 The attacker is pretending to be on The Martian Colony.

🔗 Step 5: C2 Domain

From the "Reply-To" address:

negeja3921@pashter.com

The attacker might be using:

pashter.com as their Command & Control domain.

✅ Final Answers (TL;DR)

Question

Answer

Email service used

emkei.cz

Reply-To address

negeja3921@pashter.com

File disguise

ZIP file spoofed as PDF

Attacker name

Pestero Negeja

Attacker location

The Martian Colony

C2 Domain

pashter.com

🔧 Tools I Used

Notepad++ – View email headers

file (Linux) – Detect real file types

CyberChef – Decode base64

ExifTool – Extract file metadata

VirusTotal – Scan suspicious files
