# John-The-Ripper---Cheatsheet-
Included example commands for using unshadow to merge passwd and shadow files. Added explanation of formats and how to crack system hashes using John the Ripper with wordlists like rockyou.txt.

---

## 📚 Table of Contents

- 🧠 [John the Ripper Cheat Sheet](#john-the-ripper-cheat-sheet)
- 🔑 [Basic John Usage](#basic-john-usage)
- 🧪 [Cracking Linux System Hashes](#cracking-linux-system-hashes-etcpasswd-etcshadow)
- 🏆 [Top John the Ripper Commands](#top-john-the-ripper-commands)
- ⚙️ [Example Hash Formats](#example-hash-formats)
- 💬 [Author's Note](#authors-note)



---


# 🧠 John the Ripper Cheat Sheet
Personal cheat sheet with John the Ripper commands used in CTFs and pentesting.

---

## 🔑 Basic John Usage

| Command | Description |
|--------|-------------|
| `john [file]` | Basic cracking with default options |
| `john --wordlist=/path/to/wordlist.txt [file]` | Use a specific wordlist (e.g., rockyou.txt) |
| `john --format=raw-md5 --wordlist=/path/to/wordlist.txt [file]` | Specify hash format manually |
| `john --list=formats` | List all supported hash formats |
| `john --single --format=[format] [file]` | Use single crack mode |
| `john --wordlist=[wordlist] --rule=[rule] [file]` | Use custom rules from config file |
| `john --show [file]` | Show cracked passwords |
| `john --restore` | Resume a paused session |

---

## 🧪 Cracking Linux System Hashes (/etc/shadow)

On real Linux systems, password hashes are stored in `/etc/shadow`, and usernames in `/etc/passwd`.
To crack those hashes:

unshadow /etc/passwd /etc/shadow > unshadowed.txt

unshadow passwd shadow > unshadowed.txt` | Merge `/etc/passwd` and `/etc/shadow` into crackable file |
john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt` | Crack unshadowed Linux hashes |

---

## 🏆 Top John the Ripper Commands

1. `john hash.txt`  
   – Basic cracking with default config and wordlist

2. `john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt`  
   – Uses RockYou list to crack hashes

3. `john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt`  
   – Cracks raw MD5 hashes with wordlist

4. `john --list=formats`  
   – Lists all available hash formats

5. `unshadow passwd shadow > unshadowed.txt`  
   – Merges passwd and shadow files

6. `john --wordlist=rockyou.txt --format=sha512crypt unshadowed.txt`  
   – Cracks Linux user hashes (sha512crypt)

7. `john --single --format=raw-md5 hash.txt`  
   – Uses single crack mode (based on usernames, etc.)

8. `john --wordlist=rockyou.txt --rules [file]`  
   – Custom rule-based cracking

9. `john --show hash.txt`  
   – Displays cracked credentials

10. `john --restore`  
    – Restores previously saved session

---

## ⚙️ Example Hash Formats

| Format | Description |
|--------|-------------|
| `raw-md5` | Raw MD5 hashes |
| `sha256crypt` | Linux SHA-256 password hash |
| `sha512crypt` | Linux SHA-512 password hash |
| `bcrypt` | Blowfish-based hash (used by some Linux distros) |
| `nt` | Windows NT hash |
| `md5crypt` | MD5-based UNIX hash |
| `zip`, `rar`, `pdf` | File-based hash formats |

Run `john --list=formats` for a full list.



💬 Author's Note
This list was compiled for your own use and practice through CTF challenges and test environments like TryHackMe and Hack The Box.
Do not use these commands on networks without permission. 🛡️
