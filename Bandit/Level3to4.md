# [Level 3 -> 4](http://overthewire.org/wargames/bandit/bandit4.html)

 找到躲起來的檔案。

## Level Goal

The password for the next level is stored in a hidden file in the inhere directory.


### Commands you may need to solve this level

ls, cd, cat, file, du, find

## Writeups

先使用```ls```瀏覽目前目錄開始：

```shell
bandit3@melinda:~$ ls
inhere
```
很順利的找到```inhere```這個目錄。接著我們進去目錄裡，找找隱藏起來的檔案：

```shell
bandit3@melinda:~$ cd inhere/
bandit3@melinda:~/inhere$
```
還是先例行慣例，先執行```ls```看看：

```shell
bandit3@melinda:~/inhere$ ls
bandit3@melinda:~/inhere$
```

是空的，但題目本來就說隱藏起來了，這一切感覺很正常。接下來直接使用```ls -la```找找看吧：

```shell
bandit3@melinda:~/inhere$ ls -la
total 12
drwxr-xr-x 2 root    root    4096 Nov 14  2014 .
drwxr-xr-x 3 root    root    4096 Nov 14  2014 ..
-rw-r----- 1 bandit4 bandit3   33 Nov 14  2014 .hidden
```
很高興，我們找到它了（```.hidden```）。現在用老方法```cat```Flag 出來：

```shell
bandit3@melinda:~/inhere$ cat .hidden
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```
恭喜！得到第四組的 Flag：```pIwrPrtPN36QITSp3EQaw936yaFoFgAB```。
> [Next level（Level 4 -> 5）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level4to5.md) 
