# [Level 22 -> 23](http://overthewire.org/wargames/bandit/bandit23.html)

接下來開始，需要對 shell script 有些瞭解。

## Level Goal

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.



### Commands you may need to solve this level

cron, crontab, crontab(5) (use “man 5 crontab” to access this)

## Writeups

這題依然跟```cron```有關，就讓我們直接看看```cronjob_bandit23```在做什麼：

```shell
bandit22@melinda:/etc/cron.d$ cat cronjob_bandit23
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
bandit22@melinda:/etc/cron.d$ cat /usr/bin/cronjob_bandit23.sh
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

照邏輯來說，答案就藏在```/tmp/$mytarget```中。所以我們需要知道```$mytarget```到底是什麼。最簡單的方式，就是讓電腦跑一次：


```shell
bandit22@melinda:/etc/cron.d$ echo I am user bandit23 | md5sum | cut -d ' ' -f 1
8ca319486bfbbc3663ea0fbe81326349
bandit22@melinda:/etc/cron.d$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n
```

Flag：```jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n```。

> [Next level（Level 23 -> 24）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level23to24.md) 
