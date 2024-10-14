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



