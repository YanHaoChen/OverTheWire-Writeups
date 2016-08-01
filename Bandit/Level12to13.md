# [Level 12 -> 13](http://overthewire.org/wargames/bandit/bandit13.html)

不斷的解壓縮。

## Level Goal

The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)


### Commands you may need to solve this level

grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd, mkdir, cp, mv

### Helpful Reading Material

> [Hex dump on Wikipedia](http://en.wikipedia.org/wiki/Hex_dump)

## Writeups

因```/home/bandit12```的權限需要 root ，所以我們需要像提示中所說，把檔案移至```tmp```路徑下，才能自在運用、嘗試：

```shell
bandit12@melinda:~$ mkdir /tmp/nullname
bandit12@melinda:~$ cp data.txt /tmp/nullname
bandit12@melinda:~$ cd /tmp/nullname
bandit12@melinda:/tmp/nullname$ ls
data.txt
```

接下來觀察一下```data.txt```是什麼東西：

```shell
bandit12@melinda:/tmp/nullname$ cat data.txt
0000000: 1f8b 0808 34da 6554 0203 6461 7461 322e  ....4.eT..data2.
0000010: 6269 6e00 013f 02c0 fd42 5a68 3931 4159  bin..?...BZh91AY
0000020: 2653 5982 c194 8a00 0019 ffff dbfb adfb  &SY.............
0000030: bbab b7d7 ffea ffcd fff7 bfbf 1feb eff9  ................
0000040: faab 9fbf fef2 fefb bebf ffff b001 3b18  ..............;.
0000050: 6400 001e a000 1a00 6468 0d01 a064 d000  d.......dh...d..
...
...
```

我們可以發現他是一個轉為 hexdump 的檔案。現在我們利用```xxd```把它轉回二進制檔：

```shell
bandit12@melinda:/tmp/nullname$ xxd -r data.txt databin
bandit12@melinda:/tmp/nullname$ ls
data.txt  databin
bandit12@melinda:/tmp/nullname$ file databin
databin: gzip compressed data, was "data2.bin", from Unix, last modified: Fri Nov 14 10:32:20 2014, max compression
```

現出原形了，是一個```gzip```的壓縮檔。我們現在試著解開它看看：

```shell
bandit12@melinda:/tmp/nullname$ gzip -d databin
gzip: databin: unknown suffix -- ignored
```
遇到了```unknown suffix```的狀況。因此再補上副檔名```.gz```試試看：

```shell
bandit12@melinda:/tmp/nullname$ mv databin databin.gz
bandit12@melinda:/tmp/nullname$ ls
data.txt  databin.gz
bandit12@melinda:/tmp/nullname$ gzip -d databin.gz
bandit12@melinda:/tmp/nullname$ ls
data.txt  databin
bandit12@melinda:/tmp/nullname$ file databin
databin: bzip2 compressed data, block size = 900k
```
成功解開了！接下來就是一連串的看檔案類別還有解壓縮：

```shell
bandit12@melinda:/tmp/nullname$ bzip2 -d databin
bzip2: Can't guess original name for databin -- using databin.out
bandit12@melinda:/tmp/nullname$ ls
data.txt  databin.out

bandit12@melinda:/tmp/nullname$ file databin.out
databin.out: gzip compressed data, was "data4.bin", from Unix, last modified: Fri Nov 14 10:32:20 2014, max compression
bandit12@melinda:/tmp/nullname$ zcat databin.out > databin

bandit12@melinda:/tmp/nullname$ file databin
databin: POSIX tar archive (GNU)
bandit12@melinda:/tmp/nullname$ tar -xvf databin
data5.bin

bandit12@melinda:/tmp/nullname$ file data5.bin
data5.bin: POSIX tar archive (GNU)
bandit12@melinda:/tmp/nullname$ tar -xvf data5.bin
data6.bin

bandit12@melinda:/tmp/nullname$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
bandit12@melinda:/tmp/nullname$ bzip2 -d data6.bin
bzip2: Can't guess original name for data6.bin -- using data6.bin.out

bandit12@melinda:/tmp/nullname$ file data6.bin.out
data6.bin.out: POSIX tar archive (GNU)
bandit12@melinda:/tmp/nullname$ tar -xvf data6.bin.out
data8.bin

bandit12@melinda:/tmp/nullname$ file data8.bin
data8.bin: gzip compressed data, was "data9.bin", from Unix, last modified: Fri Nov 14 10:32:20 2014, max compression
bandit12@melinda:/tmp/nullname$ zcat data8.bin > data9

bandit12@melinda:/tmp/nullname$ file data9
data9: ASCII text

bandit12@melinda:/tmp/nullname$ cat data9
The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
```

> 使用```zcat```可以取代加上副檔名```.gz```再使用```gzip```解壓縮的動作。


終於... 取得第十三組的 Flag：```8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL```。


> [Next level（Level 13 -> 14）](https://github.com/YanHaoChen/OverTheWire-Writeups/blob/master/Bandit/Level13to14.md) 
