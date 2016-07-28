# [Level 0 -> 1](http://overthewire.org/wargames/bandit/bandit1.html)

在這題中，學習基本的檔案讀取（```ls```、```cat```）。

## Level Goal

The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH to log into that level and continue the game.

### Commands you may need to solve this level

ls, cd, cat, file, du, find

## Writeups

首先，以使用者 bandit0 的帳號登入 bandit.labs.overthewire.org：

```shell
$ ssh -l bandit0 bandit.labs.overthewire.org
```
輸入完密碼，就可以開始找提示中所提到的 **readme** 囉！先使用```ls```瀏覽目前目錄開始：

```shell
bandit0@melinda:~$ ls
readme
```
可以發現 **readme** 的確在當前的目錄中。接下來看看裡面寫了些什麼。在這裡，我們使用```cat```：

```shell
bandit0@melinda:~$ cat readme
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```

一切都很順利。也恭喜取得第一組 Flag：```boJ9jbbUNNfktd78OOpsqOltutMc3MY1```。
> [Next level（Level 1 -> 2）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level1to2.md) 
