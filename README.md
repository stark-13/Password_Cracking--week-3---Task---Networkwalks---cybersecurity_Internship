# Password_Cracking--week-3---Task---Networkwalks---cybersecurity_Internship
# 🔐 Networkwalks Cybersecurity Internship — Week 3: Password Cracking

**Author:** Radsaran Ehalaivan  
**Intern ID:** NW-084-232 (Batch B084)  
**LinkedIn:** [Radsaran Ehalaivan](https://www.linkedin.com/in/radsaran-ehalaivan)  

---

## 📋 Overview

This repository documents the practical tasks completed during **Week 3** of the **Networkwalks Cybersecurity Internship**. The objective of these labs is to understand how password-protected files store cryptographic hashes, how to extract those hashes, and how dictionary attacks are performed using both command-line utilities in Kali Linux and browser-based security tools.

> **Disclaimer:** *All activities and techniques documented in this repository were performed strictly for educational purposes within a controlled lab environment provided by Networkwalks.*

---

## 🛠️ Tools & Environments Used

* **Operating Systems:** Kali Linux (VirtualBox VM) & Windows 11
* **CLI Tools:** `pdf2john`, John the Ripper (JTR)
* **Wordlist:** `rockyou.txt`
* **Web Tools:** [Networkwalks Hash Calculator](https://networkwalks.com/hash-calculator/) & [Networkwalks Password Cracker](https://networkwalks.com/password-cracker/)

---

## 🧪 Task 1: Cracking a Protected PDF with John the Ripper (CLI)

*Note: While the standard lab instructions suggested using **Johnny** (the GUI frontend for John the Ripper), I opted to use the **John the Ripper CLI** directly in Kali Linux to gain a deeper understanding of the underlying terminal workflow.*

### Step 1: Target Acquisition
Obtained the password-protected target file (`My Locked PDF1.pdf`, renamed to `lock.pdf` on the Kali Desktop) provided by Networkwalks.

### Step 2: Hash Extraction
Used `pdf2john` to extract the encryption hash from the PDF and save it into a `.hash` file:

```bash
pdf2john lock.pdf > lockedpdf.hash
cat lockedpdf.hash
```

### Step 3: Dictionary Attack
Executed John the Ripper against the extracted hash using the `rockyou.txt` wordlist:

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt lockedpdf.hash
```

* **Recovered Password:** `good-luck`
* **Time Elapsed:** ~9 seconds

### Step 4: Flag Capture
Unlocked the PDF using the recovered password (`good-luck`) and retrieved the hidden flag:
* **Flag:** `nw{cybersecurity_flag_captured_2608}`

---

## 🌐 Task 2: Password Cracking with Networkwalks Web Tools

To compare CLI workflows with browser-based utilities, the same target PDF was analyzed on a Windows 11 host using Networkwalks' online tools.

### Step 1: Local Hash Extraction
1. Navigated to the [Networkwalks Hash Calculator](https://networkwalks.com/hash-calculator/).
2. Loaded `My Locked PDF1.pdf` (parsed locally in the browser without uploading).
3. Extracted the `pdf2john` / `hashcat` compatible hash string (Revision: R4, Version: V4, Key length: 128-bit).

### Step 2: Dictionary Attack
1. Pasted the extracted `$pdf$...` hash into the [Networkwalks Password Cracker](https://networkwalks.com/password-cracker/).
2. Ran the dictionary wordlist attack and successfully matched the password: `good-luck`.

---

## 🛡️ Key Takeaways & Remediation

* **Vulnerability:** Even when strong encryption standards (like 128-bit RC4/AES in PDFs) are used, the security of the file is only as strong as the password chosen by the user. Common words or phrases present in public wordlists like `rockyou.txt` can be cracked almost instantaneously.
* **Mitigation:** Always enforce strong password policies—use long, randomly generated passphrases containing a mix of uppercase letters, lowercase letters, numbers, and special characters to defend against dictionary and brute-force attacks.
