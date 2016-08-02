# [Level 16 -> 17](http://overthewire.org/wargames/bandit/bandit17.html)

使用```nmap```掃描網路服務。

## Level Goal

The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

### Commands you may need to solve this level

ssh, telnet, nc, openssl, s_client, nmap

### Helpful Reading Material

> [Port scanner on Wikipedia](http://en.wikipedia.org/wiki/Port_scanner) 
> 
> [OpenSSL Cookbook - Testing with OpenSSL](https://www.feistyduck.com/library/openssl-cookbook/online/ch-testing-with-openssl.html)


## Writeups

提示中，提到網路服務開在```31000-32000 port```之間，且只有其中一個```port```會在你輸入正確 Flag 後，給你下一關的 sshkey。先解決第一件事情，找到有哪些```port```是開著的。在此我們使用```nmap```：

```shell
bandit16@melinda:~$ nmap 127.0.0.1 -p 31000-32000

Starting Nmap 6.40 ( http://nmap.org ) at 2016-08-02 06:57 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00064s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 0.11 seconds
```

接下來一個一個嘗試，發現```31790```就是我們要找的：

```shell
bandit16@melinda:~$ cat /etc/bandit_pass/bandit16 | openssl s_client -connect 127.0.0.1:31790 -quiet
depth=0 CN = li190-250.members.linode.com
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = li190-250.members.linode.com
verify return:1
Correct!
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----

read:errno=0
```

接下來就是把鑰匙存下來，來登入```bandit17```囉：

```shell
bandit16@melinda:~$ mkdir /tmp/savekeyto17
bandit16@melinda:~$ cd /tmp/savekeyto17
bandit16@melinda:/tmp/savekeyto17$ cat /etc/bandit_pass/bandit16 | openssl s_client -connect 127.0.0.1:31790 -quiet > sshkey17
depth=0 CN = li190-250.members.linode.com
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = li190-250.members.linode.com
verify return:1
read:errno=0
```

但沒辦法直接使用這隻鑰匙，因為他的權限問題：

```shell
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0664 for 'sshkey17' are too open.
It is required that your private key files are NOT accessible by others.
```

所以我們現在更改一下鑰匙的權限，改成只有擁有者可以讀寫：

```shell
bandit16@melinda:/tmp/savekeyto17$ chmod 600 sshkey17
bandit16@melinda:/tmp/savekeyto17$ ls -la
total 7868
drwxrwxr-x 2 bandit16 bandit16    4096 Aug  2 07:10 .
drwxrwx-wt 1 root     root     8036352 Aug  2 07:16 ..
-rw------- 1 bandit16 bandit16    1685 Aug  2 07:10 sshkey17
```

接著```ssh```進入```bandit17```:

```shell
bandit16@melinda:/tmp/savekeyto17$ ssh -l bandit17 -i sshkey17 127.0.0.1
...
...
bandit17@melinda:~$
```

成功登入囉！接下來光明正大取出這題的 Flag：

```shell
bandit17@melinda:~$ cat /etc/bandit_pass/bandit17
xLYVMN9WE5zQ5vHacb0sZEVqbrp7nBTn
```

> [Next level（Level 17 -> 18）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level17to18.md) 
