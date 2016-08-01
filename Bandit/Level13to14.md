# [Level 13 -> 14](http://overthewire.org/wargames/bandit/bandit14.html)

使用```ssh```的不同方式。

## Level Goal

The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on


### Commands you may need to solve this level

ssh, telnet, nc, openssl, s_client, nmap

### Helpful Reading Material

> [SSH/OpenSSH/Keys](https://help.ubuntu.com/community/SSH/OpenSSH/Keys)

## Writeups

你可以發現，```sshkey```就在目錄裡：

```shell
bandit13@melinda:~$ ls
sshkey.private
```

接下來，連過去就是了。我們需要參數```-i```讓連線夾帶```sshkey```：

```shell
bandit13@melinda:~$ ssh -i sshkey.private bandit14@127.0.0.1
```

這題沒有直接給你 Flag，但還是恭喜你，通過了。

> [Next level（Level 14 -> 15）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level14to15.md) 
