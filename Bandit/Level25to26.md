# [Level 25 -> 26](http://overthewire.org/wargames/bandit/bandit26.html)

想也沒想到，編輯器那麼好用。

## Level Goal

Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.

## Writeups

這題的提示不多，只說從```bandit25```登入```bandit26```很簡單。讓我們來看看```bandit25```有什麼：

```shell
bandit25@melinda:~$ ls
bandit26.sshkey
```
感覺起來，應該可以直接```ssh```進去：

```shell
bandit25@melinda:~$ ssh -i bandit26.sshkey -l bandit26 127.0.0.1
...
...
 For questions or comments, contact us through IRC on
  irc.overthewire.org.


  _                     _ _ _   ___   __
 | |                   | (_) | |__ \ / /
 | |__   __ _ _ __   __| |_| |_   ) / /_
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/
Connection to 127.0.0.1 closed.
```

果然沒有那麼簡單... 提示指出我們看到的並不是```/bin/bash```，而是其他的東西...。為了知道是什麼，我們從```/etc/passwd```下手，找出```bandit26```登入時會發生什麼事：

```shell
bandit25@melinda:~$ cat /etc/passwd | grep bandit26
bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
```

果然跟我們想的差很多，不是```/bin/bash```而是```/usr/bin/showtext```。讓我們來看看```/usr/bin/showtext```做了些什麼：

```shell
bandit25@melinda:~$ cat /usr/bin/showtext
#!/bin/sh

more ~/text.txt
exit 0
```

原來只是讓我們看到一堆文字而已。但在此使用到```more```反而是讓我們可以動手腳的地方。因為```more```在使用的期間，可以鍵入```v```開啟文字編輯器，讓我們可以好好利用。首先，把 terminal 輸出行數小於我們看到的```text.txt```，再連線一次：

```shell
ssh -i bandit26.sshkey -l bandit26 127.0.0.1:
...
...
  _                     _ _ _   ___   __
 | |                   | (_) | |__ \ / /
 | |__   __ _ _ __   __| |_| |_   ) / /_
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
--More--(83%)
```

輸入```v```，進入編輯器模式：

```shell
  _                     _ _ _   ___   __
 | |                   | (_) | |__ \ / /
 | |__   __ _ _ __   __| |_| |_   ) / /_
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
"~/text.txt" [readonly] 6L, 258C                                                            1,3           Top
```
輸入```:```執行讀取指令，讀取```/etc/bandit_pass/bandit26```：

```shell
  _                     _ _ _   ___   __
 | |                   | (_) | |__ \ / /
 | |__   __ _ _ __   __| |_| |_   ) / /_
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
:r /etc/bandit_pass/bandit26
```

持續按```enter```讀完內容，最後就可以到 Flag 了：

```shell
  _                     _ _ _   ___   __
5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z
 | |                   | (_) | |__ \ / /
 | |__   __ _ _ __   __| |_| |_   ) / /_
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \
                                                                                            4,1           Top
```

終於找到了！Flag：```5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z```。
