![image](https://github.com/user-attachments/assets/b39c4665-5b45-437b-a8c1-a6f3749a314e)## Processes and Jobs
- This module taught me how to view and interact with processes in various mannersComputers execute various programs to complete instructions and tasks. In modern computing, software is split into two categories: operating system kernels and processes. When Linux starts up, it launches an initialiser(init) process that launches other processes which launch more processes until the command line shell is obtained. The shell launches processes in response to the commands the user enters.

### Listing Processes
- Learnt how to list running processes using ps command.
- As ps is a very old utility, its usage is a bit of a mess. There are two ways to specify arguments.
1. "Standard" Syntax: in this syntax, you can use -e to list "every" process and -f for a "full format" output, including arguments. These can be combined into a single argument -ef.
2. "BSD" Syntax: in this syntax, you can use a to list processes for all users, x to list processes that aren't running in a terminal, and u for a "user-readable" output. These can be combined into a single argument aux.
These two methods, ps -ef and ps aux result in slightly different, but cross-recognizable output.
#### Thought Process
- Since they mentioned that /challenge/run has been renamed, I used ps -ef to discover the renamed process.
- Commands Used: ps -ef; /challenge/10386-run-15051
#### Output:
![image](https://github.com/user-attachments/assets/66a39695-4674-4050-9ab3-f4decbff178e)
### Killing Processes
- 'kill' command will terminate a process in a way that gives it a chance to get its affairs in order before ceasing to exist.
#### Thought Process
- /challenge/run will not run as long as /challenge/dont_run is running. So we must kill that process first, and then run /challenge/run
- Commands Used: kill 73(PID of /challenge/dont_run);/challenge/run 
#### Output
![image](https://github.com/user-attachments/assets/55837059-dcbb-4b2c-9d2b-a02e68af53b7)
### Interrupting Processes
- To get rid of a process clogging up the terminal, use Ctrl-C.
- Commands used: /challenge/run; Ctrl-C on keyboard
#### Output
![image](https://github.com/user-attachments/assets/4f8859dc-4c1a-4405-b9d5-26c963236b1d)
### Suspending Processes
- You can suspend processes to the background with Ctrl-Z.
- Commands Used: /challenge/run; Ctrl-Z; /challenge/run
#### Output
![image](https://github.com/user-attachments/assets/5e9176e7-831e-426c-ba82-03ad37fe97fe)
### Resuming Processes
- To resume processes, your shell provides the fg command, a builtin that takes the suspended process, resumes it, and puts it back in the foreground of your terminal.
- Commands Used: /challenge/run; Ctrl-Z; fg
#### Output 
![image](https://github.com/user-attachments/assets/4665d4ba-f347-4d0a-b13e-bc4430b903bf)
### Backgrounding Processes 
- You can also resume processes in the background with the bg command! This will allow the process to keep running, while giving you your shell back to invoke more commands in the meantime.
- Commands Used: /challenge/run; Ctrl-Z; bg; /challenge/run
#### Output
![image](https://github.com/user-attachments/assets/8ea907fd-7d4b-45d9-b0e2-44c25f41b4e8)
### Foregrounding Processes
- You can foreground a backgrounded process with fg just like you foreground a suspended process.
- Commands Used: /challenge/run; Ctrl-Z; bg; fg
#### Output
![image](https://github.com/user-attachments/assets/9675db06-f82d-442a-b78d-6cd585d80a1d)
### Starting Backgrounded Processes
- You can background a process straight off the bat by appending &.
- Commands Used: /challenge/run &
#### Output
![image](https://github.com/user-attachments/assets/ff4c6bbe-093d-4284-9747-33e98a7026aa)
### Process Exit Codes
- You can access the exit code of the most recently-terminated command using the special ? variable (prepend it with $)
- Commands that succeed typically return 0 and commands that fail typically return a non-zero value, most commonly 1 but sometimes an error code that identifies a specific failure mode.
- Commands Used: /challenge/get-code; echo $?; /challenge/submit-code 148
#### Output
![image](https://github.com/user-attachments/assets/2ee2d641-3458-41e1-8577-18f0a7a8e0fb)
## Perceiving Permissions
- Learnt about Linux Permissions. You can check out a permissions of a file or directory using ls -l.
### Changing File Ownership
- We can change the ownership of files via the chown (change owner) command.
- Typically, chown can only be invoked by the root user.
- Commands Used: chown hacker /flag; cat /flag
#### Output
![image](https://github.com/user-attachments/assets/224ccaff-fbb8-4094-a768-619f4c31f370)
### Groups and Files
- Files have both an owning user and group. A group can have multiple users in it, and a user can be a member of multiple groups.
- a user can check what groups they are a part of using ID
- Group ownership can be changed with the chgrp (change group) command
- Commands Used: chgrp hacker /flag; cat /flag
#### Output
![image](https://github.com/user-attachments/assets/3f73efc4-f2c1-4f09-bd30-26f8a7908d24)
### Fun with Groups Names
- There is a convention in Linux that every user has their own group, but this does not have to be the case
#### Thought Process
- Use id to find the current group, change group, read flag
- Commands used: id; chgrp grp17400 /flag; cat /flag
#### Output
![image](https://github.com/user-attachments/assets/aa308337-ae0a-4844-9ed9-6283db7c6871)
### Changing Permissions
- Like ownership, file permissions can also be changed. This is done with the chmod (change mode) command.
- You can specify the MODE in two ways: as a modification of the existing permissions mode, or as a completely new mode to overwrite the old one.
- u+r, as above, adds read access to the user's permissions
- g+wx adds write and execute access to the group's permissions
= o-w removes write access for other users
- a-rwx removes all permissions for the user, group, and world
#### Thought Process
- Use a+r or o+r to give read permissions to other users since root is owner of /flag file, then use cat to read /flag
- Commands Used: chmod a+r /flag; cat /flag
#### Output 
![image](https://github.com/user-attachments/assets/973beeb5-b267-4a12-aa9b-85b6e89adbd1)
### Executable Files
- When you invoke a program, such as /challenge/run, Linux will only actually execute it if you have execute-access to the program file.
#### Thought Process
- Use chmod to give execution permissions to user, then execute /challenge/run
- Commands Used: chmod a+x /challenge/run; /challenge/run
#### Output
![image](https://github.com/user-attachments/assets/a6cb3772-ba19-40f4-b01f-93ce1ea281cd)
### Permission Tweaking Practice
#### Thought Process
- Give other users write+execute permissions, so use o+wx
- Give owner execute permissions, so use u+x
- Give group write+execute permissions, so use g+wx (can also do a+wx)
- Remove group and world read permissions, so use g-r, o-r
- Remove write and execute permissions from user and world, so use u-wx,o-wx
- Remove write permissions from group, so do g-w
- Give write permissions to group, and write and execute permissions to other users so do g+w, o+wx
- Give owner execution permissions, so do u+x
- Now do chmod a+r /flag, then cat /flag to obtain the flag
#### Output
![image](https://github.com/user-attachments/assets/3b9e261f-0c76-4842-8a27-395ebd4110b9)
### Permissions Setting Practice
- chmod can also simply set permissions altogether, overwriting the old ones. This is done by using = instead of - or +.
#### Thought Process
- Use the = and , sign to set the permissions, following the instructions given in the level.
#### Output
![image](https://github.com/user-attachments/assets/a4203c90-ee84-4ee4-a09a-b3e532599984)
### The SUID Bit
- The "Set User ID" (SUID) permissions bit allows the user to run a program as the owner of that program's file.
- Giving the SUID bit to an executable owned by root can give attackers a possible attack vector to become root.
#### Thought Process
- Set SUID bit for /challenge/getroot, execute getroot program then do cat /flag.
#### Output
![image](https://github.com/user-attachments/assets/e2b142bc-6e0a-434c-b928-dcc8572703ab)
## Untangling Users
### Becoming root with su
- su is a setuid binary. Because it has the SUID bit set, su runs as root. Running as root, it can start a root shell. Before allowing the user to elevate privileges to root, it checks to make sure that the user knows the root password.
#### Thought Process
- Password is given as hack-the-planet, Provide it to su
#### Output
![image](https://github.com/user-attachments/assets/e2fdc411-3000-4351-b55f-d1dd477cb164)
### Other users with su
- Giving a username as an argument to su allows to switch to that user
#### Thought Process
- Switch to zardus user, give password dont-hack-me, then run /challenge/run
#### Output
![image](https://github.com/user-attachments/assets/952af01c-d3d5-4c06-8151-908773fc36f3)
### Cracking passwords
- When you enter a password for su, it compares it against the stored password for that user. These passwords used to be stored in /etc/passwd, but because /etc/passwd is a globally-readable file, this is not good for passwords, these were moved to /etc/shadow.
- When you input a password into su, it one-way-encrypts (hashes) it and compares the result against the stored value. If the result matches, su grants you access to the user.
- use john command
#### Thought Process
- Use john command to find password of zardus
- aardvark         (zardus)
- do su zardus
#### Output
![image](https://github.com/user-attachments/assets/23016d1b-856d-461d-9983-cf82c4a785a6)
### Using sudo
- Unlike su, which defaults to launching a shell as a specified user, sudo defaults to running a command as root
- Commands Used: sudo cat /flag
#### Output
![image](https://github.com/user-attachments/assets/46c1b9e1-a694-493b-aa6a-c717577aa768)
## Chaining Commands
### Chaining with Semicolons
- The easiest way to chain commands is ;.
#### Thought Process
- Use /challenge/pwn; /challenge/college
#### Output 
![image](https://github.com/user-attachments/assets/a05af4e5-0ff3-45d1-a2f8-b7d800dac48b)
### Your First Shell Script
- By convention, shell scripts are frequently named with a sh suffix
#### Thought Process
- Use nano or vim to open a command line editor, I used vim.
- Enter insert mode and enter /challenge/pwn; /challenge/college
- Press esc to get out of insert mode, then type :wq to save and exit the file
- Run it by doing bash x.sh
#### Output
![image](https://github.com/user-attachments/assets/c8a9aba7-ce09-4c68-b20d-4f6fad81e0e2)
### Redirecting Script Output
- Shell treats .sh files like a command, so it can be piped
#### Thought Process
- Create a file using vim containing /challenge/pwn;/challenge/college
- bash filename.sh|/challenge/solve
#### Output
![image](https://github.com/user-attachments/assets/8585cec3-4c57-4f9e-ba7e-73c6c6b7080a)
### Executable Shell Scripts
- No need to manually invoke bash. If your shell script file is executable, simply invoke it via its relative or absolute path.
#### Thought Process
- Create a file containing /challenge/solve
- Use chmod to give execution permissions to user
- execute file by calling path
#### Output 
![image](https://github.com/user-attachments/assets/d24a58d7-d57e-40fb-9148-abc182a25884)
## Pondering PATH
### The PATH Variable
- There is a special shell variable, called PATH, that stores a bunch of directory paths in which the shell will search for programs corresponding to commands.
- Without a PATH, bash cannot find the command.
#### Thought Process
- Redirect the PATH to either a blank string or a directory where rm is absent, causing the /challenge/run program to return flag instead.
#### Output
![image](https://github.com/user-attachments/assets/39851208-1347-4d84-95da-240c78c51975)
### Setting PATH
By adding directories to or replacing directories in this list, you can expose programs to be launched using their bare name.
#### Thought Process
- win command exists in /challenge/more_commands so set the PATH to that, then /challenge/run, as it calls the win command by its bare name
#### Output
![image](https://github.com/user-attachments/assets/afce570c-b4d0-42c0-9526-85ada78dca4c)
### Adding Commands
#### Thought Process
- create a file called win, containing cat /flag
- add a new directory to PATH by doing PATH="/home/hacker:$PATH"
- chmod +x win
- /challenge/run
#### OUTPUT
![image](https://github.com/user-attachments/assets/a20018c6-86ea-47f2-95ef-9dc24146edae)
### Hijacking Commands
#### Thought Process
- create a custom script called rm in /home/hacker
- make it do cat /flag instead
- do PATH="/home/hacker:$PATH", this places /home/hacker at the start of the PATH variable, since it prioritises left to right, it will only run the custom rm command instead.
- do /challenge/run
#### OUTPUT
![image](https://github.com/user-attachments/assets/3b8e4b49-52d8-43f0-830d-414b89098d5b)
