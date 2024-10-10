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
-Commands used: /challenge/challenge -p(returns int value to enter as argument to obtain flag); /challenge/challenge -g 998
### Help for Builtins
-Commands used: help challenge; challenge --secret <value>
## File Globbing
### Matching by *
- * is a glob. When it encounters a * character in any argument, the shell will treat it as "wildcard" and try to replace that argument with any files that match the pattern.
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
- > is used to redirect stdout to files
- 
