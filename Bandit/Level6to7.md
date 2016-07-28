# [Level 6 -> 7](http://overthewire.org/wargames/bandit/bandit6.html)

再學多一點```find```的使用方式。

## Level Goal

The password for the next level is stored somewhere on the server and has all of the following properties: - owned by user bandit7 - owned by group bandit6 - 33 bytes in size

### Commands you may need to solve this level

ls, cd, cat, file, du, find, grep

## Writeups

這題的提示其實都可以當成```find```的搜尋參數，所以我們就直接使用```find```來找 Flag 吧：

```shell
find / -user bandit7 -group bandit6 -size 33c -exec ls -la '{}' \;
...
...
-rw-r----- 1 bandit7 bandit6 33 Nov 14  2014 /var/lib/dpkg/info/bandit7.password
...
```

加上了```ls -la```，在第一時間確認搜尋到的檔案是否符合我們要找的檔案。確認完後，就可以把 Flag```cat```出來：

```shell
bandit6@melinda:~$ cat /var/lib/dpkg/info/bandit7.password
HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
```

恭喜！得到第七組的 Flag：```HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs```。

> [Next level（Level 7 -> 8）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level7to8.md) 
