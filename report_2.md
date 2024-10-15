## Processes and Jobs
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



