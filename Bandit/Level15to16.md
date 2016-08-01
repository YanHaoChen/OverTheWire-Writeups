# [Level 15 -> 16](http://overthewire.org/wargames/bandit/bandit16.html)

現在嘗試用```SSL```進行連線。

## Level Goal

The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…

### Commands you may need to solve this level

ssh, telnet, nc, openssl, s_client, nmap

### Helpful Reading Material

> [Secure Socket Layer/Transport Layer Security on Wikipedia](http://en.wikipedia.org/wiki/Secure_Socket_Layer) 
> 
> [OpenSSL Cookbook - Testing with OpenSSL](https://www.feistyduck.com/library/openssl-cookbook/online/ch-testing-with-openssl.html)


## Writeups

我們可以利用```openssl s_client```與協定為 SSL 的網路服務進行連線。在此有個關鍵，就是需要使用參數```-ign_eof```接收 server 回傳的 Flag。所以我們的指令為：

```shell
bandit15@melinda:~$ cat /etc/bandit_pass/bandit15 | openssl s_client -connect 127.0.0.1:30001 -ign_eof
CONNECTED(00000003)
depth=0 CN = li190-250.members.linode.com
verify error:num=18:self signed certificate
verify return:1
depth=0 CN = li190-250.members.linode.com
verify return:1
---
Certificate chain
...
...
...
---
Correct!
cluFn7wTiGryunymYOu4RcffSxQluehd

read:errno=0
```
> 也可以嘗試使用```-quiet```取代```-ign_eof```，可以幫你省略很多不必要的資訊。 

這題的 Flag 是：```cluFn7wTiGryunymYOu4RcffSxQluehd```。

> [Next level（Level 16 -> 17）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level16to17.md) 
