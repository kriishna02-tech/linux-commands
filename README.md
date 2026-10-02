# 🐧 Linux Command Cheat Sheet

> My practical Linux reference for AI / Backend Engineering
> Goal: **remember what to use, not memorize everything**

---

# ⚡ 1. Commands I’ll Use All The Time

```bash
pwd
ls -lah
cd folder
cd ..
mkdir project
touch file.txt
cp file.txt copy.txt
mv old.txt new.txt
rm file.txt
cat file.txt
grep "ERROR" file.log
find . -name "*.txt"
ps aux
free -h
df -h
```

### 🧠 Memory Hook

```text
pwd  → where am I?
ls   → what's here?
cd   → move
cp   → copy
mv   → move / rename
rm   → delete
cat  → read
grep → search text
find → search files
```

---

# 📂 2. Files & Folders

## Navigate

```bash
pwd
ls
ls -l
ls -a
ls -lah

cd folder
cd ..
cd ~
cd -
```

```text
.   current folder
..  parent folder
~   home
/   root
```

---

## Create

```bash
mkdir project
mkdir folder1 folder2

touch file.txt
touch a.txt b.txt
```

---

## Copy

```bash
cp file.txt copy.txt
cp file.txt folder/

cp -r project backup/
```

---

## Move / Rename

```bash
mv file.txt folder/

mv old.txt new.txt
```

---

## Delete

```bash
rm file.txt
rmdir empty-folder
rm -r folder
```

⚠️ `rm -r` deletes a directory and everything inside it.

---

# 👀 3. Read Files

```bash
cat file.txt
head file.txt
tail file.txt
less file.txt
```

Specific lines:

```bash
head -5 file.txt
tail -10 file.txt
```

Inside `less`:

```text
q = quit
```

---

# ✍️ 4. Write to Files

Print:

```bash
echo "Hello Linux"
```

Overwrite file:

```bash
echo "hello" > file.txt
```

Append:

```bash
echo "new line" >> file.txt
```

### 🧠 Remember

```text
>   replace
>>  append
```

---

# 🔗 5. Pipes

A pipe sends output from one command into another.

```bash
command1 | command2
```

Examples:

```bash
ps aux | head

grep ERROR server.log | wc -l

du -sh * | sort -h
```

### 🧠 Think

```text
command
   ↓
output
   ↓
next command
```

---

# 🔎 6. Search Inside Files — grep

Basic:

```bash
grep "ERROR" server.log
```

Ignore uppercase/lowercase:

```bash
grep -i "error" server.log
```

Show line numbers:

```bash
grep -n "ERROR" server.log
```

Exclude matches:

```bash
grep -v "INFO" server.log
```

Count matches:

```bash
grep -c "ERROR" server.log
```

Multiple patterns:

```bash
grep -E "ERROR|WARNING" server.log
```

Search multiple files:

```bash
grep -l "ERROR" *.txt
```

### ⭐ Useful Combo

```bash
grep ERROR server.log | wc -l
```

---

# 🔍 7. Find Files

Everything:

```bash
find .
```

Files only:

```bash
find . -type f
```

Directories only:

```bash
find . -type d
```

Find `.txt`:

```bash
find . -type f -name "*.txt"
```

Case insensitive:

```bash
find . -type f -iname "*.txt"
```

Count files:

```bash
find . -type f | wc -l
```

Filter results:

```bash
find . | grep project
```

---

# 🔢 8. Count / Sort / Duplicates

## Count

```bash
wc -l file.txt
wc -w file.txt
wc -c file.txt
```

```text
-l = lines
-w = words
-c = bytes
```

---

## Sort

```bash
sort names.txt
sort -r names.txt
sort -n numbers.txt
sort -nr numbers.txt
```

### 🧠 Remember

```text
-n  numeric
-r  reverse

-nr = biggest number first
```

---

## Duplicates

```bash
sort names.txt | uniq
```

Count occurrences:

```bash
sort names.txt | uniq -c
```

Most common:

```bash
sort names.txt | uniq -c | sort -nr
```

Top 2:

```bash
sort names.txt | uniq -c | sort -nr | head -2
```

---

# 🌟 9. Wildcards

All `.txt` files:

```bash
*.txt
```

Example:

```bash
ls *.txt
```

One unknown character:

```bash
file?.txt
```

---

# 🔐 10. Permissions

Check permissions:

```bash
ls -l
```

Example:

```text
-rwxr-xr-x
```

Meaning:

```text
r = read
w = write
x = execute
```

Numbers:

```text
r = 4
w = 2
x = 1
```

---

## Common Permissions

```bash
chmod 600 secret.txt
chmod 644 notes.txt
chmod 755 script.sh
chmod 700 private.sh
chmod 640 config.txt
chmod 444 readonly.txt
```

### 🧠 Remember These

```text
600 → private file

644 → normal file

755 → executable/script

700 → private executable/folder
```

Add execute:

```bash
chmod +x script.sh
```

Remove execute:

```bash
chmod -x script.sh
```

---

# 👤 11. User Info

```bash
whoami
id
groups
```

---

# ⚙️ 12. Processes

Simple:

```bash
ps
```

All processes:

```bash
ps aux
```

First few:

```bash
ps aux | head
```

Find process:

```bash
pgrep sleep
```

Kill process:

```bash
kill PID
```

Example:

```bash
kill 2450
```

---

# 🏃 13. Foreground & Background

Run normally:

```bash
sleep 300
```

Run in background:

```bash
sleep 300 &
```

Show shell jobs:

```bash
jobs
```

Pause:

```text
Ctrl + Z
```

Resume in background:

```bash
bg
```

Bring back:

```bash
fg
```

Stop:

```text
Ctrl + C
```

### 🧠 Important

```text
jobs   → jobs from MY terminal

ps aux → processes from the SYSTEM
```

---

# 📊 14. System Health

Uptime:

```bash
uptime
```

Memory:

```bash
free -h
```

Disk:

```bash
df -h
```

Directory size:

```bash
du -sh .
```

Size of everything here:

```bash
du -sh *
```

Sort by size:

```bash
du -sh * | sort -h
```

Live process monitor:

```bash
top
```

Snapshot:

```bash
top -b -n 1 | head -20
```

### 🧠 Remember

```text
free → RAM
df   → disk/filesystem
du   → folder/file size
top  → processes/resources
```

---

# 💻 15. System Information

```bash
uname -a
hostname
uptime
```

---

# 🛠️ 16. Services

Check service:

```bash
systemctl status cron
```

Is it running?

```bash
systemctl is-active cron
```

### 🧠 Remember

```text
systemctl → services
```

---

# 📜 17. Logs

Recent logs:

```bash
journalctl -n 20
```

Errors:

```bash
journalctl -p err -n 20
```

Specific service:

```bash
journalctl -u cron -n 20
```

### 🧠 Remember

```text
journalctl → logs
```

---

# 🌐 18. Networking

IP addresses:

```bash
ip addr
```

Routes:

```bash
ip route
```

Test connectivity:

```bash
ping -c 4 8.8.8.8
```

Open/listening ports:

```bash
ss -tulpn
```

### 🧠 Mental Model

```text
ip addr  → what IP do I have?

ip route → where does traffic go?

ping     → can I reach it?

ss       → what ports/services are open?
```

---

# 📦 19. apt — Install Software

Version:

```bash
apt --version
```

Refresh packages:

```bash
sudo apt update
```

Install:

```bash
sudo apt install PACKAGE
```

Example:

```bash
sudo apt install python3.14-venv
```

Remove:

```bash
sudo apt remove PACKAGE
```

Package info:

```bash
apt show curl
```

Installed packages:

```bash
apt list --installed
```

Updates available:

```bash
apt list --upgradable
```

---

# 🌱 20. Environment Variables

Check common variables:

```bash
echo $HOME
echo $USER
echo $SHELL
echo $PATH
```

Create:

```bash
AI_PROJECT="linux-day5"
```

Read:

```bash
echo $AI_PROJECT
```

Export:

```bash
export AI_PROJECT
```

View environment:

```bash
env
```

Search environment:

```bash
env | grep AI_PROJECT
```

### Used For

```text
API keys
database URLs
settings
debug flags
model configuration
```

---

# 🛣️ 21. PATH

```bash
echo $PATH
```

Example:

```text
/usr/local/bin:/usr/bin:/bin
```

Linux checks these folders when you run commands.

---

# 🕵️ 22. Where Does a Command Come From?

```bash
which python3
which bash
which grep
which curl
which ssh
```

More locations:

```bash
whereis bash
whereis python3
```

Command type:

```bash
type cd
type ls
type clear
```

---

# 📦 23. tar — Backups & Archives

Create:

```bash
tar -czf backup.tar.gz folder/
```

View contents:

```bash
tar -tzf backup.tar.gz
```

Extract:

```bash
tar -xzf backup.tar.gz
```

Extract somewhere:

```bash
tar -xzf backup.tar.gz -C extracted/
```

### 🧠 Flags

```text
c → create
x → extract
t → show contents
z → gzip
f → filename
C → destination folder
```

---

# 🔗 24. Symbolic Links

Create:

```bash
ln -s /path/to/original shortcut
```

Example:

```bash
ln -s ~/project/config.txt config-link.txt
```

Check:

```bash
ls -l config-link.txt
```

### 🧠 Remember

```text
copy → new file

symlink → shortcut/reference
```

---

# 🌍 25. curl — HTTP / APIs

Get webpage/API:

```bash
curl https://example.com
```

Headers only:

```bash
curl -I https://example.com
```

Follow redirects:

```bash
curl -L https://example.com
```

Save response:

```bash
curl -L https://example.com -o example.html
```

### 🧠 Flags

```text
-I → headers
-L → follow redirect
-o → save as file
```

Very useful later for testing APIs:

```bash
curl http://localhost:8000
```

---

# 🖥️ 26. SSH — Remote Servers

Version:

```bash
ssh -V
```

Location:

```bash
which ssh
```

Connect:

```bash
ssh user@server
```

Example syntax:

```bash
ssh ubuntu@server-ip
```

### Common Errors

```text
Could not resolve hostname
→ hostname problem

No route to host
→ network/host unreachable
```

---

# 🐍 27. Python Virtual Environment

Create project:

```bash
mkdir ai-demo
cd ai-demo
```

Create environment:

```bash
python3 -m venv .venv
```

Activate:

```bash
source .venv/bin/activate
```

Check:

```bash
which python
which python3
which pip
```

Deactivate:

```bash
deactivate
```

Delete environment:

```bash
rm -rf .venv
```

### 🧠 Mental Model

```text
System Python
     ↓
Project
     ↓
.venv
     ↓
project packages
```

---

# 📜 28. Bash Scripts

Create:

```bash
nano system-check.sh
```

Example:

```bash
#!/bin/bash

echo "=== SYSTEM CHECK ==="

whoami
pwd
which python3
free -h
df -h
```

Make executable:

```bash
chmod +x system-check.sh
```

Run:

```bash
./system-check.sh
```

### Shebang

```bash
#!/bin/bash
```

means:

```text
run this script using Bash
```

---

# 🔁 29. Bash Loop

```bash
for i in {1..15}; do
    echo $i
done
```

One line:

```bash
for i in {1..15}; do echo $i; done
```

---

# ✏️ 30. Nano Shortcuts

Open file:

```bash
nano file.txt
```

```text
Ctrl + O → save
Enter    → confirm
Ctrl + X → exit
```

---

# ⌨️ 31. Terminal Shortcuts

```text
Tab      → autocomplete

Ctrl + R → search history

Ctrl + A → start of line

Ctrl + E → end of line

Ctrl + L → clear screen

Ctrl + C → stop process

Ctrl + Z → pause process
```

---

# 🩺 32. Linux Troubleshooting Cheat Flow

When something breaks:

```bash
uptime
```

⬇️

```bash
free -h
```

⬇️

```bash
df -h
```

⬇️

```bash
du -sh * | sort -h
```

⬇️

```bash
ps aux
```

⬇️

```bash
systemctl status SERVICE
```

⬇️

```bash
journalctl -u SERVICE -n 20
```

⬇️

```bash
ip addr
ip route
```

⬇️

```bash
ping -c 4 8.8.8.8
```

⬇️

```bash
ss -tulpn
```

### 🧠 Think

```text
CPU/load
↓
RAM
↓
disk
↓
large files
↓
process
↓
service
↓
logs
↓
network
↓
ports
```

---

# 🤖 33. AI / Backend Project Routine

When opening a project:

```bash
cd project
ls -lah
```

Activate Python environment:

```bash
source .venv/bin/activate
```

Verify Python:

```bash
which python
```

Check environment:

```bash
env
```

Check processes:

```bash
ps aux
```

Check resources:

```bash
free -h
df -h
```

Test backend:

```bash
curl http://localhost:PORT
```

Done:

```bash
deactivate
```

---

# 🧠 Commands Worth Memorizing

Don't memorize everything.

Memorize these:

```bash
pwd
ls -lah
cd
mkdir
touch

cp
mv
rm

cat
head
tail

grep
find

ps aux
pgrep
kill

free -h
df -h
du -sh

systemctl
journalctl

ip addr
ip route
ping
ss -tulpn

apt
env
export
which

tar
curl
ssh

python3 -m venv .venv
source .venv/bin/activate
deactivate
```

Everything else can be looked up.

---

# 🚨 Things I Personally Messed Up

These are worth remembering because I actually made these mistakes:

```text
chmod +x  → ADD execute permission
chmod -x  → REMOVE execute permission
```

```text
tar -c → create
tar -x → extract
tar -C → destination directory
```

```text
df → whole filesystem
du → files/directories
```

```text
jobs → current terminal jobs
ps aux → system processes
```

```text
systemctl → services
journalctl → logs
```

```text
source .venv/bin/activate
NOT
source .venv/bin/active
```

```text
grep -v → exclude matches
grep -V → grep version
```
