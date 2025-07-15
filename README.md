# Email-Phishing-Analyzer-The-Planet's-Prestige-Challenge
This repository contains the work done on the "The Planet's Prestige" challenge from Blue Team Labs.

🧩 PuzzleToCoCanDa – BTLO CTF Write-up
🚀 Challenge Summary

This challenge is from Blue Team Labs Online. We received a phishing email with suspicious attachments. The goal was to investigate and answer questions like:

    Who sent the email?

    What service did they use?

    Where is the attacker "located"?

    What’s hidden in the attachments?

📬 Email Header Analysis

    From (spoofed): billjobs@microapple.com

    Return-Path: Same as above

    SPF Check: ❌ Failed (not authorized)

    Source IP: 93.99.104.210

    Email Service Used: emkei.cz (a spoofing email tool)

    Reply-To Address: negeja3921@pashter.com

✅ Conclusion: The attacker used emkei.cz to spoof the email address and send a fake message.
📁 Attachment Analysis

We got a file named PuzzleToCoCanDa.pdf.

But when we checked it using the file command:

file PuzzleToCoCanDa.pdf
# Output: Zip archive data...

🧠 It was actually a ZIP file, not a PDF!

After unzipping, we got:

    DaughtersCrown.jpeg

    GoodiesMajor.pdf

    Money.xlsx

    $-Money.xlsx

📄 Who is the Attacker?

We checked metadata from the file GoodiesMajor.pdf using exiftool.

Author: Pestero Negeja
🧑‍💻 That’s the name of the attacker.
🧪 What Was Hidden?

In Money.xlsx, we found a Base64-encoded message.
We decoded it using CyberChef.

📝 Decoded message:

The Martian Colony, Beside Interplanetary Spaceport.
Send me 1 Billion CooCoins 💰 in cash 🤑 with a spaceship 🚀

😄 Looks like our attacker is an alien criminal!
🕸️ Command & Control (C2) Domain

From the Reply-To address: negeja3921@pashter.com
➡️ The domain pashter.com is likely the attacker’s C2 (Command & Control).
✅ Final Answers (For the Challenge)
❓ Question	✅ Answer
Email service used by attacker	emkei.cz
Reply-To email address	negeja3921@pashter.com
Spoofed attachment type	ZIP file (disguised as PDF)
Name of the attacker	Pestero Negeja
Attacker’s "location"	The Martian Colony
Command & Control domain	pashter.com
🛠️ Tools I Used

    Notepad++ – For checking email headers

    CyberChef – For decoding Base64

    ExifTool – For checking PDF metadata

    file (Linux) – To identify file types

    emldump.py – (Optional) to extract email attachments

    VirusTotal – To scan suspicious files
