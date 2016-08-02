# [Level 18 -> 19](http://overthewire.org/wargames/bandit/bandit19.html)

對```ssh```下指令，多一些瞭解。

## Level Goal

The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

### Commands you may need to solve this level

ssh, ls, cat

## Writeups

成功登入```bandit18```時，會馬上中斷連線：

```shell
$ ssh -l bandit18 bandit.labs.overthewire.org

This is the OverTheWire game server. More information on http://www.overthewire.org/wargames

Please note that wargame usernames are no longer level<X>, but wargamename<X>
e.g. vortex4, semtex2, ...
...
...
Byebye !

Connection to bandit.labs.overthewire.org closed.
```

現在知道可以登入進去，但會在執行完後中斷連線。所以試著在他還沒中斷連線前，向主機下指令：

```shell
$ ssh -l bandit18 bandit.labs.overthewire.org cat /etc/bandit_pass/bandit18
...
...
bandit18@bandit.labs.overthewire.org's password:
kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
```

> 在指令的後端```cat /etc/bandit_pass/bandit18```，指的是當連線成功後要對目標主機下的指令。

很好，我們成功取得了這關的 Flag：```kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd```。

> [Next level（Level 19 -> 20）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level19to20.md) 
