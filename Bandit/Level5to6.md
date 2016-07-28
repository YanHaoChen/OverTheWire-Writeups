# [Level 5 -> 6](http://overthewire.org/wargames/bandit/bandit4.html)

找到特定大小的檔案。

## Level Goal

The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties: - human-readable - 1033 bytes in size - not executable




### Commands you may need to solve this level

ls, cd, cat, file, du, find


## Writeups

登入後，進入目錄```inhere```：

```shell
bandit5@melinda:~$ cd inhere/
bandit5@melinda:~/inhere$
```
一樣先執行```ls```看看：

```shell
bandit5@melinda:~/inhere$ ls
maybehere00  maybehere03  maybehere06  maybehere09  maybehere12  maybehere15  maybehere18
maybehere01  maybehere04  maybehere07  maybehere10  maybehere13  maybehere16  maybehere19
maybehere02  maybehere05  maybehere08  maybehere11  maybehere14  maybehere17
```

迎面而來的是一堆資料夾，遇到這種狀況就要善用指令```find```，並依提示（1033bytes）進行搜尋：

```shell
bandit5@melinda:~/inhere$ find ./ -type f -size 1033c
./maybehere07/.file2
```

這樣就可以很快速的找到它了（```./maybehere07/.file2```）！
>-size 參數的使用方式
>
> -size n[ckMGTP]
> 
> True if the file's size, rounded up, in 512-byte blocks  is n.  If n is followed by a c, then the primary is true if the file's size is n bytes (characters). Similarly if n is followed by a scale indicator then the file's size is compared to n scaled as:
> 
> ```
>            k       kilobytes (1024 bytes)
>            M       megabytes (1024 kilobytes)
>            G       gigabytes (1024 megabytes)
>            T       terabytes (1024 gigabytes)
>            P       petabytes (1024 terabytes)
>```

用一個比較有趣的方式把它```cat```出來：

```shell
bandit5@melinda:~/inhere$ find ./ -type f -size 1033c -exec cat '{}' \;
DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```
參數```-exec```後面可以接，找到符合的檔案後要執行的指令。```'{}'```則代表找到的檔案本身，最後記得加上```\;```代表```-exec```的結尾。

恭喜！得到第六組的 Flag：```DXjZPULLxYr17uwoI01bNLQbtFemEgo7```。
