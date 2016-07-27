# [Level 2 -> 3](http://overthewire.org/wargames/bandit/bandit3.html)

 一樣是檔名的問題，這次跟空白有關。

## Level Goal

The password for the next level is stored in a file called spaces in this filename located in the home directory

### Commands you may need to solve this level

ls, cd, cat, file, du, find

## Writeups

以使用者 bandit2 的帳號登入 bandit.labs.overthewire.org：

```shell
$ ssh -l bandit2 bandit.labs.overthewire.org
```
輸入完密碼（也就是剛剛在 bandit1 中獲得的 Flag），一樣先使用```ls```瀏覽目前目錄開始：

```shell
bandit2@melinda:~$ ls
spaces in this filename
```
乍看起來，或許不止一個檔案。所以再試著確認一下：

```shell
bandit2@melinda:~$ ls -la
total 24
drwxr-xr-x   2 root    root    4096 Nov 14  2014 .
drwxr-xr-x 172 root    root    4096 Jul 10 14:12 ..
-rw-r--r--   1 root    root     220 Apr  9  2014 .bash_logout
-rw-r--r--   1 root    root    3637 Apr  9  2014 .bashrc
-rw-r--r--   1 root    root     675 Apr  9  2014 .profile
-rw-r-----   1 bandit3 bandit2   33 Nov 14  2014 spaces in this filename
```
可以確認他是一個檔案了，現在想辦法打開它。以往的經驗來說，應該是這樣開的：

```shell
bandit2@melinda:~$ cat spaces in this filename
cat: spaces: No such file or directory
cat: in: No such file or directory
cat: this: No such file or directory
cat: filename: No such file or directory
```
可以發現```cat```將空白認為是把多個檔案分開的用的符號，所以才會出現這些訊息回報。檔名有空白，我們需要換成這樣的方式：

```shell
bandit2@melinda:~$ cat spaces\ in\ this\ filename
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```
這樣就可以成功打開這個檔案，並得到第三組的 Flag：```UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK ```。
