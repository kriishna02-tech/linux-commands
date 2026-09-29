[linux_days_1_to_3_theory_commands_only.md](https://github.com/user-attachments/files/32799272/linux_days_1_to_3_theory_commands_only.md)
# Linux Learning Journey — Days 1 to 3 🐧

A practical beginner Linux ref# Linux Learning Journey — Days 1 to 3 🐧

A practical beginner Linux reference covering terminal basics, file handling, text processing, permissions, users, and process management.

---

# Day 1 — Terminal & Filesystem Basics

## 📍 Navigation

| Command | Description |
|---|---|
| `whoami` | Show the current logged-in user |
| `pwd` | Show the full path of the current working directory |
| `ls` | List files and directories |
| `ls -l` | Long listing with permissions, owner, size, and time |
| `ls -a` | Show hidden files |
| `ls -lh` | Long listing with human-readable sizes |
| `ls -lah` | Long listing + hidden files + readable sizes |
| `cd folder` | Enter a directory |
| `cd ..` | Go to the parent directory |
| `cd .` | Stay in the current directory |
| `cd ~` | Go to the home directory |
| `cd -` | Go back to the previous directory |
| `clear` / `Ctrl+L` | Clear the terminal screen |

### Important Path Symbols

| Symbol | Meaning |
|---|---|
| `/` | Filesystem root |
| `~` | Home directory |
| `.` | Current directory |
| `..` | Parent directory |

### Absolute vs Relative Paths

Absolute path:

```text
/home/alex/linux-lab/documents/notes.txt
```

Relative path:

```text
documents/notes.txt
```

Think:

```text
Absolute path = full address
Relative path = directions from where you are now
```

---

## 📁 Creating Files & Directories

| Command | Description |
|---|---|
| `mkdir folder` | Create a directory |
| `mkdir dir1 dir2 dir3` | Create multiple directories |
| `touch file.txt` | Create an empty file |
| `touch one.txt two.txt` | Create multiple files |

### Important

```bash
mkdir notes.txt
```

creates a directory named `notes.txt`.

```bash
touch notes.txt
```

creates a regular file.

Linux does not treat `.txt` as magical. The name alone does not define whether something is a file or directory.

---

## 📂 Copying, Moving & Renaming

| Command | Description |
|---|---|
| `cp source destination` | Copy a file |
| `cp fileA fileB` | Copy fileA into fileB |
| `mv source destination` | Move a file |
| `mv oldname newname` | Rename a file |

Examples:

```bash
cp documents/notes.txt downloads/
mv downloads/test.txt projects/
mv projects/app.txt projects/main.txt
```

Copy and rename:

```bash
cp documents/notes.txt backup/notes-copy.txt
```

---

## 🗑️ Deleting Files & Directories

| Command | Description |
|---|---|
| `rm file.txt` | Delete a file |
| `rmdir folder` | Delete an empty directory |
| `rm -r folder` | Delete a directory and everything inside it |

### Safe Habit

Before recursive deletion:

```bash
pwd
ls
```

Then verify the target.

---

## 👻 Hidden Files

Hidden files usually start with `.`

Example:

```bash
touch .config
```

Normal listing:

```bash
ls
```

Hidden listing:

```bash
ls -a
```

Remember:

```text
.  = current directory
.. = parent directory
```

---

## 📄 Viewing File Content

| Command | Description |
|---|---|
| `cat file` | Show the full file |
| `head file` | Show the first 10 lines |
| `head -5 file` | Show the first 5 lines |
| `tail file` | Show the last 10 lines |
| `tail -5 file` | Show the last 5 lines |
| `less file` | Scroll through a file interactively |

Useful `less` controls:

| Key | Action |
|---|---|
| `↑ / ↓` | Move through file |
| `/word` | Search |
| `n` | Next search result |
| `q` | Quit |

---

## 📝 Writing Text & Redirection

| Command | Description |
|---|---|
| `echo "text"` | Print text |
| `echo "text" > file.txt` | Overwrite file with text |
| `echo "text" >> file.txt` | Append text |

Remember:

```text
>  = overwrite
>> = append
```

---

## 🔍 Inspecting Directory Structure

```bash
find .
```

Example:

```text
.
./documents
./documents/linux.txt
./documents/notes.txt
./projects
./projects/main.txt
```

---

## 🔁 Basic Bash Loop

```bash
for i in {1..15}; do echo "line $i" >> notes.txt; done
```

---

## ⌨️ Useful Terminal Shortcuts

| Shortcut | Description |
|---|---|
| `↑` | Previous command |
| `↓` | Next command |
| `Ctrl+R` | Search command history |
| `Tab` | Autocomplete |
| `Ctrl+A` | Move to start of line |
| `Ctrl+E` | Move to end of line |
| `Ctrl+L` | Clear screen |
| `Ctrl+C` | Stop current command |

---

## 🧠 Day 1 Mental Model

```text
Who am I?
↓
Where am I?
↓
What is here?
↓
What path do I need?
↓
What command should I use?
↓
How do I verify it?
```

---

# Day 2 — Search, Filter, Count & Sort

## 🔎 `grep`

| Command | Description |
|---|---|
| `grep "word" file` | Show lines containing the word |
| `grep -i "word" file` | Ignore uppercase/lowercase |
| `grep -n "word" file` | Show matching line numbers |
| `grep -v "word" file` | Show lines that do NOT match |
| `grep -c "word" file` | Count matching lines |
| `grep -l "word" file` | Show filename if it contains a match |
| `grep -E "A|B" file` | Match A OR B |

Examples:

```bash
grep "ERROR" server.log
grep -i "alice" server.log
grep -n "ERROR" server.log
grep -v "INFO" server.log
grep -E "ERROR|WARNING" server.log
```

---

## 🔢 `wc`

| Command | Description |
|---|---|
| `wc file` | Show lines, words, and bytes |
| `wc -l file` | Count lines |
| `wc -w file` | Count words |
| `wc -c file` | Count bytes |

---

## 🔗 Pipes `|`

```bash
grep "ERROR" server.log | wc -l
```

Mental model:

```text
find ERROR lines
↓
count them
```

---

## 🔃 `sort` and `uniq`

| Command | Description |
|---|---|
| `sort file` | Sort alphabetically |
| `sort -r file` | Reverse sort |
| `uniq` | Remove consecutive duplicate lines |
| `uniq -c` | Count consecutive duplicates |
| `sort -nr` | Numeric sort, highest first |

Examples:

```bash
sort names.txt | uniq
sort names.txt | uniq -c
sort names.txt | uniq -c | sort -nr
sort names.txt | uniq -c | sort -nr | head -2
```

### Why `sort -nr`?

```text
-n = numeric
-r = reverse
```

So `sort -nr` sorts numbers from largest to smallest.

---

## 🔍 `find`

| Command | Description |
|---|---|
| `find . -type f` | Find files only |
| `find . -type d` | Find directories only |
| `find . -name "*.txt"` | Find `.txt` files |
| `find . -iname "*.txt"` | Case-insensitive filename search |

Examples:

```bash
find . -name "*.txt" | wc -l
find . -type f | grep "notes"
```

---

## 💾 Saving Filtered Output

```bash
grep "ERROR" server.log > errors.txt
grep -v "INFO" server.log > problems.txt
```

Verify:

```bash
cat errors.txt
cat problems.txt
```

---

## 🧠 Day 2 Mental Model

```text
Get data
↓
Filter it
↓
Count / sort / rank it
↓
Display or save result
```

---

# Day 3 — Permissions, Users & Processes

## 🔐 File Permissions

Example:

```text
-rw-r--r--
```

Breakdown:

```text
-   rw-   r--   r--
    owner group others
```

File type:

```text
- = regular file
d = directory
```

Permission letters:

| Letter | Meaning |
|---|---|
| `r` | read |
| `w` | write |
| `x` | execute/access |

Numeric values:

| Permission | Value |
|---|---|
| `r` | 4 |
| `w` | 2 |
| `x` | 1 |

Examples:

```text
7 = rwx = 4+2+1
6 = rw- = 4+2
5 = r-x = 4+1
4 = r--
```

---

## 🔧 `chmod`

```bash
chmod 600 file
chmod 644 file
chmod 755 file
```

Meaning:

```text
600 = rw-------
644 = rw-r--r--
755 = rwxr-xr-x
700 = rwx------
640 = rw-r-----
444 = r--r--r--
```

The three digits represent:

```text
owner | group | others
```

---

## 👤 Users & Groups

| Command | Description |
|---|---|
| `whoami` | Show current username |
| `id` | Show UID, GID, and groups |
| `groups` | Show groups the user belongs to |

---

## ⚙️ Processes

A process is a running program.

```text
PID = Process ID
```

### `ps`

```bash
ps
```

Shows processes attached to the current shell.

### `ps aux`

```bash
ps aux
```

Shows a much broader process list.

Useful columns:

| Column | Meaning |
|---|---|
| `USER` | Process owner |
| `PID` | Process ID |
| `%CPU` | CPU usage |
| `%MEM` | Memory usage |
| `STAT` | Process state |
| `COMMAND` | Program/command |

---

## 😴 `sleep`

`sleep` is a standard Unix/Linux command.

```bash
sleep 300
```

means:

> wait for 300 seconds, then exit.

Examples:

```bash
sleep 5
sleep 30
sleep 300
sleep 2m
sleep 1h
```

It is useful for safe process-management practice.

---

## 🏃 Background Processes

```bash
sleep 300 &
```

The `&` runs the command in the background.

Example output:

```text
[1] 1303
```

Meaning:

```text
1    = shell job number
1303 = PID
```

---

## 🧰 Job Control

| Command / Shortcut | Description |
|---|---|
| `jobs` | Show shell jobs |
| `Ctrl+Z` | Pause current foreground job |
| `bg` | Continue paused job in background |
| `fg` | Bring job to foreground |
| `Ctrl+C` | Stop foreground process |

---

## 🔎 Finding Processes

```bash
pgrep sleep
```

or:

```bash
ps aux | grep sleep
```

---

## 🛑 Killing Processes

```bash
kill PID
```

Example:

```bash
kill 1303
```

Verify:

```bash
pgrep sleep
```

---

## 📊 `top`

Live system/process monitor:

```bash
top
```

Useful information:

```text
load average
CPU usage
memory usage
running/sleeping processes
PID
%CPU
%MEM
COMMAND
```

Press:

```text
q
```

to quit.

One-shot view:

```bash
top -b -n 1 | head -20
```

---

## 🧠 Day 3 Mental Model

Permissions:

```text
Who owns this?
↓
Who can read?
↓
Who can write?
↓
Who can execute?
```

Processes:

```text
What is running?
↓
What is its PID?
↓
Foreground or background?
↓
Pause, resume, or stop?
```

---

# Common Mistakes From Days 1–3

## `mkdir` vs `touch`

```bash
mkdir notes.txt   # directory
touch notes.txt   # file
```

## Wrong relative path

Check:

```bash
pwd
ls
```

## `>` vs `>>`

```text
>  overwrite
>> append
```

## Case-sensitive options

```bash
grep -v   # invert match
grep -V   # version
```

## Wrong `find` syntax

Wrong:

```bash
find . type -f
```

Correct:

```bash
find . -type f
```

## Wrong pipeline order

Better:

```bash
sort names.txt | uniq -c
```

## `rm` vs `rm -r`

```bash
rm file.txt
rm -r folder
```

---

# Command Cheat Sheet

## Day 1

```bash
whoami
pwd
ls
ls -lah
cd
mkdir
touch
cp
mv
rm
rmdir
find .
cat
head
tail
less
echo
history
```

## Day 2

```bash
grep
grep -i
grep -n
grep -v
grep -c
grep -E
wc
wc -l
sort
sort -r
sort -nr
uniq
uniq -c
find . -type f
find . -type d
find . -name "*.txt"
|
>
>>
```

## Day 3

```bash
chmod
whoami
id
groups
ps
ps aux
sleep
jobs
pgrep
bg
fg
kill
top
```

---

# Final 3-Day Mental Model

```text
Day 1:
Navigate → Create → Move → Read → Delete → Verify

Day 2:
Search → Filter → Count → Sort → Save

Day 3:
Permissions → Users → Processes → Control
```

---
erence covering terminal basics, file handling, text processing, permissions, users, and process management.

---

# Day 1 — Terminal & Filesystem Basics

## 📍 Navigation

| Command | Description |
|---|---|
| `whoami` | Show the current logged-in user |
| `pwd` | Show the full path of the current working directory |
| `ls` | List files and directories |
| `ls -l` | Long listing with permissions, owner, size, and time |
| `ls -a` | Show hidden files |
| `ls -lh` | Long listing with human-readable sizes |
| `ls -lah` | Long listing + hidden files + readable sizes |
| `cd folder` | Enter a directory |
| `cd ..` | Go to the parent directory |
| `cd .` | Stay in the current directory |
| `cd ~` | Go to the home directory |
| `cd -` | Go back to the previous directory |
| `clear` / `Ctrl+L` | Clear the terminal screen |

### Important Path Symbols

| Symbol | Meaning |
|---|---|
| `/` | Filesystem root |
| `~` | Home directory |
| `.` | Current directory |
| `..` | Parent directory |

### Absolute vs Relative Paths

Absolute path:

```text
/home/alex/linux-lab/documents/notes.txt
```

Relative path:

```text
documents/notes.txt
```

Think:

```text
Absolute path = full address
Relative path = directions from where you are now
```

---

## 📁 Creating Files & Directories

| Command | Description |
|---|---|
| `mkdir folder` | Create a directory |
| `mkdir dir1 dir2 dir3` | Create multiple directories |
| `touch file.txt` | Create an empty file |
| `touch one.txt two.txt` | Create multiple files |

### Important

```bash
mkdir notes.txt
```

creates a directory named `notes.txt`.

```bash
touch notes.txt
```

creates a regular file.

Linux does not treat `.txt` as magical. The name alone does not define whether something is a file or directory.

---

## 📂 Copying, Moving & Renaming

| Command | Description |
|---|---|
| `cp source destination` | Copy a file |
| `cp fileA fileB` | Copy fileA into fileB |
| `mv source destination` | Move a file |
| `mv oldname newname` | Rename a file |

Examples:

```bash
cp documents/notes.txt downloads/
mv downloads/test.txt projects/
mv projects/app.txt projects/main.txt
```

Copy and rename:

```bash
cp documents/notes.txt backup/notes-copy.txt
```

---

## 🗑️ Deleting Files & Directories

| Command | Description |
|---|---|
| `rm file.txt` | Delete a file |
| `rmdir folder` | Delete an empty directory |
| `rm -r folder` | Delete a directory and everything inside it |

### Safe Habit

Before recursive deletion:

```bash
pwd
ls
```

Then verify the target.

---

## 👻 Hidden Files

Hidden files usually start with `.`

Example:

```bash
touch .config
```

Normal listing:

```bash
ls
```

Hidden listing:

```bash
ls -a
```

Remember:

```text
.  = current directory
.. = parent directory
```

---

## 📄 Viewing File Content

| Command | Description |
|---|---|
| `cat file` | Show the full file |
| `head file` | Show the first 10 lines |
| `head -5 file` | Show the first 5 lines |
| `tail file` | Show the last 10 lines |
| `tail -5 file` | Show the last 5 lines |
| `less file` | Scroll through a file interactively |

Useful `less` controls:

| Key | Action |
|---|---|
| `↑ / ↓` | Move through file |
| `/word` | Search |
| `n` | Next search result |
| `q` | Quit |

---

## 📝 Writing Text & Redirection

| Command | Description |
|---|---|
| `echo "text"` | Print text |
| `echo "text" > file.txt` | Overwrite file with text |
| `echo "text" >> file.txt` | Append text |

Remember:

```text
>  = overwrite
>> = append
```

---

## 🔍 Inspecting Directory Structure

```bash
find .
```

Example:

```text
.
./documents
./documents/linux.txt
./documents/notes.txt
./projects
./projects/main.txt
```

---

## 🔁 Basic Bash Loop

```bash
for i in {1..15}; do echo "line $i" >> notes.txt; done
```

---

## ⌨️ Useful Terminal Shortcuts

| Shortcut | Description |
|---|---|
| `↑` | Previous command |
| `↓` | Next command |
| `Ctrl+R` | Search command history |
| `Tab` | Autocomplete |
| `Ctrl+A` | Move to start of line |
| `Ctrl+E` | Move to end of line |
| `Ctrl+L` | Clear screen |
| `Ctrl+C` | Stop current command |

---

## 🧠 Day 1 Mental Model

```text
Who am I?
↓
Where am I?
↓
What is here?
↓
What path do I need?
↓
What command should I use?
↓
How do I verify it?
```

---

# Day 2 — Search, Filter, Count & Sort

## 🔎 `grep`

| Command | Description |
|---|---|
| `grep "word" file` | Show lines containing the word |
| `grep -i "word" file` | Ignore uppercase/lowercase |
| `grep -n "word" file` | Show matching line numbers |
| `grep -v "word" file` | Show lines that do NOT match |
| `grep -c "word" file` | Count matching lines |
| `grep -l "word" file` | Show filename if it contains a match |
| `grep -E "A|B" file` | Match A OR B |

Examples:

```bash
grep "ERROR" server.log
grep -i "alice" server.log
grep -n "ERROR" server.log
grep -v "INFO" server.log
grep -E "ERROR|WARNING" server.log
```

---

## 🔢 `wc`

| Command | Description |
|---|---|
| `wc file` | Show lines, words, and bytes |
| `wc -l file` | Count lines |
| `wc -w file` | Count words |
| `wc -c file` | Count bytes |

---

## 🔗 Pipes `|`

```bash
grep "ERROR" server.log | wc -l
```

Mental model:

```text
find ERROR lines
↓
count them
```

---

## 🔃 `sort` and `uniq`

| Command | Description |
|---|---|
| `sort file` | Sort alphabetically |
| `sort -r file` | Reverse sort |
| `uniq` | Remove consecutive duplicate lines |
| `uniq -c` | Count consecutive duplicates |
| `sort -nr` | Numeric sort, highest first |

Examples:

```bash
sort names.txt | uniq
sort names.txt | uniq -c
sort names.txt | uniq -c | sort -nr
sort names.txt | uniq -c | sort -nr | head -2
```

### Why `sort -nr`?

```text
-n = numeric
-r = reverse
```

So `sort -nr` sorts numbers from largest to smallest.

---

## 🔍 `find`

| Command | Description |
|---|---|
| `find . -type f` | Find files only |
| `find . -type d` | Find directories only |
| `find . -name "*.txt"` | Find `.txt` files |
| `find . -iname "*.txt"` | Case-insensitive filename search |

Examples:

```bash
find . -name "*.txt" | wc -l
find . -type f | grep "notes"
```

---

## 💾 Saving Filtered Output

```bash
grep "ERROR" server.log > errors.txt
grep -v "INFO" server.log > problems.txt
```

Verify:

```bash
cat errors.txt
cat problems.txt
```

---

## 🧠 Day 2 Mental Model

```text
Get data
↓
Filter it
↓
Count / sort / rank it
↓
Display or save result
```

---

# Day 3 — Permissions, Users & Processes

## 🔐 File Permissions

Example:

```text
-rw-r--r--
```

Breakdown:

```text
-   rw-   r--   r--
    owner group others
```

File type:

```text
- = regular file
d = directory
```

Permission letters:

| Letter | Meaning |
|---|---|
| `r` | read |
| `w` | write |
| `x` | execute/access |

Numeric values:

| Permission | Value |
|---|---|
| `r` | 4 |
| `w` | 2 |
| `x` | 1 |

Examples:

```text
7 = rwx = 4+2+1
6 = rw- = 4+2
5 = r-x = 4+1
4 = r--
```

---

## 🔧 `chmod`

```bash
chmod 600 file
chmod 644 file
chmod 755 file
```

Meaning:

```text
600 = rw-------
644 = rw-r--r--
755 = rwxr-xr-x
700 = rwx------
640 = rw-r-----
444 = r--r--r--
```

The three digits represent:

```text
owner | group | others
```

---

## 👤 Users & Groups

| Command | Description |
|---|---|
| `whoami` | Show current username |
| `id` | Show UID, GID, and groups |
| `groups` | Show groups the user belongs to |

---

## ⚙️ Processes

A process is a running program.

```text
PID = Process ID
```

### `ps`

```bash
ps
```

Shows processes attached to the current shell.

### `ps aux`

```bash
ps aux
```

Shows a much broader process list.

Useful columns:

| Column | Meaning |
|---|---|
| `USER` | Process owner |
| `PID` | Process ID |
| `%CPU` | CPU usage |
| `%MEM` | Memory usage |
| `STAT` | Process state |
| `COMMAND` | Program/command |

---

## 😴 `sleep`

`sleep` is a standard Unix/Linux command.

```bash
sleep 300
```

means:

> wait for 300 seconds, then exit.

Examples:

```bash
sleep 5
sleep 30
sleep 300
sleep 2m
sleep 1h
```

It is useful for safe process-management practice.

---

## 🏃 Background Processes

```bash
sleep 300 &
```

The `&` runs the command in the background.

Example output:

```text
[1] 1303
```

Meaning:

```text
1    = shell job number
1303 = PID
```

---

## 🧰 Job Control

| Command / Shortcut | Description |
|---|---|
| `jobs` | Show shell jobs |
| `Ctrl+Z` | Pause current foreground job |
| `bg` | Continue paused job in background |
| `fg` | Bring job to foreground |
| `Ctrl+C` | Stop foreground process |

---

## 🔎 Finding Processes

```bash
pgrep sleep
```

or:

```bash
ps aux | grep sleep
```

---

## 🛑 Killing Processes

```bash
kill PID
```

Example:

```bash
kill 1303
```

Verify:

```bash
pgrep sleep
```

---

## 📊 `top`

Live system/process monitor:

```bash
top
```

Useful information:

```text
load average
CPU usage
memory usage
running/sleeping processes
PID
%CPU
%MEM
COMMAND
```

Press:

```text
q
```

to quit.

One-shot view:

```bash
top -b -n 1 | head -20
```

---

## 🧠 Day 3 Mental Model

Permissions:

```text
Who owns this?
↓
Who can read?
↓
Who can write?
↓
Who can execute?
```

Processes:

```text
What is running?
↓
What is its PID?
↓
Foreground or background?
↓
Pause, resume, or stop?
```

---

# Common Mistakes From Days 1–3

## `mkdir` vs `touch`

```bash
mkdir notes.txt   # directory
touch notes.txt   # file
```

## Wrong relative path

Check:

```bash
pwd
ls
```

## `>` vs `>>`

```text
>  overwrite
>> append
```

## Case-sensitive options

```bash
grep -v   # invert match
grep -V   # version
```

## Wrong `find` syntax

Wrong:

```bash
find . type -f
```

Correct:

```bash
find . -type f
```

## Wrong pipeline order

Better:

```bash
sort names.txt | uniq -c
```

## `rm` vs `rm -r`

```bash
rm file.txt
rm -r folder
```

---

# Quick Revision Cheat Sheet

## Day 1

```bash
whoami
pwd
ls
ls -lah
cd
mkdir
touch
cp
mv
rm
rmdir
find .
cat
head
tail
less
echo
history
```

## Day 2

```bash
grep
grep -i
grep -n
grep -v
grep -c
grep -E
wc
wc -l
sort
sort -r
sort -nr
uniq
uniq -c
find . -type f
find . -type d
find . -name "*.txt"
|
>
>>
```

## Day 3

```bash
chmod
whoami
id
groups
ps
ps aux
sleep
jobs
pgrep
bg
fg
kill
top
```

---

# Final 3-Day Mental Model

```text
Day 1:
Navigate → Create → Move → Read → Delete → Verify

Day 2:
Search → Filter → Count → Sort → Save

Day 3:
Permissions → Users → Processes → Control
```

---

# Quick Self-Test

1. What does `pwd` do?
2. What is the difference between `.` and `..`?
3. What does `cd -` do?
4. Difference between `mkdir` and `touch`?
5. What does `>` do?
6. What does `>>` do?
7. How do you count `ERROR` lines in a log?
8. What does `grep -v` do?
9. Why use `sort` before `uniq -c`?
10. What does `sort -nr` do?
11. What does `find . -type f` show?
12. What does `chmod 640 file` mean?
13. What does `x` mean?
14. What is a PID?
15. What does `sleep 300 &` do?
16. What does `jobs` show?
17. Difference between `bg` and `fg`?
18. What does `kill PID` do?
19. What information does `top` show?
20. Why is `sleep` useful for process practice?

---

*Days 1–3 complete. Next: system information, disk, memory, services, logs, and basic networking.*
