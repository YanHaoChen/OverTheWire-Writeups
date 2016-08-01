# [Level 11 -> 12](http://overthewire.org/wargames/bandit/bandit12.html)

Rot13 編碼。

## Level Goal

The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions


### Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

### Helpful Reading Material

> [Rot13 on Wikipedia](http://en.wikipedia.org/wiki/Rot13)

## Writeups

使用```tr```進行交換對應字母：

```shell
bandit11@melinda:~$ cat data.txt | tr '[a-m][n-z][A-M][N-Z]' '[n-z][a-m][N-Z][A-M]'
The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
```

第十二組的 Flag：```5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu```。

> [Next level（Level 12 -> 13）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level12to13.md) 
