# [Level 1 -> 2](http://overthewire.org/wargames/bandit/bandit2.html)

奇耙的檔案名稱`-`，再加上```cat```的業障太重。

## Level Goal

The password for the next level is stored in a file called - located in the home directory
### Commands you may need to solve this level

ls, cd, cat, file, du, find

### Helpful Reading Material

>[Google Search for “dashed filename”](https://www.google.com/search?q=dashed+filename)
>
>[Advanced Bash-scripting Guide - Chapter 3 - Special Characters](http://tldp.org/LDP/abs/html/special-chars.html)

## Writeups

首先，以使用者 bandit1 的帳號登入 bandit.labs.overthewire.org：

```shell
$ ssh -l bandit1 bandit.labs.overthewire.org
```
輸入完密碼（也就是剛剛在 bandit0 中獲得的 Flag），一樣先使用```ls```瀏覽目前目錄開始：

```shell
bandit1@melinda:~$ ls
-
```
看到的東西沒有錯，就只有 **-** 這樣。既然提示都說密碼在這個檔案裡了，就不管什麼先```cat```下去好了：

```shell
bandit1@melinda:~$ cat -

```
恩...```cat```停住了。只好乖乖的看 **Helpful Reading Material** 的提示，Google 搜尋 **dashed filename**。這下才知道 **-** 是特殊字元，會影響```cat```判讀，把 **-** 當成給予參數時的特殊字元，而不是我們希望它讀取的檔案名稱。

### 消除```cat```的業障
這時候只要明確的指出檔案的絕對目錄位置即可。先使用```pwd```得知目前目錄的絕對位置，然後使用```cat```：

```shell
bandit1@melinda:~$ pwd
/home/bandit1
bandit1@melinda:~$ cat /home/bandit1/-
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```
或者直接用這樣的方式：

```shell
bandit1@melinda:~$ cat ./-
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```
就可以成功消除```cat```的業障，讓它告訴你第二組的 Flag：```CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9```。
> [Next level（Level 2 -> 3）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level2to3.md) 
