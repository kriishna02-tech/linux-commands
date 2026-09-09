# Linux Commands — Learning Journey 🐧

A personal reference of Linux commands I'm learning and practicing, organized by category.

---

## 📍 Navigation

| Command | Description |
|---|---|
| `pwd` | Print current working directory (shows full path) |
| `ls` | List files and folders in current directory |
| `ls -lt` | List in long format, sorted by modified time |
| `ls -lh` | List in long format, with human-readable file sizes |
| `ls -la` | List all files including hidden ones (starting with `.`) |
| `cd foldername` | Change into a folder |
| `cd ..` | Move up one directory level |
| `cd` or `cd ~` | Go to home directory |
| `whoami` | Display current logged-in user |
| `clear` / `Ctrl+L` | Clear the terminal screen |

---

## 🕒 Date & Time

| Command | Description |
|---|---|
| `date` | Show current system date and time |
| `date +%T` | Show time only (HH:MM:SS) |
| `date +%H` | Show hour only |
| `date +%M` | Show minutes only |
| `date +%d-%m-%Y` | Show date in DD-MM-YYYY format |
| `date +%A` | Show weekday name |

---

## 📄 Viewing File Content

| Command | Description |
|---|---|
| `cat file` | Print entire file content at once |
| `more file` | View file page by page (forward only) |
| `less file` | View file page by page, scroll both directions, supports search (`/word`, `n` for next, `q` to quit) |
| `head -5 file` | Show top 5 lines of a file |
| `tail -5 file` | Show bottom 5 lines of a file |
| `wc -l file` | Count number of lines in a file |
| `wc file` | Count lines, words, and characters |

---

## 📝 Creating & Editing Files

| Command | Description |
|---|---|
| `touch file.txt` | Create a new empty file |
| `touch file{1..5}` | Create multiple files at once (file1–file5) using brace expansion |
| `echo "text" > file.txt` | Write text into a file (overwrites existing content) |
| `echo "text" >> file.txt` | Append text to a file (keeps existing content) |
| `nano file.txt` | Edit file with nano — `Ctrl+O` to save, `Ctrl+X` to exit |
| `vi file.txt` | Edit file with vi — `i` for insert mode, `Esc` to exit insert mode, `:wq` to save & quit, `:q!` to quit without saving |

---

## 🗑️ Deleting Files & Folders

| Command | Description |
|---|---|
| `rm file.txt` | Delete a file |
| `mkdir foldername` | Create a new directory |
| `rmdir foldername` | Delete a directory (only if empty) |
| `rm -rf foldername` | Force-delete a directory and everything inside it |

---

## 📂 Copying & Moving

| Command | Description |
|---|---|
| `cp file.txt /dest/path/` | Copy a file into another folder |
| `cp fileA fileB` | Copy content of fileA into fileB |
| `mv file.txt /dest/path/` | Move (cut-paste) a file into another folder |
| `mv oldname newname` | Rename a file (same command as move, same folder) |

---

## 🔍 Searching & Filtering

| Command | Description |
|---|---|
| `grep "word" file` | Search for a word, print matching lines |
| `grep -i "word" file` | Case-insensitive search |
| `grep -v "word" file` | Show lines that **don't** match |
| `grep -c "word" file` | Count matching lines |
| `grep -l "word" file` | Show only the filename if a match is found |
| `grep -n "word" file` | Show matching lines with line numbers |
| `egrep "word1|word2" file` | Search for multiple words (OR condition) |
| `find /path -name filename` | Find a file by name starting from a given path |

---

## 🔃 Sorting & Comparing

| Command | Description |
|---|---|
| `sort file` | Sort lines alphabetically (A→Z) |
| `sort -r file` | Sort lines in reverse (Z→A) |
| `sort file \| uniq` | Remove duplicate (consecutive) lines |
| `split -l 3 file` | Split a file into multiple files, 3 lines each |
| `cmp fileA fileB` | Check if two files are identical (byte by byte) |
| `diff -u fileA fileB` | Show detailed differences between two files (unified diff format) |
| `shuf file` | Randomly shuffle the lines of a file |

---

## 🌟 Wildcards

| Pattern | Description |
|---|---|
| `*` | Matches any characters — e.g. `ls file*` lists all files starting with "file" |
| `{1..5}` | Brace expansion — e.g. `touch file{1..5}` creates file1 through file5 |

---

## 🛠️ Compiling & Running Programs

| Command | Description |
|---|---|
| `gcc -o output file.c` | Compile a C source file into an executable |
| `g++ -o output file.cpp` | Compile a C++ source file into an executable |
| `./output` | Run a compiled program in the current directory |

---

## 📌 Notes to Self

- `>` overwrites a file, `>>` appends — easy to mix these up.
- `cp`/`rm` need `-r` to work on directories.
- Always `ls` before deleting something you're not 100% sure about.
- `less` > `more` for big files — supports backward scroll and search.
- vi opens in **Normal mode** by default — press `i` before typing anything.

---

*Last updated: work in progress — adding more commands as I learn (`history`, `man`, `which`, permissions, and beyond).*
