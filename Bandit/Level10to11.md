# [Level 10 -> 11](http://overthewire.org/wargames/bandit/bandit11.html)

解碼被```Base64```編碼過的文字。

## Level Goal

The password for the next level is stored in the file data.txt, which contains base64 encoded data


### Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

### Helpful Reading Material

> [Base64 on Wikipedia](http://en.wikipedia.org/wiki/Base64)

## Writeups

要解碼```base64```很簡單，只需要這樣：

```shell
bandit10@melinda:~$ base64 -d data.txt
The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
```

第十一組的 Flag：```IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR```。

> [Next level（Level 11 -> 12）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level11to12.md) 
