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
