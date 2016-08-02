# [Level 19 -> 20](http://overthewire.org/wargames/bandit/bandit20.html)

瞭解```setuid```。

## Level Goal

To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used to setuid binary.

### Helpful Reading Material

> [setuid on Wikipedia](http://en.wikipedia.org/wiki/Setuid)

## Writeups

此題最主要的目的，就是讓闖關者，可以知道```setuid```。在目錄中的```bandit20-do```就是一個示範：

```shell
bandit19@melinda:~$ ls -la
total 28
drwxr-xr-x   2 root     root     4096 Nov 14  2014 .
drwxr-xr-x 172 root     root     4096 Jul 10 14:12 ..
-rw-r--r--   1 root     root      220 Apr  9  2014 .bash_logout
-rw-r--r--   1 root     root     3637 Apr  9  2014 .bashrc
-rw-r--r--   1 root     root      675 Apr  9  2014 .profile
-rwsr-x---   1 bandit20 bandit19 7370 Nov 14  2014 bandit20-do
bandit19@melinda:~$ ./bandit20-do
Run a command as another user.
  Example: ./bandit20-do id
```

我們可以發現檔案```bandit20-do```的擁有者權限第三格為```s```，也代表他在執行時，有著```setuid```的特性，也就是不管誰執行它，都會以擁有者的權限執行。所以我們現在可以用```bandit19```的權限，執行```bandit20-do```，並提取只有```bandit20```才能打開的```/etc/bandit_pass/bandit20```：

```
bandit19@melinda:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```

很順利！這關的 Flag 是：```GbKksEFF4yrVs6il55v6gwY5aVje5f0j```。

> [Next level（Level 20 -> 21）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level20to21.md) 
