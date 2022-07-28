# My Programming Cheatsheets

Putting things in this file helps me to synthetize and see if I really understood concepts I've learned during my learning journey.
It can also useful as a reminder and mini tutos.
I know the title of this file not really suits its purpose ;)
Initially, it was really about doing a cheatsheet, but when I realize how benefic it was for my comprehension, I drift a bit :)

---

## Summary

- [Flowchart and Pseudocode](#flowchart-and-pseudocode)
- [Shell](#shell)
- [Git](#git)
- [RegEx](#regex)
- [Docker](#docker)
- [Python](#python)
- [HTML](#html)
- [CSS](#css)
- [Javascript](#javascript)
- [SQL](#sql)
- [MongoDB](#mongodb)

---

## Flowchart and Pseudocode

[Back to summary](#summary)  
Before writing any line of code, it is good to know exactly what your algorithm should do.  
Flowchart and pseudocode are your friend for that.  
![flowchart](https://user-images.githubusercontent.com/78802772/175765499-8e722355-de85-4479-a099-76a4bc01aea6.jpg)
![pseudocode](https://user-images.githubusercontent.com/78802772/175765501-85a8d973-cb9d-455c-be76-ac514f818e1f.jpg)
![Designelements-Flowchart](https://user-images.githubusercontent.com/78802772/175765681-eb94a7a6-89db-4b8d-941d-27fef82e5a3b.png)

---

## Shell

[Back to summary](#summary)

- [Shortcuts](#shortcuts)
- [Variables](#variables)
- [IO Redirection](#io-redirection)
- [pipes](#pipes)
- [Command Lists](#command-lists)
- [Directory Operations](#directory-operations)
- [ls Options](#ls-options)
- [Search Files](#search-files)
- [File Operations](#file-operations)
- [Watch a Command](#watch-a-command)
- [Process Management](#process-management)
- [Nano Shortcuts](#nano-shortcuts)
- [File Permissions](#file-permissions)
- [File Permission Numbers](#file-permission-numbers)

---

### Shortcuts

[Back to summary](#shell)

```text

CTRL-c      Stop current command
CTRL-z      Sleep program
CTRL-a      Go to start of line
CTRL-e      Go to end of line
CTRL-u      Cut from start of line
CTRL-k      Cut to end of line
CTRL-r      Search history
!!          Repeat last command
!abc        Run last command starting with abc
!abc:p      Print last command starting with abc
!$          Last argument of previous command
ALT-.       Last argument of previous command
!*          All arguments of previous command
^abc^123    Run previous command, replacing abc with 123
$_          Value of inline previous command


```

---

### Variables

[Back to summary](#shell)

```text
env                 Show environment variables
echo $NAME          Output value of $NAME variable
export NAME=value   Set $NAME to value
$PATH               Executable search path
$HOME               Home directory
$SHELL              Current shell
```

---

### IO Redirection

[Back to summary](#shell)

```text
cmd < file        Input of cmd from file
cmd1 <(cmd2)      Output of cmd2 as file input to cmd1
cmd > file        Standard output (stdout) of cmd to file
cmd > /dev/null   Discard stdout of cmd
cmd >> file       Append stdout to file
cmd 2> file       Error output (stderr) of cmd to file
cmd 1>&2          stdout to same place as stderr
cmd 2>&1          stderr to same place as stdout
cmd &> file       Every output of cmd to file
```

---

### Pipes

[Back to summary](#shell)

```text
cmd1 | cmd2       stdout of cmd1 to cmd2
cmd1 |& cmd2      stderr of cmd1 to cmd2
```

---

### Command Lists

[Back to summary](#shell)

```text
cmd1 ; cmd2     Run cmd1 then cmd2
cmd1 && cmd2    Run cmd2 if cmd1 is successful
cmd1 || cmd2    Run cmd2 if cmd1 is not successful
cmd &           Run cmd in a subshell
```

---

### Directory Operations

[Back to summary](#shell)

```text
pwd         Show current directory
mkdir dir   Make directory dir
cd dir      Change directory to dir
cd ..       Go up a directory
ls          List files
```

---

### ls Options

[Back to summary](#shell)

```text
-a    Show all (including hidden)
-R    Recursive list
-r    Reverse order
-t    Sort by last modified
-S    Sort by file size
-l    Long listing format
-1    One file per line
-m    Comma- separated output
-Q    Quoted output
```

---

### Search Files

[Back to summary](#shell)

```text
grep pattern files      Search for pattern in files
grep -i                 Case insensitive search
grep -r                 Recursive search
grep -v                 Inverted search
grep -o                 Show matched part of file only
find /dir/ -name name*  Find files starting with name in dir
find /dir/ -user name   Find files owned by name in dir
find /dir/ -mmin num    Find files modifed less than num minutes ago in dir
whereis command         Find binary/source/manual for command
locate file             Find file (quick search of system index)
```

---

### File Operations

[Back to summary](#shell)

```text
touch file1       Create file1
cat file1 file2   Concatenate files and output
less file1        View and paginate file1
file file1        Get type of file1
cp file1 file2    Copy file1 to file2
mv file1 file2    Move file1 to file2
rm file1          Delete file1
head file1        Show first 10 lines of file1
tail file1        Show last 10 lines of file1
tail -F file1     Output last lines of file1 as it changes
```

---

### Watch a Command

[Back to summary](#shell)

```text
watch -n 5 'ntpq -p'    Issue the 'ntpq -p' command every 5 seconds and display output
```

---

### Process Management

[Back to summary](#shell)

```text
ps            Show snapshot of processes
top           Show real time processes
kill pid      Kill process with id pid
pkill name    Kill process with name name
killall name  Kill all processes with names beginning name
```

---

### Nano Shortcuts

[Back to summary](#shell)

Files

```text
Ctrl-R    Read file
Ctrl-O    Save file
Ctrl-X    Close file
```

Cut and Paste

```text
ALT-A     Start marking text
CTRL-K    Cut marked text or line
CTRL-U    Paste text
```

Navigate File

```text
ALT-/     End of file
CTRL-A    Beginning of line
CTRL-E    End of line
CTRL-C    Show line number
CTRL-_    Go to line number
```

Search File

```text
CTRL-W    Find
ALT-W     Find next
CTRL-\    Search and replace
```

---

### File Permissions

[Back to summary](#shell)
Change mode of file to 775

```shell
chmod 775 file
```

Recurs ively chmod folder to 600

```shell
chmod -R 600 folder
```

Change file owner to user and group to group

```shell
chown user:group file
```

---

### File Permission Numbers

[Back to summary](#shell)  
First digit is owner permis sion, second is group and third is everyone.

```text
4   read (r)
2   write (w)
1   execute (x)
```

---
