# 🏴‍☠️ OverTheWire Bandit — Complete Walkthrough (Levels 0-6)

> **Author:** Muhammad Sadiq  
> **Date:** 2026  
> **Platform:** [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)  
> **Levels Completed:** 0 — 6  
> **Focus:** Linux CLI, SSH, Permissions, File Management





These skills are directly applicable to# OverTheWire Bandit Walkthrough: Levels 0-13

A comprehensive guide to solving the first 14 levels of the Bandit wargame.

---

## Introduction

Bandit is a wargame from OverTheWire designed to teach Linux command-line skills and security concepts. This walkthrough covers levels 0 through 13, providing step-by-step solutions and explanations for each challenge.

**Prerequisites:**
- SSH client installed on your local machine
- Basic understanding of Linux command line
- Terminal access

**Connection Information:**
- Host: `bandit.labs.overthewire.org`
- Port: `2220`
- Protocol: SSH

---
**
## Level 0 → Level 1

### Objective
The password for the next level is stored in a file called `readme` located in the home directory.

### Solution
Establish an SSH connection to the Bandit server and read the file.

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

Password: `bandit0`

Once connected, list the files and read the readme file:

```bash
bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme
```

### Password for Level 1
```
6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR
```

### Explanation
This level introduces basic SSH connectivity and the `cat` command for reading files.

---

## Level 1 → Level 2

### Objective
The password is stored in a file called `-` located in the home directory.

### Solution
Connect using the password from the previous level:

```bash
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

Password: `6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR`

The challenge involves reading a file with a hyphen in its name. In Linux, a hyphen alone is interpreted as a command option, so it cannot be referenced directly. Use the `./` prefix to specify the file explicitly.

```bash
bandit1@bandit:~$ cat ./-
```

### Password for Level 2
```
PK8fYLZg2hnHSz83plBL1iEPKdD3QToB
```

### Explanation
This level demonstrates how to handle filenames that begin with special characters, particularly the hyphen which is typically used for command options.

---

## Level 2 → Level 3

### Objective
The password is stored in a file called `spaces in this filename` located in the home directory.

### Solution
Connect as bandit2:

```bash
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

Password: `PK8fYLZg2hnHSz83plBL1iEPKdD3QToB`

The filename contains spaces, which need to be escaped or quoted. You can either:
1. Use quotes around the filename
2. Escape each space with a backslash

```bash
bandit2@bandit:~$ ls
spaces in this filename
bandit2@bandit:~$ cat ./"spaces in this filename"
```

Alternatively, using escape characters:
```bash
bandit2@bandit:~$ cat spaces\ in\ this\ filename
```

### Password for Level 3
```
7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME
```

### Explanation
This level teaches how to handle filenames with spaces, a common issue in Linux systems.

---

## Level 3 → Level 4

### Objective
The password is stored in a hidden file inside the `inhere` directory.

### Solution
Connect as bandit3:

```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220
```

Password: `7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME`

Navigate to the `inhere` directory and list all files including hidden ones:

```bash
bandit3@bandit:~$ ls
inhere
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$ ls -la
```

The hidden file begins with a dot (`.`). Read it:

```bash
bandit3@bandit:~/inhere$ cat .hidden
```

### Password for Level 4
```
xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq
```

### Explanation
This level introduces hidden files in Linux, which start with a dot and can be viewed using the `-a` flag with `ls`.

---

## Level 4 → Level 5

### Objective
The password is stored in a file in the `inhere` directory. The file is not human-readable, but among several files, one contains the password in ASCII.

### Solution
Connect as bandit4:

```bash
ssh bandit4@bandit.labs.overthewire.org -p 2220
```

Password: `xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq`

Navigate to `inhere` and examine the files:

```bash
bandit4@bandit:~$ ls
inhere
bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
```

Use the `file` command to identify file types and find the one containing text:

```bash
bandit4@bandit:~/inhere$ file ./-file*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```

The ASCII text file contains the password:

```bash
bandit4@bandit:~/inhere$ cat ./-file07
```

### Password for Level 5
```
6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG
```

### Explanation
This level teaches how to identify file types using the `file` command, useful when dealing with binary or data files.

---

## Level 5 → Level 6

### Objective
The password is stored in a file with specific properties: human-readable, 1033 bytes in size, and not executable.

### Solution
Connect as bandit5:

```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220
```

Password: `6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG`

Navigate to the `inhere` directory which contains many folders and files:

```bash
bandit5@bandit:~$ cd inhere
bandit5@bandit:~/inhere$ ls
maybehere00  maybehere01  maybehere02  maybehere03  maybehere04  maybehere05  maybehere06  maybehere07  maybehere08  maybehere09  maybehere10  maybehere11  maybehere12  maybehere13  maybehere14  maybehere15  maybehere16  maybehere17  maybehere18  maybehere19
```

Use the `find` command to locate files with the specified properties:

```bash
bandit5@bandit:~/inhere$ find . -type f -size 1033c -exec file {} \;
```

Or use `xargs` to process the output:

```bash
bandit5@bandit:~/inhere$ find . -type f -size 1033c | xargs strings
```

### Password for Level 6
```
pXa26xhMWaC2SvDotA4r9EgZkulOeSBW
```

### Explanation
This level introduces the powerful `find` command with filters for file type (`-type`), size (`-size`), and combining it with `xargs` for processing results.

---

## Level 6 → Level 7

### Objective
The password is stored somewhere on the server with specific properties:
- Owned by user `bandit7`
- Owned by group `bandit6`
- Size of 33 bytes

### Solution
Connect as bandit6:

```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

Password: `pXa26xhMWaC2SvDotA4r9EgZkulOeSBW`

Search from the root directory (`/`) with the specified conditions:

```bash
bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null -exec cat {} \;
```

The `2>/dev/null` redirects error messages (permission denied) to null, making the output cleaner.

### Password for Level 7
```
Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3
```

### Explanation
This level demonstrates more advanced `find` usage with user, group, and size filters, and introduces error redirection.

---

## Level 7 → Level 8

### Objective
The password is stored in the file `data.txt` next to the word `millionth`.

### Solution
Connect as bandit7:

```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
```

Password: `Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3`

Search for the word `millionth` in the file:

```bash
bandit7@bandit:~$ ls
data.txt
bandit7@bandit:~$ cat data.txt | grep millionth
```

### Password for Level 8
```
VR1ljMayciFxbnUokuQmJFw6QC9VKtub
```

### Explanation
This level introduces the `grep` command for searching text patterns within files.

---

## Level 8 → Level 9

### Objective
The password is stored in `data.txt` and appears only once. The file contains many lines of text and passwords.

### Solution
Connect as bandit8:

```bash
ssh bandit8@bandit.labs.overthewire.org -p 2220
```

Password: `VR1ljMayciFxbnUokuQmJFw6QC9VKtub`

Sort the file and find the unique line that appears only once:

```bash
bandit8@bandit:~$ sort data.txt | uniq -u
```

### Password for Level 9
```
EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl
```

### Explanation
This level teaches how to use `sort` and `uniq` together to find unique lines in a file.

---

## Level 9 → Level 10

### Objective
The password is stored in `data.txt` among several human-readable strings preceded by one or more `=` characters.

### Solution
Connect as bandit9:

```bash
ssh bandit9@bandit.labs.overthewire.org -p 2220
```

Password: `EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl`

Use `strings` to extract human-readable text and `grep` to find lines with `=`:

```bash
bandit9@bandit:~$ strings data.txt | grep '='
```

### Password for Level 10
```
B0s2khmbT9u0geKuOoVGW3JZKhndE3BG
```

### Explanation
This level introduces the `strings` command to extract readable text from binary files.

---

## Level 10 → Level 11

### Objective
The password is stored in `data.txt` in Base64 format.

### Solution
Connect as bandit10:

```bash
ssh bandit10@bandit.labs.overthewire.org -p 2220
```

Password: `B0s2khmbT9u0geKuOoVGW3JZKhndE3BG`

Decode the Base64 encoded data:

```bash
bandit10@bandit:~$ strings data.txt | base64 -d
```

### Password for Level 11
```
pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro
```

### Explanation
This level demonstrates Base64 encoding and decoding, a common data encoding method.

---

## Level 11 → Level 12

### Objective
The password is stored in `data.txt` where all lowercase and uppercase letters are rotated 13 positions (ROT13).

### Solution
Connect as bandit11:

```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
```

Password: `pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro`

Apply the ROT13 transformation using `tr`:

```bash
bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

### Password for Level 12
```
GROozWPO8QyN0mGrjUkID0WCYkZiQxrN
```

### Explanation
This level introduces ROT13 cipher and the `tr` command for character translation.

---

## Level 12 → Level 13

### Objective
The password is stored in `data.txt`, which is a hexdump of a file that has been compressed multiple times.

### Solution
Connect as bandit12:

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
```

Password: `GROozWPO8QyN0mGrjUkID0WCYkZiQxrN`

Create a working directory and process the hexdump:

```bash
bandit12@bandit:~$ cd /tmp
bandit12@bandit:/tmp$ mkdir bandit12_solution
bandit12@bandit:/tmp$ cd bandit12_solution
bandit12@bandit:/tmp/bandit12_solution$ cp ~/data.txt .
```

Reverse the hexdump to binary:

```bash
bandit12@bandit:/tmp/bandit12_solution$ xxd -r data.txt > data.bin
```

Identify file type and decompress repeatedly:

```bash
bandit12@bandit:/tmp/bandit12_solution$ file data.bin
data.bin: gzip compressed data, was "data2.bin", ...

bandit12@bandit:/tmp/bandit12_solution$ mv data.bin data.gz
bandit12@bandit:/tmp/bandit12_solution$ gzip -d data.gz

bandit12@bandit:/tmp/bandit12_solution$ file data
data: bzip2 compressed data, block size = 900k

bandit12@bandit:/tmp/bandit12_solution$ mv data data.bz2
bandit12@bandit:/tmp/bandit12_solution$ bzip2 -d data.bz2

bandit12@bandit:/tmp/bandit12_solution$ file data
data: gzip compressed data, was "data4.bin", ...

bandit12@bandit:/tmp/bandit12_solution$ mv data data.gz
bandit12@bandit:/tmp/bandit12_solution$ gzip -d data.gz

bandit12@bandit:/tmp/bandit12_solution$ file data
data: POSIX tar archive (GNU)

bandit12@bandit:/tmp/bandit12_solution$ mv data data.tar
bandit12@bandit:/tmp/bandit12_solution$ tar -xf data.tar

bandit12@bandit:/tmp/bandit12_solution$ file data5.bin
data5.bin: POSIX tar archive (GNU)

bandit12@bandit:/tmp/bandit12_solution$ mv data5.bin data5.tar
bandit12@bandit:/tmp/bandit12_solution$ tar -xf data5.tar

bandit12@bandit:/tmp/bandit12_solution$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k

bandit12@bandit:/tmp/bandit12_solution$ mv data6.bin data6.bz2
bandit12@bandit:/tmp/bandit12_solution$ bzip2 -d data6.bz2

bandit12@bandit:/tmp/bandit12_solution$ file data6
data6: POSIX tar archive (GNU)

bandit12@bandit:/tmp/bandit12_solution$ mv data6 data6.tar
bandit12@bandit:/tmp/bandit12_solution$ tar -xf data6.tar

bandit12@bandit:/tmp/bandit12_solution$ file data8.bin
data8.bin: gzip compressed data, was "data9.bin", ...

bandit12@bandit:/tmp/bandit12_solution$ mv data8.bin data8.gz
bandit12@bandit:/tmp/bandit12_solution$ gzip -d data8.gz

bandit12@bandit:/tmp/bandit12_solution$ file data8
data8: ASCII text

bandit12@bandit:/tmp/bandit12_solution$ cat data8
```

### Password for Level 13
```
qQYQiHOBPR8zR61qxYqX45quvihF2uzk
```

### Explanation
This level teaches:
- Hexdump reversal using `xxd -r`
- File type identification with `file`
- Decompression of multiple formats: `gzip`, `bzip2`, and `tar`
- Recursive file processing

---

## Level 13 → Level 14

### Objective
The password for level 14 is stored in `/etc/bandit_pass/bandit14` and can only be read by user `bandit14`. A private SSH key is provided to connect as `bandit14`.

### Solution
Connect as bandit13:

```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
```

Password: `qQYQiHOBPR8zR61qxYqX45quvihF2uzk`

The SSH key is located in the home directory:

```bash
bandit13@bandit:~$ ls
sshkey.private
```

From your local machine (after exiting the SSH session), copy the key:

```bash
scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private ~/bandit14_key
```

Set proper permissions and connect as bandit14:

```bash
chmod 600 ~/bandit14_key
ssh -i ~/bandit14_key bandit14@bandit.labs.overthewire.org -p 2220
```

Read the password file:

```bash
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
```

### Password for Level 14
```
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

### Explanation
This level introduces:
- SSH key-based authentication
- `scp` for copying files
- Permission management with `chmod`
- Direct password file access

---

## Summary of Passwords

| Level | Password |
|-------|----------|
| 0→1 | `6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR` |
| 1→2 | `PK8fYLZg2hnHSz83plBL1iEPKdD3QToB` |
| 2→3 | `7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME` |
| 3→4 | `xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq` |
| 4→5 | `6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG` |
| 5→6 | `pXa26xhMWaC2SvDotA4r9EgZkulOeSBW` |
| 6→7 | `Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3` |
| 7→8 | `VR1ljMayciFxbnUokuQmJFw6QC9VKtub` |
| 8→9 | `EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl` |
| 9→10 | `B0s2khmbT9u0geKuOoVGW3JZKhndE3BG` |
| 10→11 | `pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro` |
| 11→12 | `GROozWPO8QyN0mGrjUkID0WCYkZiQxrN` |
| 12→13 | `qQYQiHOBPR8zR61qxYqX45quvihF2uzk` |
| 13→14 | `MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS` |

---

## Key Commands Reference

| Command | Purpose |
|---------|---------|
| `ssh` | Connect to remote servers |
| `ls` | List directory contents |
| `cat` | Display file contents |
| `cd` | Change directory |
| `file` | Determine file type |
| `find` | Search for files |
| `grep` | Search text patterns |
| `sort` | Sort lines |
| `uniq` | Filter unique lines |
| `strings` | Extract text from binaries |
| `base64` | Encode/decode Base64 |
| `tr` | Translate characters |
| `xxd` | Hexdump/undo hexdump |
| `gzip` | Compress/decompress |
| `bzip2` | Compress/decompress |
| `tar` | Archive files |
| `scp` | Copy files over SSH |
| `chmod` | Change permissions |

---

## Conclusion

The Bandit wargame provides an excellent foundation in Linux command-line skills and security concepts. By completing these levels, you've learned:

1. **Basic navigation and file operations** (levels 0-3)
2. **Handling special characters and hidden files** (levels 1-4)
3. **File identification and searching** (levels 4-8)
4. **Text manipulation and encoding** (levels 7-11)
5. **Compression and archive formats** (level 12)
6. **SSH key authentication** (level 13)

Continue with levels 14 and beyond to further develop your skills in networking, scripting, and system administration. penetration testing, SOC analysis, and system administration.

**Next Steps:**
- Continue to Bandit Levels 7-14
- Start TryHackMe rooms
- Build a home lab
- Practice CTFs regularly

---

## 🔗 Resources

- [OverTheWire Bandit](https://overthewire.org/wargames/bandit/)
- [Linux Command Cheat Sheet](https://www.geeksforgeeks.org/linux-commands-cheat-sheet/)
- [TryHackMe — Linux Fundamentals](https://tryhackme.com/room/linuxfundamentalspart1)
- [Explain Shell](https://explainshell.com/)

---

## 📝 Final Thoughts

The Bandit wargame is an excellent foundation for anyone starting in cybersecurity. These first 6 levels cover:

✅ Basic SSH connections  
✅ File navigation  
✅ Hidden files  
✅ Special filenames  
✅ File properties  
✅ Data extraction  
## 💬 Connect With Me

> 📧 **Email:** [muhammadsadiq.cyber@gmail.com](mailto:muhammadsadiq.cyber@gmail.com)  
> 🔗 **LinkedIn:** [linkedin.com/in/muhammadsadiqcyber](https://linkedin.com/in/muhammadsadiqcyber)  
> 🐙 **GitHub:** [github.com/muhammadsadiqX1](https://github.com/muhammadsadiqX1)  
> 🏴 **TryHackMe:** [tryhackme.com/p/muhammadsadiqX1](https://tryhackme.com/p/muhammadsadiqX1)

---

> *"Break things, learn faster, secure better."* 🔴



*Made with ❤️ by Muhammad Sadiq | Red Team Operator in Training*
