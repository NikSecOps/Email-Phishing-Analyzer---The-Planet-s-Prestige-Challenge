# 🧩 PuzzleToCoCanDa – BTLO Phishing CTF Write-up

This was a fun challenge on Blue Team Labs Online where I had to investigate a suspicious phishing email. The email looked like it came from “billjobs@microapple.com”, but it was clearly fake. Here's how I solved it step-by-step.

---

## 📧 Step 1: Checking the Email Header

When I looked at the email header, I saw that the **SPF check failed**, which means the sender wasn’t authorized to send from that domain. It looked like the email came from `billjobs@microapple.com`, but the real sender used a spoofing tool called **emkei.cz**.

There was also a **Reply-To** address: `negeja3921@pashter.com`. That’s probably where they expected replies to go.

---

## 📂 Step 2: The Suspicious Attachment

The email had an attachment called `PuzzleToCoCanDa.pdf`. But when I used the `file` command in Linux to check it, it said:

Zip archive data...


So it wasn’t a PDF — it was actually a **ZIP file**. I renamed it and unzipped it.

Inside the ZIP file, I found:
- A picture: `DaughtersCrown.jpeg`
- A PDF: `GoodiesMajor.pdf`
- Two Excel files: `Money.xlsx` and `$-Money.xlsx`

---

## 🕵️ Step 3: Who Sent This?

I used `exiftool` on the PDF file (`GoodiesMajor.pdf`) to see if there was any hidden metadata. Boom — it showed the **author** as:

Pestero Negeja


So that’s the name of the person behind this phishing email.

---

## 🔍 Step 4: What’s Inside the Excel File?

I opened the Excel file and saw some weird Base64 text in it. I copied it and pasted it into [CyberChef](https://gchq.github.io/CyberChef/), which decoded it.

Here’s the message I got:

The Martian Colony, Beside Interplanetary Spaceport.
Send me 1 Billion CooCoins 💰 in cash 🤑 with a spaceship 🚀


😂 So yeah, the attacker is pretending to be on Mars. Fun twist!

---

## 🌐 Step 5: Command and Control Domain

Since the Reply-To address was `negeja3921@pashter.com`, I figured that **pashter.com** was the domain being used for command and control.

---
![Raw Email Header in Notepad++]<img width="2118" height="1214" alt="screely-1752616449276" src="https://github.com/user-attachments/assets/683a53eb-7069-4159-87f7-e9c15655a435" />
> The email header of the suspicious message titled **"A Hope to CooCamba"** is opened in Notepad++ for forensic inspection.
## ✅ Final Summary

Here’s what I found out:

- The attacker used **emkei.cz** to spoof the email
- The real attachment was a ZIP file pretending to be a PDF
- The attacker’s name is **Pestero Negeja**
- They’re pretending to be in **The Martian Colony**
- Their C2 domain is probably **pashter.com**

---

## 🧠 What I Learned

- Always check the **SPF/DKIM/DMARC** in email headers
- Use the `file` command to find disguised files
- Metadata can reveal important clues
- CyberChef is super useful for decoding
- Phishing emails can be creative (and weird)

---

Thanks for reading! 🙌
