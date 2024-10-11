# Report 1 - Linux Luminarium
## Hello Hackers
### Intro to Commands
- Teaches about the terminal and how to invoke a command
- Command used: hello (returns flag)
### Intro to Arguments
- Teaches about arguments and the echo command which returns all the arguments in the terminal
- Command used: hello hackers(returns flag)
## Pondering Paths
- Teaches about the basics of the Linux file paths. Filesystem is like a tree, with a root directory, which contains more directories and files. Each file and directory is referred by its path. Each piece of the path is demarcated by a /
### The Root
- Teaches about the root directory.
- Command used: /pwn(invokes the program which returns the flag)
### Program and absolute paths
= Uses absolute path
- Command used: /challenge/run (returns flag)
### Position thy self
- Introduction to cd
- Command used: cd /proc/215/fd; /challenge/run
### Position elsewhere
- Command used: cd /var/log; /challenge/run (returns flag)
### Position Yet Elsewhere
- Command used: cd /home; /challenge/run
### implicit relative paths, from /
- Teaches what a relative path is. A Relative path is any path that doesn't start at the root.
- Command used: cd / ; challenge/run
### explicit relative paths, from /
- Command used: cd / ; ./challenge/run
### implicit relative paths
- Command used: cd /challenge; ./run
### home sweet home
- Command used: /challenge/run ~/x
## Comprehending Commands
### cat: not the pet, but the command!
- cat reads out the contents of the file
- cat will concatenate 2 files if multiple arguments are given
- if no arguments are given, cat will read from the terminal input and output it.
- Commands used: cat /flag
### catting absolute paths
- Commands used: cat /flag
### more catting practice
- Commands used: cat /usr/share/distro-info/flag
### grepping for a needle in a haystack
- Sometimes, the files that are called by cat are too large, grep command solves this problem as it allows us to search in the contents
- Commands used: grep pwn.college /challenge/data.txt
### listing files
- ls will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided.
- Commands used: ls /challenge; /challenge/15492-renamed-run-4966
### touching files
- You can create a new, blank file by touching it with the touch command
- Commands used: touch /tmp/pwn; touch /tmp/college; /challenge/run
### removing files
- You can delete/remove a file in Linux using the rm command.
- Commands used: rm delete_me; /challenge/check
### hidden files
- Invoke ls with -a flag to view hidden files
- Commands used: ls / -a
### An Epic Filesystem Quest
- Commands used: Repetitive use of ls; ls -a; cat; cd
### making directories
- Use mkdir to create a directory
- Commands used: cd; mkdir pwn; touch college; /challenge/run
### finding files
- The find command takes optional arguments describing the search criteria and the search location. If you don't specify a search criteria, find matches every file. If you don't specify a search location, find uses the current working directory (.).
- Commands used: find / -name flag; cat /path
### linking files
- Symbolic links are created with the ln command with the -s argument
- Commands used: ln -s /flag /home/hacker/not-the-flag
## Digesting Documentation
### Learning from Documentation
- The correct usage of programs depends, in a large part, in the proper specification of arguments to them.
- Commands used: /challenge/challenge --giveflag
### Learning Complex Usage
- Commands used: /challenge/challenge --printfile /flag
### Reading Manuals
- Commands used: man challenge;/challenge/challenge --jfrbcz 448
### Searching Manuals
- Commands used: man challenge; /flag
### Searching for Manuals
- Commands used: man man; man -k challenge; man txquyaewtr; /challenge/challenge -txquyaewtr 599
### Helpful Programs
- Commands used: /challenge/challenge -p(returns int value to enter as argument to obtain flag); /challenge/challenge -g 998
### Help for Builtins
- Commands used: help challenge; challenge --secret <value>
## File Globbing
### Matching by *
- '*' is a glob. When it encounters a * character in any argument, the shell will treat it as "wildcard" and try to replace that argument with any files that match the pattern.
- Commands used: cd /ch*; /challenge/run
###  Matching with ?
- When it encounters a ? character in any argument, the shell will treat it as single-character wildcard. This works like *, but only matches one character.
- Commands used: cd /?ha??enge; /challenge/run
### Matching with []
- The square brackes are, essentially, a limited form of ?, in that instead of matching any character, [] is a wildcard for some subset of potential characters, specified within the brackets.
- Commands used: cd /challenge/files; /challenge/run file_[bash]
### Matching paths with []
- Commands used: /challenge/run /challenge/files/file_[bash]
### Mixing globs
- Commands used: /challenge/run [cep]*
### Exclusionary Globbing
- If the first character in the brackets is a ! or (in newer versions of bash) a ^, the glob inverts, and that bracket instance matches characters that aren't listed.
- Commands used: /challenge/run [^pwn]*
## Practicing Piping
### Redirecting Output
- '>' is used to redirect stdout to files
- Commands Used: echo PWN > COLLEGE
### Redirecting more output
- Commands Used: /challenge/run > myflag; cat myflag
### Appending output
- You can redirect input in append mode using >> instead of >
- Commands used: /challenge/run >> /home/hacker/the-flag; cat the-flag
### Redirecting errors
- A File Descriptor (FD) is a number the describes a communication channel in Linux
- FD 0: Standard Input
- FD 1: Standard Output
- FD 2: Standard Error
- a > without a number implies 1>, which redirects FD 1 (Standard Output)
- Commands used: /challenge/run > myflag 2> instructions; cat myflag
### Redirecting input
- Use < to redirect input to a program
- Commands Used: echo COLLEGE > PWN; /challenge/run < PWN
### Grepping stored results
- Commands Used: /challenge/run > /tmp/data.txt; grep pwn /tmp/data.txt
### Grepping live results
- the | (pipe) operator: Standard output from the command to the left of the pipe will be connected to (piped into) the standard input of the command to the right of the pipe.
- Commands Used: /challenge/run | grep pwn
### Grepping errors
- The shell has a >& operator, which redirects a file descriptor to another file descriptor. This means that we can have a two-step process to grep through errors: first, we redirect standard error to standard output (2>& 1) and then pipe the now-combined stderr and stdout as normal (|)
- Commands Used: /challenge/run 2>&1 | grep pwn
### Duplicating piped data with tee
- The tee command, named after a "T-splitter" from plumbing pipes, duplicates data flowing through your pipes to any number of files provided on the command line.
- Commands used: /challenge/pwn | tee intercepted_output | /challenge/college; cat intercepted_output; /challenge/pwn --secret AqjfFt1z | /challenge/college
### Writing to multiple programs
- Commands used: /challenge/hack | tee >( /challenge/the ) >( /challenge/planet )
### Split-piping stderr and stdout
- the challenge is that the | operator links the stdout of the left command with the stdin of the right command.
- Commands Used: /challenge/hack > > /challenge/planet 2> > /challenge/the
## Shell Variables
### Printing Variables
- Variables can be printed by using echo command and prefixing $ to the variable name
- Commands Used: echo #FLAG
### Setting Variables
- Use <var_name>=<value> to assign a value to a variable (no spaces)
- The $ is only prepended to access variables.
- Commands Used: PWN=COLLEGE
### Multi-word Variables
- Use double quotes to read the part after = as a single token.
- Commands Used: PWN="COLLEGE YEAH"
### Exporting Variables
- When you export your variables, they are passed into the environment variables of child processes.
- To go to the child shell use sh
- Commands Used: PWN=COLLEGE; COLLEGE=PWN; export PWN; sh; /challenge/run PWN
### Printing Exported Variables
- env command: it'll print out every exported variable set in your shell
- Command used: env
### Storing Command Output
- One can read the output of a command by storing it in a variable
- Command Used: PWN=$(/challenge/run); echo $PWN
### Reading Input
- To read input from user use 'read'
- -p argument lets you specify a prompt
- Commands Used: read -p "INPUT:" PWN
### Reading Files
- files can be read with the shell using read
- Commands Used: read PWN < /challenge/read_me
