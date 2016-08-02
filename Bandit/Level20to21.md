# [Level 20 -> 21](http://overthewire.org/wargames/bandit/bandit21.html)

先前的```nc```及```setuid```混搭。

## Level Goal

There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

NOTE: To beat this level, you need to login twice: once to run the setuid command, and once to start a network daemon to which the setuid will connect.

NOTE 2: Try connecting to your own network daemon to see if it works as you think

### Commands you may need to solve this level

ssh, nc, cat

## Writeups

首先，瞭解一下```suconnect```：

```shell
bandit20@melinda:~$ ls -la
total 28
drwxr-xr-x   2 root     root     4096 Nov 14  2014 .
drwxr-xr-x 172 root     root     4096 Jul 10 14:12 ..
-rw-r--r--   1 root     root      220 Apr  9  2014 .bash_logout
-rw-r--r--   1 root     root     3637 Apr  9  2014 .bashrc
-rw-r--r--   1 root     root      675 Apr  9  2014 .profile
-rwsr-x---   1 bandit21 bandit20 8006 Nov 14  2014 suconnect
bandit20@melinda:~$ ./suconnect
Usage: ./suconnect <portnumber>
This program will connect to the given port on localhost using TCP. If it receives the correct password from the other side, the next password is transmitted back.
```

很明顯的，我們需要開啟一個網路服務監聽，讓```suconnect```把密碼吐出來。先來執行第一步，開啟一個網路服務，並在他人連線進來時回傳 Flag：

```shell
bandit20@melinda:~$ nc -l 127.0.0.1 33333 < /etc/bandit_pass/bandit20

```

現在開啟另一個 terminal 登入```bandit20```，執行```suconnect```：

```shell
bandit20@melinda:~$ ./suconnect 33333
Read: GbKksEFF4yrVs6il55v6gwY5aVje5f0j
Password matches, sending next password
```

現在看回執行網路服務的 terminal：

```shell
bandit20@melinda:~$ nc -l 127.0.0.1 33333 < /etc/bandit_pass/bandit20
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr
```

成功取得 Flag：```gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr```。

> [Next level（Level 21 -> 22）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level21to22.md) 
