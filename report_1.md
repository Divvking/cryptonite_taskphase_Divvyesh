# Report 1 - Linux Luminarium
## Hello Hackers
### Intro to Commands
Teaches about the terminal and how to invoke a command
Command used: hello (returns flag)
### Intro to Arguments
Teaches about arguments and the echo command which returns all the arguments in the terminal
Command used: hello hackers(returns flag)
## Pondering Paths
Teaches about the basics of the Linux file paths. Filesystem is like a tree, with a root directory, which contains more directories and files. Each file and directory is referred by its path. Each piece of the path is demarcated by a /
### The Root
Teaches about the root directory.
Command used: /pwn(invokes the program which returns the flag)
### Program and absolute paths
Uses absolute path
Command used: /challenge/run (returns flag)
### Position thy self
Introduction to cd
Command used: cd /proc/215/fd; /challenge/run
### Position elsewhere
Command used: cd /var/log; /challenge/run (returns flag)
### Position Yet Elsewhere
Command used: cd /home; /challenge/run
### implicit relative paths, from /
Teaches what a relative path is. A Relative path is any path that doesn't start at the root.
Command used: cd / ; challenge/run
### explicit relative paths, from /
Command used: cd / ; ./challenge/run
### implicit relative paths
Command used: cd /challenge; ./run
### home sweet home
Command used: /challenge/run ~/x

