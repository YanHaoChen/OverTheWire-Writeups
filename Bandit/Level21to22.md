# [Level 21 -> 22](http://overthewire.org/wargames/bandit/bandit22.html)

定時執行：```cron```。

## Level Goal

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

### Commands you may need to solve this level

cron, crontab, crontab(5) (use “man 5 crontab” to access this)

## Writeups

首先，依提示觀察一下```/etc/cron.d/```：

```shell
bandit21@melinda:/etc/cron.d$ ls
behemoth4_cleanup  cronjob_bandit24       melinda-stats          natas25_cleanup~  semtex0-32   sysstat
cron-apt           cronjob_bandit24_root  natas-session-toucher  natas26_cleanup   semtex0-64   vortex0
cronjob_bandit22   leviathan5_cleanup     natas-stats            natas27_cleanup   semtex0-ppc  vortex20
cronjob_bandit23   manpage3_resetpw_job   natas25_cleanup        php5              semtex5
```

每一個檔案，敘述著個別在特定時間要做什麼事情。來看有關此關的敘述```cronjob_bandit22```：

```shell
bandit21@melinda:/etc/cron.d$ cat cronjob_bandit22
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

我們可以發現，```bandit22```不斷在執行```/usr/bin/cronjob_bandit22.sh```。就讓我們看看它到底做了什麼：

```shell
bandit21@melinda:/etc/cron.d$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

看來一切的答案，就放在```/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv```裡面：

```shell
bandit21@melinda:/etc/cron.d$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
```

成功取得 Flag：```Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI```。

> [Next level（Level 22 -> 23）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level22to23.md) 
