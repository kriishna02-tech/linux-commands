Linux Day 1 Notes — Beginner Terminal & Filesystem Fundamentals

1. Goal of Day 1

The goal of Day 1 is to become comfortable with the Linux terminal and understand how to:

identify the current user

identify the current working directory

list files and directories

move around the filesystem

create files and directories

copy, move, rename, and delete files

inspect directory structures

work with hidden files

read file contents

use basic shell redirection

use command history and terminal shortcuts

understand common beginner errors

By the end of this material, a beginner should be able to work confidently inside a Linux directory using the terminal.

2. Understanding the Linux Terminal Prompt

A Linux prompt may look like this:

user@computer:~/linux-lab$

A simplified interpretation:

user        -> current username
computer    -> computer or hostname
~           -> current directory is the user's home directory
$           -> normal user shell prompt

The ~ symbol represents the current user's home directory.

For example:

/home/alex

may be represented as:

~

So:

cd ~

means:

Go to the current user's home directory.

3. Finding Out Who and Where You Are

whoami

Displays the current username.

whoami

Example output:

alex

Useful when working on servers, virtual machines, or systems with multiple user accounts.

pwd

pwd means:

print working directory

It displays the full path of the directory currently being used.

pwd

Example:

/home/alex/linux-lab

A good Linux habit is to run pwd before using destructive commands if there is any uncertainty about the current location.

4. Listing Files and Directories

ls

Lists files and directories in the current location.

ls

Example:

documents  downloads  projects

ls -l

Displays detailed information.

ls -l

Example:

drwxr-xr-x 2 alex alex 4096 Sep 26 10:30 documents

The columns roughly mean:

drwxr-xr-x   permissions and file type
2            hard-link count
alex         owner
alex         group
4096         size in bytes
Sep 26 10:30 last modification time
documents    name

ls -a

Shows all files, including hidden ones.

ls -a

Hidden files begin with a dot:

.config
.bashrc
.profile

Linux does not require a special hidden-file attribute. A filename beginning with . is normally treated as hidden by tools such as ls.

ls -h

The -h option means:

human-readable

It is most useful with long listing output:

ls -lh

Instead of displaying:

4096

Linux may display:

4.0K

ls -lah

A commonly useful combination:

ls -lah

It means:

l -> long listing

a -> include hidden files

h -> human-readable sizes

5. Navigating the Filesystem

cd

cd means:

change directory

Example:

cd documents

This enters the documents directory.

cd ..

Moves to the parent directory.

Example:

/home/alex/linux-lab/documents

Running:

cd ..

moves to:

/home/alex/linux-lab

The symbol:

..

means:

parent directory

cd .

The symbol:

.

means:

current directory

Therefore:

cd .

does not really move anywhere.

The . symbol is still important because many Linux commands use it to represent the current directory.

Example:

find .

means:

search starting from the current directory.

cd ~

Moves to the user's home directory.

cd ~

Example result:

/home/alex

cd -

Moves back to the previous directory.

Example:

cd /var/log
cd /etc
cd -

The final command returns to:

/var/log

This is a very useful shell shortcut.

6. Absolute and Relative Paths

Understanding paths is one of the most important Linux skills.

Absolute path

Starts from the filesystem root /.

Example:

/home/alex/linux-lab/documents/notes.txt

Command example:

cd /home/alex/linux-lab/documents

Relative path

Starts from the current directory.

If the current directory is:

/home/alex/linux-lab

then:

cd documents

uses a relative path.

Similarly:

cat documents/notes.txt

refers to a file relative to the current directory.

7. Creating Directories

mkdir

mkdir means:

make directory

Example:

mkdir documents

Create several directories at once:

mkdir documents downloads projects

This creates three separate directories.

Important beginner mistake

This command:

mkdir a.txt b.txt

creates directories named:

a.txt
b.txt

It does not create text files.

Linux file extensions are mostly naming conventions. A name ending in .txt does not automatically make something a text file.

Use touch to create regular empty files.

8. Creating Files

touch

Creates an empty file if it does not already exist.

touch notes.txt

Create multiple files:

touch one.txt two.txt three.txt

Create a file inside another directory:

touch documents/linux.txt

9. Viewing Directory Structures

find

A simple and useful way to display everything under a directory:

find .

Example:

.
./documents
./documents/linux.txt
./documents/notes.txt
./downloads
./projects
./projects/main.txt

To inspect a specific directory:

find final-test

Important: paths are interpreted relative to the current working directory unless an absolute path is supplied.

If already inside final-test, running:

find final-test

looks for:

final-test/final-test

Instead, use:

find .

10. Copying Files

cp

cp means:

copy

Example:

cp documents/notes.txt downloads/

The original file remains in documents, while a copy appears in downloads.

Copy and rename in one command

cp documents/notes.txt backup/notes-copy.txt

This copies the file and gives the copied version a different name.

11. Moving and Renaming Files

mv

mv means:

move

Move a file:

mv downloads/test.txt projects/

Rename a file

Linux uses the same mv command for renaming.

mv projects/app.txt projects/main.txt

Conceptually:

old path -> new path

12. Deleting Files and Directories

Deletion commands should be used carefully.

rm

Deletes regular files.

rm notes.txt

rmdir

Deletes an empty directory.

rmdir empty-folder

It fails if the directory contains files or subdirectories.

rm -r

Deletes a directory recursively, including its contents.

rm -r temp

The -r option means:

recursive

This can delete an entire directory tree, so always verify the target first.

Recommended habit:

pwd
ls

Then use the delete command.

13. Hidden Files

Any filename beginning with a dot is normally hidden.

Create one:

touch .config

A normal listing may not show it:

ls

But this will:

ls -a

Example:

.  ..  .config  documents  projects

Here:

.   -> current directory
..  -> parent directory

14. Reading File Contents

cat

Displays the whole file.

cat notes.txt

Example output:

Linux is powerful
Day 1 practice

Best for small files.

head

Displays the beginning of a file.

head notes.txt

Usually shows the first 10 lines.

Show only the first 5 lines:

head -5 notes.txt

Show only the first line:

head -1 notes.txt

tail

Displays the end of a file.

tail notes.txt

Show the last 5 lines:

tail -5 notes.txt

Show the last line:

tail -1 notes.txt

15. Reading Larger Files with less

For larger files, less is usually better than cat.

less notes.txt

Useful keys inside less:

Up / Down Arrow   move through the file
Page Up / Down    move by larger sections
/text             search for text
n                 next search result
q                 quit

Example search:

/line 10

Then press:

n

to find the next match.

16. Writing Text into Files

echo

Prints text.

echo "Hello Linux"

Output:

Hello Linux

17. Output Redirection

Redirection lets command output be sent into files.

>

Writes output to a file and replaces existing content.

echo "Linux is powerful" > notes.txt

If notes.txt already contains text, its previous contents are replaced.

>>

Appends output to the end of a file.

echo "Day 1 practice" >> notes.txt

Now the file contains both lines.

Simple rule:

>   overwrite
>>  append

This distinction is important.

18. A First Bash Loop

Although loops are more advanced than basic Day 1 Linux usage, a simple loop is useful for generating practice data.

Example:

for i in {1..15}; do echo "line $i" >> notes.txt; done

This appends:

line 1
line 2
line 3
...
line 15

Important syntax:

for i in {1..15}; do

When written on one line, semicolons separate the parts of the command.

Correct:

for i in {1..15}; do echo "line $i"; done

Incorrect:

for i in (1..15)

Bash uses brace expansion:

{1..15}

not parentheses for this example.

19. Multiple Commands on One Line

Normally commands can be written on separate lines:

cd documents
touch notes.txt

They can also be separated with a semicolon:

cd documents; touch notes.txt

This is different from writing:

cd documents touch notes.txt

The last form passes extra words as arguments to cd, so Bash may produce an error such as:

cd: too many arguments

20. Understanding Command Errors

Errors are useful feedback.

command not found

Example:

pw

Output:

pw: command not found

This means Bash could not find a command named pw.

The intended command may have been:

pwd

No such file or directory

Example:

cat docs/notes.txt

may fail if the current directory does not contain docs.

Always ask:

Where am I?

Check with:

pwd

Then inspect:

ls

Is a directory

Example:

rm a.txt

may return:

rm: cannot remove 'a.txt': Is a directory

This means the object named a.txt is actually a directory.

Check:

ls -l

The first character indicates the type:

d   directory
-   regular file

21. Terminal History

history

Displays previously executed commands.

history

Show only recent commands:

history | tail -10

The pipe | will be studied more deeply later, but in this example it sends the output of history into tail.

22. Useful Terminal Keyboard Shortcuts

Up Arrow / Down Arrow

Move through previously used commands.

Useful for quickly rerunning or editing previous commands.

Ctrl + R

Search command history interactively.

Press:

Ctrl + R

Then type part of a previous command.

Example:

find

Bash may locate an earlier command such as:

find .

Tab Completion

Start typing a file or directory name and press:

Tab

Example:

cd doc

Press Tab and Bash may complete it to:

cd documents/

This saves time and reduces typing mistakes.

Ctrl + A

Move the cursor to the beginning of the current command line.

Ctrl + E

Move the cursor to the end of the current command line.

Ctrl + L

Clear the terminal screen.

Equivalent in effect to running:

clear

Ctrl + C

Interrupt the currently running command.

This is one of the most important shell shortcuts.

23. Useful Day 1 Command Summary

Command

Purpose

whoami

Show current username

pwd

Show current working directory

ls

List files and directories

ls -l

Detailed listing

ls -a

Show hidden files

ls -lah

Detailed + hidden + readable sizes

cd DIR

Enter a directory

cd ..

Move to parent directory

cd ~

Go to home directory

cd -

Go to previous directory

mkdir DIR

Create directory

touch FILE

Create empty file

cp SRC DEST

Copy

mv SRC DEST

Move or rename

rm FILE

Delete file

rmdir DIR

Delete empty directory

rm -r DIR

Delete directory recursively

find .

Display/search directory tree

cat FILE

Display entire file

head FILE

Show beginning of file

tail FILE

Show end of file

less FILE

Interactive file viewer

echo TEXT

Print text

history

Show previous commands

24. Important Symbols Learned

Symbol

Meaning

/

Filesystem root / path separator

~

Current user's home directory

.

Current directory

..

Parent directory

>

Redirect and overwrite

>>

Redirect and append

`

`

Send one command's output to another command

The pipe symbol | is only introduced here briefly and is normally studied in more detail in the next stage.

25. Practice Lab

Create a safe practice directory:

mkdir ~/linux-lab
cd ~/linux-lab

Create:

mkdir documents downloads projects

Create files:

touch documents/notes.txt
touch documents/linux.txt
touch downloads/test.txt
touch projects/app.txt

Verify:

find .

Copy:

cp documents/notes.txt downloads/

Move:

mv downloads/test.txt projects/

Rename:

mv projects/app.txt projects/main.txt

Create a hidden file:

touch .config

Inspect:

ls -lah

Add text:

echo "Linux practice" > documents/notes.txt
echo "Day 1" >> documents/notes.txt

Read:

cat documents/notes.txt

26. Final Practice Challenge

Without following exact commands line by line, create this structure:

final-test/
├── .config
├── backup/
│   └── notes-copy.txt
├── docs/
│   ├── linux.txt
│   └── notes.txt
└── projects/
    └── main.txt

Requirements:

Create all directories.

Create docs/linux.txt.

Create docs/notes.txt.

Put some text inside docs/notes.txt.

Copy that file into backup/ as notes-copy.txt.

Create projects/app.txt.

Rename projects/app.txt to projects/main.txt.

Create .config inside final-test.

Verify using:

find final-test

Inspect hidden files and file details:

ls -lah final-test

27. Common Beginner Mistakes

Mistake 1: Confusing files and directories

mkdir notes.txt

creates a directory, not a regular text file.

Use:

touch notes.txt

for an empty file.

Mistake 2: Forgetting the current directory

A relative path only works relative to the current location.

Before troubleshooting:

pwd
ls

Mistake 3: Forgetting that . and .. have meanings

.   current directory
..  parent directory

Mistake 4: Using > when >> was intended

echo "new text" > file.txt

replaces previous content.

echo "new text" >> file.txt

adds to the end.

Mistake 5: Running rm -r carelessly

Always verify:

pwd
ls

before recursively deleting important-looking paths.

Mistake 6: Assuming file extensions define file type

Linux does not treat .txt, .png, or .java as magical file types by filename alone.

Names are names.

A directory can even be named:

example.txt

28. Expert Habits to Start Building Early

1. Check location before destructive commands

pwd

2. Inspect before deleting

ls

3. Use Tab completion

It is faster and reduces typos.

4. Use command history

Up Arrow
Ctrl + R

5. Prefer understanding paths over memorizing commands

Many beginner problems are actually path problems.

6. Read error messages

Linux usually tells you what went wrong.

7. Practice in a safe lab directory

Avoid experimenting with destructive commands in important system directories.

29. Day 1 Revision Checklist

A learner should be able to answer these questions without notes:

What does pwd do?

What is the difference between . and ..?

What does ~ represent?

What does cd - do?

What is the difference between mkdir and touch?

How is a file copied?

How is a file renamed?

What is the difference between rm and rmdir?

What does rm -r do?

How are hidden files named in Linux?

What is the difference between ls, ls -l, and ls -a?

What is the difference between cat, head, tail, and less?

What is the difference between > and >>?

Why might a relative path fail?

How can command history be searched?

What does Tab completion do?

30. Minimum Commands to Remember After Day 1

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
find
cat
head
tail
less
echo
history

Do not try to memorize every possible option.

The more important skill is understanding:

where you are
what path you are using
what object you are modifying
what the command will do

31. Core Mental Model

When working in Linux, think in this order:

Who am I?
↓
Where am I?
↓
What exists here?
↓
What path do I need?
↓
What action should I perform?
↓
How can I verify the result?

A useful command pattern is:

whoami
pwd
ls

Then perform the task.

Finally verify with tools such as:

ls
ls -lah
find .
cat filename

This habit prevents many beginner mistakes.
