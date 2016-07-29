# [Level 8 -> 9](http://overthewire.org/wargames/bandit/bandit9.html)

現在需要使用```uniq```，區分檔案內不同的地方及重複狀況。

## Level Goal

The password for the next level is stored in the file data.txt and is the only line of text that occurs only once


### Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

### Helpful Reading Material

> [The unix commandline: pipes and redirects](http://www.westwind.com/reference/os-x/commandline/pipes.html)

## Writeups

為了要快速辨別檔案內的字串出現次數，我們可以使用```uniq```，也記得```uniq```是需要跟```sort```一起用才會有效果：

```shell
bandit8@melinda:~$ sort data.txt | uniq -u
UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```

使用參數```-u```，是要顯示只出現一次的字串，也就是第九組的 Flag：```UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR```。

> [Next level（Level 9 -> 10）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level9to10.md) 
