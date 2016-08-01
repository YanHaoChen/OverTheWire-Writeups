# [Level 14 -> 15](http://overthewire.org/wargames/bandit/bandit15.html)

有趣的工具```nc```。

## Level Goal

The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

### Commands you may need to solve this level

ssh, telnet, nc, openssl, s_client, nmap

### Helpful Reading Material

> [How the Internet works in 5 minutes (YouTube)](https://www.youtube.com/watch?v=7_LPdttKXPc) (Not completely accurate, but good enough for beginners)
> 
> [IP Addresses](http://computer.howstuffworks.com/web-server5.htm)
> 
> [IP Address on Wikipedia](http://en.wikipedia.org/wiki/IP_address)
> 
> [Localhost on Wikipedia](http://en.wikipedia.org/wiki/IP_address)
> 
> [Ports](http://computer.howstuffworks.com/web-server8.htm)
> 
> [Port (computer networking) on Wikipedia](http://en.wikipedia.org/wiki/Port_(computer_networking))

## Writeups

我們可以利用```nc```輕易的進行網路服務監聽或者資料傳送。在這題，就是要我們將```bandit14```的 Flag 餵給```port 30000```。所以我們這麼做： 

```shell
bandit14@melinda:~$ cat /etc/bandit_pass/bandit14 | nc 127.0.0.1 30000
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
```
又再次看到 Flag 了，這題的 Flag 是：```BfMYroe26WYalil77FoDi9qh59eK5xNr```。

> [Next level（Level 15 -> 16）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level15to16.md) 
