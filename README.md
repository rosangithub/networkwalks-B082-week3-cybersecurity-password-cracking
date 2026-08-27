<div align="center">

# 🔐 Password Cracking with John the Ripper (Johnny) & Network Walks Tools

**Auditing password strength using offline and online hash-cracking tools in an isolated lab environment**

</div>

<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Tool-John%20the%20Ripper-0070C0?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/GUI-Johnny-E87500?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Skill-Password%20Auditing-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Tool-Network%20Walks%20Hash%20Tools-238F89?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
</p>

---

## 📋 Project Overview

This project demonstrates how to audit the strength of a password-protected file using two complementary approaches:

1. **Offline cracking** with **John the Ripper**, using its GUI front-end **Johnny**.
2. **Online/hash-service cracking** using the **Network Walks Hash Calculator** and **Network Walks Password Cracker**.

The goal is to take a password-protected file, extract its hash, and attempt to recover the original password using a wordlist (dictionary attack) — demonstrating why weak or common passwords are easy to break, and why strong, unique passwords matter.

All testing in this report was carried out **only against a file I created and own myself**, inside a controlled lab environment.

---

## 🎯 Objectives

- Understand how password hashing and password cracking work.
- Extract the hash from a password-protected file.
- Configure and run John the Ripper (via the Johnny GUI) against the hash.
- Configure and run the Network Walks Hash Calculator and Password Cracker as an alternative method.
- Successfully recover the plaintext password using a wordlist/dictionary attack.
- Document the full process, including tools, steps, and results.

---

## ⚠️ Legal & Ethical Disclaimer

This project is provided for **educational and authorized security-testing purposes only**.

Password cracking tools such as John the Ripper must only be used against files, accounts, or systems that you **own** or have **explicit, written authorization** to test. Using these tools against systems or data you do not own or lack authorization for is illegal in most jurisdictions and may violate laws such as the Computer Fraud and Abuse Act (US), the Computer Misuse Act (UK), or equivalent local legislation.

By following or reusing this report, you agree that:

- You will only test files/systems you own or are authorized to test.
- This material is provided "as is," with no warranty of any kind.
- The author accepts no liability for any misuse, damage, or legal consequences arising from the use of this information.
- You are solely responsible for complying with all applicable laws in your jurisdiction.

---

## 🧠 Introduction to Password Cracking

Password cracking is the process of recovering or guessing a password, usually from its hashed form, in order to verify its strength or regain access to protected data. Since most systems store passwords as **hashes** rather than plain text, cracking tools work by generating password guesses, hashing each one, and comparing the result against the stored hash until a match is found.

Common cracking methods include:

- **Dictionary attack** — tries words from a predefined wordlist of common/leaked passwords.
- **Brute-force attack** — tries every possible character combination.
- **Rule-based / hybrid attack** — applies transformations (capitalization, number substitution, etc.) to wordlist entries to mimic real human password habits.

Password cracking is used both maliciously by attackers and legitimately by security professionals to test and strengthen password security — the latter only when performed with proper authorization.

---

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| **John the Ripper (Johnny)** | Offline password-cracking tool used to test the strength of password hashes through dictionary, brute-force, and rule-based attacks. Johnny provides a graphical interface for configuring and monitoring cracking sessions. |
| **Network Walks Hash Calculator** | Online utility used to generate the hash value of the password-protected file. |
| **Network Walks Password Cracker** | Online tool used to run a dictionary attack against the generated hash using an uploaded wordlist. |

---

## 🏗️ Lab Setup

| 🧩 Component | ⚙️ Configuration |
|---|---|
| Host OS | Windows |
| Cracking Tool (Offline) | John the Ripper — Johnny GUI |
| Cracking Tool (Online) | Network Walks Hash Calculator / Password Cracker |
| Target File | Password-protected file (owned by author) |
| Wordlist | Custom / common password wordlist |

---

# 🧩 Part 1 — Password Cracking with Johnny (John the Ripper GUI)

## Step 1. Download and Install Johnny

Downloaded and installed **Johnny**, the graphical front-end for John the Ripper, on the host machine. Johnny simplifies password auditing by providing a visual interface instead of requiring pure command-line operation.

![alt text](johnny-install.png)

---

## Step 2. Calculate the Hash of the Password-Protected File

Before Johnny can attempt to crack a password, the protected file must be converted into a hash format John the Ripper understands. This was done using the appropriate `*2john` utility for the file type (e.g. `zip2john`, `pdf2john`, `office2john`), which extracts the hash and saves it to a `.txt` file.

```bash
zip2john protected_file.zip > hash.txt
```

![alt text](hash-calculation.png)

---

## Step 3. Configure the Settings in Johnny

Opened Johnny and configured the cracking session:

- Selected the **attack mode** (Dictionary).
- Selected the **wordlist** to use.
- Left default rules enabled to catch common variations (capitalization, digits, etc.).

![alt text](johnny-settings.png)

---

## Step 4. Upload the Hash File into Johnny

Loaded the `hash.txt` file generated in Step 2 into Johnny using **Open Password Hash File**, then started the cracking session.

![alt text](upload-hash-johnny.png)

---

## Step 5. Password Found

Johnny worked through the wordlist, hashing each candidate and comparing it against the target hash. Once a match was found, Johnny displayed the recovered plaintext password in the results pane.

![alt text](password-found-johnny.png)

**Result:**

```text
Hash file:   hash.txt
Attack mode: Dictionary
Password:    [recovered password]
Time taken:  [duration]
```

---

# 🧩 Part 2 — Password Cracking with Network Walks Tools

## Step 1. Download the Password-Protected File

The target file, secured with a password, was prepared and made ready for hash extraction.

![alt text](target-file.png)

---

## Step 2. Calculate the Hash Using the Network Walks Hash Calculator

The password-protected file was uploaded into the **Network Walks Hash Calculator**, which processed the file and generated its corresponding hash value.

![alt text](networkwalks-hash-calculator.png)

---

## Step 3. Upload the Hash to the Network Walks Password Cracker

The generated hash was copied and uploaded into the **Network Walks Password Cracker**, which tests the hash against candidate passwords until a match is found.

![alt text](networkwalks-upload-hash.png)

---

## Step 4. Upload a Wordlist

A wordlist containing common/likely password candidates was uploaded into the cracker to run a dictionary attack against the target hash.

![alt text](networkwalks-wordlist-upload.png)

---

## Step 5. Password Cracked

The Network Walks Password Cracker hashed each word in the wordlist and compared it to the target hash. Once a match was found, the tool displayed the corresponding plaintext password.

![alt text](networkwalks-password-cracked.png)

**Result:**

```text
Hash uploaded:  [hash value]
Wordlist used:  [wordlist name]
Password:       [recovered password]
```

---

# ✅ Verification

| 🔎 Test | 🧾 Method | 🎯 Expected Result |
|---|---|---|
| Hash extracted correctly | `zip2john` / Network Walks Hash Calculator | Valid hash string generated |
| Johnny loads hash | Open Password Hash File in Johnny | Hash listed and ready to crack |
| Dictionary attack runs | Start session in Johnny / Network Walks Cracker | Progress shown, attempts counted |
| Password recovered | Compare cracked value to original password | Matches the original password |

---

# 📚 What I Learned

### 1. Hashing vs Cracking
Passwords are never stored in plain text — they're stored as hashes. Cracking tools don't "decrypt" a hash; they guess repeatedly, hash each guess, and check for a match.

### 2. Wordlist Quality Matters
A cracking attempt is only as good as the wordlist used. Common or previously leaked passwords are cracked almost instantly, while strong, unique passwords resist dictionary attacks entirely.

### 3. GUI vs Online Tools
Johnny made it easier to visualize and manage a local cracking session, while the Network Walks tools offered a quick way to calculate hashes and run cracking attempts without local setup — useful for fast checks.

### 4. Why Strong Passwords Matter
This exercise reinforced how quickly weak or dictionary-based passwords fall to basic tools, highlighting the importance of long, random, unique passwords and additional protections like salting and multi-factor authentication.

---

# 🔒 Security & Ethical Use

This project is intended strictly for **educational purposes** and was performed only against a file created and owned by the author. These tools and techniques must never be used against systems, accounts, or files without explicit authorization.

---

# 🔗 Tools & Resources

- **John the Ripper:** https://www.openwall.com/john/
- **Johnny (GUI):** https://openwall.info/wiki/john/johnny
- **Network Walks:** https://networkwalks.com/

---

## Author

### Rosan Shrestha
- Cyber Security Intern at Networkwalks
- **LinkedIn:** https://www.linkedin.com/in/rosanshrestha

## 📌 Project Information

**Project:** Password Cracking with John the Ripper (Johnny) & Network Walks Tools
