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
- find : command to find
- .(dot) : current directory
- 1033c : 1033 byte, c = byte, k = kilo can refer [here](https://ostechnix.com/find-files-bigger-smaller-x-size-linux/)
- -exec ls -sh {} + : list all file under directory with file size
- | : let you to have two or more command in one line
- grep -i : filter only ascii and ignore case sensitive

Only one file listed and you can read the file.

![Screenshot 2021-03-01 at 8 16 15 PM](https://user-images.githubusercontent.com/32232422/109597232-b1cf4500-7acc-11eb-98d3-2f75b65c4c93.png)

The password is `DXjZPULLxYr17uwoI01bNLQbtFemEgo7`.
