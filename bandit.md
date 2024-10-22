# Level 0
- Command Used: ssh bandit0@bandit.labs.overthewire.org -p 2220
# Level 0->1
- Next password given in readme
- Used cat readme to read contents of file
- Used ssh bandit1@bandit.labs.overthewire.org -p 2220 and password ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
# Level 1->2
- Used cat ./- to read the password
- Used ssh bandit2@bandit.labs.overthewire.org -p 2220 and password 263JGJPfgU6LtdEvgfWU1XP5yac29mFx
# Level 2->3
- cat spaces\ in\ this\ filename
- Password MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
# Level 3->4
- cd inhere; ls -a; cat ...Hiding-From-You
- Password 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
# Level 4->5
- Use file command (Used to determine file type)
- cd inhere;file ./-*
- ./-file07: ASCII text
- cat ./-file07
- Password 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
# Level 5->6
- cd inhere; ls -a
- Using the knowledge provided in the question, size = 1033 bytes and file being readable by human
- find -type f -size 1033c
- cat ./maybehere07/.file2
- HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
# Level 6->7
- Using find with username argument bandit7, group argument bandit6 and size of file being 33 bytes
- find / -type f -user bandit7 -group bandit6 -size 33c
- cat /var/lib/dpkg/info/bandit7.password
- morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
# Level 7->8
- Using grep command to search for the word millionth in it, as we know that the password hash is right next to it
- grep millionth data.txt
- dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
# Level 8->9
- The password for the next level is stored in the file data.txt and is the only line of text that occurs only once
- uniq is a command that filters input and writes to the output. Specifically, it filters based on identical lines. It has a flag -u, which filters for unique lines (lines that appear only ones). It can also count (-c) or only return duplicate lines (-d).
- uniq is often used with sort, lines need to be sorted for uniq to work.
- cat data.txt|sort|uniq -u
- 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
# Level 9->10
- The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.
- The strings command finds human-readable strings in files. Specifically, it prints sequences of printable characters. Its main use is for non-printable files like hex dumps or executables.
- strings data.txt|grep ===
- FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
# Level 10->11
- The password for the next level is stored in the file data.txt, which contains base64 encoded data
- VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
- Linux has a command called base64 that allows for encoding and decoding in Base64. For decoding, we need to use the flag -d.
- cat data.txt|base64 -d
- The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
# Level 11->12
- The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions
- There are no inbuilt commands for doing ROT13 on Linux
- Used tr to substitute
- cat data.txt|tr 'A-Za-z' 'N-ZA-Mn-za-m'
- The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
# Level 12->13
- The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)
- Hexdumps are used when looking at data that cannot be represented in strings i.e. is not readable. A hexdump has three main columns. The first shows the address, the second the hex representation of the data on that address and the last shows the actual data as strings. '.' are values which cannot be represented.
- For the command line xxd can be used. xxd <input_file> <output_file> creates hexdumps. When using the -r flag, it reverts the hexdump.
- bzip2 is a command which allows for compressing and decompressing (-d) files. file ext .bz2
- gzip is another compression command.
![image](https://github.com/user-attachments/assets/1a7dd0f7-a654-48e4-9d81-821d1f1db1db)
- For gzip compressed files the header is \x1F\x8B\x08. Looking at the first line, we see that these are the first bytes of the file.
![image](https://github.com/user-attachments/assets/c9f2d17c-9c8a-486a-b5c1-6cab3e492b5a)
- This time we have a different magic number. Googling tells us that BZ (= ‘425a’) is the file signature for bzip and the next two bytes h (= ‘68’) indicate the version, in this case, it is version 2. So we can rename the file with the appropriate file ending (.bz2) and decompress it with bzip2 -d
![image](https://github.com/user-attachments/assets/816eae69-f972-4783-a259-1a2db84030e6)
- it is again gzip compressed, decompressing again
- it appears that we are now having an archive
- tar is a command that creates archive files (-cf). It also allows extracting these files again (-xf). A tar archive generally ends with .tar.
- data5.bin hexdump shows data6.bin, so using tar on data5.bin
- data6.bin is bzip2 compressed
- unarchiving data6.bin.out
- decompressing gzip encoded data8.bin
- The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
# Level 13->14
- The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on
- The public key is placed on the computers that should allow access (the remote host) to the user that owns the private key. The -i flag allows login with the private key.
- ssh -i sshkey.private bandit14@localhost
- cat /etc/bandit_pass/bandit14
- MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
# Level 14->15
- The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.
- nc or netcat is a command that allows to read and write data over a network connection.
- To connect to a service (as client) on a network the command syntax is the following: nc <host> <port>.
- nc localhost 30000; enter password MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS obtained from /etc/bandit_pass/bandit14
- password is 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
# Level 15->16
- The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.
  - Helpful note: Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the “CONNECTED COMMANDS” section in the manpage.
- OpenSSL is a library for secure communication over networks. It implements the Transport Layer Security (TLS) and Secure Sockets Layer (SSL) cryptographic protocols that are, for example, used in HTTPS to secure the web traffic.

- openssl s_client is the implementation of a simple client that connects to a server using SSL/TLS.
- openssl s_client -connect localhost:30001
- pasting password of current level 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
- kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
# Level 16->17
- The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.
- Port scanning is a method to find open ports on a host.
- nmap is a network scanner. For this task, use -p flag to choose which ports to scan. By default, nmap scans top 1000 ports (not first 1000). To scan all 65535 ports use -p-. -sV flag scans the version/service.
- nmap -sV localhost -p 31000-32000
- cd /tmp
- touch pvt.key
- nano pvt.key, paste RSA Key obtained from attempting to use openssl s_client -connect localhost:31790
- chmod 400 pvt.key
- ssh -i pvt.key bandit17@localhost -p 2220
# Level 17->18
- diff command compares files line by line
- diff passwords.old passwords.new
- new password: x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
# Level 18->19
- The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.
- ‘.bashrc’ is a file that is run every time a terminal is loaded. This means it is also run when logging in through SSH because this also loads a terminal.
- Instead of logging into the machine with SSH, we execute a command through SSH instead. We use cat to read the .
- ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
- bandit18@bandit.labs.overthewire.org's password:cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
# Level 19->20
- To gain access to the next level, you should use the setuid binary in the homedirectory. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.
- ./bandit20-do
Run a command as another user.
  Example: ./bandit20-do id
- ./bandit20-do cat /etc/bandit_pass/bandit20
- Password: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
# Level 20->21
- There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).
- Using ’netcat’, we can create a connection in server mode - which listens for inbound connection.
- Running the setuid binary with port 1234 means it will connect to our netcat server, receive the password inputted through echo and sends back the next password.
- echo '0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO'|nc -l -p 1234 &
- ./suconnect 1234
        Read: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
        Password matches, sending next password
        EeoULMCra2q0dSkYj561DX7s1CpBuOBt
# Level 21->22
- A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.
- ls -la /etc/cron.d
- ![image](https://github.com/user-attachments/assets/e58ead3f-fb21-4f57-aa91-e2a1fcfa5c1e)
- This cronjob runs the /usr/bin/cronjob_bandit22.sh file as bandit22 user. The five stars indicate it is run every minute, every day. To know what exactly is executed, we need to take a look at the bash file
- ![image](https://github.com/user-attachments/assets/986d0d5e-6eb2-43bf-b544-99ea024aeffa)
- This file creates a file in the ’tmp’ folder and gives read permission to everyone (indicated by the last 4). Then it copies the input of the bandit22 password file into the newly created file. So the password to the next level is in this created file.
- cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
- Password: tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
# Level 22->23
- A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.
- ls -la /etc/cron.d
- cat /etc/cron.d/cronjob_bandit23
- cat /usr/bin/cronjob_bandit23.sh
- echo I am user bandit23|md5sum|cut -d ' ' -f 1
- cat /tmp/8ca319486bfbbc3663ea0fbe81326349
- Password: 0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
# Level 23->24
- ls -la /etc/cron.d
- cat /etc/cron.d/cronjob_bandit24
- cat /usr/bin/cronjob_bandit24.sh
- The script executes and deletes all files in the folder ‘/var/spool/bandit24’. This is the case because it is run as bandit24 user, so the variable ‘myname’ contains the value ‘bandit24’.
- Inside the if statement is the code to execute a script, but only if the owner is bandit23. Then the file will be deleted.
- Creating a script to give password for bandit24
- create inside temp folder
- script reads the content of the file and stores in a temp folder in a temp file called password.
- Give appropriate permissions
- cp pswd.sh /var/spool/bandit24/foo
- Password:gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
# Level 24->25
- A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.
- nc localhost 30002
- #!/bin/bash

for i in {0..9}{0..9}{0..9}{0..9}
do

echo "gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8 $i" >> list.txt;
done
cat list.txt | nc localhost 30002 > result.txt
- sort result.txt 
- password: iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
- ![image](https://github.com/user-attachments/assets/3f5ff6f0-b1ac-448f-a5a0-838bbfbd52cb)
# Level 25->26
- Try connecting to bandit26 using the ssh key given in the question
- shell is not /bin/bash but something else
- cat /etc/passwd|grep bandit26
- /usr/bin/showtext is a shell
- more command displays the contents of a file
- If we make the terminal window smaller, more will go into command mode. reduce size of the terminal and run ssh command with RSA key again, now on 
  clicking V, it opens vi, which is a text editor
- To spawn a shell, we can use :shell
- To change the shell, do :set shell=/bin/bash
- now use :shell
- do cat /etc/bandit_pass/bandit26
- password: s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ
# Level 26->27
- bandit27-do allows user to run command as another user
- ./bandit27-do cat /etc/bandit_pass/bandit27
- Password: upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB
# Level 27->28
- There is a git repository at ssh://bandit27-git@localhost/home/bandit27-git/repo via the port 2220. The password for the user bandit27-git is the same as for the user bandit27. Clone the repository and find the password for the next level.
- git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo
- read the README file in the repo folder to obtain password
- password: Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN
# Level 28->29
- Same method as previous question, but on doing cat README.md
- ![image](https://github.com/user-attachments/assets/888dd595-7ca9-4d63-b845-11b2dfdf6b8a)
- This time, the README has Markdown format ('.md'). It mentions, but does not contain the password. We can take a look at the git history to see, if a past version of the README file contained the password. First, we check out the log.
- git log
- ![image](https://github.com/user-attachments/assets/ecdb4720-48a4-4f0d-ac61-d450d13d2bb3)
- git show 817e303aa6c2b207ea043c7bba1bb7575dc4ea73
- ![image](https://github.com/user-attachments/assets/86f51848-4363-44a7-91b0-7e05d67f8754)
- password: 4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7
# Level 29->30
- Git branching is another feature of the version control system. It allows you to split the development into different branches. Specifically, there is a master branch from which the software can be taken and it can be separately worked on. You can change and add features while still maintaining a working master branch. Once the work is done, it can be integrated into the master branch again. This allows for additional version control.
- There is a git repository at ssh://bandit29-git@localhost/home/bandit29-git/repo via the port 2220. The password for the user bandit29-git is the same as for the user bandit29. Clone the repository and find the password for the next level.
- readme.md contains the following data
- ![image](https://github.com/user-attachments/assets/1a5fc5a2-3102-4929-a5fa-447bd7dfcab1)
- git branch -a
- git checkout dev
- Password in readme.md
- Password: qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL
# Level 30->31
- There is a git repository at ssh://bandit30-git@localhost/home/bandit30-git/repo via the port 2220. The password for the user bandit30-git is the same as for the user bandit30. Clone the repository and find the password for the next level.
- The README does not give us any information. Checking the git tag, we find a point in the history called ‘secret’, which looks promising.
- git tag
- git show secret
- Password: fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy
# Level 31->32
- Same method as last question
- Git Commit saves the currently made changes with a message describing these changes. The flag -a makes sure all modified/deleted files are staged.
- Git Push updates local changes in remote repositories. When pushing for the first time, you should also define the branch with -u.
- Git Ignore is a file with the filename ‘.gitignore’. In this file, all file names/extensions that should be ignored by the commit are written. This means if a file which is in the ignore file is created/changed, it will not be part of the commit/repository. Git ignore also allows for wildcards.
- Git Add updates what files will be part of the next commit. The -f flag forces files to be able to be committed, even when they are normally ignored.
- Contents of README.md:File name: key.txt
                        Content: 'May I come in?'
                        Branch: master
- echo 'May I come in?' > key.txt
- git add -f key.txt
- git commit -a
- git push -u origin master
- password: 3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K
# Level 32->33
- the variable $0 has a reference to a shell
- This allows us to escape the shell
- whoami reveals that we are bandit33
- so we can read the password
- cat /etc/bandit_pass/bandit33
- Password: tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0




