# [Level 0](http://overthewire.org/wargames/bandit/bandit0.html)

在這題中，其實就是學習基本的```ssh```指令運用。

## Level Goal

The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

### Commands you may need to solve this level

ssh

## Writeups

確定安裝好 ssh 後，打開 terminal 並輸入：

```shell
//方法一
$ ssh bandit0@bandit.labs.overthewire.org

//方法二
$ ssh -l bandit0 bandit.labs.overthewire.org
``` 
以使用者 bandit0 登入 bandit.labs.overthewire.org。這時候他會要求你輸入密碼，就像 Level Goal 中提示的一樣：```bandit0```

```shell
...

bandit0@bandit.labs.overthewire.org's password:
```
輸入完後，恭喜你過了 Level 0！

```shell
bandit0@melinda:~$
```