## Introduction
Hello and Assalamualaikum. Today we gonna try to play [Bandit wargames](https://overthewire.org/wargames/bandit/). To start this game, you must connect to the server by using any SSH client such as putty or MobaXTerm. You can use any operating system such windows, linux and mac, but if you are running virtual machine, it may failed to connect to overthewire.org server if it is configured to NAT. You may resolve it by changing NAT to Bridged Adapter.

## Level 0
The first is just pretty straight forward. We just need to connect to bandit.labs.overthewire.org server with username: `bandit0` and password `bandit0` on port 2220.

```
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

![Screenshot 2021-03-01 at 6 37 25 AM](https://user-images.githubusercontent.com/32232422/109512619-1fda2480-7a59-11eb-944e-6e9ec3c025a2.png)

## Level 1
Now we have to connect to the server with username: `bandit1`, but the password is stored on readme. Remember we already connect to bandit0 user before on level 0. So we can use `find` command to find specific file name. Then we can use `ls` to list out all files on current directory as you can see readme is on our current directory.

![Screenshot 2021-03-01 at 6 56 18 AM](https://user-images.githubusercontent.com/32232422/109514849-4e58ff00-7a5b-11eb-94e0-0338dd3d8a96.png)

Then we can read the readme file by using `cat` command.

![Screenshot 2021-03-01 at 6 58 22 AM](https://user-images.githubusercontent.com/32232422/109515073-882a0580-7a5b-11eb-908a-7f81fef63176.png)

So the password for bandit1 is `boJ9jbbUNNfktd78OOpsqOltutMc3MY1`. Now we can ssh to the same server for bandit1 by using the password.

`ssh bandit1@bandit.labs.overthewire.org -p 2220`

![Screenshot 2021-03-01 at 7 01 36 AM](https://user-images.githubusercontent.com/32232422/109515708-3b92fa00-7a5c-11eb-9622-d423ff01087c.png)

We are bandit1 now. If we run `whoami` command, it will tell you about the username for current user.

![Screenshot 2021-03-01 at 7 02 08 AM](https://user-images.githubusercontent.com/32232422/109516150-b825d880-7a5c-11eb-862b-cf3d80dc9060.png)

## Level 2
The goal is to find password for bandit2 on bandit1 home directory. If we try to list the file by using `ls` command, we can see a file named '-'. This is dashed filename and the way to read the file is by giving full path of the file. We can use `pwd` to know current path.

![Screenshot 2021-03-01 at 5 55 52 PM](https://user-images.githubusercontent.com/32232422/109585369-44191e00-7ab8-11eb-90cd-feaa4ffd0346.png)

We also can use other syntax such as:

![Screenshot 2021-03-01 at 5 58 20 PM](https://user-images.githubusercontent.com/32232422/109585464-6dd24500-7ab8-11eb-94c5-2ab24bcc53fc.png)

The password for next user is `CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9` and try to ssh to bandit2.
```
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

## Level 3
On current directory, there is a file named space in the filename. The file name is containing spaces, and the way to read the file are by using quotes '' or escape \ for spaces. You also can type `cat`, type the first character of the file and press tab.

![Screenshot 2021-03-01 at 6 14 32 PM](https://user-images.githubusercontent.com/32232422/109586392-fd2c2800-7ab9-11eb-8764-8b92fec1a1b4.png)

The password is `UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK`.

## Level 4
The goal is to find password on hidden file in inhere directory. Use `cd` to change directory and list out the file in currect directory. It will prompt nothing. The challenge already said that the file is a hidden file, so we can use `ls -la` to view hidden file.

![Screenshot 2021-03-01 at 6 21 29 PM](https://user-images.githubusercontent.com/32232422/109587087-50eb4100-7abb-11eb-8b39-229c99675d9f.png)

As you can see, there are .hidden file, any file started with dot `.` will treat as hidden file. Thus, the password is `pIwrPrtPN36QITSp3EQaw936yaFoFgAB`.

## Level 5
The goal is to find password on a file that is stored in human-readable file in the inhere directory. You have to change directory to inhere folder and list out the files. If we try to read one of the file, it give garbage character. That is binary file which is cannot be represented in ASCII table. We can use `file` command to know what type of the file. The file type is data but we want ASCII file. We can use `*` to check all file.

![Screenshot 2021-03-01 at 6 44 37 PM](https://user-images.githubusercontent.com/32232422/109588957-6dd54380-7abe-11eb-9937-bd0614bdc164.png)

As you can see, there is only one ASCII format on -file07. You also can use `grep -i` to grep only ASCII character. -i means ignore case.

![Screenshot 2021-03-01 at 6 45 55 PM](https://user-images.githubusercontent.com/32232422/109589180-c99fcc80-7abe-11eb-8e28-de3ab8df1a31.png)

So the password is `koReBOKuIDDepwhWk7jZC0RTdopnAYKh`.

## Level 6
The next goals to find password on somewhere file on inhere directory and the file have these properties:
1. human-readable
2. 1033 bytes in size
3. not executable

We can use `find` command to find specific file with specific properties. 
```
find . -size 1033c -exec ls -sh {} + | xargs file | grep -i ascii
```
- `find` : command to find
- `.(dot)` : current directory
- `1033c` : 1033 byte, c = byte, k = kilo can refer [here](https://ostechnix.com/find-files-bigger-smaller-x-size-linux/)
- `-exec ls -sh {} +` : list all file under directory with file size
- `|` : let you to have two or more command in one line
- `grep -i` : filter only ascii and ignore case sensitive

**UPDATED**: _Add `! -executable` to find non executable file. `find . -size 1033c ! -executable -exec ls -sh {} + | xargs file | grep -i ascii`_

Only one file listed and you can read the file.

![Screenshot 2021-03-01 at 8 16 15 PM](https://user-images.githubusercontent.com/32232422/109597232-b1cf4500-7acc-11eb-98d3-2f75b65c4c93.png)

The password is `DXjZPULLxYr17uwoI01bNLQbtFemEgo7`.

## Level 7
The password for the next level is stored somewhere on the server and has all of the following properties:
1. owned by user bandit7
2. owned by group bandit6
3. 33 bytes in size

The hint is stored somewhere, this means we gonna find it on all directories. We can start to find it on root folder (`/`). If you confuse between `/` and `/root`, you can [read here](https://superuser.com/questions/1072071/linux-folder-and-root-folder). In this challenge, we still use `find` command and some options.

```
find / -type f -group bandit6 -user bandit7 -size 33c -print 2>/dev/null
```
- `find` : command to find
- `/` : root directory, parent dir
- `-type f` : choose regular file type
- `-group bandit6` : specify the user is bandit6
- `-user bandit7` : specify the user is bandit7
- `-size 33c` : specify the size of the must 33byte. The flag can refer [here](https://ostechnix.com/find-files-bigger-smaller-x-size-linux/)
- `-print 2>/dev/null` : removes error or dont display error

Only one file found.

![Screenshot 2021-03-01 at 9 12 52 PM](https://user-images.githubusercontent.com/32232422/109603198-65890280-7ad6-11eb-94b1-a4ca71502140.png)

The password is `HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs`.

## Level 8
The password for the next level is stored in the file data.txt next to the word millionth. This is pretty straight forward. We just read the file and grep `millionth`.
```
cat data.txt | grep -i millionth
```

![Screenshot 2021-03-02 at 2 12 40 AM](https://user-images.githubusercontent.com/32232422/109633636-28843680-7afd-11eb-88d3-62ded8310746.png)

The password is `cvX2JJa4CFALtqS87jk27qwqGhBM9plV`.

## Level 9
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once. This means we have to remove duplicate data and this can be archieve using `sort` and `uniq -u` to sort unique data.

![Screenshot 2021-03-02 at 2 30 05 AM](https://user-images.githubusercontent.com/32232422/109635443-389d1580-7aff-11eb-9f0c-f132d044122d.png)

The password is `UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR`.

## Level 10
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters. If we try to read the file using `cat`, it will throw garbage character. Those characters are binary and cannot be converted into ASCII format.

![Screenshot 2021-03-02 at 2 42 52 AM](https://user-images.githubusercontent.com/32232422/109636929-042a5900-7b01-11eb-8de9-dbadf3abaf84.png)

To read ASCII character, we can use `strings` command to read human-readble text and filter '=' using `grep`.

![Screenshot 2021-03-02 at 2 39 38 AM](https://user-images.githubusercontent.com/32232422/109637119-350a8e00-7b01-11eb-88d0-a08e94e7e956.png)

The password is `truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk`.

## Level 11
The password for the next level is stored in the file data.txt, which contains base64 encoded data. We have to decode base64 format encoded using `base64 -d`, `-d` stands for decode. You can read more [here](https://en.wikipedia.org/wiki/Base64).

![Screenshot 2021-03-02 at 2 48 49 AM](https://user-images.githubusercontent.com/32232422/109638041-633c9d80-7b02-11eb-8f19-bd7654b71f7a.png)

The password is `IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR`.

## Level 12
The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions. This is classic CTF(Capture The Flag) questions which is called ROT13. We can decode the message using `tr`. `'A-Za-z' 'N-ZA-Mn-za-m'` tell us to replace A to N, B to O and etc. You can read it more [here](https://stackoverflow.com/questions/5442436/using-rot13-and-tr-command-for-having-an-encrypted-email-address).

```
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

![Screenshot 2021-03-02 at 2 57 08 AM](https://user-images.githubusercontent.com/32232422/109638805-4e143e80-7b03-11eb-8feb-ae9514f7cd76.png)

The password is `5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu`.

## Level 13
On this level, the password is stored on data.txt in [hexdump](https://en.wikipedia.org/wiki/Hex_dump) format. Hexdump convert any binary or data into hex format and if you notice the data also contains ASCII text on the right side. The hint for this level is repeatly compressed, thus we have to repeatly decompress the file. First we have to covert the hexdump into binary file. At this moment, we dont know the type of the file, it can be zip file, png, jpeg, exe and etc. But first we have to create folder on tmp directory because on our current directory, we dont have permission to create file. Use `mkdir` to create directory and `cp` to copy file from source to destination.

```
mkdir /tmp/test
cp data.txt /tmp/test
```

Now we can convert the hexdump format into binary file using `xxd -r` to revert the hexdump and save it into a file named data. Then, use `file` to check the type of binary file. For this example, it is gzip file, thus we must rename the file extension to .gz. Then try to decompress the data.gz using `gzip -d data.gz`. Since it is repeatly compressed file, we have to repeadly decompress the file as well. The steps just involves:
1. check the type of binary file by using `file`.
2. rename the file extension based on first step.
3. decompress the file.
4. If the output file from decompressed is not an text file, repeat the process to step 1 again.

File extensions that involves are .gz, .bz2, and .tar only. Tools can use:
1. `gzip -d` : .gz only, -d stands for decode
2. `bzip2 -d` : .bzip2 only, -d stands for decode
3. `tar xvf` : .tar only, x-extract, v-verbose, f-file name type. [details](https://www.tecmint.com/18-tar-command-examples-in-linux/)

![Screenshot 2021-03-02 at 11 53 51 PM](https://user-images.githubusercontent.com/32232422/109772258-a0606880-7bb2-11eb-80a4-ba3b9e6dc5cb.png)

The password is `8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL`.

## Level 14
The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. There is a file named sshkey.private which contain RSA Private key. So we just have to copy the RSA file and save into our machine. Then, ssh to the server using bandit14 as the user.

![Screenshot 2021-03-03 at 12 10 57 AM](https://user-images.githubusercontent.com/32232422/109775421-58434500-7bb6-11eb-905a-fbaaa35d7e65.png)

```
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```
Now we can read the password at /etc/bandit_pass/bandit14.

![Screenshot 2021-03-03 at 12 22 32 AM](https://user-images.githubusercontent.com/32232422/109775660-a2c4c180-7bb6-11eb-9686-9c2151aa6604.png)

The password is `4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e`.

## Level 15
The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost. We can send data by using `echo` to send data and [netcat](https://en.wikipedia.org/wiki/Netcat) `nc` to connect to the localhost. Ip address for the localhost is 127.0.0.1.

![Screenshot 2021-03-03 at 12 51 14 AM](https://user-images.githubusercontent.com/32232422/109783010-5d0bf700-7bbe-11eb-91a4-348bb6faae34.png)

The password is `BfMYroe26WYalil77FoDi9qh59eK5xNr`.

## Level 16
The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption. We can use `openssl s_client` to connect to the server that use SSL. Netcat does not support SSL.

```
echo "BfMYroe26WYalil77FoDi9qh59eK5xNr" | openssl s_client -connect 127.0.0.1:30001 -ign_eof
```
or
```
echo "BfMYroe26WYalil77FoDi9qh59eK5xNr" | openssl s_client -connect 127.0.0.1:30001 -quiet
```
You can see the password if you scroll untill the bottom. `-ign_eof` is for inhibit shutting down the connection when end of file is reached in the input. We also can use `-quiet` and the function same like `-ign_eof` but it does not print session and certification information.

The password is `cluFn7wTiGryunymYOu4RcffSxQluehd`.

## Level 17
The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000.
1. Find out which ports is exists
2. Then find port who speak on SSL
3. Only one port will give the password, other will send back whatever you give.

To find open port in range 31000-32000 on server, we can use [`nmap`](https://en.wikipedia.org/wiki/Nmap) to scan port on the network.
```
nmap -sV -T4 -v -p 31000-32000 127.0.0.1 
```
- `-sV` : scan service
- `-T4` : Speed time
- `-v` : verbose mode
- `-p` : specify port range
- `127.0.0.1` : localhost ip address

If we scroll down, we'll there are 5 ports open, and two ports have SSL. One is SSl/echo and one is SSl/unknown.

![Screenshot 2021-03-03 at 7 50 20 AM](https://user-images.githubusercontent.com/32232422/109832365-1eddfa00-7bf5-11eb-8f57-930aab269913.png)

We can try both ports, and the right one will not print back the data you sent before.
```
echo "cluFn7wTiGryunymYOu4RcffSxQluehd" | openssl s_client -connect 127.0.0.1:31790 -quiet
```

![Screenshot 2021-03-03 at 7 55 58 AM](https://user-images.githubusercontent.com/32232422/109833530-310c6800-7bf6-11eb-8999-1c3cc30f0c9b.png)

Now just copy the RSA KEY and save into a file name sshkey2.private or anything you like, give read and write permission using [chmod](https://www.cyberciti.biz/faq/unix-linux-bsd-chmod-numeric-permissions-notation-command/), and try to connect to the server with bandit17 user.

```
chmod 600 sshkey2.private
ssh -i sshkey2.private bandit17@bandit.labs.overthewire.org -p 2220
```

And thats it

## Level 18
There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new. You can use `diff` to find the difference in both files.

```
diff passwords.old passwords.new
```

![Screenshot 2021-03-03 at 5 32 21 PM](https://user-images.githubusercontent.com/32232422/109897861-30042680-7c48-11eb-88ab-5979e7af0e51.png)

The password is `kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd`.
 
## Level 19
The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH. We have to ssh to server using `bash --noprofile` to start a shell without any user configuration since someone already modified bash configuration. [Read more here](https://superuser.com/questions/1277825/ssh-automatically-logging-out) and [here](https://stackoverflow.com/questions/9357464/how-to-start-a-shell-without-any-user-configuration).
 
```
ssh bandit18@bandit.labs.overthewire.org -p 2220 "bash --noprofile --norc"
```
 
![Screenshot 2021-03-03 at 5 50 44 PM](https://user-images.githubusercontent.com/32232422/109899080-2085dd00-7c4a-11eb-9288-747f406e0906.png)

The password is `IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x`.

## Level 20
To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary. After login, you can see there is a binary file. If we try to run, it says to give any command to run as other user.

![Screenshot 2021-03-03 at 6 23 44 PM](https://user-images.githubusercontent.com/32232422/109901378-d0a91500-7c4d-11eb-9f16-a8faa8dab753.png)

When we try to read the password on `/etc/bandit_pass/bandit20`, it says permission denied. We dont have permission to read the password. Noted that when we  use `ls -la` to check permission on password file, we can see only group `bandit20` can read the password file. Thats why we cannot read the password file since we are bandit19.

![Screenshot 2021-03-03 at 6 13 44 PM](https://user-images.githubusercontent.com/32232422/109902054-b9b6f280-7c4e-11eb-9356-2b2748518b34.png)

But when we check permission on binary file, it has group bandit20, thus, we can read the password by using `bandit20-do`.

```
./bandit20-do cat /etc/bandit_pass/bandit20
```

![Screenshot 2021-03-03 at 6 14 09 PM](https://user-images.githubusercontent.com/32232422/109902952-00f1b300-7c50-11eb-9232-40554dc6a301.png)

The password is `GbKksEFF4yrVs6il55v6gwY5aVje5f0j`.

## Level 21
There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21). This level need you to run two separate terminal or split the terminal to see the differences. Im using iTerm2 to split the window, you can use Tmux or other terminal emulator.

![Screenshot 2021-03-03 at 9 24 35 PM](https://user-images.githubusercontent.com/32232422/109915809-4e2d4f00-7c67-11eb-8e7a-2f5b87fa1c9f.png)

First, on the left side, we gonna set a listener using `nc` on port 1234. You can use any port except other than already used by this server. Then on the right side, we gonna connect to the port 1234 using `./suconnect`.

![Screenshot 2021-03-03 at 9 24 52 PM](https://user-images.githubusercontent.com/32232422/109916194-09ee7e80-7c68-11eb-8ec8-e43e0b68c80f.png)

After that, one the left side, copy bandit20 password and paste on the terminal and press enter.

![Screenshot 2021-03-03 at 9 26 17 PM](https://user-images.githubusercontent.com/32232422/109916264-24c0f300-7c68-11eb-9208-078e508be1d0.png)

Then, the suconnect will check if the password is correct or not, icorrect, it will reply bandit21's password.

![Screenshot 2021-03-03 at 9 12 32 PM](https://user-images.githubusercontent.com/32232422/109916366-59cd4580-7c68-11eb-907c-9e30ddac0ffa.png)

 The password is `gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr`.
