# [Level 4 -> 5](http://overthewire.org/wargames/bandit/bandit4.html)

辨別檔案型別。

## Level Goal

The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.




### Commands you may need to solve this level

ls, cd, cat, file, du, find


## Writeups

先使用```ls```瀏覽目前目錄開始：

```shell
bandit3@melinda:~$ ls
inhere
```
接著進入目錄```inhere```：

```shell
bandit4@melinda:~$ cd inhere/
bandit4@melinda:~/inhere$
```
還是先例行慣例，先執行```ls```看看：

```shell
bandit4@melinda:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
```

看到這一幕，第一個想到的應該就是一個一個慢慢找。但其實我們可以不用這麼做，因為關鍵的提示```human-readable```。所以我是這樣做的：

```shell
bandit4@melinda:~/inhere$ file ./-file*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```
使用```file```，識別每個檔案的型別。我們可以發現```-file07```的型別是```ASCII text```，這應該就是所謂的```human-readable```的檔案。所以我們直接```cat```它看看：

```shell
bandit4@melinda:~/inhere$ cat ./-file07
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```
的確找到它了，恭喜！得到第五組的 Flag：```koReBOKuIDDepwhWk7jZC0RTdopnAYKh```。
