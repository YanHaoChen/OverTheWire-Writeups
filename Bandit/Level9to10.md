# [Level 9 -> 10](http://overthewire.org/wargames/bandit/bandit10.html)

用```strings```找```human-readable```的字串，串其實很簡單。

## Level Goal

The password for the next level is stored in the file data.txt in one of the few human-readable strings, beginning with several ‘=’ characters.



### Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

## Writeups

用```strings```就可以直接找出檔案中```human-readable```的字串：

```shell
bandit9@melinda:~$ strings data.txt
}g(sn
6I5O
epr~F=K
 $ly
6yHYKqt\T8sb
7?YD=
)ux(
...
...
```

接下來，依第二個提示，利用```grep```找尋開頭是```=```的字串：

```shell
bandit9@melinda:~$ strings data.txt | grep ^=
========== password
========== ism
========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
```

恭喜！找到了第十組的 Flag：```truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk```。

> [Next level（Level 10 -> 11）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level10to11.md) 
