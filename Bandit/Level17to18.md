# [Level 17 -> 18](http://overthewire.org/wargames/bandit/bandit18.html)

使用```diff```比較新舊檔案差異的地方。

## Level Goal

There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19

### Commands you may need to solve this level

cat, grep, ls, diff

## Writeups

這題解題很快，只需要這樣：

```shell
bandit17@melinda:~$ ls
passwords.new  passwords.old
bandit17@melinda:~$ diff passwords.new passwords.old
42c42
< kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
---
> BS8bqB1kqkinKJjuxL6k072Qq9NRwQpR
```
箭頭```<```指出的是```password.new```，箭頭```>```則是指```passwords.old```。所以這題的 Flag 就是：```kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd```。

> [Next level（Level 18 -> 19）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level18to19.md) 
