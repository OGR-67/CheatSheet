# My Programming Cheatsheets

Putting things in this file helps me to synthesize and see if I really
understood concepts I've learned during my learning journey.  
It can also be useful as a reminder and mini tutos.
I know the title of this file not really suits its purpose ;)
Initially, it was really about doing a cheatsheet, but when I realize how
benefit it was for my comprehension, I drift a bit :)

---

## Summary

- [Google search](#google-search)
- [Flowchart and Pseudocode](#flowchart-and-pseudocode)
- [Design Patterns](#design-patterns)
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

## Google Search

[Back to summary](#summary)

A short list of filters that can be specified directly inside the search bar.  

- `:site.com` to search in a particular website
- `-term` to excludea term
- `filetype:pdf` to search for a specific filetype file
- `before:YYYY-MM-DD` ou `after:YYYY-MM-DD` for a dated search
- `"term"` to search for a specific term

more to come soon...

---

## Flowchart and Pseudocode

[Back to summary](#summary)  
Before writing any line of code, it is good to know exactly what your algorithm
should do.  
Flowchart and pseudocode are your friend for that.  
![flowchart](https://user-images.githubusercontent.com/78802772/175765499-8e722355-de85-4479-a099-76a4bc01aea6.jpg)
![pseudocode](https://user-images.githubusercontent.com/78802772/175765501-85a8d973-cb9d-455c-be76-ac514f818e1f.jpg)
![Design elements-Flowchart](https://user-images.githubusercontent.com/78802772/175765681-eb94a7a6-89db-4b8d-941d-27fef82e5a3b.png)

---

## Design Patterns

[Back to summary](#summary)  

- [Creational Design Patterns](#creational-design-patterns)
- [Structural Design Patterns](#structural-design-patterns)
- [Behavioral Design Patterns](#behavioral-design-patterns)

I'll use javascript ecmascript 6 to illustrate.

---

### Creational Design Patterns

[Back to summary](#design-patterns)  

This type of design patterns represents all patterns dedicated to object creation.
Here are some of most used:

- Constructor pattern  
- Factory pattern  
- Singleton pattern  

#### Constructor pattern

![constructor_pattern_diagram](./images/constructor_pattern.png)

As you can see, the constructor pattern is composed by two elements:

- The parent  
- The object (or instance)  

```javascript
// Parent
class Movie {
  constructor(data) {
    this._title = data.title;
    this._actor = data.actor;
    this._duration = data.duration;
    this._picture = data.picture;
    this._thumbnail = data.thumbnail;
    this._released_in = data.released_in;
    this._synopsis = data.synopsis;
  }

  get title() {
    return this._title;
}

  get actor() {
    return this._actor;
  }

  // etc...
}


// Object
const MovieExample = new Movie(dataExample);

```

---

#### Factory Pattern

![factory pattern schema](images/factory_pattern.png)

This pattern delegates the objects construction a factory class. This class will
take an argument of type and will create the needed object.  

Imagine we have two constructors, one creating object from old data and one from
new data. Here is how you would implement that:  

```javascript
class MovieFactory {
  constructor(data, type) {
    if (type === "oldApi"){
      return new OldMovie(data)
    
    } else if (type === "newApi"){
      return new NewMovie(data)
    
    } else {
      throw new Error("Type must be 'oldApi' or 'newApi'");

    }
  }
}

// creating an object from old data
const oldMovies = oldMoviesData.map(movie => new OldMovie(movie, "oldApi"));

```

---

#### Singleton Pattern

![singleton_pattern](images/singleton_pattern.png)

The only purpose of this pattern is to ensures that the object can be instantiated
only once.  
It's a great choice for resources management.  

```javascript
class DB {
   constructor(url, login, password) {
       if (DB.exists) {
           return DB.instance
       }

       this._url = url
       this._login = login
       this._password = password

       DB.exists = true
       DB.instance = this
   }
}
```

At first instantiating, the class variable `exists` is set to true and the class
variable `instance` is set to the instance itself.  
If we try to instantiate the class again, the constructor will return the class
variable `instance` value and will not instantiate a new object.  

---

### Structural Design Patterns

[Back to summary](#design-patterns)  

This family of patterns allows to manage and put together objects in bigger
structures.

#### Adapter pattern

![adapter pattern schema](images/adaptater_pattern.png)

This pattern is composed by 3 actors:

- the `Client`: the element which is requesting.  
- the `Adapter`: the object which will be used by the client.  
- the `Adaptee`: the object that will be used by the adapter.  

A example of use case is for an API update which redefined how you should use it.
You can create a adapter so you have almost no code to adapt.  

Here is a practical example

```javascript

// How V1 works
const apiV1 = new ApiV1(arg1, arg2)       // We need to instantiate
const results1 = await apiV1.getResults() // Then call the method

// How V2 works
const results2 = await ApiV2.getResults(arg2, arg1) // no instanciation (static)
                                                    // and arguments order different

// Adapter
class ApiAdapter {
  constructor (arg1, arg2) {  // Because we want to use the new version like
                              // we used the old one, we need a constructor

      this.arg1 = arg1;       // because we want to instantiate the adapter
      this.arg2 = arg2;
  }

  async getResults() {
    return await ApiV2.getResults(this.arg2, this.arg1) // Here is the trick,
                                                        // we return the result of
                                                        // the call of new Api's
                                                        // method
  }
}

const adapterApi = new ApiAdapter(arg1, arg2);        // The usage is the same as
                                                      // the old one but in reality
                                                      // we use the new API
const adapterResults = await adapterApi.getResults();

```

#### Decorator pattern

This pattern allows to add fonctionality to an object without overcharging it or
complexify it. It is not a good practice to decorate a decorator.  

![decorator pattern](images/decorator_pattern.png)

Composed by 3 elements:

- Client: The object or function that calls the decorator
- Component: The object without the new fonctionality
- Decorator: This object recovers the components, overcharges it with new
fonctionality, and returns it.

```javascript
// A very simple car class, also known as the component
class Car {
  constructor() {
    this.wheelCount = 4;
    this.steeringWheelPosition = "left";
  }
}

// The decorator
function carWithColor(car, color) {
  car.color = color;
  return car
}

// How it works
const blueCar = carWithColor(new Car(), "blue");

```

#### Proxy Pattern

The purpose of a proxy is to be the intermediary between two hosts to facilitate
and monitor their exchanches.  
A proxy can be needed when an object becomes too complex or when we want to cache
some informations.  
Caching information has the advantage to save ressources and in case of an external
API, limitting the number of requests.  

![proxy_pattern](images/proxy_pattern.png)

The idea is simple:

- At first request, the process is like if there is no proxy, but we save the result
in the cache.  
- At the second request, we check if something is cached and we return it without
actually do the request.  

```javascript
// Cache usecase

class FetchMoviesProxy {
   constructor() {
       this.cache = []
   }

   async fetchMovies() {
       if (this.cache.length) { // Check if something is cached
           return this.cache
       }

       const MoviesApi = new FetchMovies()  // If not do the normal fetch
       const moviesData = await MoviesApi.get()

       this.cache.push(moviesData) // And append the results to the cache
       return moviesData
   }
}
```

### Behavioral Design Patterns

[Back to summary](#design-patterns)  

comming...

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

CTRL + L    clear terminal
CTRL-C      Stop current command
CTRL-Z      Sleep program
CTRL-A      Go to start of line
CTRL-E      Go to end of line
CTRL-U      Cut from start of line
CTRL-K      Cut to end of line
CTRL-R      Search history
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
apropos keyword       find a specific command relative to given keyword
reset                 reset terminal session
cmd1 ; cmd2           Run cmd1 then cmd2
cmd1 && cmd2          Run cmd2 if cmd1 is successful
cmd1 || cmd2          Run cmd2 if cmd1 is not successful
cmd &                 Run cmd in a subshell

command | column -t   format output of command to a table

history               get the commands passed history
!n                    execute command number n of the history

```

---

### Directory Operations

[Back to summary](#shell)

```text
pwd         Show current directory
mkdir dir   Make directory dir
cd dir      Change directory to dir
cd ..       Go up a directory
cd -        get back to previous directory
pushd dir   add dir to directory stack
popd        go to first diectory of stack and pop it from stack
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
touch file1           Create file1
cat file1 file2       Concatenate files and output
less file1            View and paginate file1
file file1            Get type of file1
cp file1 file2        Copy file1 to file2
mv file1 file2        Move file1 to file2
rm file1              Delete file1
head file1            Show first 10 lines of file1
tail file1            Show last 10 lines of file1
tail -F file1         Output last lines of file1 as it changes

truncate -s 0 file    Delete file content, 0 is the index form where to truncate

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
CTRL - Z      set process to the background and sleep it
fg            get back to slept foreground
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

## Git

[Back to summary](#summary)

- [GIT BASICS](#git-basics)
- [SETUP](#setup)
- [NAVIGATION](#navigation)
- [SETUP & INIT](#setup-and-init)
- [STAGE & SNAPSHOT](#stage-and-snapshot)
- [BRANCH & MERGE](#branch-and-merge)
- [INSPECT & COMPARE](#inspect-and-compare)
- [TRACKING PATH CHANGES](#tracking-path-changes)
- [IGNORING PATTERNS](#ignoring-patterns)
- [SHARE & UPDATE](#share-and-update)
- [REWRITE HISTORY](#rewrite-history)
- [TEMPORARY COMMITS](#temporary-commits)
- [CREATE ALIAS](#create-alias)
- [CONCRETE CASES](#concrete-cases)

---

### GIT BASICS

[Back to summary](#git)  
[A very simple git here](https://rogerdudler.github.io/git-guide/)
![image](https://user-images.githubusercontent.com/78802772/175573903-81fb168e-e60b-49e3-bbd3-73cb7cd58f29.png)

---

### SETUP

[Back to summary](#git)

Set a name that is identifiable for credit when review version history

```shell
git config --global user.name “[firstname lastname]”
```

Set an email address that will be associated with each history marker

```shell
git config --global user.email “[valid-email]”
```

Set automatic command line coloring for Git for easy reviewing

```shell
git config --global color.ui auto
git config --global color.ui true
```

---

### NAVIGATION

[Back to summary](#git)  
Shortcuts list to navigate through diff view

```text
Next line             : return
Next page             : space bar
Previous page         : w
Quit viewing the diff : q
Help                  : h
```

---

### SETUP AND INIT

[Back to summary](#git)  
Initialize an existing directory as a Git repository

```shell
git init
```

Clone a local repository

```shell
git clone <path/to/repository>
```

clone a remote directory

```shell
git clone [url]
git clone username@host:/path/to/repository
```

---

### STAGE AND SNAPSHOT

[Back to summary](#git)  
Show modified files in working directory, staged for your next commit

```shell
git status
```

Add a file as it looks now to your next commit (stage)

```shell
git add [file]
git add *
```

Unstage a file while retaining the changes in working directory

```shell
git reset [file]
```

Diff of what is changed but not staged

```shell
git diff
```

Diff of what is staged but not yet committed

```shell
git diff --staged
```

Commit your staged content as a new commit snapshot

```shell
git commit -m “[descriptive message]”
```

---

### BRANCH AND MERGE

[Back to summary](#git)  
List your branches.  
A `*` will appear next to the currently active branch

```shell
git branch
```

Rename Master branch to main (I can see you github)

```shell
git branch -M main
```

Create a new branch at the current commit

```shell
git branch [branch-name]
```

Switch to another branch and check it out into your working directory

```shell
git checkout
```

Merge the specified branch’s history into the current one

```shell
git merge [branch]
```

Show all commits in the current branch’s history

```shell
git log
```

Visualize log tree

```shell
git log --oneline --decorate --graph --all
```

---

### INSPECT AND COMPARE

[Back to summary](#git)  
Show the commit history for the currently active branch

```shell
git log
```

Show the commits on branchA that are not on branchB

```shell
git log branchB..branchA
```

Show the commits that changed file, even across renames

```shell
git log --follow [file]
```

Show the diff of what is in branchA that is not in branchB

```shell
git diff branchB...branchA
```

Show any object in Git in human-readable format

```shell
git show [SHA]
```

---

### TRACKING PATH CHANGES

[Back to summary](#git)  
Delete the file from project and stage the removal for commit

```shell
git rm [file]
```

Change an existing file path and stage the move

```shell
git mv [existing-path] [new-path]
```

Show all commit logs with indication of any paths that moved

```shell
git log --stat -M
```

---

### IGNORING PATTERNS

[Back to summary](#git)

Save a file with desired patterns as .gitignore with either direct string matches
or wildcard globs.

```text
logs/
*.notes
pattern*/
```

System wide ignore pattern for all local repositories

```shell
git config --global core.excludesfile [file]
```

---

### SHARE AND UPDATE

[Back to summary](#git)  
Add a git URL as an alias

```shell
git remote add [alias] [url]
```

Fetch down all the branches from that Git remote

```shell
git fetch [alias]
```

Merge a remote branch into your current branch to bring it up to date

```shell
git merge [alias]/[branch]
```

Transmit local branch commits to the remote repository branch

```shell
git push [alias] [branch]
```

Fetch and merge any commits from the tracking remote branch

```shell
git pull
```

---

### REWRITE HISTORY

[Back to summary](#git)  
Apply any commits of current branch ahead of specified one

```shell
git rebase [branch]
```

Clear staging area, rewrite working tree from specified commit

```shell
git reset --hard [commit]
```

---

### TEMPORARY COMMITS

[Back to summary](#git)  
Save modified and staged changes

```shell
git stash
```

List stack-order of stashed file changes

```shell
git stash list
```

Write working from top of stash stack

```shell
git stash pop
```

Discard the changes from top of stash stack

```shell
git stash drop
```

---

### CREATE ALIAS

[Back to summary](#git)

To create an alias for a command, use the following syntax:

```text
git config --global alias.[aliasName] ["Command to alias"]
```

---

### CONCRETE CASES

[Back to summary](#git)

![git_workflow](https://images.edrawmax.com/what-is/gitflow-diagram/2-git-flow-model.png)

#### Fast-Forward merge

```text
    HEAD
     |
chase-branch        escaped
     |                 |
     A <----- B <----- C

>>> git merge escaped

                    escaped
                       |
     A <----- B <----- C
                       |
                  chase-branch
                       |
                      HEAD

```

#### Change history

```text
        Branch A
          |
        HEAD
          |
A <------ B
   \
    \
      --- C
          |
        Branch B
                
>>> git rebase branch B

            Branch A
              |
            HEAD
              |
A <--- C <--- B
       |
    Branch B
```

#### Remove ignored file

- When file is ignored but is tracked for whatever reason, you can always execute
`git rm <file>` to remove the file from both repository and working area.  
- If you want to leave it in your working directory (which is often when dealing
with mistakenly tracked files), you can tell Git to remove it only from repository
but not from working area with `git rm --cached <file>`

#### Change a letter case in the filename of an already tracked file

```text
>>> git mv File.txt file.txt
>>> git commit -am "Lowercase file.txt"
```

#### Recommit based on the last commit

- When you want to change the last commit (the one that is pointed by HEAD),
use `git commit --amend`  
- If you want to change only commited files but no edit message, use
`git commit --amend --no-edit`  
- Moreover, you can skip git add command and update last commit with all current
changes in working area: `git commit --amend --no-edit -a`  
- You can even edit the date of commit using
`git commit --amend --no-edit --date="1987-08-03"`  

#### Classic branch merge

```text
        HEAD
         |
        work
         |
A <----- B
 \
  \----- C
         |
another-piece-of-work

>>> git merge another-piece-of-work

                 HEAD
                  |
                 work
                  |
A <----- B <----- D
 \               /
  \----- C <----/
         |
another-piece-of-work
```

#### Edit an old commit

Rebase and change pick by edit in front of the commit you want to edit.

```text
commit to edit
      |
      A <----- B <----- C
                        |
                  current commit
                        |
                      HEAD

>>> git rebase -i HEAD~~
```

#### Find the commits you have been

`git reflog` records where you have been previously. You can find any commit you
have been on with this tool and find commits that you have lost accidentally
(for example by rebase, amend).  
There are even more powerful selectors. Do you want to know what were you working
on yesterday?  
`git show -q HEAD@{1.day.ago}`

#### Split a commit

- On multiple files `git reset HEAD~` then add files one by one
- On a single file, do the same if index is not clean then  

```text
>>> git add -p <file>

# Here is a description of each option:
# 
#     y stage this hunk for the next commit
#     n do not stage this hunk for the next commit
#     q quit; do not stage this hunk or any of the remaining hunks
#     a stage this hunk and all later hunks in the file
#     d do not stage this hunk or any of the later hunks in the file
#     g select a hunk to go to
#     / search for a hunk matching the given regex
#     j leave this hunk undecided, see next undecided hunk
#     J leave this hunk undecided, see next hunk
#     k leave this hunk undecided, see previous undecided hunk
#     K leave this hunk undecided, see previous hunk
#     s split the current hunk into smaller hunks
#     e manually edit the current hunk
#     ? print hunk help
```

#### Too many commits

The easiest way to make one commit out of two (or more) is to squash them with
`git rebase -i` command and choose squash option for all but the first commit you
want to preserve.  
Remember that you don't need to know the commit SHA-1 hashes when specifying
them in `git rebase -i` command. When you know that you want to go 2 commits
back, you can always run `git rebase -i HEAD^^` or `git rebase -i HEAD~2`.  

#### Pick branches

```text
      HEAD             ---- B - feature-b
       |              /
current-work - Z <--- A - feature-a
                      \
                       ---- C1 <--- C2 - feature-c

>>> git cherry-pick feature-a
>>> git cherry-pick feature-b
>>> git cherry-pick feature-c
# resolve merge conflict
>>> git add -A
>>> git cherry-pick --continue

                    HEAD
                     |
              pick-your-features
                     |
Z <--- A <--- B <--- C
```

#### Complex rebasing

```text
                your-master
                     |
A <--- B <--- C <--- D
        \
         E <--- F <--- G - issue-555
          \
           H <--- I
                  |
            rebase-complex
                  |
                 HEAD


>>> git rebase issue-555 --onto your-master


                                  HEAD
                  your-master      |
                     |        rebase-complex 
                     |             |
A <--- B <--- C <--- D <--- H <--- I
        \
         E <--- F <--- G - issue-555
```

Means: Take the rebase-complex branch, figure out the patches since it diverged
from the issue-555 branch, and replay these patches in the rebase-complex branch
as if it was based directly off the your-master branch instead.  
`git rebase --onto` allows you to move a branch to a different place.  
`git rebase issue-555 --onto your-master` means get all commits that are not in
issue-555 and place them onto your-master branch.

```text
                                  HEAD
                  your-master      |
                     |        rebase-complex 
                     |             |
A <--- B <--- C <--- D <--- H <--- I
        \
         E <--- F <--- G - issue-555

>>> git rebase issue-555 --onto your-master

                                  HEAD
                  your-master      |
                     |        rebase-complex 
                     |             |
A <--- B <--- C <--- D <--- H <--- I
                      \
                      E <--- F <--- G - issue-555

---
```

#### Invalid commits order

With `git rebase -i <ref>` you can then change the order of commits

#### Check wich file was modified in the current commit

`git log -p -1`

#### Find commits where a specific word was introduced

`git log -S <word>`

#### Find bug

Let's say that the word "bug" introduced a bug, but you have introduced that word
on different commits.  
You don't want to search by hand for that bug.  

- `git bisect start` to start bisect
- `git bisect bad HEAD` tells that last commit to be buggy is the current one.
- `git bisect good 1.0` tells that the 1.0 version and all before isn't buggy.  
- `git bisect run sh -c "grep -v bug <file-to-test>` tells that git must execute
to all commits between the good and bad this command. Because we invert the search,
we will just keep non buggy version meaning all version without the "bug" word.

## RegEx

[Back to summary](#summary)

- [Anchors](#anchors)
- [Character Classes](#character-classes)
- [POSIX](#posix)
- [Assertions](#assertions)
- [Quantifiers](#quantifiers)
- [Escape Sequences](#escape-sequences)
- [Common Metacharacters](#common-metacharacters)
- [Special Characters](#special-characters)
- [Groups and Ranges](#groups-and-ranges)
- [Pattern Modifiers](#pattern-modifiers)
- [String Replacement](#string-replacement)

---

### Anchors

[Back to summary](#regex)

```text
^           Start of string, or start of line in multiline pattern
\A          Start of string
$           End of string, or end of line in multi-line pattern
\Z          End of string
\b          Word boundary
\B          Not word boundary
\<          Start of word
\>          End of word
```

---

### Character Classes

[Back to summary](#regex)

```text
\c          Control character
\s          White space
\S          Not white space
\d          Digit
\D          Not digit
\w          Word
\W          Not word
\x          Hexadecimal digit
\O          Octal digit
```

---

### POSIX

[Back to summary](#regex)

```text
[:upper:]   Uppercase letters
[:lower:]   Lowercase letters
[:alpha:]   All letters
[:alnum:]   Digits and letters
[:digit:]   Digits
[:xdigit:]  Hexadecimal digits
[:punct:]   Punctu ation
[:blank:]   Space and tab
[:space:]   Blank characters
[:cntrl:]   Control characters
[:graph:]   Printed characters
[:print:]   Printed characters and spaces
[:word:]    Digits, letters and underscore
```

---

### Assertions

[Back to summary](#regex)

```text
?=          Lookahead assertion
?!          Negative lookahead
?<=         Lookbehind assertion
?!= or ?<!  Negative lookbehind
?>          Once-only Subexp ression
?()         Condition [if then]
?()|        Condition [if then else]
?#          Comment
```

---

### Quantifiers

[Back to summary](#regex)

```text
*           0 or more
+           1 or more
?           0 or 1
{3}         Exactly 3
{3,}        3 or more
{3,5}       3, 4 or 5
```

---

### Escape Sequences

[Back to summary](#regex)

```text
\           Escape following character
\Q          Begin literal sequence
\E          End literal sequence
```

---

### Common Metacharacters

[Back to summary](#regex)

```text
^   [   .   $
{   *   (   \
+   )   |   ?
<   >
```

---

### Special Characters

[Back to summary](#regex)

```text
\n          New line
\r          Carriage return
\t          Tab
\v          Vertical tab
\f          Form feed
\xxx        Octal character xxx
\xhh        Hex character hh
```

---

### Groups and Ranges

[Back to summary](#regex)

```text
.           Any character except new line (\n)
(a|b)       a or b
(...)       Group
(?:...)     Passive (non-c apt uring) group
[abc]       Range (a or b or c)
[^abc]      Not (a or b or c)
[a-q]       Lower case letter from a to q
[A-Q]       Upper case letter from A to Q
[0-7]       Digit from 0 to 7
\x          Group/ sub pattern number " x"
```

---

### Pattern Modifiers

[Back to summary](#regex)

```text
g           Global match
i *         Case-insensitive
m *         Multiple lines
s *         Treat string as single line
x *         Allow comments and whitespace in pattern
e *         Evaluate replacement
U *         Ungreedy pattern
```

---

### String Replacement

[Back to summary](#regex)

```text
$n          nth non-passive group
$2          "xyz" in /^(abc (xy z))$/
$1          "xyz" in /^(?:a bc) (xyz)$/
$`          Before matched string
$'          After matched string
$+          Last matched string
$&          Entire matched string
```

---

## Docker

[Back to summary](#summary)

- [docker overview](#docker-overview)
- [docker image](#docker-image)
- [docker container](#docker-container)
- [docker ports](#docker-ports)
- [docker basic commands](#docker-basic-commands)
- [docker workflow](#docker-workflow)
- [developing with containers](#developing-with-containers)
- [docker compose](#docker-compose)
- [Dockerfile](#dockerfile)
- [private docker repo with aws](#private-docker-repo-with-aws)
- [deploy containerized app](#deploy-containerized-app)
- [docker volumes](#docker-volumes)

---

### Docker overview

[Back to summary](#docker)  

(from docker's documentation)
Docker is an open platform for developing, shipping, and running applications.
Docker enables you to separate your applications from your infrastructure so you
can deliver software quickly. With Docker, you can manage your infrastructure in
the same ways you manage your applications. By taking advantage of Docker’s
methodologies for shipping, testing, and deploying code quickly, you can
significantly reduce the delay between writing code and running it in production.

---

### Docker image

[Back to summary](#docker)  

An image is a read-only template with instructions for creating a Docker container.
Often, an image is based on another image, with some additional customization.
For example, you may build an image which is based on the ubuntu image,
but installs the Apache web server and your application, as well as the
configuration details needed to make your application run.

---

### Docker container

[Back to summary](#docker)  

A container is a runnable instance of an image. You can create, start, stop, move,
or delete a container using the Docker API or CLI. You can connect a container to
one or more networks, attach storage to it, or even create a new image based on its
current state.

---

### Docker ports

[Back to summary](#docker)  

![docker ports](https://www.code4it.dev/static/7e983e27425fb44d41cf3189d3835b92/84f4d/Docker-ports.png)
The way docker works, by default, your local machine and your container can't work
together. You will have to specify a port for your container and a port for your
local machine. This process is made during the `docker run` command. See above.
You can't alocate two containers to the same port, that's sounds logical.

---

### Docker basic commands

[Back to summary](#docker)  

#### docker pull

To pull an image from a registery, run the following command  
`docker pull [OPTIONS] NAME[:TAG|@DIGEST]`
If no tag is specified, the version that will be pulled will be the latest.  

#### docker images

With this command `docker images`, you can see all the images you have available
on your local machine.  

#### delete an image

To delete an image, it has to be used by no container, including the not running
ones.
`docker rmi imageID`

#### docker run

With this command `docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]` you
will instance the Docker image with the specified options.  
This command is for creating new a container.

- The `-d` option is for running container in detached mode so you will only get
container reference as an output.  
- The `--name awesomeName` to specify the name of the container.
- To define ports bindings use `-p3000:3001` option. The second is the container
port, the first the local's.  
- Specify the network with the following options: `--net networkName`  
- Also, you can specify environment variables using this:
`-e VARIABLE_NAME=VALUE`  
Example:

```shell
$ docker run -d \
> -p 3000:30001 \
> -e PASSWORD=password \
> --name=my-container \
> --net my-network \
> image
```

#### docker ps

This command lets you see all containers running.  
`docker ps [-a]`  Add the `-a` option see every containers.  
`docker ps [OPTIONS]`

#### delete a container

To delete a container, it must be not running.
`docker rm container`

#### docker stop | start

This command lets you start or stop an existing container.  
`docker stop [containerID | containerName]`
`docker start [containerID | containerName]`

#### Fecth the logs of a container

`docker logs [OPTIONS] [containerID | containerName]`
string the logs with `-f` option.

#### access terminal of a container

Depending of the version of linux your container is running, use one of the
following commands.  

```shell
docker exec -it [containerID | containerName] /bin/bash
docker exec -it [containerID | containerName] /bin/sh
```

---

### Docker workflow

[Back to summary](#docker)  

![docker_workflow](images/docker_workflow.png)

---

### Developing with containers

[Back to summary](#docker)  

When containers are in the same docker network, they can communicate with each
others using there names.  
Applications from outside needs to use the port.
![docker_server](images/docker_server.png)

This schema is during development process. When you package your application into
its own image, everything is on the same docker network, so accessable by names.

You can see available networks using the following command `docker network ls`  
To create a new network, use the following command
`docker network create my_network`

---

### Docker compose

[Back to summary](#docker)  

Using docker compose you can simplify the running process especially if you run
multiple services that have to work together.  
Let's say you have the following commands to run your services.  

```shell
docker network create mongo-network

docker run -d \
-p 27017:27017 \
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD=password \
--net mongo-network \
--name mongodb \
mongo

docker run -d \
-p 8080:8081 \
-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
-e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
-e ME_CONFIG_MONGODB_SERVER=mongodb \
--net mongo-network \
--name mongo-express \
mongo-express
```

First, check your docker compose version.  
then create a yaml file like this:

```yaml
version:"3"
servives:
  mongodb: # MongoDB service, also sets name
    image: mongo
    ports:
      - 27017:27017
    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=password
  mongo-express: # Mongo-express service
    image: mongo-express
    ports:
      - 8080:8081
    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
      - ME_CONFIG_MONGODB_ADMINPASSWORD=password
      - ME_CONFIG_MONGODB_SERVER=mongodb
```

To run now the yaml file, use `docker-compose -f mongo.yaml up`: use docker-compose
to read a file named mongo.yaml start sevices specified inside it.  
If no network is specified in the yaml file, a default network is created.  
To stop the services, remove the containers and the network, use
`docker-compose -f mongo.yaml down`  

---

### Dockerfile

[Back to summary](#docker)  

Dockerfile is a blueprint for building Docker images.  
The Dockerfile allows you to package your application into a Docker image.  
It also HAS TO be save as "Dockerfile" with no extension.
Assume our previous example app was in `app/` folder.

```Dockerfile
# install node v13.0 running on alpine
FROM node:13-alpine

# optionnaly define environment variables, 
# but its more versatile to set the docker-compose file
ENV MONGO_DB_USERNAME=admin \
    MONGO_DB_PASSWORD=password

# linux command to run
# executed once at build time and get written into your Docker image as a new layer
RUN mkdir -p /home/app

# Where to put witch files
# Here copy everything inside my local app/ directory to the home/app container directory
COPY ./app /home/app

# CMD lets you define a default command to run when your container starts.
CMD ["node", "home/app/sever.js"]
```

Now, to build the image based on the Dockerfile and the docker-compose file present
in `app/` directory, we can run the following command:  
`docker build -t my-app:1.0 .`
Now run the image to verify that:

- application starts successfully
- application environment is configured correctly
Note that when you adjust the Dockerfile, you must rebuild the image.  

---

### private docker repo with aws

[Back to summary](#docker)  

WORK IN PROGRESS

---

### deploy containerized app

[Back to summary](#docker)  

WORK IN PROGRESS

---

### Docker volumes

[Back to summary](#docker)  

WORK IN PROGRESS

---

## Python

[Back to summary](#summary)

- [pip](#pip)
- [venv](#venv)
- [buildin functions or methods](#python-buildin-functions-or-methods)
- [lambda](#lambda)
- [generator](#generator)
- [buildin error type](#buildin-error-type)
- [assert](#assert)
- [buildin modules](#python-buildin-modules)
- [class](#class)
- [abstract class](#abstract-class)
- [database](#database)
- [file](#file)
- [Django](#django)
- [Pygame](#pygame)
- [PySimpleGUI](#pysimplegui)

---

### pip

[Back to summary](#python)  
The pip module is the default pakage manager for python, like npm for node.  
To install a module

```shell
pip install <package_name>
pip3 install <package_name>
```

To update

```shell
pip install <package_name> --upgrade
pip install <package_name> -U
```

A useful module to check and update every installed module

```shell
pip install pip-review

pip-review --interactive
requests==0.14.0 is available (you have 0.13.2)
Upgrade now? [Y]es, [N]o, [A]ll, [Q]uit y
```

To unsinstall

```shell
pip uninstall <package_name>
```

Install all module from a list of modules file

```shell
pip install -r requirements.txt
```

To create that file according to what is installed (best use with virtual env)

```shell
pip freeze > requirements.txt
```

---

### venv

[Back to summary](#python)  
Create a virtual env

```shell
python -m venv venv_name
```

activate venv for that terminal session
on unix

```shell
source venv_name/bin/activate
```

on windows

```shell
source venv_name/Scripts/activate
```

to desactivate venv

```shell
deactivate
```

---

### Python buildin functions or methods

[Back to summary](#python)

- [numbers](#numbers)
- [string](#string)
- [list](#list)
- [set](#set)
- [dictionary](#dictionary)
- [all functions](#all-functions)

---

#### numbers

[Back to summary](#python-buildin-functions-or-methods)

```text
int       Returns the integer object from a float or a string containing digits.
float     Returns a floating-point number object from a number or string containing
          digits with decimal point or scientific notation.
complex   Returns a complex number with real and imaginary components.
hex       Converts a decimal integer into a hexadecimal number with 0x prefix.
oct       Converts a decimal integer in an octal representation with 0o prefix.
pow       Returns the power of the specified numbers.
abs       Returns the absolute value of a number without considering its sign.
round     Returns the rounded number.
```

---

#### string

[Back to summary](#python-buildin-functions-or-methods)

```text
str.capitalize()        Returns the copy of the string with its first character
                        capitalized and the rest of the letters are in lowercased.
string.casefold()       Returns a lowered case string. It is similar to the
                        lower() method, but the casefold() method converts more
                        characters into lower case.
string.center()         Returns a new centered string of the specified length,
                        which is padded with the specified character. The
                        default character is space.
string.count()          Searches (case-sensitive) the specified substring in the
                        given string and returns an integer indicating occurrences
                        of the substring.
string.endswith()       Returns True if a string ends with the specified suffix
                        (case-sensitive), otherwise returns False.
string.expandtabs()     Returns a string with all tab characters \t replaced with
                        one or more space, depending on the number of characters
                        before \t and the specified tab size.
string.find()           Returns the index of the first occurence of a substring
                        in the given string (case-sensitive). If the substring is
                        not found it returns -1.
string.index()          Returns the index of the first occurence of a substring in
                        the given string.
string.isalnum()        Returns True if all characters in the string are 
                        alphanumeric (either alphabets or numbers). If not, it
                        returns False.
string.isalpha()        Returns True if all characters in a string are alphabetic
                        (both lowercase and uppercase) and returns False if at
                        least one character is not an alphabet.
string.isascii()        Returns True if the string is empty or all characters in
                        the string are ASCII.
string.isdecimal()      Returns True if all characters in a string are decimal
                        characters. If not, it returns False.
string.isdigit()        Returns True if all characters in a string are digits or
                        Unicode char of a digit. If not, it returns False.
string.isidentifier()   Checks whether a string is valid identifier string or not.
                        It returns True if the string is a valid identifier
                        otherwise returns False.
string.islower()        Checks whether all the characters of a given string are
                        lowercased or not. It returns True if all characters are
                        lowercased and False even if one character is uppercase.
string.isnumeric()      Checks whether all the characters of the string are
                        numeric characters or not. It will return True if all
                        characters are numeric and will return False even if one
                        character is non-numeric.
string.isprintable()    Returns True if all the characters of the given string
                        are Printable. It returns False even if one character is
                        Non-Printable.
string.isspace()        Returns True if all the characters of the given string are
                        whitespaces. It returns False even if one character is
                        not whitespace.
string.istitle()        Checks whether each word's first character is upper case
                        and the rest are in lower case or not. It returns True if
                        a string is titlecased; otherwise, it returns False. The
                        symbols and numbers are ignored.
string.isupper()        Returns True if all characters are uppercase and False
                        even if one character is not in uppercase.
string.join()           Returns a string, which is the concatenation of the
                        string (on which it is called) with the string elements
                        of the specified iterable as an argument.
string.ljust()          Returns the left justified string with the specified width.
                        If the specified width is more than the string length,
                        then the string's remaining part is filled with the
                        specified fillchar.
string.lower()          Returns the copy of the original string wherein all the
                        characters are converted to lowercase.
string.lstrip()         Returns a copy of the string by removing leading
                        characters specified as an argument.
string.maketrans()      Returns a mapping table that maps each character in the
                        given string to the character in the second string at
                        the same position. This mapping table is used with the
                        translate() method, which will replace characters as per
                        the mapping table.
string.partition()      Splits the string at the first occurrence of the
                        specified string separator sep argument and returns a
                        tuple containing three elements, the part before the
                        separator, the separator itself, and the part after the
                        separator.
string.replace()        Returns a copy of the string where all occurrences of a
                        substring are replaced with another substring.
string.rfind()          Returns the highest index of the specified substring
                        (the last occurrence of the substring) in the given string.
string.rindex()         Returns the index of the last occurence of a substring 
                        in the given string.
string.rjust()          Returns the right justified string with the specified
                        width. If the specified width is more than the string
                        length, then the string's remaining part is filled with 
                        the specified fill char.
string.rpartition()     Splits the string at the last occurrence of the specified
                        string separator sep argument and returns a tuple
                        containing three elements, the part before the separator,
                        the separator itself, and the part after the separator.
string.rsplit()         Splits a string from the specified separator and returns
                        a list object with string elements.
string.rstrip()         Returns a copy of the string by removing the trailing
                        characters specified as argument.
string.split()          Splits the string from the specified separator and
                        returns a list object with string elements.
string.splitlines()     Splits the string at line boundaries and returns a list of
                        lines in the string.
string.startswith()     Returns True if a string starts with the specified
                        prefix. If not, it returns False.
string.strip()          Returns a copy of the string by removing both the
                        leading and the trailing characters.
string.swapcase()       Returns a copy of the string with uppercase characters
                        converted to lowercase and vice versa. Symbols and
                        letters are ignored.
string.title()          Returns a string where each word starts with an uppercase
                        character, and the remaining characters are lowercase.
string.translate()      Returns a string where each character is mapped to its
                        corresponding character in the translation table.
string.upper()          Returns a string in the upper case. Symbols and numbers 
                        remain unaffected.
string.zfill()          Returns a copy of the string with '0' characters padded to
                        the left. It adds zeros (0) at the beginning of the string
                        until the length of a string equals the specified width 
                        parameter.
```

---

#### list

[Back to summary](#python-buildin-functions-or-methods)

```text
list.append()   Adds a new item at the end of the list.
list.clear()    Removes all the items from the list and make it empty.
list.copy()     Returns a shallow copy of a list.
list.count()    Returns the number of times an element occurs in the list.
list.extend()   Adds all the items of the specified iterable (list, tuple, set,
                dictionary, string) to the end of the list.
list.index()    Returns the index position of the first occurance of the
                specified item. Raises a ValueError if there is no item found.
list.insert()   Inserts an item at a given position.
list.pop()      Returns an item from the specified index position and also removes
                it from the list. If no index is specified, the list.pop() method
                removes and returns the last item in the list.
list.remove()   Removes the first occurance of the specified item from the list.
                It the specified item not found then throws a ValueError.
list.reverse()  Reverses the index positions of the elements in the list. The
                first element will be at the last index, the second element will
                be at second last index and so on.
list.sort()     Sorts the list items in ascending, descending, or in custom order.
```

---

#### set

[Back to summary](#python-buildin-functions-or-methods)

```text
set.add()                 Adds an element to the set. If an element is already exist
                          in the set, then it does not add that element.
set.clear()               Removes all the elements from the set.
set.copy()                Returns a shallow copy of the set.
set.difference()          Returns the new set with the unique elements that are not
                          in the another set passed as a parameter.
set.difference_update()   Updates the set on which the method is called with the
                          elements that are common in another set passed as an
                          argument.
set.discard()             Removes a specific element from the set.
set.intersection()        Returns a new set with the elements that are common in
                          the given sets.
set.intersection_update() Updates the set on which the instersection_update()
                          method is called, with common elements among the
                          specified sets.
set.isdisjoint()          Returns true if the given sets have no common elements.
                          Sets are disjoint if and only if their intersection is
                          the empty set.
set.issubset()            Returns true if the set (on which the issubset() is
                          called) contains every element of the other set passed
                          as an argument.
set.pop()                 Removes and returns a random element from the set.
set.remove()              Removes the specified element from the set. If the
                          specified element not found, raise an error.
set.symmetric_difference() Returns a new set with the distinct elements found in
                          both the sets.
set.symmetric_difference_update() Updates the set on which the
                          instersection_update() method called, with the
                          elements that are common among the specified sets.
set.union()               Returns a new set with distinct elements from all the
                          given sets.
set.update()              Updates the set by adding distinct elements from the
                          passed one or more iterables.
```

---

#### dictionary

[Back to summary](#python-buildin-functions-or-methods)

```text
dict.clear()      Removes all the key-value pairs from the dictionary.
dict.copy()       Returns a shallow copy of the dictionary.
dict.fromkeys()   Creates a new dictionary from the given iterable (string,
                  list, set, tuple) as keys and with the specified value.
dict.get()        Returns the value of the specified key.
dict.items()      Returns a dictionary view object that provides a dynamic view
                  of dictionary elements as a list of key-value pairs. This
                  view object changes when the dictionary changes.
dict.keys()       Returns a dictionary view object that contains the list of
                  keys of the dictionary.
dict.pop()        Removes the key and return its value. If a key does not exist
                  in the dictionary, then returns the default value if specified,
                  else throws a KeyError.
dict.popitem()    Removes and return a tuple of (key, value) pair from the
                  dictionary. Pairs are returned in Last In First Out (LIFO) order.
dict.setdefault() Returns the value of the specified key in the dictionary. If
                  the key not found, then it adds the key with the specified
                  defaultvalue. If the defaultvalue is not specified then it set
                  None value.
dict.update()     Updates the dictionary with the key-value pairs from another
                  dictionary or another iterable such as tuple having key-value
                  pairs.
dict.values()     Returns the dictionary view object that provides a dynamic view
                  of all the values in the dictionary. This view object changes
                  when the dictionary changes.
```

---

#### all functions

The following lists all the built-in functions of Python 3.
[Back to summary](#python-buildin-functions-or-methods)

```text
abs()           Returns the absolute value of the given number and returns a
                magnitude of a complex number.
all()           Checks whether all the elements in an iterable are truthy values
                or not. It returns True if all elements in the given iterable are
                nonzero or true. Else, it returns False.
any()           Returns True if at least one element in the given iterable is
                truthy value or boolean True. Returns False for empty or falsy
                value (such as 0, False, none).
ascii()         Returns a string containing a printable representation of an
                object for non-alphabats or invisible characters such as tab,
                carriage return, form feed etc.
bin()           Converts an integer number to a binary string prefixed with '0b'.
bool()          Converts a value to the bool class object containing either True
                or False
bytearray()     Returns a bytearray object which is an array of the given bytes.
                The bytearray class is a mutable sequence of integers in the range
                of 0 to 256.
bytes()         Returns an immutable object of the bytes class initialized with
                the sequence of integers in the range of 0 to 256
callable()      Returns True if the object passed is callable, False if not. In
                Python, classes, methods, and instances are callable because
                calling a class returns a new instance, instances are callable
                if their class includes `__call__()` method.
chr()           Returns the string representing a character whose Unicode code
                point is the integer
classmethod()   Transforms a method into a class method
complex()       Returns a complex number (an object of complex class) for the
                provided real value and imaginary*1j value, or converts a string
                or number to a complex number.
dict()          Creates a dictionary object from the specified keys and values,
                or iterables of keys and values or mapping objects.
delattr()       Deletes the named attribute from the object if the object allows
                it.
dir()           Returns a list of valid attributes of the specified object. If no
                argument passed, it returns the list of names in the current local
                scope.
divmod()        Returns a tuple of two numbers where first number is the
                quotient and the second is the remainder.
exec()          Executes the Python code block passed as a string or a code
                object. The string is parsed as Python statements and then executed.
enumerate()     Returns an object of enumerate class for the given iterable,
                sequence, iterator, or object that supports iteration. The returned
                enumerate object contains tuples for each items of the iterable
                that includes an index (from start which defaults to 0) and the
                values obtained from iterating over iterable.
filter()        Calls the specified function which returns boolen for each item of
                the specified iterable.
float()         Returns an object of the `float` class that represent a floating
                point number converted from a number or string.
format()        Allows multiple substitutions and value formatting. This method
                lets us concatenate elements within a string through positional
                formatting.
frozenset()     Returns an immutable set object with elements from the given
                iterable. Iterables can be list, set, dictionary, tuple, string.
getattr()       Returns the value of the attribute of an object. If the named
                attribute does not exist, default is returned if provided,
                otherwise AttributeError is raised.
hex()           Converts an integer number to a lowercase hexadecimal string
                prefixed with "0x".
hash()          Returns the hash value of the specified object. The hash values
                are used in data storage and to access data in a small time per
                retrieval, and storage space only fractionally greater than the
                total space required for the data or records themselves. In
                Python, hash values are used to compare dictionary keys to
                access values.
hasattr()       Checks if an object of the class has the specified attribute.
help()          It displays the documentation of modules, functions, classes,
                keywords etc.
__import__()    The __import__() method is called by the import statement.
                This method can change the semantics of the import statement which
                is strongly discouraged .
id()            Returns an identity of an object. In Python, every variable or
                literal values are objects and each object has a unique identity
                as an integer number that remains constant for that object through
                out its life time.
int()           Returns an integer object constructed from a number or string,
                or return 0 if no arguments are given.
input()         Allows user to input values.
isinstance()    Checks if the object is an instance of the specified class or any
                of its subclass.
issubclass()    Checks if the specified class is the subclass of the specified
                subclass.
iter()          Returns an iterator object that represents a stream of data for
                the iterable object or sentinel.
len()           Returns the length of the object. Returns total elements in an
                iterable or number of chars in a string.
list()          Returns a list from an iterable passed as arguement.
map()           Applies the specified function to every item of the passed
                iterable, yields the results, and returns an iterator.
max()           Returns the largest value from the specified iterable or multiple
                arguments.
memoryview()    Returns a memory view object of the given object. The memoryview
                object allows Python code to access the internal data of an object
                that supports the buffer protocol without copying.
min()           Returns the lowest value from the specified iterable or provided
                multiple arguments.
next()          Returns the next item from the iterator by calling its __next__()
                method.
object()        Returns a new featureless object. The object class is the base
                class of all classes in Python.
oct()           Converts an integer to octal string prefixed with "0o".
open()          Opens the file (if possible) and returns the corresponding file
                object.
ord()           Returns an integer representing the Unicode character.
pow()           Returns the specified exponent power of a number.
print()         prints the given object to the console or to the text stream file.
property()      Returns the property attribute.
range()         Returns an object of the range class which is an immutable
                sequence type. The `range()` method returns the imutable sequence
                numbers between the specified start and the stop parameter.
repr()          Returns a string containing a printable representation of an
                object. The repr() function calls the underlaying __repr__() 
                function of the object.
reversed()      Returns the reversed iterator of the given sequence. It is same
                as but in reverse order. Internally, it calls the `__reversed__()`
                method of the sequence class. If the given object is not a
                sequence, then override __reversed__() method in the class to be
                used with the reversed() function
round()         Returns a floating-point number rounded to the specified number of
                decimal point.
set()           Returns an object of the set class from the specified iterable
                and its elements. A set object is an unordered collection of
                distinct hashable objects. It cannot contain duplicate values.
setattr()       Sets the specified value to the specified attribute of the
                specified object. This is the counterpart of getattr() method.
slice()         Returns a portion of an iterable as an object of the slice class
                based on the specified range. It can be used with string, list,
                tuple, set, bytes, or range objects or custom class object that
                implements sequence methods __getitem__() and __len__() methods.
sorted()        Returns a sorted list from the items in an iterable.
str()           Returns an object of the str class with the specified value.
sum()           Returns the total of integer elements starting from left to right
                of the given iterable.
super()         Returns a proxy object that allows us to access methods of the
                base class.
tuple()         Creates an empty tuple or converts the specified iterable to a
                tuple.
type()          Either returns the type of the specified object or returns a new
                type object of the specified dynamic class, based on the specified
                class name, base classes and class body.
vars()          Returns the __dict__ attribute of the specified object. A
                __dict__ object used to store an object's writable attributes.
zip()           Takes iterables, aggregates them in a tuple, and return it.
```

---

### python buildin modules

[Back to summary](#python)

- [os](#os)
- [sys](#sys)
- [math](#math)
- [statistics](#statistics)
- [collections](#collections)
- [random](#random)
- [re](#re)

---

#### os

[Back to summary](#python-buildin-modules)  
It is possible to automatically perform many operating system tasks. The OS module
in Python provides functions for creating and removing a directory (folder),
fetching its contents, changing and identifying the current directory, etc.

```python
os.getcwd()           # get current working directory
os.mkdir("<path>")    # Makes a directory at path
os.chdir("<path>")    # changing current workign directory
os.rmdir("<path>")    # remove the directory. Not possible with current working directory
os.listdir("<path>")  # return a python list of files
os.walk("<path>")     # return (dirpath, dirnames, filenames) of directory in path
```

---

#### sys

[Back to summary](#python-buildin-modules)  

The sys module provides functions and variables used to manipulate different
parts of the Python runtime environment.

```python
sys.argv    # returns a list of command line arguments passed to a Python script.
            # Index 0 always is the file itself
sys.exit    # This causes the script to exit back to either the Python console or
            # the command prompt.
sys.maxsize # Returns the largest integer a variable can take.
sys.path    # This is an environment variable that is a search path for all Python
            # modules.
sys.version # This attribute displays a string containing the version number of
            # the current Python interpreter.
```

---

#### math

[Back to summary](#python-buildin-modules)  

Some of the most popular mathematical functions are defined in the math module.
These include trigonometric functions, representation functions, logarithmic
functions, angle conversion functions, etc. In addition, two mathematical constants
are also defined in this module.

```python
math.pi  # return a float representing pi
math.e  # It is called Euler's number and it is a base of the natural logarithm.
        # Its value is 2.718281828459045
math.radians(<number>) # convert <number> angle in degrees to its radians value
math.degrees(<number>) # convert <number> radians to its degrees value
math.sin(<number>) # |
math.cos(<number>) # |- trigonometric calculation
math.tan(<number>) # |
math.log(<number>) # returns the natural logarithm of a given number.
math.log10(<number>) # returns the base-10 logarithm of the given number.
math.exp(<number>) # returns a float number after raising e to the power of the
                   # given number
math.pow(<number>, <number>) # receives two float arguments, raises the first to
                             # the second and returns the result
math.sqrt(<number>) # returns the square root of a given number.
math.ceil(<number>)
math.floor(<number>)
```

---

#### statistics

[Back to summary](#python-buildin-modules)  

The statistics module provides functions to mathematical statistics of numeric data.

```python
statistics.mean(<list>) # calculates the arithmetic mean of the numbers in a list.
statistics.median(<list>) # returns the middle value of numeric data in a list.
statistics.mode(<list>) # returns the most common data point in the list.
statistics.stdev(<list>) # calculates the standard deviation on a given sample
                         # in the form of a list.
```

---

#### collections

[Back to summary](#python-buildin-modules)  

The collections module provides alternatives to built-in container data types such
as list, tuple and dict.

##### namedtuple()

The namedtuple() function returns a tuple-like object with named fields. These field
attributes are accessible by lookup as well as by index.

```python
student = collections.namedtuple('student', [name, age, marks])
s1 = student("Imran", 21, 98)
s1.name # "Imran"
s1[0] # same
```

---

##### OrderedDict()

The OrderedDict() function is similar to a normal dictionary object in Python.
However, it remembers the order of the keys in which they were first inserted.

```python
d1 = collections.OrderedDict()
d1['A'] = 65
d1['C'] = 67
d1['B'] = 66
d1['D'] = 68

for k,v in d1.items():
    print (k,v)
"""
A 65
C 67
B 66
D 68
"""
```

---

##### deque()

A deque object support appends and pops from either ends of a list. It is more
memory efficient than a normal list object. In a normal list object, the removal
of any item causes all items to the right to be shifted towards left by one index.
Hence, it is very slow.

```python
q=collections.deque([10,20,30,40]) # set the deque object
q.append(50) # append at the end
q.appendleft(0) # insert a the begining
q.pop() # pop last value
q.popleft() # pop first value
```

---

#### random

[Back to summary](#python-buildin-modules)  

The random module is a built-in module to generate the pseudo-random variables.
It can be used perform some action randomly such as to get a random number,
selecting a random elements from a list, shuffle elements randomly, etc.

```python
random.random() # returns a random float number between 0.0 to 1.0
random.randint(<int>,<int>) # returns a random integer between the specified integers.
random.randrange(<int>,<int>,<int>) # returns a randomly selected element from the
                                    # range created by the start, stop and step
                                    # arguments.
random.choice("sequence") # returns a randomly selected element from a non-empty
                          # sequence. An empty sequence as argument raises an
                          # IndexError.
random.shuffle(<list>) # method randomly reorders the elements in a list.
```

---

#### re

[Back to summary](#python-buildin-modules)  

The random module is a built-in module to use regular expression.  
First the meta-characters

```text
[abc] match any of the characters a, b, or c
[a-c] which uses a range to express the same set of characters.
[a-z] match only lowercase letters.
[0-9] match only digits.
\d Matches any decimal digit; this is equivalent to the class [0-9].
\D Matches any non-digit character
\s Matches any whitespace character
\S Matches any non-whitespace character
\w Matches any alphanumeric character
\W Matches any non-alphanumeric character.
. Matches with any single character except newline ‘\n'.
? match 0 or 1 occurrence of the pattern to its left
+ 1 or more occurrences of the pattern to its left
* 0 or more occurrences of the pattern to its left
\b boundary between word and non-word. /B is opposite of /b
[..] Matches any single character in a square bracket
\ It is used for special meaning characters like . to match a period
{n,m} Matches at least n and at most m occurrences of preceding
a| b Matches either a or b
```

The re.match() function in re module tries to find if the specified pattern is
present at the beginning of the given string.

```python
re.match(pattern, string)
mystr = "Welcome to TutorialsTeacher"
obj1 = match("We", mystr)
# return <re.Match object; span=(0, 2), match='We'> match object
obj.start() # 0
obj.end() # 2
```

The re.search() function searches for a specified pattern anywhere in the given
string and stops the search on the first occurrence.

```python
string = "Try to earn while you learn"
obj = search("earn", string) # return also a match object
```

re.findall(): As against the search() function, the findall() continues to search
for the pattern till the target string is exhausted. The object returns a list of
all occurrences.

```python
string = "Try to earn while you learn"
obj = findall("earn", string) # return ['earn', 'earn']
```

The re.finditer() function returns an iterator object of all matches in the
target string. For each matched group, start and end positions can be obtained
by span() attribute.

```python
string = "Try to earn while you learn"
it = finditer("earn", string)
for match in it:
    print(match.span())
"""
(7, 11)
(23, 27)
"""
```

The re.split() function works similar to the split() method of str object in
Python. It splits the given string every time a white space is found. In the
above example of the findall() to get all words, the list also contains each
occurrence of white space as a word. That is eliminated by the split() function
in re module.

```python
string = "Flat is better than nested. Sparse is better than dense."
words = split(r' ', string) # return ['Flat', 'is', 'better', 'than', 'nested.',
                            #         'Sparse', 'is', 'better', 'than', 'dense.']
```

The re.compile() function returns a pattern object which can be repeatedly used
in different regex functions. In the following example, a string 'is' is compiled
to get a pattern object and is subjected to the search() method.

```python
pattern = compile(r'[aeiou]')
string = "Flat is better than nested. Sparse is better than dense."
pattern.match(string)
```

---

---

### lambda

[Back to summary](#python)  
The def keyword is used to define a function in Python. The lambda keyword is
used to define anonymous functions in Python. Usually, such a function is meant
for one-time use. The expression does not need to always return a value. The
fonction can take multiple parameters.

```python
lambda [arguments] : expression
```

Exemple

```python
>>> def dosomething(fn):
     print('Calling function argument:')
     fn()
>>> dosomething(lambda : print('Hello World')) # passing anonymous function
Calling function argument:
Hello World
>>> myfn = lambda : print('Hello World')
>>> dosomething(myfn) # passing lambda function
```

Python has built-in functions that take other functions as arguments. The
argument function can be a normal function or a lambda function.

```python
>>> sqrList = map(lambda x: x*x, [1, 2, 3, 4]) # passing anonymous function
>>> next(sqrList)
1
>>> next(sqrList)
4
>>> next(sqrList)
9
>>> next(sqrList)
16
>>> next(sqrList)
25
```

---

### generator

[Back to summary](#python)  
Python provides a generator to create your own iterator function. A generator is
a special type of function which does not return a single value, instead, it
returns an iterator object with a sequence of values. In a generator function, a
yield statement is used rather than a return statement.  

Exemple

```python
def generator():
 yield 1
 yield 2
 yield 3

gen = generator()
next(gen) # 1
next(gen) # 2
next(gen) # 3
next(gen) # StopIteration Error
```

The below script uses the try..except block to handle the StopIteration error.
It will break the while loop once it catches the StopIteration error.

```python
gen=square_of_sequence(5)
while True:
    try:
        print ("Received on next(): ", next(gen))
    except StopIteration:
        break
```

Python also provides a generator expression, which is a shorter way of defining
simple generator functions. The generator expression is an anonymous generator function.

```python
squres = (x*x for x in range(5))
```

The generator expression can also be passed in a function. It should be passed
without parentheses, as shown below.

```python
sum(x*x for x in range(5))
```

---

### buildin error type

[Back to summary](#python)  
The following lists important built-in exceptions in Python.

```text
AssertionError Raised when the assert statement fails.
AttributeError Raised on the attribute assignment or reference fails.
EOFError  Raised when the input() function hits the end-of-file condition.
FloatingPointError Raised when a floating point operation fails.
GeneratorExit Raised when a generator's close() method is called.
ImportError  Raised when the imported module is not found.
IndexError  Raised when the index of a sequence is out of range.
KeyError  Raised when a key is not found in a dictionary.
KeyboardInterrupt Raised when the user hits the interrupt key (Ctrl+c or delete).
MemoryError  Raised when an operation runs out of memory.
NameError  Raised when a variable is not found in the local or global scope.
NotImplementedError Raised by abstract methods.
OSError   Raised when a system operation causes a system-related error.
OverflowError Raised when the result of an arithmetic operation is too large to
              be represented.
ReferenceError Raised when a weak reference proxy is used to access a garbage
               collected referent.
RuntimeError Raised when an error does not fall under any other category.
StopIteration Raised by the next() function to indicate that there is no further
              item to be returned by the iterator.
SyntaxError  Raised by the parser when a syntax error is encountered.
IndentationError Raised when there is an incorrect indentation.
TabError  Raised when the indentation consists of inconsistent tabs and spaces.
SystemError  Raised when the interpreter detects internal error.
SystemExit  Raised by the sys.exit() function.
TypeError  Raised when a function or operation is applied to an object of an
           incorrect type.
UnboundLocalError Raised when a reference is made to a local variable in a
                  function or method, but no value has been bound to that variable.
UnicodeError Raised when a Unicode-related encoding or decoding error occurs.
UnicodeEncodeError Raised when a Unicode-related error occurs during encoding.
UnicodeDecodeError Raised when a Unicode-related error occurs during decoding.
UnicodeTranslateError Raised when a Unicode-related error occurs during translation.
ValueError  Raised when a function gets an argument of correct type but improper
            value.
ZeroDivisionError Raised when the second operand of a division or module
                  operation is zero.
```

Handle those errors with try .. except statement

```python
try:
    #statements in try block
except <error_type>: # error type is optionnal but good practice
    #executed when error in try block
else:
    #executed if try block is error-free
finally:
    #executed irrespective of exception occured or not
```

---

### assert

[Back to summary](#python)  
In Python, the assert statement is used to continue the execute if the given
condition evaluates to True. If the assert condition evaluates to False, then it
raises the AssertionError exception with the specified error message.

```python
assert condition [, Error Message]
```

Exemple

```python
assert x > 0, 'Only positive numbers are allowed'
```

Get only custom error message in console

```python
def square(x):
    assert x>=0, 'Only positive numbers are allowed'
    return x*x

try:
    square(-2)
except AssertionError as msg:
    print(msg)
```

---

### class

[Back to summary](#python)

- [basics](#basics)
- [class property](#class-property)
- [method](#method)
- [Inheritance](#inheritance)
- [Access modifiers](#access-modifiers)
- [decorators](#decorators)

---

#### basics

[Back to summary](#class)  
A class in Python can be defined using the class keyword.

```python
class <ClassName>:
    <statement1>
    <statement2>
    .
    .
    <statementN>
```

Class attributes are the variables defined directly in the class that are shared
by all objects of the class. Class attributes can be accessed using the class
name as well as using the objects.

```python
class Student:
    schoolName = 'XYZ School'

>>> Student.schoolName
'XYZ School'
>>> std = Student()
>>> std.schoolName
'XYZ School'
```

The following example demonstrates the use of class attribute count.

```python
class Student:
    count = 0
    def __init__(self):
        Student.count += 1

>>> std1=Student()
>>> Student.count
1
>>> std2 = Student()
>>> Student.count
2
```

The constructor method is invoked automatically whenever a new object of a class
is instantiated.  
The constructor must have a special name \_\_init\_\_() and a special parameter
called self.  
Instance attributes are attributes or properties attached to an instance of a
class. Instance attributes are defined in the constructor.  
You can specify the values of instance attributes through the constructor. The
following constructor includes the name and age parameters, other than the self
parameter.  
You can also set default values to the instance attributes.

```python
class Student:
    def __init__(self, name, gender="Male"): # constructor method
        print('Constructor invoked')
  self.name = name
  self.type = "Student"
  self.gender = gender
```

You can delete attributes, objects, or the class itself, using the del keyword,
as shown below.

```python
>>> std = Student('Steve', 25)
>>> del std.name # deleting attribute
>>> std.name
Traceback (most recent call last):
File "<pyshell#42>", line 1, in <module>
std.name
AttributeError: 'Student' object has no attribute 'name'
>>> del std  # deleting object
>>> std.name
Traceback (most recent call last):
File "<pyshell#42>", line 1, in <module>
std.name
NameError: name 'std' is not defined
>>> del Student  # deleting class
>>> std = Student('Steve', 25)
Traceback (most recent call last):
File "<pyshell#42>", line 1, in <module>
std = Student()
NameError: name 'Student' is not defined
```

---

#### class property

[Back to summary](#class)  
In Python, a property in the class can be defined using the property() function.
The property() method in Python provides an interface to instance attributes. It
encapsulates instance attributes and provides a property, same as Java and C#.  
The property() method takes the get, set and delete methods as arguments and
returns an object of the property class.

```python
class Student:
    def __init__(self):
        self.__name=''
    def setname(self, name):
        print('setname() called')
        self.__name=name
    def getname(self):
        print('getname() called')
        return self.__name
    name=property(getname, setname)
```

In the above example, property(getname, setname) returns the property object and
assigns it to name. Thus, the name property hides the private instance attribute
\_\_name. The name property is accessed directly, but internally it will invoke
the getname() or setname() method, as shown below.  
It is recommended to use the property decorator instead of the property() method.

```python
>>> std = Student()
>>> std.name="Steve"
setname() called
>>> std.name
getname() called
'Steve'
```

---

#### method

[Back to summary](#class)  
You can define as many methods as you want in a class using the def keyword.  
Each method must have the first parameter, generally named as self, which refers
to the calling instance.  
Self is just a conventional name for the first argument of a method in the
class. A method defined as mymethod(self, a, b) should be called as
x.mymethod(a, b) for the object x of the class.  
Defining a method in the class without the self parameter would raise an
exception when calling a method.  
The method can access instance attributes using the self parameter.

```python
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    def displayInfo(self): # class method
        print('Student Name: ', self.name,', Age: ', self.age)

>>> std = Student('Steve', 25)
>>> std.displayInfo()
Student Name: Steve , Age: 25
```

---

#### Inheritance

[Back to summary](#class)  
The child class inherits data definitions and methods from the parent class.
This facilitates the reuse of features already available. The child class can
add a few more definitions or redefine a base class method.

```python
class parent:
    def __init__(self, name):
  self.name = name

class child(parent):
 def __init__(self, name, age):
  super().__init__(name) # The __init__() method forwards the parameters to the
                         # constructor of its parent class using the super()
                         # function.
  self.age = age
```

To override a method, simply define a new one with the same name inside the
child class.

---

#### Access modifiers

[Back to summary](#class)  
Classical object-oriented languages, such as C++ and Java, control the access to
class resources by public, private, and protected keywords. Private members of
the class are denied access from the environment outside the class. They can be
handled only from within the class.

---

##### public members

Public members (generally methods declared in a class) are accessible from
outside the class. The object of the same class is required to invoke a public
method. This arrangement of private instance variables and public methods
ensures the principle of data encapsulation.  
All members in a Python class are public by default. Any member can be accessed
from outside the class environment.

```python
class Student:
    schoolName = 'XYZ School' # class attribute

    def __init__(self, name, age):
        self.name=name # instance attribute
        self.age=age # instance attribute

>>> std = Student("Steve", 25)
>>> std.schoolName
'XYZ School'
>>> std.name
'Steve'
>>> std.age = 20
>>> std.age
20
```

---

##### protected members

Protected members of a class are accessible from within the class and are also
available to its sub-classes. No other environment is permitted access to it.
This enables specific resources of the parent class to be inherited by the child
class.  
Python's convention to make an instance variable protected is to add a prefix \_
(single underscore) to it. This effectively prevents it from being accessed
unless it is from within a sub-class.  
In fact, this doesn't prevent instance variables from accessing or modifying the
instance. You can still perform the following operations:

```python
class Student:
    _schoolName = 'XYZ School' # protected class attribute

    def __init__(self, name, age):
        self._name=name  # protected instance attribute
        self._age=age # protected instance attribute

>>> std = Student("Swati", 25)
>>> std._name
'Swati'
>>> std._name = 'Dipa'
>>> std._name
'Dipa'
```

However, you can define a property using property decorator and make it
protected, as shown below.  
Without the setter, you won't be able to modify \_name like this
"std.name = 'another name'", but you can still modify directly \_name value.
Hence, the responsible programmer would refrain from accessing and modifying
instance variables prefixed with \_ from outside its class.

```python
class Student:
 def __init__(self,name):
  self._name = name
 @property
 def name(self):
  return self._name
 @name.setter
 def name(self,newname):
  self._name = newname

>>> std = Student("Swati")
>>> std.name
'Swati'
>>> std.name = 'Dipa'
>>> std.name
'Dipa'
>>> std._name # still accessible
```

---

##### Private members

Python doesn't have any mechanism that effectively restricts access to any
instance variable or method. Python prescribes a convention of prefixing the
name of the variable/method with a single or double underscore to emulate the
behavior of protected and private access specifiers.  
The double underscore \_\_ prefixed to a variable makes it private. It gives a
strong suggestion not to touch it from outside the class. Any attempt to do so
will result in an AttributeError:

```python
class Student:
    __schoolName = 'XYZ School' # private class attribute

    def __init__(self, name, age):
        self.__name=name  # private instance attribute
        self.__salary=age # private instance attribute
    def __display(self):  # private method
     print('This is private method.')

>>> std = Student("Bill", 25)
>>> std.__schoolName
AttributeError: 'Student' object has no attribute '__schoolName'
>>> std.__name
AttributeError: 'Student' object has no attribute '__name'
>>> std.__display()
AttributeError: 'Student' object has no attribute '__display'
```

Python performs name mangling of private variables. Every member with a double
underscore will be changed to \_object.\_class\_\_variable. So, it can still be
accessed from outside the class, but the practice should be refrained.  
Thus, Python provides conceptual implementation of public, protected, and private
access modifiers, but not like other languages like C#, Java, C++.

```python
>>> std = Student("Bill", 25)
>>> std._Student__name
'Bill'
>>> std._Student__name = 'Steve'
>>> std._Student__name
'Steve'
>>> std._Student__display()
'This is private method.'
```

---

### decorators

[Back to summary](#class)

- [introduction](#introduction)
- [property](#property)
- [classmethod](#classmethod)
- [staticmethod](#staticmethod)

---

#### introduction

[Back to summary](#decorators)  
In programming, decorator is a design pattern that adds additional
responsibilities to an object dynamically. In Python, a function is the
first-order object. So, a decorator in Python adds additional
responsibilities/functionalities to a function dynamically without modifying a
function.  
In Python, a function can be passed as an argument to another function. It is
also possible to define a function inside another function, and a function can
return another function.
So, a decorator in Python is a function that receives another function as an
argument. The behavior of the argument function is extended by the decorator
without actually modifying it. The decorator function can be applied over a
function using the @decorator syntax.

```python
def mydecorator(fn):
 fn()
 print('How are you?')

def greet():
 print('Hello! ', end='')
>>> greet()
Hello!

@mydecorator
def greet():
 print('Hello! ', end='')
>>> greet()
Hello! How are you?
```

---

#### property

[Back to summary](#decorators)  
The \@property decorator is a built-in decorator in Python for the property()
function. Use @property decorator on any method in the class to use the method
as a property.  
You can use the following three decorators to define a property:

- @property: Declares the method as a property.
- @<property-name\>.setter: Specifies the setter method for a property that
- sets the value to a property.
- @<property-name\>.deleter: Specifies the delete method as a property that
- deletes a property.

```python
class Student:
    def __init__(self, name):
        self.__name = name

    @property
    def name(self):
        return self.__name

    @name.setter
    def name(self, value):
        self.__name=value

    @name.deleter   #property-name.deleter decorator
    def name(self, value):
        print('Deleting..')
        del self.__name

>>> s = Student('Steve')
>>> s.name
'Steve'
>>> s.name = 'Bill'
'Bill'
>>> del s.name
Deleting..
>>> s.name
Traceback (most recent call last):
File "<pyshell#16>", line 1, in <module>
    p.name
File "C:\Python37\test.py", line 6, in name
    return self.__name
AttributeError: 'Student' object has no attribute '_Student__name'
```

---

#### classmethod

[Back to summary](#decorators)  
In Python, the @classmethod decorator is used to declare a method in the class
as a class method that can be called using ClassName.MethodName(). The class
method can also be called using an object of the class.  
The @classmethod is an alternative of the classmethod() function. It is
recommended to use the @classmethod decorator instead of the function because it
is just a syntactic sugar.  

@classmethod Characteristics:

- Declares a class method.
- The first parameter must be cls, which can be used to access class attributes.
- The class method can only access the class attributes but not the instance attributes.
- The class method can be called using ClassName.MethodName() and also using object.
- It can return an object of the class.
  The class method can only access class attributes, but not the instance
  attributes. It will raise an error if trying to access the instance attribute
  in the class method.

```python
class Student:
    name = 'unknown' # class attribute
    def __init__(self):
        self.age = 20  # instance attribute

    @classmethod
    def tostring(cls):
        print('Student Class Attributes: name=',cls.name)
```

The class method can also be used as a factory method to get an object of the
class, as shown below.

```python
class Student:

    def __init__(self, name, age):
        self.name = name  # instance attribute
        self.age = age # instance attribute

    @classmethod
    def getobject(cls):
        return cls('Steve', 25)
```

---

#### staticmethod

[Back to summary](#decorators)  
The @staticmethod is a built-in decorator that defines a static method in the
class in Python. A static method doesn't receive any reference argument whether
it is called by an instance of a class or by the class itself.  
@staticmethod Characteristics

- Declares a static method in the class.
- It cannot have cls or self parameter.
- The static method cannot access the class attributes or the instance attributes.
- The static method can be called using ClassName.MethodName() and also using object.MethodName().
- It can return an object of the class.

```python
class Student:
    name = 'unknown' # class attribute

    def __init__(self):
        self.age = 20  # instance attribute

    @staticmethod
    def tostring():
        print('Student Class')
```

---

### abstract class

[Back to summary](#python)  
A class is called an Abstract class if it contains one or more abstract methods.
An abstract method is a method that is declared, but contains no implementation.
Abstract classes may not be instantiated, and its abstract methods must be
implemented by its subclasses.  
'abc' works by marking methods of the base class as abstract. This is done by
@absttractmethod decorator. A concrete class which is a sub class of such
abstract base class then implements the abstract base by overriding its abstract
methods.  
The abc module defines ABCMeta class which is a metaclass for defining abstract
base class. Following example defines Shape class as an abstract base class using
ABCMeta. The shape class has area() method decorated by abstractmethod.  
A Rectangle class now uses above Shape class as its parent and implementing the
abstract area() method. Since it is a concrete class, it can be instantiated and
imlemented area() method can be called.

```python
import abc
class Shape(metaclass=abc.ABCMeta):
   @abc.abstractmethod
   def area(self):
      pass


class Rectangle(Shape):
   def __init__(self, x,y):
      self.l = x
      self.b = y
   def area(self):
      return self.l * self.b


r = Rectangle(10, 20)
print ('area: ', r.area())
```

_Note the abstract base class may have more than one abstract methods. The child
class must implement all of them failing which TypeError will be raised._

The abc module also defines ABC helper class which can be used instead of ABCMeta
class in definition of abstract base class.  
Instead of subclassing from abstract base class, it can be registered as abstract
base by register class decorator.

```python
class Shape(abc.ABC):
   @abc.abstractmethod
   def area(self):
      pass

@Shape.register
class Rectangle():
   def __init__(self, x,y):
   self.l = x
   self.b = y
   def area(self):
      return self.l * self.b
```

---

### database

[Back to summary](#python)  
Python DB-API is a set of standards recommended by a Special Interest Group for
database module standardization. Python modules that provide database interfacing
functionality with all major database products are required to adhere to this
standard.  
Standard Python distribution has in-built support for SQLite database
connectivity. It contains sqlite3 module which adheres to DB-API 2.0 and is
written by Gerhard Haring. Other RDBMS products also have DB-API compliant modules:

- MySQL: PyMySql module
- Oracle: Cx-Oracle module
- SQL Server: PyMsSql module
- PostGreSQL: psycopg2 module
- ODBC: pyodbc module
- MondoDB: PyMongo module  
  Read documentation for more informations

---

### file

[Back to summary](#python)  
In Python, the IO module provides methods of three types of IO operations; raw
binary files, buffered binary files, and text files.

---

#### Read files

Use the 'rb' mode in the open() function to read a binary files

```python
with open('C:\myfile.txt') as f # opening a file
 lines = f.read() # reading a file

with open('C:\myfile.txt') as f # opening a file
 line1 = f.readline() # reading a line
 line2 = f.readline() # reading a line

with open('C:\myfile.txt') as f # opening a file
 lines = f.readlines() # return a list. each item of the list is a line of the file

with open('C:\myfile.txt') as f # opening a file
 for line in f:
     print(line)
```

---

##### Write

- write(s): Write the string s to the stream and return the number of characters
written.
- writelines(lines): Write a list of lines to the stream. Each line must have a
separator at the end of it.

```python
with open('C:\myfile.txt', "w") as f # opening a file with write permission
 f.write("Hello") # overwriting to file and return 5

with open('C:\myfile.txt', "a") as f # opening a file with write permission in
                                     # appedind mode
 f.write("Hello") # append to file and return 5

with open('C:\myfile.txt', "w") as f # opening a file with write permission
 f.writelines(lines)

with open('C:\binfile.bin', "wb") as f # opening a file with write permission
                                       #and binary mode
 num=[5, 10, 15, 20, 25]
 arr=bytearray(num)
 f.write(arr)
```

---

### Django

[Back to summary](#python)

- [Preparing Environnement](#preparing-environnement)
- [Create project](#create-project)
- [Database Setup](#database-setup)
- [Creating an app](#creating-an-app)
- [Creating models](#creating-models)
- [Database editing](#database-editing)
- [Administration](#administration)
- [Management](#management)
- [Views](#views)
- [Add some static files](#add-some-static-files)
- [Render Form In Template](#render-form-in-template)
- [Custom template tags and filters](#custom-template-tags-and-filters)
- [Setting Up User Accounts](#setting-up-user-accounts)
- [Allow Users to Own Their Data](#allow-users-to-own-their-data)
- [Paginator](#paginator)
- [Deploy to Heroku](#deploy-to-heroku)

---

#### Preparing Environnement

[back to summary](#django)  
Create project folder and navigate to it

```shell
mkdir project_name && cd $_
```

Create venv for the project

```shell
python -m venv env_name   # PC
python3 -m venv env_name  # Mac
```

Activate environnement (Replace "bin" by "Scripts" in Windows)

```shell
source env_name\bin\activate     # Mac
source env_name\Scripts\activate # PC
```

Install Django (and others dependencies if needed)

```shell
pip install django
```

Create requirements file

```shell
pip freeze > requirements.txt
```

Use this commmand to install all required files based on your pip freeze command

```shell
pip install -r requirements.txt
```

Version control initialisation, be sure to create appropriate gitignore

```shell
git init
```

---

#### Create project

[back to summary](#django)  
This will create a mysite directory in your current directory the manage.py file

```shell
django-admin startproject mysite (or I like to call it config)
```

You can check that everything went fine

```shell
python manage.py runserver
```

---

#### Database Setup

[back to summary](#django)  
Open up mysite/settings.py. It’s a normal Python module with module-level
variables representing Django settings.  
If you wish to use another database, install the appropriate database bindings
and change the following keys in the DATABASES 'default' item to match your
database connection settings

```text
ENGINE – 'django.db.backends.sqlite3',
         'django.db.backends.postgresql',
         'django.db.backends.mysql', or
         'django.db.backends.oracle'
```

The default value, BASE_DIR / 'db.sqlite3', will store the file in your project
directory  
NAME – The name of your database. If you’re using SQLite, the database will be a
file on your computer; in that case, NAME should be the full absolute path,
including filename, of that file.  
The default value, BASE_DIR / 'db.sqlite3', will store the file in your project
directory.  
If you are not using SQLite as your database, additional settings such as USER,
PASSWORD, and HOST must be added.  
For more details, see the reference documentation for [DATABASES](https://docs.djangoproject.com/en/4.0/ref/settings/#std:setting-DATABASES)

---

#### Creating an app

[back to summary](#django)  
Create an app_name directory and all default file/folder inside

```shell
python manage.py startapp app_name
```

Apps are "plugable", "plug in" the app into the project by adding it in installed
apps in settings.py

```python
INSTALLED_APPS = [
 'app_name',
 ...
```

Into urls.py from project folder, inculde app urls to project

```python
urlpatterns = [
 path('app_name/', include('app_name.urls')),
 path('admin/', admin.site.urls),
]
```

---

#### Creating models

[back to summary](#django)  
Create your class in the app_name/models.py file and add [fields](https://docs.djangoproject.com/en/3.2/ref/models/fields/)
It’s important to add `__str__()` methods to your models, because objects’
representations are used throughout Django’s automatically-generated admin.

```python
from django.db import models

Class ModelName(models.Model):
  """A very basic model"""
  title = models.CharField(max_length=100) #max-length is required with charfiel

  def __str__(self):
    return self.title
```

---

#### Database editing

[back to summary](#django)  
By running makemigrations, you’re telling Django that you’ve made some changes to
your models
you can specify app_name or not

```shell
python manage.py makemigrations (app_name)
```

Check the SQL commands that migration would run (identifier is given with
makemigrations command).

```shell
python manage.py sqlmigrate #identifier
```

Check for any problems in your project without migrate database

```shell
python manage.py check
```

Create tables and fields in database based on your models

```shell
python manage.py migrate
```

Hop into the interactive Python shell and play around with the free API Django
gives you

```shell
python manage.py shell
```

---

#### Administration

[back to summary](#django)  
Create a user who can login to the admin site

```shell
python manage.py createsuperuser
```

Into app_name/admin.py, add the model to administration site

```python
from django.contrib import admin
from .models import ModelName

admin.site.register(ModelName)
```

Open a web browser and go to “/admin/” on your local domain

---

#### Management

[back to summary](#django)  
Django allows you to create customs CLI commands.  
First, create required folders

```shell
mkdir app_name/management app_name/management/commands && cd $_
```

Create a python file with your command name

```shell
touch your_command_name.py
```

Edit your new python file. Create a class that will handle your command.

```python
from django.core.management.base import BaseCommand
# import anything else you need to work with (models?)

class Command(BaseCommand):
  help = "This message will be shown with the --help option after your command"

  def handle(self, args, *kwargs):
   # Task the command is supposed to do
```

You can now execute your command

```shell
python manage.py my_custom_command
```

---

#### Views

[back to summary](#django)  
Open the file app_name/views.py and put the following Python code in it.
This is the simplest view possible.

```python
from django.http import HttpResponse

def index(request):
 return HttpResponse("Hello, world. You're at the index.")
```

In the app_name/urls.py file include the following code.  
This will specif the routes of your app

```python
from django.urls import path
from . import views

app_name = "app_name"
urlpatterns = [
 path('', views.index, name='index'),
]
```

You can pass arguments to your views like in the exemple below.

```python
def detail(request, question_id):
 return HttpResponse(f"You're looking at question {question_id}")
```

And this is how you pass arguments in url

```python
urlpatterns = [
 path('<int:question_id>/', views.detail, name='detail'),
 ...
```

Finaly, we can pass arguments to template like this

```text
{% url 'app_name:view_name' question_id %}
```

This is the folder path to follow for template

```shell
app_name/templates/app_name/index.html
```

Pass values from views to template.  
We use the render shortcut here

```python
def index(request):
    page_title = "Randomecipe - Home Page"
    context = {"page_title": page_title}
    return render(request, "app_name/index.html", context)
```

Redirect to 404 page if nothing is found

```python
question = get_object_or_404(Question, pk=question_id)
```

Get a look at Django's [documentation](https://docs.djangoproject.com/en/4.0/topics/templates/)
to see how you can edit templates.

---

#### Add some static files

[back to summary](#django)  
Be sure to have this in your INSTALLED_APPS

```python
'django.contrib.staticfiles'
```

Create static folder associated with your app

```shell
mkdir app_name/static app_name/static/app_name
```

Put this on top of your template

```html
{% load static %}
```

Exemple of use static for stylesheet

```html
<link
  rel="stylesheet"
  type="text/css"
  href="{% static 'app_name/style.css' %}"
/>
```

---

#### Django Forms

[back to summary](#django)  
Create form module

```shell
touch app_name/forms.py
```

An exemple of form with Form inherit

```python
from django import forms
from .models import YourModel

class ExempleForm(forms.Form):
  exemple_field = forms.CharField(label='Exemple label', max_length=100)
```

An exemple of form with ModelForm inherit  
A ModelForm maps a model class’s fields to HTML form <in­put> elements via a Form.
Widget is optional. Use it to override default widget  
Widget [list](https://docs.djangoproject.com/en/3.2/ref/forms/widgets/)

```python
from django import forms
from .models import YourModel

class ExempleForm(forms.ModelForm):
 class meta:
  model = YourModel
  fields = ["fields"]
  labels = {"text": "label_text"}
  widget = {"text": forms.widget_name}
```

In your views, create a blank form if no data submitted

```python
if request.method != "POST":
  form = ExempleForm()
```

The form object contain's the informations submitted by the user

```python
form = ExempleForm(data=request.POST)
```

Form validation. Always use redirect function

```python
is form.isvalid()
  form.save()
  return redirect("app_name:view_name", argument=ardument)
```

In your template, add this tag to prevent "cross-site request forgery" attack

```html
{% csrf_token %}
```

---

#### Render Form In Template

[back to summary](#django)  
The most simple way to render the form, but usualy it's ugly

```html
{{ form.as_p }}
```

The | is a filter, and here for placeholder, it's a custom one. See next section
to see how to create it

```html
{{ field|placeholder:field.label }} {{ form.username|placeholder:"Your name
here"}}
```

You can extract each fields with a for loop.

```html
{% for field in form %}
```

Or by explicitly specifying the field

```html
{{form.username}}
```

---

#### Custom template tags and filters

[back to summary](#django)  
Django allows you to create customs filter for your templates
Create this folder and this file. Leave it blank.

```shell
touch app_name\templatetags\__init__.py
```

Create a python file with the name of the filter

```shell
app_name\templatetags\filter_name.py
```

Add this on top of your template

```html
{% load filter_name %}
```

To be a valid tag library, the module must contain a module-level variable named
register
that is a template.Library instance.  
Here is an exemple of filter definition.  
See the decorator? It registers your filter with your Library instance.  
You need to restart server for this to take effects.

```python
from django import template

register = template.Library()

@register.filter(name='cut')
def cut(value, arg):
   """Removes all values of arg from the given string"""
   return value.replace(arg, '')
```

Here is a link of how to make a [placeholder](https://tech.serhatteker.com/post/2021-06/placeholder-templatetags/)
custom template tag which i found essential

---

#### Setting Up User Accounts

[back to summary](#django)  
Create a "users" app. Don't forget to add app to settings.py and include the URLs
from users.  
Inside users/urls.py, add this code to include some default authentification URLs
that Django has defined.

```python
app_name = "users"
urlpatterns[
  # include default auth urls.
  path("", include("django.contribe.auth.urls"))
]
```

Basic login.html template  
Save it at save template as users/templates/registration/login.html

```html
{% if form.error %}
<p>Your username and password didn't match</p>
{% endif %}
<form method="post" action="{% url 'users:login' %}">
  {% csrf_token %} {{ form.as_p }}

  <button name="submit">Log in</button>
  <input type="hidden" name="next" value=" {% url 'app_name:index' %}" />
</form>
```

We can access to it by using

```html
<a href="{% url 'users:login' %}">Log in</a>
```

To check if user is logged in

```html
{% if user.is_authenticated %}
```

Link to logout page, and log out the user.  
Save template as users/templates/registration/logged_out.html

```html
{% url "users:logout" %}
```

Inside users/urls.py, add path to register

```python
path("register/", views.register, name="register"),
```

We write our own register() view inside users/views.py.  
For that we use UserCreationForm, a django building model.  
If method is not post, we render a blank form.  
Else, is the form pass the validity check, an user is created.  
We just have to create a registration.html template in same folder as the login
and logged_out.

```python
from django.shortcuts import render, redirect
from django.contrib.auth import login
from django.contrib.forms import UserCreationForm

def register(request):
  if request.method != "POST":
    form = UserCreationForm()
  else:
    form = UserCreationForm(data=request.POST)

    if form.is_valid():
      new_user = form.save()
      login(request, new_user)
      return redirect("app_name:index")

  context = {"form": form}
  return render(request, "registration/register.html", context)
```

---

#### Allow Users to Own Their Data

[back to summary](#django)  
Restrict access with @login_required decorator

```python
...
from django.contrib.auth.decorators import login_required
...

@login_required
def my_view(request)
  ...
```

If user is not logged in, they will be redirect to the login page.  
To make this work, you need to modify settings.py so Django knows where to find
the login page.  
Add the following at the very end.

```python
# My settings
LOGIN_URL = "users:login"
```

Add this field to your models to connect data to certain users.  
When migrating, you will be prompt to select a default value.

```python
...
from django.contrib.auth.models import User
...
owner = models.ForeignKey(User, on_delete=models.CASCADE)
```

Use this kind of code in your views to filter data of a specific user
request.user only exist when user is logged in.

```python
user_data = ExempleModel.objects.filter(owner=request.user)
```

Make sure the data belongs to the current user.  
If not the case, raise a 404.

```python
...
from django.http import Http404
...

...
if exemple_data.owner != request.user:
  raise Http404
```

Don't forget to associate user to your data in corresponding views
The "commit=false" attribute let us do that

```python
new_data = form.save(commit=false)
new_data.owner = request.user
new_data.save()
```

---

#### Paginator

[back to summary](#django)  
In app_name/views.py, import Paginator.

```python
from django.core.paginator import Paginator
```

Then, in your view, Get a list of data.

```python
exemple_list = Exemple.objects.all()
```

Set appropriate pagination

```python
paginator = Paginator(exemple_list, 5) # Show 5 items per page.
```

Get actual page number

```python
page_number = request.GET.get('page')
```

Create your Page Object, and put it in the context

```python
page_obj = paginator.get_page(page_number)
context = {
  "page_obj": page_obj,
  ...
```

The Page Object acts now like your list of data

```html
{% for item in page_obj %}
```

An exemple of what to put on the bottom of your page to navigate through Page Objects

```html
<div class="pagination">
  <span class="step-links">
    {% if page_obj.has_previous %}
    <a href="?page=1">&laquo; first</a>
    <a href="?page={{ page_obj.previous_page_number }}">previous</a>
    {% endif %}
    <span class="current">
      Page {{ page_obj.number }} of {{ page_obj.paginator.num_pages }}.
    </span>
    {% if page_obj.has_next %}
    <a href="?page={{ page_obj.next_page_number }}">next</a>
    <a href="?page={{ page_obj.paginator.num_pages }}">last &raquo;</a>
    {% endif %}
  </span>
</div>
```

---

#### Deploy to Heroku

[back to summary](#django)  
Make a [Heroku](https://heroku.com) account.  
Install Heroku [CLI](https://devcenter.heroku.com:articles/heroku-cli/).  
Install these packages

```shell
pip install psycog2 django-heroku gunicorn
```

updtate requirements.txt

```shell
pip freeze -> requirements.txt
```

At the very end of settings.py, make an Heroku ettings section.  
import django_heroku and tell django to apply django heroku settings.  
The staticfiles to false is not a viable option in production, check whitenoise
for that IMO.

```python
# Heroku settings.
import django_heroku
django_heroku.settings(locals(), staticfiles=False)
if os.environ.get('DEBUG') == "TRUE":
  DEBUG = True
  elif os.environ.get('DEBUG') == "FALSE":
  DEBUG = False
```

---

### Pygame

[back to summary](#python)

- [Pygame Project Skeleton](#pygame-project-skeleton)
- [Surfaces](#surfaces)
- [Rect](#rect)
- [Collisions](#collisions)
- [Keyboard](#keyboard)
- [Mouse](#mouse)
- [Timer](#timer)
- [Sprites](#sprites)
- [Group](#group)
- [Game state](#game-state)
- [Animation](#animation)
- [Level](#level)
- [Vectors](#vectors)
- [Camera](#camera)

---

#### Pygame Project Skeleton

Here is a good starting point of any pygame project  
[back to summary](#pygame)

```python
import pygame
import sys

SCREEN_WIDTH = 1200
SCREEN_HEIGHT = 700
FRAMERATE = 60

# Pygame init
pygame.init()
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Window title")
clock = pygame.time.Clock()

while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    screen.fill("black")

    pygame.display.update()
    clock.tick(FRAMERATE)

```

---

#### Surfaces

[back to summary](#pygame)
Everything you want to display in pygame, you have to put it on a surface.
Althougth, display is also a surface.  
Image in a surface can be plain color, rendered text or an imported image file.
Every regular surfaces needs to be put on the display surface to be visible.  
Surfaces a defined by a size (a tuple width and height)

```python

color = "red" # Color can be a color name string, Hex color string or a RGB tupple
position = (50,50) # reference point is top-left

# plain color
width = 10
height = 15
plain_color_surface = pygame.Surface((width, height))
plain_color_surface.fill(color)

# imported image. Here size is defined by image size
image_surface = pygame.image.load("image path")
image_surface.convert() # better perf with but no transparency
image_surface.convert_alpha() # same with transparency

# rendered text
string_to_render = "test string"
font_size = 50
string_font = pygame.font.Font("path to a font", font_size)
string_surf = string_font.render(string_to_render, antialias=False, color)

while True:

   # display surface
   screen.blit(plain_color_surface, position)
   screen.blit(string_surf, position)
   screen.blit(image_surface, position)

   # Check pygame.transform in documentation to scale, rotate etc...
```

---

#### Rect

[back to summary](#pygame)  

The 2 core functions of rectangles are precise positionning of surfaces and basic
collisions.  
You can get the rectangle of a surface using the get_rect() method

```python
test_rect = test_surf.get_rect(midtop=(50, 120))
```

Once you have a rect object, it has several virtual attributes which can be used
to move and align the Rect.

```text
x,y
top, left, bottom, right
topleft, bottomleft, topright, bottomright
midtop, midleft, midbottom, midright
center, centerx, centery
size, width, height
w,h
```

Examples

```python
rect1.right = 10
rect2.center = (20,30)
```

You can also use rectangles to draw. This allow you to draw plain color rectangle
without creating a surface first

```python
pygame.draw.rect(screen_surf, color, rect)
# check documentation for other shapes
```

---

#### Collisions

[back to summary](#pygame)
You can check if a rectangle collides with another with colliderect() method  
Returns 0 or 1

```python
rect1.colliderect(rect2)
```

You can chec if a point is inside a rect using collidepoint() method
Returns 0 or 1

```python
rect.collidepoint((x,y))
```

It is way most convenient to check for sprite collision.  
Using spritecollide() method

```Python
pygame.sprite.spritecollide(sprite, group, bool) # Bool to True kills the group's
                                                 # sprite when there is collision
# returns a list of collided sprites
```

---

#### Keyboard

[back to summary](#pygame)
Getting player's keyboard inputs can be achieved by two manner  
pygame.key

```python
keys = pygame.key.get_pressed()
space_key = keys[pygame.K_SPACE]
```

event loop

```python
for event in pygame.event.get()
    if event.type == pygame.KEYDOWN:
        key = event.key
```

When you I choose which one?

- Choose pygame.key inside classes
- For more general stuff, like closing the window, event loop is a better place

---

#### Mouse

[back to summary](#pygame)
Getting the mouse position can be achieved by 2 manner  
pygame.mouse:

```python
mouse_pos = pygame.mouse.get_pos()
```

event loop:

```python
for event in pygame.event.get()
    if event.type == pygame.MOUSEMOTION:
        mouse_pos = event.pos
```

Same for mouse buttons  
pygame.mouse:

```python
pygame.mouse.get_pressed()
# returns booleans of (bt1, bt2, bt3)
```

event loop:

```python
for event in pygame.event.get()
    if event.type == pygame.MOUSEBUTTONDOWN:
        mouse_button = event.button
    if event.type == pygame.MOUSEBUTTONUP:
        mouse_button = event.button
```

---

#### Timer

[back to summary](#pygame)
Timers are useful for logic and animation.  
They are created by following 3 steps:

- create a customm userevent
- trigger that event at a given interval
- add code in event loop to be execute when the timer ticks  
  You should increment timer reference value each time you create one to ot
  intefere with in-built userevent

```python
timer1 = pygame.USEREVENT + 1
timer2 = pygame.USEREVENT + 2

pygame.time.set_timer(timer1, delay)

# In game loop
for event in pygame.event.get()
    if event.type == timer1:
        # Do something
```

---

#### Sprites

[back to summary](#pygame)
Sprite class is a class that contains a surface and a rectangle with dedicated
methods.  
Just inherit from sprite class to get access to all those features.  
But to draw sprites, there is a different methodology:

- first create sprite
- place sprites in Group or GroupSingle
- draw/update all sprites in that group

```python
class Player(pygame.sprite.Sprite):
 def __init__(self):
  super().__init__()
  self.image = pygame.image.load("image path").convert_alpha()
  self.rect = self.image.get_rect(midbottom = (200, 300))

player = Player()
```

---

#### Group

[back to summary](#pygame)
2 types of groups are avaible:

- Group for multiple sprites
- GroupSingle for a single sprite  
  Notice that to check sprites collisions, sprites have to be in a different group

```python
player = pygame.sprite.GroupSingle()
player.add(Player())

mobs = pygame.sprite.Group()
mobs.add(Mob())
```

To Access to sprite object inside the group

```python
player.sprite # --> A single sprite
mobs.sprites() # --> A list of sprites
```

Empty a group

```python
mobs.empty()
```

GroupSingle and Group objects have a draw() method

```python
# In game loop
player.draw(screen)
mobs.draw(screen)
```

---

#### Game state

[back to summary](#pygame)
switching to different game states is very easy.  
We can do that by a simple if statement inside the game loop.  
Here is an exemple for a game over

```python
game_active = True

while True:
 # event loop
 #...

 if game_active:
  # game logic

 else:
  # game over logic or break to exit app

```

---

#### Animation

[back to summary](#pygame)
Animation in fact is just an image replaced by a slitly different one, fast
enough, to get the feeling that it is moving.  
All we have to do is:

- assign an image to a surface
- draw that surface
- update that surface with a new image
- erase the old surface
- draw the new surface
  This can be achieve by different manner, but the simplest is to re-draw the
  backgroung at each recursion of the game loop.

```python
player_frame1 = pygame.image.load("path/to/frame1")
player_frame2 = pygame.image.load("path/to/frame2")
player_frame3 = pygame.image.load("path/to/frame3")

player_frames = [player_frame1, player_frame2, player_frame3]
player_indice = 0

player_surf = player_frames[player_indice]
player_rect = player_surf.get_rect()


while True
 ...
 ...
 screen.blit(background_surf, background_rect)

 # Animate player
 player_indice += 0.1
 if player_indice >= len(player_frames)
  player_indice = 0
 player_surf = player_frames[int(player_indice)]

 screen.blit(player_surf, player_rect)

 ...
```

---

#### Level

[back to summary](#pygame)
The concept of making a level is based on looping through strings that we loop
through a list and display something based on which character we get.  
To keep it simple, let say we only want to display something when we get an "X".

Example of level

```python
level = [
'                       ',
'                XX     ',
'             XX        ',
'       XXXX            ',
'     XXXXXXX           ',
'XXXXXXXXXXXXXXXXXXXXXXX',
]
```

As you can see, we have here a floor and some plateforms.  
Now what we want is create a group of sprites represanting every "X" of the level.

We can say that each "X" is like a tile. Let's create that class

```python
class Tile(pygame.sprite.Sprite):
 def __init__(self, pos, size):
  super().init()
  self.image = "Whatever surface you want"
  self.rect = self.image.get_rect(topleft=pos)
```

As you can see, we have to specify a size, otherwize, our level will be pixel by
pixel and we'll not be able to see something.  
The pos argument is the coordinate we will get by looping through the level.  
All we will have to do then, is to draw every sprites.  
Let's create the level class

```python
tile_size = 64

class Level:
 def __init__(self, level, surface):
  self.display_surface = surface # will be screen actualy
  self.setup_level(level)

 def setup_level(self, level)
  self.tiles = pygame.sprite.Group()
  for row_index, row in enumerate(level):
   for col_index, cell in enumerate(row):
    if cell == "X":
     x = col_index * tile_size
     y = row_index * tile_size
     tile = Tile((x,y ), tile_size)
     self.tiles.add(tile)

 def run(self):
  self.tiles.draw(self.display_surface)
```

Just create level instance outside game loop and call the level.run() method
inside the loop. Boom! You have a level.  

Last tips:

- for screen height, you can use len(level) \* tile_size if you don't plan to
scroll verticaly
- for screen width, len(level[0]) \* tile_size

---

#### Vectors

[back to summary](#pygame)
Vector is a list with an X and a Y value. You can add a vector to coordinates to
move things.

```python
rect.center += pygame.math.Vector2(100,50)
```

---

#### Camera

[back to summary](#pygame)
You can get the feeling of a camera following the player by setting the player's
speed to 0 and move the entire level instead.  
With that, the relative speed between the level and the player is the same.

--- Work In Progress --

---

### PySimpleGUI

[back to summary](#python)

- [Indroduction](#indroduction)
- [keys](#keys)
- [Themes](#themes)

---

#### Indroduction

[back to summary](#pysimplegui)
PySimpleGUI is a easy library to make simple GUI apps.  
The core concept of this library is that the GUI is separate in rows, each row
is a list, all those is put in a layout.  
Let's get started with the basic exemple of a GUI app whith this library.

```python
import PySimpleGUI as sg

title = "Converter" # window title

layout = [
    [sg.Text("A text box"), sg.Spin(
                              ["a spin box", "That let's you", "choose an item"])],
    [sg.Text("Enter a value"), sg.Input(key="-INPUT-"),
      sg.Button("Convert", key="-BUTTON-")],
    [sg.Text("", key="-RESULT-")]
]

window = sg.Window(title, layout) # create the window object

while True:
    event, values = window.read()
    if event == sg.WIN_CLOSED:
        break
    if event == "-BUTTON-":
        entry = values["-INPUT-"] # here is how you get the value of the input box

window.close()
```

---

#### keys

[back to summary](#pysimplegui)
In the exemple above, you can see the uses of keys. Putting the key name
between 2 "-" is convention.  
Keys are useful to identify which box we refers to. For example, if you have two
buttons with "OK" text inside your app, you'll have to assign a key to at least
one of these button if you want them to act separatly (what you always want to
do in fact)

---

#### Themes

[back to summary](#pysimplegui)
Themes are a fast way to change default aspect of pySimpleGUI apps.  
Apply a theme is as simple as call the sg.theme() method before creating the window

```python
sg.theme("DarkTeal16")
```

calling

```python
sg.theme_previewer()
```

will help you choose your theme

--- Work In Progress --

---

### HTML

[Back to summary](#summary)

- [Elements](#elements)
- [Attributes](#attributes)
- [Forms](#forms)
- [Meta tags](#meta-tags)
- [lists](#lists)
- [anchor](#anchor)
- [tables](#tables)
- [events](#events)
- [web storage](#web-storage)
- [images and multimedia](#images-and-multimedia)
- [canvas and webGL](#canvas-and-webgl)
- [Workers](#workers)
- [Semantic HTML](#semantic-html)

---

#### Elements

[Back to summary](#html)  
html elements are created using tags.  
see [HTML elements reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)

---

#### Attributes

[Back to summary](#html)  
Elements in HTML have attributes; these are additional values that configure the
elements or adjust their behavior in various ways to meet the criteria the users
want.  
see [HTML attributes reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes)

---

#### Forms

[Back to summary](#html)  
The form HTML element represents a document section containing interactive
controls for submitting information.  
It is possible to use the :valid and :invalid CSS pseudo-classes to style a form
element based on whether or not the elements inside the form are valid.  
[forms attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Form#:~:text=HTMLFormElement-,Attributes,-This%20element%20includes)

---

#### Meta tags

[Back to summary](#html)  
The meta HTML element represents metadata that cannot be represented by other HTML
meta-related elements, like base, link, script, style or title.  
Metadata is data (information) about data.  
meta tags always go inside the head element, and are typically used to specify
character set, page description, keywords, author of the document, and viewport
settings.  
Metadata is used by browsers (how to display content or reload page), search
engines (keywords), and other web services.  
[meta attributes](https://www.w3schools.com/tags/tag_meta.asp#:~:text=Yes-,Attributes,-Attribute)

---

#### lists

[Back to summary](#html)  
HTML lists allow web developers to group a set of related items in lists.
2 types, ordered list or unordered list

```html
<ol>
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ol>
<ul>
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ul>
```

A last type exists, description list, which works aroud a list of terms and
description of those terms

```html
<dl>
  <dt>Coffee</dt>
  <dd>- black hot drink</dd>
  <dt>Milk</dt>
  <dd>- white cold drink</dd>
</dl>
```

---

#### anchor

[Back to summary](#html)  
The a HTML element (or anchor element), with its href attribute, creates a
hyperlink to web pages, files, email addresses, locations in the same page, or
anything else a URL can address.  
Content within each "a" should indicate the link's destination. If the href
attribute is present, pressing the enter key while focused on the "a" element will
activate it.  
[anchor attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#:~:text=Try%20it-,Attributes,-This%20element%27s%20attributes)
[examples](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#:~:text=HTMLAnchorElement-,Examples,-Linking%20to%20an)

---

#### tables

[Back to summary](#html)  

The table HTML element represents tabular data — that is, information presented
in a two-dimensional table comprised of rows and columns of cells containing data.

[list of table tags](https://www.w3schools.com/html/html_tables.asp#:~:text=HTML-,Table,-Tags)
[table attributes](https://www.scaler.com/topics/html/table-attributes-in-html/#:~:text=Table%20Attributes%20in-,HTML,-Learn%20about%20table)

example

```html
<table>
  <tr>
    <th>Person 1</th>
    <th>Person 2</th>
    <th>Person 3</th>
  </tr>
  <tr>
    <td>Emil</td>
    <td>Tobias</td>
    <td>Linus</td>
  </tr>
  <tr>
    <td>16</td>
    <td>14</td>
    <td>10</td>
  </tr>
</table>
```

---

#### events

[Back to summary](#html)  
HTML has the ability to let events trigger actions in a browser, like starting a
JavaScript when a user clicks on an element.
[list](https://www.w3schools.com/tags/ref_eventattributes.asp#:~:text=%3Cwbr%3E-,HTML,-Event%20Attributes)

---

#### web storage

[Back to summary](#html)  
The Web Storage API provides mechanisms by which browsers can store key/value
pairs, in a much more intuitive fashion than using cookies.
The two mechanisms within Web Storage are as follows:

- sessionStorage maintains a separate storage area for each given origin that's
- available for the duration of the page session (as long as the browser is open,
- including page reloads and restores)
  - Stores data only for a session, meaning that the data is stored until the
  browser (or tab) is closed.
  - Data is never transferred to the server.
  - Storage limit is larger than a cookie (at most 5MB).
- localStorage does the same thing, but persists even when the browser is closed
  and reopened.
  - stores data with no expiration date, and gets cleared only through JavaScript,
  or clearing the Browser cache / Locally Stored Data.
  - Storage limit is the maximum amongst the two.

The Web Storage API extends the Window object with two new properties
— Window.sessionStorage and Window.localStorage — which provide access to the
current domain's session and local Storage objects respectively, and a storage
event handler that fires when a storage area changes (e.g. a new item is stored.)

The StorageEvent is fired on a document's Window object when a storage area changes.

---

#### Images and multimedia

[Back to summary](#html)

---

##### images

The img HTML element embeds an image into the document.  
The src attribute is required, and contains the path to the image you want to
embed.  
The alt attribute holds a text description of the image, which isn't mandatory
but is incredibly useful for accessibility — screen readers read this description
out to their users so they know what the image means. Alt text is also displayed
on the page if the image can't be loaded for some reason: for example, network
errors, content blocking, or linkrot.  
images can be annoted using figure tag.  
[images attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Img#:~:text=user%20agent.-,Attributes,-This%20element%20includes)
[use of the srcset attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Img#:~:text=Using%20the%20srcset%20attribute)

---

##### audio

The audio HTML element is used to embed sound content in documents. It may contain
one or more audio sources, represented using the src attribute or the source
element: the browser will choose the most suitable one. It can also be the
destination for streamed media, using a MediaStream.  
The content inside the opening and closing audio tags is shown as a fallback in
browsers that don't support the element.  
[audio attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio#:~:text=support%20the%20element.-,Attributes,-This%20element%27s%20attributes)

---

##### video

The video HTML element embeds a media player which supports video playback into
the document. You can use video for audio content as well, but the audio element
may provide a more appropriate user experience.  
The content inside the opening and closing video tags is shown as a fallback in
browsers that don't support the element.  
[video attributes](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video#:~:text=support%20the%20element.-,Attributes,-Like%20all%20other)

---

#### canvas and webGL

[Back to summary](#html)  
WebGL (Web Graphics Library) is a JavaScript API for rendering high-performance
interactive 3D and 2D graphics within any compatible web browser without the use
of plug-ins. WebGL does so by introducing an API that closely conforms to OpenGL
ES 2.0 that can be used in HTML5 canvas elements. This conformance makes it
possible for the API to take advantage of hardware graphics acceleration provided
by the user's device.  
[webGL MDN link](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API)

---

#### Workers

[Back to summary](#html)  
Web Workers are a simple means for web content to run scripts in background
threads.  
A worker is an object created using a constructor that runs a named JavaScript
file. This file contains the code that will run in the worker thread; workers run
in another global context that is different from the current window. Thus, using
the window shortcut to get the current global scope (instead of self) within a
Worker will return an error.  
The worker context is represented by a DedicatedWorkerGlobalScope object in the
case of dedicated workers (standard workers that are utilized by a single script;
shared workers use SharedWorkerGlobalScope). A dedicated worker is only accessible
from the script that first spawned it, whereas shared workers can be accessed from
multiple scripts.  
[more details](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers)

---

#### Semantic HTML

[Back to summary](#html)  
Some of the benefits from writing semantic markup are as follows:

- Search engines will consider its contents as important keywords to influence the
page's search rankings
- Screen readers can use it as a signpost to help visually impaired users navigate
a page
- Finding blocks of meaningful code is significantly easier than searching through
endless divs with or without semantic or namespaced classes
- Suggests to the developer the type of data that will be populated
- Semantic naming mirrors proper custom element/component naming

with and without semantic comparison  
![comparison](https://miro.medium.com/max/1024/1*GgI7FvfCwqSpHgn_VgGEXQ.jpeg)
[list of semantic elements](https://developer.mozilla.org/fr/docs/Glossary/Semantics#:~:text=la%20t%C3%A2che%20recherch%C3%A9e.-,Les%20%C3%A9l%C3%A9ments%20s%C3%A9mantiques,-Ce%20sont%20quelques)

---

### CSS

[Back to summary](#summary)

- [selectors](#selectors)
- [pseudo selectors](#pseudo-selectors)
- [specificity and inheritance](#specificity-and-inheritance)
- [box model](#box-model)
- [typography](#typography)
- [positionning units display](#positionning-units-display)
- [layout flex grid](#layout-flex-grid)
- [shadows](#shadows)
- [colors gradients](#colors-gradients)
- [transform and transitions](#transform-and-transitions)
- [animations](#animations)
- [media queries](#media-queries)
- [css variable](#css-variable)

---

#### selectors

[Back to summary](#css)

```text
universal selector
*   will match all the elements of the document

type selector
elementname will match all element of type element name (ex: input, div, etc...)

class selector
.classname will match any elements that has a class of "classname"

id selector
#idname  will match the element that has the id "idname"

Attribute selector
[attr]  will    match all elements that have the "attr" attribute
[attr="value"]  match every elements where attr's value equals to value
[attr~="value"] match any elements where attr's value contains value. word-break
                wildcard
[attr|="value"] match if attr's value is completely equal to value or starting with
                value a directely followed by a -
[attr^="value"] match if attr's value starts with value
[attr$="value"] match if attr's value ends with value
[attr*="value"] match any elements where attr's value contains value. dumb wildcard
```

- The , selector is a grouping method that selects all the matching nodes.
Syntax: A, B Example: div, span will match both span and div elements.
- The " " (space) combinator selects nodes that are descendants of the first
element. Syntax: A B Example: div span will match all span elements that are
inside a div element.
- The > combinator selects nodes that are direct children of the first element.
Syntax: A > B Example: ul > li will match all li elements that are nested directly
inside a ul element.
- The ~ combinator selects siblings. This means that the second element follows
the first (though not necessarily immediately), and both share the same parent.
Syntax: A ~ B Example: p ~ span will match all span elements that follow a p,
immediately or not.
- The + combinator matches the second element only if it immediately follows the
first element. Syntax: A + B Example: h2 + p will match the first p element that
immediately follow an h2 element.
- The || combinator selects nodes which belong to a column. Syntax: A || B
Example: col || td will match all td elements that belong to the scope of the col.

---

#### pseudo selectors

[Back to summary](#css)

- The : pseudo allow the selection of elements based on state information that
is not contained in the document tree. Example: a:visited will match all "a"
elements that have been visited by the user. [list here](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes#:~:text=Pseudo%2D-,classes,-A%20CSS%20pseudo)
- The :: pseudo represent entities that are not included in HTML.
Example: p::first-line will match the first line of all "p" elements. [list here](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements#:~:text=original%20pseudo%2Delements.-,Index,-Pseudo%2Delements%20defined)

---

#### specificity and inheritance

[Back to summary](#css)  
Specificity is the algorithm used by browsers to determine the CSS declaration
that is the most relevant to an element, which in turn, determines the property
value to apply to the element.  
The specificity algorithm is basically a three-column value of three categories
or weights. The highest value is the more specific one

```text
 ID  CLASS  TYPE
    count  count  count

Example
:root #myApp input:required {
  color: blue;
}

weight: 102 because one id, no class and two types were given

```

---

#### box model

[Back to summary](#css)  
![box model](https://miro.medium.com/max/408/1*sKnLrT1TtqWDZg7GWoBCow.png)

---

#### typography

[Back to summary](#css)  
use [font-face](https://developer.mozilla.org/en-US/docs/Web/CSS/@font-face)
rule to import font.  
![emotions](https://miro.medium.com/max/1400/1*rb-xgrNgv7KN6xQKMH4DUQ.jpeg)
![shorthand](https://i.stack.imgur.com/OhU4S.jpg)

---

#### positionning units display

[Back to summary](#css)  
![units](https://miro.medium.com/max/880/1*XNT_kayVk-qYMQuN4BwhxA.png)
![position](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRBinLUOGA_pa6giMrLvAWiakIKJ0hUR0B9rA&usqp=CAU)
![display](https://s1.o7planning.com/fr/12049/images/23177296.png)
![float](https://www.tutorialbrain.com/wp-content/uploads/2019/03/css-float-left-right.jpg)

---

#### layout flex grid

[Back to summary](#css)  
![grid](https://res.cloudinary.com/practicaldev/image/fetch/s--X30jomsg--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://github.com/simonpaix/images/blob/main/blog/LearnPine_Grid_CheatSheet.png%3Fraw%3Dtrue)
![flex](https://i.redd.it/vd9dc7wfk9471.png)

---

#### shadows

[Back to summary](#css)  
![box](https://pbs.twimg.com/media/E-2ml4HWQAEtRXK.jpg:large)
![text](https://i7x7p5b7.stackpathcdn.com/codrops/wp-content/uploads/2014/12/text-shadow-syntax-img1.png)

---

#### colors gradients

[Back to summary](#css)  
[color gradient genetator](https://mycolor.space/gradient)

---

#### transform and transitions

[Back to summary](#css)  
![transform](https://i.pinimg.com/736x/9c/63/97/9c63971fc22015ef0616c3773393ea91.jpg)
![transition](https://1stwebdesigner.com/wp-content/uploads/2019/06/css-animation-cheat-sheets-04.png)

---

#### animations

[Back to summary](#css)

---

#### media queries

[Back to summary](#css)  
![dimentions](https://i.pinimg.com/originals/74/71/f1/7471f15602f673c1c58b235e11439e1e.png)
![syntax](https://res.cloudinary.com/practicaldev/image/fetch/s--ooUgUDOt--/c_imagga_scale,f_auto,fl_progressive,h_420,q_auto,w_1000/https://dev-to-uploads.s3.amazonaws.com/i/djb6eg9dtsbphc83q0ic.png)

---

#### css variable

[Back to summary](#css)  
CSS variables are an extremely useful feature and they enable us to do things we
were compensating with SASS. They are defined by the CSS authors and contain a
specific values that can be reused wherever needed within our project. They use
a custom notation and are accessed by using the var function.

---

##### Declaration

A CSS variable can be declared on any element, and we declare one like so:

```css
:root {
  --primary-color: #fff;
  --primary-padding: 1rem;
}
```

They are accessed by using the var function:

```css
div {
  color: var(--primary-color);
}
```

---

##### Dymamic usage

CSS variables can be accessed from the JavaScript dynamically. We can get or set
its value like for any other property:

```javascript
const el = document.querySelector(":root");

// get the value
const padding = el.style.getPropertyValue("--primary-padding");

// set the value
el.style.setProperty("--primary-padding", "3rem");
```

---

## Javascript

[Back to summary](#summary)

- [operators and type conversions](#operators-and-type-conversions)
- [closure](#closure)
- [functions and arrow functions](#functions-and-arrow-functions)
- [timeout and interval](#timeout-and-interval)
- [classes and proxies](#classes-and-proxies)
- [prototype](#prototype)
- [iterators and iterables](#iterators-and-iterables)
- [destructuring and spread](#destructuring-and-spread)
- [callbacks and promise](#callbacks-and-promise)
- [async await](#async-await)
- [ES6 syntaxes](#es6-syntaxes)
- [Working With Array](#working-with-array)
- [Working With Strings](#working-with-strings)
- [Working With Objects](#working-with-objects)
- [Loops](#loops)
- [Modules](#modules)
- [Node JS](#nodejs)
- [Tests](#tests)
- [ExpressJS](#expressjs)
- [EJS](#ejs)

---

### operators and type conversions

[Back to summary](#javascript)

#### arithmetic operators

| operator |            action            |
| :------: | :--------------------------: |
|    +     |           Addition           |
|    -     |         Subtraction          |
|    \*    |        Multiplication        |
|   \*\*   |   Exponentiation (ES2016)    |
|    /     |           Division           |
|    %     | Modulus (Division Remainder) |
|    ++    |          Increment           |
|    --    |          Decrement           |

---

#### asignement operators

| Operator |  Example  |   Same As    |
| :------: | :-------: | :----------: |
|    =     |   x = y   |    x = y     |
|    +=    |  x += y   |  x = x + y   |
|    -=    |  x -= y   |  x = x - y   |
|   \*=    |  x \*= y  |  x = x \* y  |
|    /=    |  x /= y   |  x = x / y   |
|    %=    |  x %= y   |  x = x % y   |
|  \*\*=   | x \*\*= y | x = x \*\* y |

---

#### comparison operators

| Operator |            Description            |
| :------: | :-------------------------------: |
|    ==    |             equal to              |
|   ===    |    equal value and equal type     |
|    !=    |             not equal             |
|   !==    | not equal value or not equal type |
|    >     |           greater than            |
|    <     |             less than             |
|    >=    |     greater than or equal to      |
|    <=    |       less than or equal to       |
|    ?     |         ternary operator          |

---

#### Logical Operators

| Operator | Description |
| :------: | :---------: |
|    &&    | logical and |
|   \|\|   | logical or  |
|    !     | logical not |

---

#### bitwise operators

| Operator |     Description      | Example |   Same as    | Result | Decimal |
| :------: | :------------------: | :-----: | :----------: | :----: | :-----: |
|    &     |         AND          |  5 & 1  | 0101 & 0001  |  0001  |    1    |
|    \|    |          OR          | 5 \| 1  | 0101 \| 0001 |  0101  |    5    |
|    ~     |         NOT          |   ~ 5   |    ~0101     |  1010  |   10    |
|    ^     |         XOR          |  5 ^ 1  | 0101 ^ 0001  |  0100  |    4    |
|    <<    |      left shift      | 5 << 1  |  0101 << 1   |  1010  |   10    |
|    >>    |     right shift      | 5 >> 1  |  0101 >> 1   |  0010  |    2    |
|   >>>    | unsigned right shift | 5 >>> 1 |  0101 >>> 1  |  0010  |    2    |

---

### closure

[Back to summary](#javascript)
A closure is a feature in JavaScript where an inner function has access to the
outer (enclosing) function’s variables (a scope chain).  
The closure has three scope chain: - it own scope - outer function scope - global
scope
Here is a simple example were you can litteraly see the closure

```javascript
function outer() {
   var b = 10;
   function inner() {

         var a = 20;
         console.log(a+b);
    }
   console.dir(inner);
}

>>> outer()
```

This will return an interactive list of the properties of the outer function that
is basicaly a JavaScript object.
You can see now in the scope part that there is a "Closure" key, and inside it you
will see all the variables of the outer function, so b assigned to 10 in this
exemple.  
Follow [this link](https://medium.com/@dis_is_patrick/practical-uses-for-closures-c65640ae7304)
to see some practical uses for closures.

---

### functions and arrow functions

[Back to summary](#javascript)

#### regular functions

```javascript
// Function declaration
function greet(who) {
  return `Hello, ${who}!`;
}

// Function expression
const greet = function (who) {
  return `Hello, ${who}!`;
};
```

Inside of a regular JavaScript function, this value (aka the execution context)
is dynamic.  
The dynamic context means that the value of this depends on how the function is
invoked. In JavaScript, there are 4 ways you can invoke a regular function.

- During a simple invocation the value of this equals to the global object (or
undefined if the function runs in strict mode)
- During a method invocation the value of this is the object owning the method
- During an indirect invocation using myFunc.call(thisVal, arg1, ..., argN) or
myFunc.apply(thisVal, [arg1, ..., argN]) the value of this equals to the first argument
- During a constructor invocation using new keyword this equals to the newly
created instance

Inside the body of a regular function, "arguments" is a special array-like object
containing the list of arguments with which the function has been invoked.  
If the return statement is missing, or there's no expression after return
statement, the regular function implicitely returns undefined.  
The regular functions are the usual way to define methods on classes.

---

#### arrow functions

```javascript
const greet = (who) => {
  return `Hello, ${who}!`;
};
```

No matter how or where being executed, this value inside of an arrow function
always equals this value from the outer function.  
No arguments special keyword is defined inside an arrow function, use the rest
parameters like "...args" in the function expression instead.  
If the arrow function contains one expression, and you omit the function's curly
braces, then the expression is implicitly returned.  
In contrast with regular functions, the method defined using an arrow binds this
lexically to the class instance.

---

### timeout and interval

[Back to summary](#javascript)

```javascript
function myCallback(a, b) {
  // Your code here
  // Parameters are purely optional.
  console.log(a);
  console.log(b);
}

let intervalID = setInterval(myCallback, 500, "Parameter 1", "Parameter 2");
clearInterval(intervalID);

let timeoutID = setTimeout(myCallback, 500, "Parameter 1", "Parameter 2");
clearTimeout(timeoutID);
```

---

### classes and proxies

[Back to summary](#javascript)
An important difference between function declarations and class declarations is
that while functions can be called in code that appears before they are defined,
classes must be defined before they can be constructed.  
Classes are a template for creating objects. They encapsulate data with code to
work on that data. Classes in JS are built on prototypes but also have some syntax
and semantics that are not shared with ES5 class-like semantics.

```javascript
// Class declarations
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}

// Class expression
// unnamed
let Rectangle = class {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
console.log(Rectangle.name);
// output: "Rectangle"

// named
let Rectangle = class Rectangle2 {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
console.log(Rectangle.name);
// output: "Rectangle2"
```

Methods can be defined by two manner

```javascript
function Hero(name, level) {
  this.name = name;
  this.level = level;
}

// Adding a method to the constructor
Hero.prototype.greet = function () {
  return `${this.name} says hello.`;
};

class Hero {
  constructor(name, level) {
    this.name = name;
    this.level = level;
  }

  // Adding a method to the constructor
  greet() {
    return `${this.name} says hello.`;
  }
}
```

Class methods are in reality added to the prototype.

```javascript
Hero {name: "Varg", level: 1}
__proto__:
  ▶ constructor: class Hero
  ▶ greet: ƒ greet()
```

To inherit from a parent class, use extends.

```javascript
// Creating a new class from the parent
class Mage extends Hero {
 constructor(name, level, spell) {
  // Chain constructor with super
  super(name, level);

  // Add a new property
  this.spell = spell;
 }
}

const hero2 = new Mage('Lejon', 2, 'Magic Missile');

Output
Mage {name: "Lejon", level: 2, spell: "Magic Missile"}
__proto__: Hero // See how proto is related to parent class
    ▶ constructor: class Mage
```

---

### prototype

[Back to summary](#javascript)

---

### iterators and iterables

[Back to summary](#javascript)

---

### destructuring and spread

[Back to summary](#javascript)

---

### callbacks and promise

[Back to summary](#javascript)

---

### async await

[Back to summary](#javascript)

---

### ES6 syntaxes

[Back to summary](#javascript)

---

### Working With Array

[Back to summary](#javascript)

#### reduce()

The reduce() method executes a user-supplied "reducer" callback function on each
element of the array, in order, passing in the return value from the calculation
on the preceding element. The final result of running the reducer across all
elements of the array is a single value.

```javascript
function find_average(array) {
  //   acc is accumulator and curr is current value being processed
  //   0 is the initial value of the accumulator
  return (
    array.reduce((acc, curr) => {
      return acc + curr;
    }, 0) / array.length
  );
}
```

---

#### reverse()

The reverse() METHOD reverses an array in place. The first array element becomes
the last, and the last array element becomes the first.

```javascript
const array1 = ["one", "two", "three"];
console.log("array1:", array1);
// expected output: "array1:" Array ["one", "two", "three"]

// Careful: reverse is destructive -- it changes the original array.
array1.reverse();
console.log("array1:", array1);
// expected output: "array1:" Array ["three", "two", "one"]
```

---

#### join()

The join() METHOD creates and returns a new string by concatenating all of the
elements in an array (or an array-like object), separated by commas or a specified
separator string. If the array has only one item, then that item will be returned
without using the separator.

```javascript
console.log(elements.join());
// expected output: "Fire,Air,Water"

console.log(elements.join(""));
// expected output: "FireAirWater"

console.log(elements.join("-"));
// expected output: "Fire-Air-Water"
```

---

#### map()

The map() METHOD creates a new array populated with the results of calling a
provided function on every element in the calling array.

```javascript
// Exemples
// Return a new array with the square root of all element values:
const numbers = [4, 9, 16, 25];
const newArr = numbers.map(Math.sqrt)
// [2, 3, 4, 5]

// Multiply all the values in an array with 10:
const numbers = [65, 44, 12, 4];
const newArr = numbers.map(myFunction)

function myFunction(num) {
  return num * 10;
}

// Convert array of strings to an array of numbers
["1", "2", "3"].map((str) => parseInt(str)));
```

---

#### entries()

The entries() method returns an object of type Array Iterator which contains the
couple Key/value for each elements of the array

```javascript
const array1 = ["a", "b", "c"];

const iterator1 = array1.entries();

console.log(iterator1.next().value);
// expected output: Array [0, "a"]

console.log(iterator1.next().value);
// expected output: Array [1, "b"]
```

---

#### Utility Functions

##### some

Parameters:

- predicate - Function that returns true or false.
- array - List of items to test.  
  Description:
- If predicate returns true for any item, some returns true. Otherwise it
returns false.

```javascript
const some = (predicate, array) => {
  array.reduce((acc, value) => {
    acc || predicate(value);
  }, false);
};
```

---

##### all

Parameters:

- predicate - Function that returns true or false.
- array - List of items to test.  
  Description:
- If predicate returns true for every item, all returns true. Otherwise it returns
false.

```javascript
const all = (predicate, array) => {
  array.reduce((acc, value) => {
    acc && predicate(value);
  }, true);
};
```

---

##### none

Parameters:

- predicate - Function that returns true or false.
- array - List of items to test.
  Description:
- If predicate returns false for every item, none returns true. Otherwise it
returns false.

```javascript
const none = (predicate, array) => {
  array.reduce((acc, value) => {
    !acc && !predicate(value);
  }, false);
};
```

---

##### filter

Parameters:

- predicate - Function that returns true or false.
- array - List of items to filter.
  Description:
- Returns a new array. If predicate returns true, that item is added to the new
array. Otherwise that item is excluded from the new array.

```javascript
const filter = (predicate, array) =>
  array.reduce((newArray, item) => {
    if (predicate(item) === true) {
      newArray.push(item);
    }

    return newArray;
  }, []);
```

---

##### reject

Parameters:

- predicate - Function that returns true or false.
- array - List of items to filter.
  Description:
- Just like filter, but with the opposite behavior.
  -If predicate returns false, that item is added to the new array. Otherwise
  that item is excluded from the new array.

```javascript
const reject = (predicate, array) =>
  array.reduce((newArray, item) => {
    if (predicate(item) === false) {
      newArray.push(item);
    }

    return newArray;
  }, []);
```

---

##### find

Parameters:

- predicate - Function that returns true or false.
- array - List of items to search.
  Description:
- Returns the first element that matches the given predicate. If no element
matches then undefined is returned.

```javascript
const find = (predicate, array) =>
  array.reduce((result, item) => {
    if (result !== undefined) {
      return result;
    }

    if (predicate(item) === true) {
      return item;
    }

    return undefined;
  }, undefined);
```

---

#### partition

Parameters:
-predicate - Function that returns true or false.
-array - List of items.
Description:

- "Partitions" or splits an array into two based on the predicate. If predicate
returns true, the item goes into list 1. Otherwise the item goes into list 2.

```javascript
const partition = (predicate, array) =>
  array.reduce(
    (result, item) => {
      const [list1, list2] = result;

      if (predicate(item) === true) {
        list1.push(item);
      } else {
        list2.push(item);
      }

      return result;
    },
    [[], []]
  );
```

---

#### pluck

Parameters

- key - Key name to pluck from the object
- array - List of items.
  Description
- Plucks the given key off of each item in the array. Returns a new array of
these values.

```javascript
const pluck = (key, array) =>
  array.reduce((values, current) => {
    values.push(current[key]);

    return values;
  }, []);

// Examples
pluck("name", [{ name: "Batman" }, { name: "Robin" }, { name: "Joker" }]);
// ['Batman', 'Robin', 'Joker']

pluck(0, [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
]);
// [1, 4, 7]
```

---

#### scan

Parameters

- reducer - Standard reducer function that receives two parameters - the
accumulator and current element from the array.
- initialValue - The initial value for the accumulator.
- array - List of items.
  Description
- Works just like reduce but instead just the single result, it returns a list of
every reduced value on the way to the single result.

```javascript
const scan = (reducer, initialValue, array) => {
  const reducedValues = [];

  array.reduce((acc, current) => {
    const newAcc = reducer(acc, current);

    reducedValues.push(newAcc);

    return newAcc;
  }, initialValue);

  return reducedValues;
};

// Examples
const add = (x, y) => x + y;
const multiply = (x, y) => x * y;

scan(add, 0, [1, 2, 3, 4, 5, 6]);
// [1, 3, 6, 10, 15, 21] - Every number added from 1-6

scan(multiply, 1, [1, 2, 3, 4, 5, 6]);
// [1, 2, 6, 24, 120, 720] - Every number multiplied from 1-6
```

---

### Working With Strings

[Back to summary](#javascript)

#### split()

The split() method divides a String into an ordered list of substrings, puts
these substrings into an array, and returns the array.

```javascript
const str = "The quick brown fox jumps over the lazy dog.";

const words = str.split(" ");
console.log(words[3]);
// expected output: "fox"

const chars = str.split("");
console.log(chars[8]);
// expected output: "k"

const strCopy = str.split();
console.log(strCopy);
// expected output: Array ["The quick brown fox jumps over the lazy dog."]
```

---

#### substring()

The substring() method returns the part of the string between the start and end
indexes, or to the end of the string.

```javascript
const str = "Google";

console.log(str.substring(1, 3));
// expected output: "oo"
```

---

### Working With Objects

[Back to summary](#javascript)

#### 3 ways to loop through objects

Get an Array of keys

```javascript
const courses = {
  java: 10,
  javascript: 55,
  nodejs: 5,
  php: 15,
};

const keys = Object.keys(courses);
// [ 'java', 'javascript', 'nodejs', 'php' ]
```

---

Get an Array of values

```javascript
const animals = {
  tiger: 1,
  cat: 2,
  monkey: 3,
  elephant: 4,
};
Object.values(animals);
// [1, 2, 3, 4]
```

---

Get an Array of [Key / Value] pairs

```javascript
const animals = {
  tiger: 1,
  cat: 2,
  monkey: 3,
  elephant: 4,
};

Object.entries(animals);
//[[ 'tiger', 1 ], [ 'cat', 2 ], [ 'monkey', 3 ], [ 'elephant', 4 ]]

// Also works with arrays
const array1 = ["one", "two", "three"];

Object.entries(array1);
// [["0", "one"], ["1", "two"], ["2", "three"]]
```

---

### Loops

[Back to summary](#javascript)

JavaScript supports different kinds of loops:

- for - loops through a block of code a number of times
- for/in - loops through the properties of an object
- for/of - loops through the values of an iterable object
- while - loops through a block of code while a specified condition is true
- do/while - also loops through a block of code while a specified condition is true

---

#### for

Basic for loop

```javascript
for (let i = 0; i < 5; i++) {
  // Executed 5 times
  // At each excecution, i is incremented by 1
  ...
}
```

---

#### for ... in

Loops through enumerable properties of a given object

```javascript
let myArray = ["a", "b", "c"];
let myObject = {
  a: "one",
  b: "two",
  c: "three",
};

for (index in myArray) {
  console.log(index);
  // 0
  // 1
  // 2
}

for (key in myObject) {
  console.log(key);
  // a
  // b
  // c
}
```

---

#### for ... of

Loops through values of an array

```javascript
let myArray = ["a", "b", "c"];

for (let value of myArray) {
  console.log(value);
  // "a"
  // "b"
  // "c"
}
```

---

#### forEach

The forEach() method executes a provided function once for each array element.

```javascript
const array1 = ["a", "b", "c"];

array1.forEach((element) => console.log(element));

// expected output: "a"
// expected output: "b"
// expected output: "c"
```

---

#### while

Basic while loop, loops whenever the condition is true

```javascript
let n = 0;
let x = 0;
while (n < 3) {
  n++;
  x += n;
}
```

---

#### do ... while

Same as while loop but because the condition is tested after the instruction, it
will be executed at least one time.

```javascript
let i = 0;
do {
  i += 1;
  console.log(i);
} while (i < 5);
```

---

### Modules

[Back to summary](#javascript)
Modules are js file. You can import the entire module or just some objects inside
you current script.  
There are different kinds of importing methods, depending on what you want to do
and due to new ES6 import method.

---

#### ES5 method

first create a module to import

```javascript
// myModule.js

function doThings() {
  console.log("doing stuffs");
}

function doAnotherThings() {
  console.log("doing another stuffs");
}

exports.doThings = doThings;
exports.doAnotherThings = doAnotherThings;

// or

module.exports = {
  doThings,
  doAnotherThings,
};

// note that if your module exports only one things, it is handy to do so:

module.exports = thingToExport;
```

Then we can import those functions

```javascript
const myModule = require("./myModule");

myModule.doThings();
myModule.doAnotherThings();

// or

const { doThings, doAnotherThings } = require("./myModule");

doThings();
doAnotherThings();
```

---

#### ES6 method

One important thing about ES6 method is that module and script have to be in .mjs
extension or add <"type": "module"> in your package.json.  
Again, create a module to import. We can specify a default export which will be
imported if nothing's specified. Note that we specify export when declaring objects.

```javascript
// myModule.mjs

export function doThings() {
  console.log("doing stuffs");
}

export function doAnotherThings() {
  console.log("doing another stuffs");
}

export default () => console.log("default");
```

And now we can import the module

```javascript
// We can import default

import myDefaultFunction from "./myModule.mjs";

myDefaultFunction(); // default

// or we can import all

import * as myModule from "./module.mjs";

myModule.doThings();
myModule.doAnotherThings();
myModule.default(); // because we didn't specify a name in the import statement,
                    // the name is default, which makes sense

// or a selective import

import { doThings, default as new_name } from "./module.mjs";

doThings();
new_name();
```

---

### nodeJS

[Back to summary](#javascript)
Init node to create package.json

```shell
npm init
npm init -y (validate every default fields)
```

Install external node module for your project

```shell
npm install package_name
```

Install external node module to your system

```shell
npm install -g package_name
```

---

### Tests

[Back to summary](#javascript)
We can test node apps using Assert and Mocha  
First require assert in your test file, for exemple, index.test.js

```javascript
const assert = require("assert").strict;
// strict property alows us to use specials equalities tests recommended by node
```

Next change "test" value like this in package.json

```json
...
"scripts": {
    "test": "mocha index.test.js"
},
...
```

We can mow write a test in our test file

```javascript
describe("Test group name", function () {
  // We "describe" a test group
  it("should give a given result", function () {
    // Be descriptive in your tests name
    // some code
  });

  it("should do a specific thing", function () {
    // Be descriptive in your tests name
    // some code
  });
});

describe("An other test group name", function () {
  // We "describe" an other test group
  it("should give a given result", function () {
    // Be descriptive in your tests name
    // some code
  });

  it("should do a specific thing", function () {
    // Be descriptive in your tests name
    // some code
  });
});
```

In your test code you can use for exemple

```javascript
// Check equality
assert.strictEqual(content, expectedFileContents);

// Check inequality
assert.notStrictEqual(content, expectedFileContents);

// Throw error
assert.throws(fn, error, message);
/*
fn <Function> 
error <RegExp> | <Function> | <Object> | <Error>
message <string>

Expects the function fn to throw an error.
error and message are optional
*/
```

To run the test

```shell
npm test
```

Output if test pass

```shell
> todos@1.0.0 test your_file_path/your_app
> mocha index.test.js



Test group name
    ✓ should give a given result
    ✓ should do a specific thing

An other test group name
    ✓ should give a given result
    ✓ should do a specific thing

  3 passing (36ms)
```

For async code, better use async / await with mocha, less code and more readable

```javascript
...
describe("saveToFile()", function() {
    it("should save a single TODO", async function() {
        let todos = new Todos();
        todos.add("save a CSV");
        await todos.saveToFile();

        assert.strictEqual(fs.existsSync('todos.csv'), true);
        let expectedFileContents = "Title,Completed\nsave a CSV,false\n";
        let content = fs.readFileSync("todos.csv").toString();
        assert.strictEqual(content, expectedFileContents);
    });
});
```

---

Hooks also exists

- before This hook is executed BEFORE the FIRST test
- beforeEach This hook is executed BEFORE EACH case tests
- after This hook is executed AFTER the last case test
- afterEach This hook isexecuted AFTER EACH tests

```javascript
describe("saveToFile()", function() {
    beforeEach(function () {
     // We create a todo and add a value to it before each case tests
        this.todos = new Todos();
        this.todos.add("save a CSV");
    });

    afterEach(function () {
     // After each case tests, if a todos.csv file exists, we delete it
        if (fs.existsSync("todos.csv")) {
            fs.unlinkSync("todos.csv");
        }
    });
});
```

Awesome, our tests are automated and organized, easy to run, easy to maintain

---

### expressJS

[Back to summary](#javascript)  
Install express

```shell
npm install express
```

Install BODY-PARSER for forms management

```shell
npm i body-parser
```

Install EJS for templating

```shell
npm install ejs
```

Install NODEMON to autorefresh server at any modification

```shell
npm install -g nodemon
```

Web app boiler plate

```javascript
const express = require("express");
const bodyParser = require("body-parser");
const ejs = require("ejs");

// #### App settup ####
const app = express();
app.set("view engine", "ejs"); // Tell express to use ejs rendering engine

app.use(bodyParser.urlencoded({ extended: true }));
app.use(express.static("public")); // Serves statics files in root/public folder

// #### Routes ####
// Home
app.get("/", (req, res) => {
  someInfoVar = "Some info";
  context = {
    someInfo: someInfoVar, // In template, access this value with someInfo key
  };
  res.render(__dirname + "/views/home.ejs", context);
});

// #### Port Listening ####
const PORT = process.env.PORT || 3000;
app.listen(PORT, function () {
  console.log(`Server started on port ${PORT}`);
});
```

Work with API in node using axios

```javascript
// Install axios package first
var axios = require("axios").default;

var options = {
  method: "GET",
  url: "https://url-of-the-api.com",
  params: { param1: "value", param2: "value" },
  headers: {
    // Read API's doc to found appropriate headers
    host: "host-url.com",
    key: "SIGN-UP-FOR-KEY",
  },
};

axios
  .request(options)
  .then((response) => {
    console.log(response.data);
  })
  .catch((error) => {
    console.error(error);
  });
```

Serve Static files

```javascript
app.use(express.static("public"));

/* You can mow access files that are in public folder
Examples:
  http://localhost:3000/css/style.css
  http://localhost:3000/js/app.js
  http://localhost:3000/images/bg.png
*/
```

Deploy App to heroku

```text
Follow well made tutorial from heroku's devcenter documentation
https://devcenter.heroku.com/articles/deploying-nodejs
```

---

### EJS

[Back to summary](#javascript)

#### Tags

Use inside .ejs templates

- Text
  - `<%`  Scriptlet tag, for control-flow, no output
  - `<%_` Whitespace Slurping Scriptlet tag, strips all whitespace before it

- Variable
  - `<%=` Outputs the value into the template (HTML escaped)
  - `<%-` Outputs the unescaped value into the template

- Comment
  - `<%#` Comment tag, no execution, no output

- Litteral
  - `<%%` Outputs a literal '<%'

- Ending tags
  - `%>` Plain ending tag
  - `-%>` Trim-mode ('newline slurp') tag, trims following newline
  - `_%>` ‘Whitespace Slurping’ ending tag, removes all whitespace after it

#### Includes

Includes are relative to the template with the include call. (This requires the
'filename' option.) For example if you have "./views/users.ejs" and
"./views/user/show.ejs" you would use `<%- include('user/show'); %>`.

You'll likely want to use the raw output tag `<%-` with your include to avoid
double-escaping the HTML output.

```html
<ul>
  <% users.forEach(function(user){ %> <%- include('user/show', {user: user}); %>
  <% }); %>
</ul>
```

---

## SQL

[Back to summary](#summary)  

- [SELECT](#select)  
- [DISTINCT](#distinct)  
- [WHERE](#where)
- [Logical operators](#sql-logical-operators)
- [GROUP BY](#group-by)
- [HAVING](#having)
- [ORDER BY](#order-by)
- [AS](#as)
- [LIMIT](#limit)
- [CASE](#case)
- [UNION](#union)
- [INTERSECT](#intersect)
- [MINUS or EXCEPT](#minus-or-except)
- [INSERT INTO](#insert-into)
- [UPDATE](#update)
- [DELETE](#delete)
- [TRUNCATE](#truncate)
- [CREATE DATABASE](#create-database)
- [DROP DATABASE](#drop-database)
- [INNER JOIN](#inner-join)
- [LEFT or RIGHT JOIN](#left-or-right-join)
- [FULL JOIN](#full-join)
- [Subqueries](#subqueries)
- [CREATE INDEX](#create-index)

---

### SELECT

[Back to summary](#sql)  

The common usage of SQL is reading datas from a database. This is done with the
`SELECT` command, which returns records in a result table.  
This command can select one or more column of a table.

```sql
SELECT column FROM my_table             -- a single column
SELECT column1, column2 FROM my_table   -- 2 columns
SELECT * FROM my_table                  -- all columns
```

And a more advanced query

```sql
SELECT *
FROM table
WHERE condition
GROUP BY expression
HAVING condition
{ UNION | INTERSECT | EXCEPT }
ORDER BY expression
LIMIT count
OFFSET start
```

- [Click here to see all SQL functions](https://docs.snowflake.com/en/sql-reference/functions-all.html)

---

### DISTINCT

[Back to summary](#sql)  

SELECT returns all data of one of more columns. This command can return
duplicated records. To avoid this, simply put the `DISTINCT` keyword after `SELECT`.

```sql
SELECT DISTINCT my_column -- DISTINCT  is replaced with UNIQUE in Oracle
FROM tableau
```

---

### WHERE

[Back to summary](#sql)  

`WHERE` in a SQL query allows to extract records that validate a condition.

```sql
SELECT column(s) FROM my_table WHERE condition

-- Exemple
SELECT * FROM client WHERE city = 'paris'
```

| Opérateur   | Description                                                    |
|-------------|----------------------------------------------------------------|
| =           | equals to                                                      |
| <>          | not equals to                                                  |
| !=          | not equals to                                                  |
| >           | more than                                                      |
| <           | less than                                                      |
| >=          | more or equals                                                 |
| <=          | less or equals                                                 |
| IN          | list of possible values                                        |
| BETWEEN     | value between the giver interval                               |
| LIKE        | search specifying the beginning, middle or end of a string     |
| IS NULL     | Value is null                                                  |
| IS NOT NULL | Value is nor null                                              |

---

### SQL Logical Operators

All of the following operators can be used in combinaison with the NOT operator

#### AND / OR

```sql
SELECT columm
FROM table_name
WHERE condition1 AND condition2
```

#### IN

```sql
SELECT columm
FROM table
WHERE columm IN ( value1, value2, value3, ... )
```

#### BETWEEN

```sql
SELECT *
FROM table_name
WHERE columm BETWEEN 'value1' AND 'value2'

```

#### LIKE

The `LIKE` operator is used in `WHERE` clause in SQL queries. This keyword can
search for a pattern using wildcards.

- `_` represents 1 of any characters
- `*` represents 0, 1 or more of any characters
In use:
- `%a` all strings finishing with `a`
- `a%` all strings starting with `a`
- `%a%` all strings containing `a`

```sql
SELECT *
FROM table
WHERE column LIKE 'a%'
```

#### IS NULL / IS NOT NULL

In SQL, `IS` allows us to filter results containing the `NULL` value. This is
important because `NULL` is unknown and in consequence cannot be filtered by
comparison operators.

```sql
SELECT *
FROM table_name
WHERE column IS NULL

SELECT *
FROM table_name
WHERE column IS NOT NULL
```

---

### GROUP BY

[Back to summary](#sql)  

The `GROUP BY` command is used to group several results and apply a specific
function on that group.

```sql
SELECT column1, function(column2)
FROM table_name
GROUP BY column1
```

The functions available:

- `AVG()` for the average
- `COUNT()` count the number of rows concerned
- `MAX()` get the highest value
- `MIN()` get the lowest value
- `SUM()` calculates sum of several rows

Exemple

```sql
SELECT client, SUM(prices)
FROM purchase
GROUP BY client
```

---

### HAVING

[Back to summary](#sql)  

The keyword `HAVING` has the same purpose as `WHERE` but allows to filter using
functions.  

```sql
SELECT col1, SUM(col2)
FROM table_name
GROUP BY col1
HAVING fonction(col2) operator value1
```

This means `SELECT` columns from `table_name` by grouping rows that have
identical values as `col1` and that validate the `HAVING` condition.

---

### ORDER BY

[Back to summary](#sql)  

Allows us to sort the results. Can be achieved on a single or multiple columns,
by ascending (default) or descending order.  

```sql
SELECT col1, col2
FROM table_name
ORDER BY col1

SELECT col1, col2, col3
FROM table_name
ORDER BY col1 DESC, col2 ASC -- ASC is optional because its by default.
```

---

### AS

[Back to summary](#sql)  

This keyword let's you alliases object for better presentation of the results.  
This kind of renaming is only for the current query, it doesn't rename the object.

```sql
SELECT col1 AS c1, col2
FROM table_name

SELECT *
FROM table_name AS t1
```

---

### LIMIT

[Back to summary](#sql)  

Defines the maximum number of records to return.  This limition is done after
retrieving all the records, so it does not improve the performances.

```sql
SELECT *
FROM table_name
LIMIT 10
```

You can define an offset

```sql
SELECT *
FROM table
LIMIT 10 OFFSET 5 -- PostGreSQL

SELECT *
FROM table
LIMIT 5, 10; -- mySQL first value is the offset, second one the limit

```

---

### CASE

[Back to summary](#sql)  

This keyword is the if / else statement of sql.  
It creates a new columns named by default `CASE`.

```sql
SELECT id, name, percentage, unit_price, quantity, 
    CASE 
      WHEN percentage=1 THEN 'normal price'
      WHEN percentage>1 THEN 'expensive price'
      ELSE 'cheap price'
    END
FROM `purchase`

SELECT id, name, percentage, unit_price, quantity, 
  CASE quantity
    WHEN 0 THEN 'Error'
    WHEN 1 THEN '5% payback'
    WHEN 2 THEN '6% payback'
    WHEN 3 THEN '8% payback'
    ELSE '10% payback'
  END
 FROM purchase
```

---

### UNION

[Back to summary](#sql)  

This keyword allows to return records that correspond to 2 tables or more.  
![union](https://sql.sh/wp-content/uploads/2013/01/sql-ensemble-union-300.png)  
Each query has to have the same amount of columns. It does not display the
duplicates.  
To see duplicates use `UNION ALL` instead.

```sql
SELECT * FROM table1
UNION
SELECT * FROM table2
```

---

### INTERSECT

[Back to summary](#sql)  

Returns the intersection of results of 2 queries. In other terms it returns
records that are similar between 2 tables.  
![intersect](https://sql.sh/wp-content/uploads/2013/02/sql-ensemble-intersect-300.png)

```sql
SELECT * FROM `table1`
INTERSECT
SELECT * FROM `table2`
```

Not available on mySQL but there is an alternative shown below.

```sql
SELECT DISTINCT value FROM `table1`
WHERE value IN (
  SELECT value 
  FROM `table2`
);
```

---

### MINUS or EXCEPT

[Back to summary](#sql)  

This command returns the records of the first instruction without including the
results of the second.  
If a record is a result in both queries, it will not be returned.

- `EXCEPT` for PostGreSQL
- `MINUS` for MySQL and Oracle
![except](https://sql.sh/wp-content/uploads/2013/03/sql-ensemble-minus-300.png)

```sql
SELECT * FROM table1
EXCEPT
SELECT * FROM table2
```

---

### INSERT INTO

[Back to summary](#sql)  

This command is use to insert data into a table. This can be achieved record by
record or for multiple records at a time.

```sql
INSERT INTO table_name VALUES ('value 1', 'value 2', ...) -- single record

INSERT INTO table_name (column_1, column_2, ...)          -- single record
 VALUES ('value 1', 'value 2', ...)

INSERT INTO client (firstname, lastname, city, age)       -- multiple records
 VALUES
 ('Rébecca', 'Armand', 'Saint-Didier-des-Bois', 24),
 ('Aimée', 'Hebert', 'Marigny-le-Châtel', 36),
 ('Marielle', 'Ribeiro', 'Maillères', 27),
 ('Hilaire', 'Savary', 'Conie-Molitard', 58);

```

There is a special keyword with MySQL, `ON DUPLICATE KEY` that allows us to
update datas when a record already exists in a table.

```sql
INSERT INTO table (a, b, c)
VALUES (1, 20, 68)
ON DUPLICATE KEY UPDATE a=a+1
```

---

### UPDATE

[Back to summary](#sql)  

This allows you to modify existing records. Most often, this command is used in
combination with `WHERE`

```sql
UPDATE table_name
SET col1 = 'value 1', col2 = 'value 2', col3 = 'value 3'
WHERE condition
```

---

### DELETE

[Back to summary](#sql)  

Deletes records from a table. It is good practice to backup the table or database
before deleting records.

```sql
DELETE FROM table_name
WHERE condition
```

WARNING - If not `WHERE` condition is given, then ALL records will be deleted.

---

### TRUNCATE

[Back to summary](#sql)  

Deletes all records of a table without deleting the table itself. The result is
the same as using `DELETE` without `WHERE` condition.  
The only difference is that `TRUNCATE` will reset the value of the auto-increment
if there is one, `DELETE` don't.  

```sql
TRUNCATE TABLE table_name
```

---

### CREATE DATABASE

[Back to summary](#sql)  

Create a new database with the given name.  

```sql
CREATE DATABASE my_database
```

With MySQL, if a database with the same name already exists, the query will
return an error.  
To avoid this, use the following syntax

```sql
CREATE DATABASE IF NOT EXISTS my_database
```

---

### DROP DATABASE

[Back to summary](#sql)  

Delete a database and all its contents. Use with a lot of care!! Backup if not
sure what you are doing or don't do it :)

```sql
DROP DATABASE my_database
DROP DATABASE IF EXISTS my_database -- Avoid error if database doesn't exist

```

---

### INNER JOIN

[Back to summary](#sql)  

Returns records that validates the conditions in both tables
![inner join](https://sql.sh/wp-content/uploads/2013/02/sql-ensemble-intersect-300.png)

```sql
SELECT *
FROM A
INNER JOIN B ON A.key = B.key
```

---

### LEFT or RIGHT JOIN

[Back to summary](#sql)  

Returns records from the left / right table, even if the condition isn't true in
the other table.
![left join](https://sql.sh/wp-content/uploads/2013/03/sql-left-join-300.png)

```sql
SELECT *
FROM A
LEFT JOIN B ON A.key = B.key
```

And without B intersection
![left join](https://sql.sh/wp-content/uploads/2012/12/sql-left-join-exclude-300.png)

```sql
SELECT *
FROM A
LEFT JOIN B ON A.key = B.key
WHERE B.key IS NULL
```

---

### FULL JOIN

[Back to summary](#sql)  

![full join](https://sql.sh/wp-content/uploads/2013/01/sql-ensemble-union-300.png)

```sql
SELECT *
FROM A
FULL JOIN B ON A.key = B.key
```

or without intersection
![full join without intersection](https://sql.sh/wp-content/uploads/2012/12/sql-outer-join-exclude-300.png)

```sql
SELECT *
FROM A
FULL JOIN B ON A.key = B.key
WHERE A.key IS NULL
OR B.key IS NULL
```

---

### Subqueries

[Back to summary](#sql)  

- `EXISTS`: Check if records exists

  ```sql
  SELECT col1
  FROM table1
  WHERE EXISTS (
      SELECT col2
      FROM table2
      WHERE col3 = 10
    )
  ```

- `ALL`: compare if all values of a the validate a condition

  ```sql
  SELECT *
  FROM table1
  WHERE condition > ALL (
      SELECT *
      FROM table2
      WHERE condition2
  )
  ```

- `ANY` or `SOME`: compare if al least one value of a set validates a condition

  ```sql
  SELECT *
  FROM table1
  WHERE condition > ANY (
      SELECT *
      FROM table2
      WHERE condition2
  )
  ```

---

### CREATE INDEX

[Back to summary](#sql)  

- What is an index? Index are ressources that allows faster access to requested
datas. With an index place on one or many columns, the system can first search
datas on index and then knowing where to find the records requested.
- inconvenience: Those ressources takes additional storage spaces and insert new
records if slower because the index are updated at each insert.

```sql
CREATE INDEX index_name ON table_name       -- create index on multiple columns
CREATE INDEX index_name ON table_name (col1)-- create index on a single column
```

To specify that each value of a column should be unique, use the following syntax:

```sql
CREATE UNIQUE INDEX index_name ON table_name (col1)
```

---

## MongoDB

[Back to summary](#summary)

- [Mongo Shell](#mongo-shell)

### CRUD operations

- [Create](#create)
- [Read](#read)
- [Update](#update)
- [Delete](#delete)

### ODM

- [Mongoose](#mongoose)

---

### Mongo Shell

[Back to summary](#mongodb)  
open mongo shell

```shell
mongo
```

Commands list

```shell
help
```

Show Databases, collections, users...

```shell
show dbs
show collections
show users
```

Switch to a specific database (create it if doesn't exist)

```shell
use db_name
```

To show in which DB you currently are

```shell
db
```

---

### Create

[Back to summary](#mongodb)

- db.collection.insertOne() inserts a single document into a collection. If the
document does not specify an \_id field, MongoDB adds the \_id field with an
ObjectId value to the new document.

```javascript
db.movies.insertOne(
  // If the movies collection (SQL table equivalent)
  {
    // doesn't exist, it will be created
    title: "The Favourite",
    genres: ["Drama", "History"],
    runtime: 121,
    rated: "R",
    year: 2018,
    directors: ["Yorgos Lanthimos"],
    cast: ["Olivia Colman", "Emma Stone", "Rachel Weisz"],
    type: "movie",
  }
);
```

- db.collection.insertMany() can insert multiple documents into a collection.
Pass an array of documents to the method. If the documents do not specify an
\_id field, MongoDB adds the \_id field with an ObjectId value to each document

```javascript
db.movies.insertMany([
  {
    title: "Jurassic World: Fallen Kingdom",
    genres: ["Action", "Sci-Fi"],
    runtime: 130,
    rated: "PG-13",
    year: 2018,
    directors: ["J. A. Bayona"],
    cast: ["Chris Pratt", "Bryce Dallas Howard", "Rafe Spall"],
    type: "movie",
  },
  {
    title: "Tag",
    genres: ["Comedy", "Action"],
    runtime: 105,
    rated: "R",
    year: 2018,
    directors: ["Jeff Tomsic"],
    cast: ["Annabelle Wallis", "Jeremy Renner", "Jon Hamm"],
    type: "movie",
  },
]);
```

---

### Read

[Back to summary](#mongodb)

- Use the db.collection.find() method in the MongoDB Shell to query documents in
a collection. To read all documents in the collection, pass an empty document as
the query filter parameter to the find method.

```javascript
db.movies.find(); // all
db.accounts.findOne({ account_id: 893421 }); // One
```

- To select documents which match an equality condition, specify the condition
as a "field: value" pair in the query filter document.

```javascript
db.movies.find({
  title: "Titanic",
});
```

- Use [query operators](https://docs.mongodb.com/manual/reference/operator/query/#query-selectors)
in a query filter document to perform more complex comparisons and evaluations.
Query operators in a query filter document have the following form:
{ field1: { operator1: value1 }, ... }

```javascript
db.movies.find({
  rated: {
    $in: ["PG", "PG-13"],
  },
});
```

- A compound query can specify conditions for more than one field in the
collection's documents. Implicitly, a logical AND conjunction connects the
clauses of a compound query so that the query selects the documents in the
collection that match all the conditions.

```javascript
db.movies.find({
  countries: "Mexico",
  imdb.rating: {
    $gte: 7
    }
  })
```

---

### Update

[Back to summary](#mongodb)

To update a document, MongoDB provides [update operators](https://docs.mongodb.com/manual/reference/operator/update/)
such as $set, to modify field values.

- Use the db.collection.updateOne() method to update the first document that
matches a specified filter.

```javascript
db.movies.updateOne( { title: "Tag" },
{
  $set: {
    plot: "One month every year, five highly competitive friends \
    hit the ground running for a no-holds-barred game of tag"
  }
  { $currentDate: { lastUpdated: true } }
})
```

- Use the db.collection.updateMany() to update all documents that match a
specified filter.

```javascript
db.listingsAndReviews.updateMany(
  { security_deposit: { $lt: 100 } },
  {
    $set: { security_deposit: 100, minimum_nights: 1 },
  }
);
```

-To replace the entire content of a document except for the \_id field, pass an
entirely new document as the second argument to db.collection.replaceOne(). When
replacing a document, the replacement document must contain only field/value pairs.
Do not include update operators expressions. The replacement document can have
different fields from the original document. In the replacement document, you can
omit the \_id field since the \_id field is immutable; however, if you do include
the \_id field, it must have the same value as the current value.

```javascript
db.accounts.replaceOne(
  { account_id: 371138 },
  { account_id: 893421, limit: 5000, products: ["Investment", "Brokerage"] }
);
```

---

### Delete

[Back to summary](#mongodb)

- To delete all documents from a collection, pass an empty filter document {} to
the db.collection.deleteMany() method.

```javascript
db.movies.deleteMany({});
```

- You can specify criteria, or filters, that identify the documents to delete.
The filters use the same syntax as read operations.

```javascript
db.movies.deleteMany({ title: "Titanic" });
```

- To delete at most a single document that matches a specified filter (even though
multiple documents may match the specified filter) use the db.collection.deleteOne()
method.

```javascript
db.movies.deleteOne({ cast: "Brad Pitt" });
```

---

### Mongoose

[Back to summary](#mongodb)

- [Terminologies](#terminologies)
- [Schemas](#schemas)
- [Models](#models)
- [Data Validation](#data-validation)
- [Fetch Record](#fetch-record)
- [Update Record](#update-record)
- [Delete Record](#delete-record)
- [Helpers](#helpers)

---

#### Terminologies

---

[Back to summary](#mongoose)

##### Collections

‘Collections’ in Mongo are equivalent to tables in relational databases. They can
hold multiple JSON documents.

##### Documents

‘Documents’ are equivalent to records or rows of data in SQL. While a SQL row can
reference data in other tables, Mongo documents usually combine that in a document.

##### Fields

‘Fields’ or attributes are similar to columns in a SQL table.

##### Schema

While Mongo is schema-less, SQL defines a schema via the table definition. A
Mongoose ‘schema’ is a document data structure (or shape of the document) that is
enforced via the application layer.

##### Model

‘Models’ are higher-order constructors that take a schema and create an instance
of a document equivalent to records in a relational database.

---

##### Schemas

---

[Back to summary](#mongoose)

Everything in Mongoose starts with a Schema. Each schema maps to a MongoDB
collection and defines the shape of the documents within that collection.  
Each key in our code blogSchema defines a property in our documents which will be
cast to its associated [SchemaType](https://mongoosejs.com/docs/schematypes.html).

```javascript
import mongoose from "mongoose";
const { Schema } = mongoose;

mongoose.connect("mongodb://localhost:27017/booksDB"); // Connect to booksDB
// Create it if inexistant

const blogSchema = new Schema({
  title: String, // String is shorthand for {type: String}
  author: String,
  body: String,
  comments: [{ body: String, date: Date }],
  date: { type: Date, default: Date.now },
  hidden: Boolean,
  meta: {
    votes: Number,
    favs: Number,
  },
});

// It's good practice to close connection to db when uneeded
mongoose.connection.close().then(() => {
  console.log("\nDisconnect...");
});
```

To use our schema definition, we need to convert our blogSchema into a Model we
can work with. To do so, we pass it into mongoose.model(modelName, schema)

```javascript
const Blog = mongoose.model("Blog", blogSchema);
// ready to go!
```

By default, Mongoose adds an \_id property to your schemas.

```javascript
const schema = new Schema();

schema.path("_id"); // ObjectId { ... }
```

---

#### Models

---

[Back to summary](#mongoose)

Mongoose Schema vs. Model:

- A Mongoose model is a wrapper on the Mongoose schema. A Mongoose schema defines
the structure of the document, default values, validators, etc., whereas a Mongoose
model provides an interface to the database for creating, querying, updating,
deleting records, etc.

```javascript
// Defining Model
MyModel = mongoose.model('ModelsName', modelSchema)

// Create Instance
let myInstance = new MyModel({
 field: "value"
})

myInstance.save()
   .then(doc => {
     console.log(doc)
   })
   .catch(err => {
     console.error(err)
   })

/*
{
  _id: 5a78fe3e2f44ba8f85a2409a, -> The _id field is auto-generated by Mongo and
                                    is a primary key of the collection.
  Its value is a unique identifier for the document.
  field: "value", -> The value of the field is returned
  __v: 0 -> __v is the versionKey property set on each document when first
            created by Mongoose.
  Its value contains the internal revision of the document.
}
*/
```

---

#### Data Validation

---

[Back to summary](#mongoose)

When creating your schemas, you can specify [validation rules](https://mongoosejs.com/docs/validation.html)
Each field type can have the required validator.  
If validation doesn't pass, it will raise a ValidationError and give you details
of that failure.

```javascript
const mongoose = require("mongoose");

const exempleSchema = new mongoose.Schema({
  firstField: String,
  FieldWithValidation: {
    // Mongoose will check if the value is a number between 1 and 10
    type: Number,
    min: 1,
    max: 10,
    // We define here that FieldWithValidation field is required
    // If we don't provide this field, it will raise an error when we attempt to
    // save the document
    required: true,
  },
});
```

---

#### Fetch Record

---

[Back to summary](#mongoose)

Use find() method to fetch record

```javascript
MyModel.find({
  field: "value", // search query
})
  .then((doc) => {
    console.log(doc);
  })
  .catch((err) => {
    console.error(err);
  });
```

---

#### Update Record

---

[Back to summary](#mongoose)

Use findOneAndUpdate() method to update a single record.  
For performance reasons, Mongoose won’t return the updated document so we need to
pass an additional parameter to ask for it

```javascript
MyModel.findOneAndUpdate(
  {
    field: "value", // search query
  },
  {
    field: "new value", // field:values to update
  },
  {
    new: true, // return updated doc
    runValidators: true, // validate before update
  }
)
  .then((doc) => {
    console.log(doc);
  })
  .catch((err) => {
    console.error(err);
  });
```

---

#### Delete Record

---

[Back to summary](#mongoose)

Use the findOneAndRemove call to delete a record. It returns the original document
that was removed

```javascript
MyModel.findOneAndRemove({
  field: "value",
})
  .then((response) => {
    console.log(response);
  })
  .catch((err) => {
    console.error(err);
  });
```

---

#### Helpers

---

[Back to summary](#mongoose)

- Virtual Property  
  A virtual property is not persisted to the database. We can add it to our schema
  as a helper to get and set values.

```javascript
let mongoose = require("mongoose");

let userSchema = new mongoose.Schema({
  firstName: String,
  lastName: String,
});

module.exports = mongoose.model("User", userSchema);

/*
Let’s create a virtual property called fullName which can be used to set values on
firstName and lastName and retrieve them as a combined value when read:
*/
userSchema.virtual("fullName").get(function () {
  return this.firstName + " " + this.lastName; // Now we can get full name from
                                               // firstname and lastname
});

userSchema.virtual("fullName").set(function (name) {
  let str = name.split(" ");

  // Now we can set fistName and lastName from fullname:
  // model.fullName = 'Thomas Anderson'
  this.firstName = str[0];
  this.lastName = str[1];
});
```

- Instance Methods  
  We can create custom helper methods on the schema and access them via the model
  instance

```javascript
userSchema.methods.getInitials = function () {
  // Returns the initials for the current user
  return this.firstName[0] + this.lastName[0];
};

// This method will be accessible via a model instance
let model = new UserModel({
  firstName: "Thomas",
  lastName: "Anderson",
});

let initials = model.getInitials();

console.log(initials); // This will output: TA
```

- Static Methods  
  Similar to instance methods, we can create static methods on the schema. Let’s
  create a method to retrieve all users in the database

```javascript
userSchema.statics.getUsers = function () {
  return new Promise((resolve, reject) => {
    this.find((err, docs) => {
      if (err) {
        console.error(err);
        return reject(err);
      }

      resolve(docs);
    });
  });
};

// Calling getUsers on the Model class will return all the users in the database
UserModel.getUsers()
  .then((docs) => {
    console.log(docs);
  })
  .catch((err) => {
    console.error(err);
  });
```

- Middleware  
  Middleware are functions that run at specific stages of a pipeline. Mongoose
  supports middleware for the following operations
  - Aggregate - Document - Model - Query
  For instance, models have pre and post functions that take two parameters - Type
  of event (‘init’, ‘validate’, ‘save’, ‘remove’) - A callback that is executed
  with "this" referencing the model instance
  Let’s add two fields called createdAt and updatedAt to our userSchema

```javascript
let mongoose = require("mongoose");

let userSchema = new mongoose.Schema({
  firstName: String,
  lastName: String,
  createdAt: Date,
  updatedAt: Date,
});

module.exports = mongoose.model("User", userSchema);
```

When model.save() is called, there is a pre(‘save’, …) and post(‘save’, …) event
that is triggered.  
For the second parameter, you can pass a function that is called when the event is
triggered.  
These functions take a parameter to the next function in the middleware chain.
Let’s add a pre-save hook and set values for createdAt and updatedAt

```javascript
userSchema.pre("save", function (next) {
  let now = Date.now();

  this.updatedAt = now;
  // Set a value for createdAt only if it is null
  if (!this.createdAt) {
    this.createdAt = now;
  }

  // Call the next function in the pre-save chain
  next();
});
```

Let’s create and save our model

```javascript
let UserModel = require('./user')

let model = new UserModel({
  fullName: 'Thomas Anderson'
}

msg.save()
   .then(doc => {
     console.log(doc)
   })
   .catch(err => {
     console.error(err)
   })
/*
{ _id: 5a7bbbeebc3b49cb919da675,
  firstName: 'Thomas',
  lastName: 'Anderson',
  updatedAt: 2018-02-08T02:54:38.888Z,
  createdAt: 2018-02-08T02:54:38.888Z,
  __v: 0 }
*/
```

- Plugins  
  Suppose that we want to track when a record was created and last updated on
  every collection in our database.  
  Instead of repeating the above process, we can create a plugin and apply it to
  every schema.  
  Let’s create a plugin

```javascript
module.exports = function timestamp(schema) {

  // Add the two fields to the schema
  schema.add({
    createdAt: Date,
    updatedAt: Date
  })
```

To use this plugin, we simply pass it to the schemas that should be given this functionality

```javascript
let timestampPlugin = require("./plugins/timestamp");

emailSchema.plugin(timestampPlugin);
userSchema.plugin(timestampPlugin);
```

- Query Building  
  There are lots of [Queries](https://mongoosejs.com/docs/api/query.html)
  we can use in mongoose.  

Here is an example

```javascript
UserModel.find()                   // find all users
         .skip(100)                // skip the first 100 items
         .limit(10)                // limit to 10 items
         .sort({firstName: 1})      // sort ascending by firstName
         .select({firstName: true} // select firstName only
         .exec()                   // execute the query
         .then(docs => {
            console.log(docs)
          })
         .catch(err => {
            console.error(err)
          })
```

--- Work In Progress ---
