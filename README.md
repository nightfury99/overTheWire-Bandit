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

