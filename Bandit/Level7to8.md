# [Level 7 -> 8](http://overthewire.org/wargames/bandit/bandit8.html)

是時候學習```grep```了。

## Level Goal

The password for the next level is stored in the file data.txt next to the word **millionth**


### Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

## Writeups

首先，看看```data.txt```的資料是長什麼樣子。使用```head```觀察前十行的資料：

```shell
bandit7@melinda:~$ head -n 10 data.txt
Kunming's	0D0KZ3TdLRBXD8lyd7Bj2hAqnxaMInQe
multitude's	8MFZa8yOjTt6m8PvxteTp7XTDFLiuFAk
audibility	ZeLj0yAw7ylmEoLxSUEqF4iB43c9DN4h
unadvised	Pgp8X2LSVdNrmIKcJ7Oe8eqTzEVfhGbR
Brecht's	uKyKryNUZYFuTQpwRlDqucLLIUbiIMF0
Alvin	IpQIV6mpjticdB790obqXAvYkAgnDV8E
insufficient	cgHhWVJahfDqFIe82vOliryQQ8ihGlGN
Sauterne	UhPBp0A04GkIRfvZnUt1UdwlKU2ViYUd
cluster	1GeFZ0B6rsEtJ5Sqb5h8Wv7UwG15DQzb
ember's	f2XPIE1iDHW9oHPyodPyfTz87DAbWmXu
```

我們可以發現資料的格式是這樣子的：

```shell
[單字] [雜湊字串]
```

依提示，找單字是```millionth```的雜湊字串，就是這題的 Flag。透過```grep```可以很簡單地達到這個目的：

```shell
bandit7@melinda:~$ cat data.txt | grep millionth
millionth	cvX2JJa4CFALtqS87jk27qwqGhBM9plV
```

恭喜！得到第八組的 Flag：```cvX2JJa4CFALtqS87jk27qwqGhBM9plV```。

> [Next level（Level 8 -> 9）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level8to9.md) 
