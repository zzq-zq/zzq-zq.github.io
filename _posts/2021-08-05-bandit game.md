---

layout: post
title: Bandit Game
date: 2021-08-05
categories: blog
tags: [bandit]
description: 文章。

---



## level 0

- ### Level Goal

  The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

  #### *Commands you may need to solve this level*

  ls, cd, cat, file, du, find

- ### problem solving process

  ```bash
  bandit0@bandit:~$ ls
  readme
  bandit0@bandit:~$ cat readme
  boJ9jbbUNNfktd78OOpsqOltutMc3MY1
  ```



## level 1

- ### Level Goal

  The password for the next level is stored in a file called **-** located in the home directory

  #### *Commands you may need to solve this level*

  ls, cd, cat, file, du, find

  ```bash
  du 命令
  
  du命令作用是估计文件系统的磁盘已使用量，常用于查看文件或目录所占磁盘容量。
  du命令与df命令不同，df命令是统计磁盘使用情况，详见linux命令详解之df命令。
  du命令会直接到文件系统内查找所有文件数据，所以命令执行时会耗费一点儿时间。
  在默认情况下，输出结果大小是以KB为单位的。如果想以MB为单位，使用-m参数即可，如果只想知道目录占了多少容量，使用-s参数即可。
  
  eg:
  bandit1@bandit:~$ du  #默认情况下，只统计目录的容量大小。
  20      .
  
  bandit1@bandit:~$ du -a  #统计目录和文件的容量大小。
  4       ./.bashrc
  4       ./.profile
  4       ./.bash_logout
  4       ./-
  20      .
  ```

  #### *Helpful Reading Material*

  https://tldp.org/LDP/abs/html/special-chars.html

- ### problem solving process

  ```bash
  bandit1@bandit:~$ ls
  -
  bandit1@bandit:~$ cat ./-
  CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
  ```



## level 2

- ### Level Goal

  The password for the next level is stored in a file called spaces in this filename located in the home directory

  #### *Commands you may need to solve this level*

  ls, cd, cat, file, du, find

  #### *Helpful Reading Material*

  我们将介绍如何创建，读取和复制文件名中具有空格的文件。

  1）使用空格创建文件名

  要在文件名中创建包含空格的文件，请按照显示的命令运行该命令

  ```bash
  $ touch'firstname secondname'
  ```

  例如，要创建一个名为“inaxide文档”的文件，请使用下面的语法

  ```bash
  $ touch 'linoxide docs'
  ```

  2）在文件名中读取包含空格的文件

  您可以使用“CAT”命令或使用您的首选文本编辑器打开文档，例如Vim，Nano或Gedit。

  ```bash
  $  cat 'linoxide docs'
  ```

  或者，您可以使用以下语法

  ```bash
  $ cat file\\ name\\ with\\ spaces
  ```

  让我们在`'linoxide docs'`文件中添加一些文本

  ```bash
  $ echo "Hello guys! Welcome to Linoxide" >> 'linoxide docs'
  ```

  要查看文件，请执行以下命令

  ```bash
  $ cat linoxide\\ docs
  ```

  **3) 用空格创建目录名**

  要[创建](https://linoxide.com/linux-mkdir-command/)中间有空格的[目录](https://linoxide.com/linux-mkdir-command/)名称，请使用以下语法

  ```bash
  $ mkdir firstname\\ secondname
  ```

  **请注意反斜杠后的空格**

  例如，要创建一个名为“ ***linoxide files\*** ”的目录，请运行

  ```bash
  $ mkdir linoxide\\ files
  ```

  **4) 导航到目录名称中有空格的目录**

  要导航到目录名称中包含空格的目录，请使用以下语法

  ```bash
  $ cd  directory\\ name
  ```

  要导航到目录“linoxide files”，请执行以下命令

  ```bash
  $ cd linoxide\\ files
  ```

  <img src="/img/article/1.png"/>

  **5) 复制目录名中有空格的目录**

  要将目录名称中包含空格的目录复制到其他位置，请使用以下语法

  ```bash
  $ cp -R directory\\ name  /destination/path
  ```

  或者

  ```bash
  $ cp -R 'directory name'  /destination/path/
  ```

  例如复制`'linoxide files'` 到`/home/james`路径执行

  ```bash
  $ cp -R 'linoxide files'  /home/james/
  ```

  <img src="/img/article/2.png"/>

  或者

  ```bash
  $ cp -R linoxide\\ files /home/james       
  ```

  <img src="/img/article/3.png"/>

  file命令：该命令用来识别文件类型，也可用来辨别一些文件的编码格式。它是通过查看文件的头部信息来获取文件类型，而不是像Windows通过扩展名来确定文件类型的。

  [Untitled](https://www.notion.so/40dc352659d74872bdf8f659b3a003dc)

- ### problem solving process

  ```bash
  bandit2@bandit:~$ ls
  spaces in this filename
  
  bandit2@bandit:~$ file spaces\\ in\\ this\\ filename
  spaces in this filename: ASCII text
  
  bandit2@bandit:~$ cat spaces\\ in\\ this\\ filename
  UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
  
  bandit2@bandit:~$ cat 'spaces in this filename'
  UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
  
  bandit2@bandit:~$ cat "spaces in this filename"
  UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
  ```

  

## level 3

- ### Level Goal

  The password for the next level is stored in a hidden file in the inhere directory.

  #### *Commands you may need to solve this level*

  ls, cd, cat, file, du, find

  在linux系统中如果想查看当前目录中的隐藏文件可以在 ls 或ll 后面加上 -a 参数，a 参数你可以理解成 all 。

  藏的文件，可以在文件的前面加 `.` 比如`mv test .test` 这样文件就会被隐藏

- ### problem solving process

  ```bash
  bandit3@bandit:~$ ls
  inhere
  bandit3@bandit:~$ cd inhere/
  bandit3@bandit:~/inhere$ ls
  bandit3@bandit:~/inhere$ ls -a  #可查看隐藏文件，linux中隐藏文件通常前面有个.
  .  ..  .hidden
  bandit3@bandit:~/inhere$ cat .hidden
  pIwrPrtPN36QITSp3EQaw936yaFoFgAB
  ```



## level 4

- ### Level Goal

  The password for the next level is stored in the only human-readable file in the **inhere** directory. Tip: if your terminal is messed up, try the “reset” command.

  #### *Commands you may need to solve this level*

  ls, cd, cat, file, du, find

- ### problem solving process

  ```bash
  bandit4@bandit:~$ ls
  inhere
  bandit4@bandit:~$ cd inhere/
  bandit4@bandit:~/inhere$ ls
  -file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
  
  bandit4@bandit:~/inhere$ cat ./-file0*  #可找到密码
  �¯`2ғ�%��rL~5�g��� �������p,k�;��r*��        �.!��C��J     �dx,�e�)�#��5��
                                                                                     ��p��V�_���ׯ�mm������h!TQO�`�4"aל�?��r�l$�?h�9('���!y�e�#�x�O��=�ly���~��A�f����-E�{���m�����ܗMkoReBOKuIDDepwhWk7jZC0RTdopnAYKh
  �T�?�i��j��îP�F�l�n��J����{��@�e�0$�in=��_b�5FA�P7sz��gN
  
  or
  
  bandit4@bandit:~/inhere$ file ./*
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
  bandit4@bandit:~/inhere$ cat ./-file07
  koReBOKuIDDepwhWk7jZC0RTdopnAYKh
  
  or
  
  bandit4@bandit:~/inhere$ strings ./*  ##文件均已执行，因此前面加./
  !TQO
  koReBOKuIDDepwhWk7jZC0RTdopnAYKh
  ```



## level 5

- ### Level Goal

  The password for the next level is stored in a file somewhere under the **inhere** directory and has all of the following properties:

  - human-readable
  - 1033 bytes in size
  - not executable

  #### *Commands you may need to solve this level*

  ls, cd, cat, file, du, find

- ### problem solving process

  ```bash
  find ##可以直接列出所有文件
  find / ##递归查询从根目录开始的所有文件
  ls -l ##显示不隐藏的文件与文件夹的详细信息
  ls -R ##只是列出了本目录下的所有目录和文件，但是目录下的文件不会循环的列出。
  ls -lR ##上两种结合显示 
  find /sbin /usr/sbin -executable \\! -readable -print ##search for files which are executable but not readable 搜索可执行的文件但不可读取
  find \\! -executable -size 1033c ##c表示for bytes,\\!表示不可(非)参照上条
  
  bandit5@bandit:~$ find \\! -executable -size 1033c
  ./inhere/maybehere07/.file2
  bandit5@bandit:~$ cat ./inhere/maybehere07/.file2
  DXjZPULLxYr17uwoI01bNLQbtFemEgo7
  ```



## level 6

- ### Level Goal

  The password for the next level is stored **somewhere on the server** and has all of the following properties:

  - owned by user bandit7
  - owned by group bandit6
  - 33 bytes in size

  #### *Commands you may need to solve this level*

  ls, cd, cat, file, du, find, grep

- ### problem solving process

  ```bash
  -user uname ##file is owned by user uname(numeric user ID allowed) 表示用户由谁拥有
  -group gname ##file belongs to group gname(numeric group ID allowed)
  
  find / -size 33c -user bandit7 -group bandit6 ##依题意
  find: ‘/root’: Permission denied
  find: ‘/home/bandit28-git’: Permission denied
  find: ‘/home/bandit30-git’: Permission denied
  find: ‘/home/bandit5/inhere’: Permission denied
  find: ‘/home/bandit27-git’: Permission denied
  find: ‘/home/bandit29-git’: Permission denied
  find: ‘/home/bandit31-git’: Permission denied
  find: ‘/lost+found’: Permission denied
  find: ‘/etc/ssl/private’: Permission denied
  find: ‘/etc/polkit-1/localauthority’: Permission denied
  find: ‘/etc/lvm/archive’: Permission denied
  find: ‘/etc/lvm/backup’: Permission denied
  find: ‘/sys/fs/pstore’: Permission denied
  find: ‘/proc/tty/driver’: Permission denied
  find: ‘/proc/28451/task/28451/fd/6’: No such file or directory
  find: ‘/proc/28451/task/28451/fdinfo/6’: No such file or directory
  find: ‘/proc/28451/fd/5’: No such file or directory
  find: ‘/proc/28451/fdinfo/5’: No such file or directory
  find: ‘/cgroup2/csessions’: Permission denied
  find: ‘/boot/lost+found’: Permission denied
  find: ‘/tmp’: Permission denied
  find: ‘/run/lvm’: Permission denied
  find: ‘/run/screen/S-bandit28’: Permission denied
  find: ‘/run/screen/S-bandit0’: Permission denied
  find: ‘/run/screen/S-bandit30’: Permission denied
  find: ‘/run/screen/S-bandit5’: Permission denied
  find: ‘/run/screen/S-bandit7’: Permission denied
  find: ‘/run/screen/S-bandit1’: Permission denied
  find: ‘/run/screen/S-bandit12’: Permission denied
  find: ‘/run/screen/S-bandit11’: Permission denied
  find: ‘/run/screen/S-bandit10’: Permission denied
  find: ‘/run/screen/S-bandit3’: Permission denied
  find: ‘/run/screen/S-bandit29’: Permission denied
  find: ‘/run/screen/S-bandit15’: Permission denied
  find: ‘/run/screen/S-bandit8’: Permission denied
  find: ‘/run/screen/S-bandit13’: Permission denied
  find: ‘/run/screen/S-bandit19’: Permission denied
  find: ‘/run/screen/S-bandit9’: Permission denied
  find: ‘/run/screen/S-bandit27’: Permission denied
  find: ‘/run/screen/S-bandit2’: Permission denied
  find: ‘/run/screen/S-bandit14’: Permission denied
  find: ‘/run/screen/S-bandit16’: Permission denied
  find: ‘/run/screen/S-bandit22’: Permission denied
  find: ‘/run/screen/S-bandit4’: Permission denied
  find: ‘/run/screen/S-bandit31’: Permission denied
  find: ‘/run/screen/S-bandit24’: Permission denied
  find: ‘/run/screen/S-bandit21’: Permission denied
  find: ‘/run/screen/S-bandit25’: Permission denied
  find: ‘/run/screen/S-bandit23’: Permission denied
  find: ‘/run/screen/S-bandit20’: Permission denied
  find: ‘/run/shm’: Permission denied
  find: ‘/run/lock/lvm’: Permission denied
  find: ‘/var/spool/bandit24’: Permission denied
  find: ‘/var/spool/cron/crontabs’: Permission denied
  find: ‘/var/spool/rsyslog’: Permission denied
  find: ‘/var/tmp’: Permission denied
  find: ‘/var/lib/apt/lists/partial’: Permission denied
  find: ‘/var/lib/polkit-1’: Permission denied
  /var/lib/dpkg/info/bandit7.password
  find: ‘/var/log’: Permission denied
  find: ‘/var/cache/apt/archives/partial’: Permission denied
  find: ‘/var/cache/ldconfig’: Permission denied
  
  bandit6@bandit:~$ find / -size 33c -user bandit7 -group bandit6 2>/dev/null  ##过滤掉权限被拒绝的或没有这样的文件目录的，2筛选>放入数字垃圾中
  /var/lib/dpkg/info/bandit7.password
  bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
  HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
  ```



## level 7

- ### Level Goal

  The password for the next level is stored in the file **data.txt** next to the word **millionth**

  #### *Commands you may need to solve this level*

  grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

- ### problem solving process

  ```bash
  bandit7@bandit:~$ ls
  data.txt
  bandit7@bandit:~$ cat data.txt | grep millionth
  millionth       cvX2JJa4CFALtqS87jk27qwqGhBM9plV
  ```



## level 8

- ### Level Goal

  The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once

  #### *Commands you may need to solve this level*

  grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

  #### *Helpful Reading Material*

  - [Piping and Redirection](https://ryanstutorials.net/linuxtutorial/piping.php)

- ### problem solving process

  ```bash
  man uniq
  NAME
         uniq - report or omit repeated lines ##删除重复行，当重复的行并不相邻时，uniq 命令是不起作用的
  DESCRIPTION
         Filter adjacent matching lines from INPUT (or standard input), writing to
         OUTPUT (or standard output). ##从输入（或标准输入）中过滤相邻的匹配线，写入输出（或标准输出）。
  man sort
  NAME
         sort - sort lines of text files
  DESCRIPTION
         Write sorted concatenation of all FILE(s) to standard output. ##将所有文件的分类连接写入标准输出。
  ##sort命令和uniq命令结合，前者先把重复项写到一起，后者剔除重复项
  
  检查文件并删除文件中重复出现的行，并在行首显示该行重复出现的次数。使用如下命令：
  uniq -c testfile
  
  bandit8@bandit:~$ cat data.txt | sort | uniq -c
       10 07KC3ukwX7kswl8Le9ebb3H3sOoNTsR2
       10 0efnqHY1ZTNRu4LsDX4D73DsxIQq7RuJ
       10 0N65ZPpNGkUJePzFxctCRZRXVrCbUGfm
       10 0Xo6DLyK5izRqEtBA7sW2SRmlAixWYSg
       10 10XitczY5Dz7UMoseKIeFWSzzwQrylfw
       10 1ETSsKgjfQj1cJeFzXLJWzKzza3iWcJa
       10 1T6qw9I32d71cS3TTvwmVp1WsxPFDJ9I
       10 2bFz9F0yRwxGzVCZ4Er04bk00qfUrzWb
       10 2CxmtCkpNL5ZjuoNzAtShkPXf5T43W7s
       10 337o85y4OymIh99WPUtotkb114evfAkC
       10 33xpPQhjt4Q2mqtX4sCVRwH2Zyh82E8R
       10 4SMqyZZztep75cte6xxKpVL49pKUkV8N
       10 5AdqWjoJOEdx5tJmZVBMo0K2e4arD3ZW
       10 5cO8XuoQWrzsyeOWDht8zgUIVWSRDaeC
       10 6PF22p6O8TphCTZot9ApZx8VfGuo8rd5
       10 7KaMzgnYMUeMISP9vuT3Dvsc06qfqa9u
       10 7uhj3nhe4AS0esnnEZHBAZN67fJ8BFjM
       10 8jtZmvqp9PTi8tp1oybBM663NQH3fhII
       10 8NtHZnWzCA8HswoJSCU7Ojg8nP3eKpsA
       10 aR2QhaBoDMncvJqPWkvLXMzEx9meBIbX
       10 BccauS9LeE8NUz4HVLXUwE8M1LWisPlG
       10 bRnktwNdxFy2RPZIshXJikswwEzJGvJ9
       10 cIPbot7oYveUPNxDMhv1hiri50CqpkTG
       10 cR6riSWC0ST7ALZ2i1e47r3gc0QxShGo
       10 CUqLkjIo0Jz9fNgrjPxiPa7PGGC1wpTQ
       10 dGnfD2LoqTiO1MBf2vmqw1KKEWSHfMKJ
       10 dqd5wTVO1cVPJoEY7GGkCdGxG6ZYqW98
       10 dqnvnNxL4QR3ALq95ckhZwEpl77cRgF4
       10 DqPqVp8YCjZ1vFsclwRTg13EuSc2D52X
       10 dV0aGGhk6mB4ZJX1aTTluAUIvLWToTYr
       10 DxxLvJl6cGHXLT7OW4xqS7Qrfny1K01l
       10 e5HFl4ur1rAxPPv2mHzg1uYKMuos4fwp
       10 Ef509iQpb5gQJsjz5dMXLxpeAfkbLOrw
       10 eTHlmI3pFZ4FQASs32Dm0ETVZWHlP0I1
       10 f0tri5KLH5eiTU0zQOqWvXTsrl1ekqnU
       10 f6ZuiZizTliaMOkVYXZMudtaReSYMnkP
       10 flyKxCbHB8uLTaIB5LXqQNuJj3yj00eh
       10 g1VkH2pk3cmr6aY4np1Dcpm0HF7G9IDT
       10 g9xRXSlVNiV4EhUAl1p6uPUWcyEewDK6
       10 gqyF9CW3NNIiGW27AtWVNPqp3i1fxTMY
       10 h2IsJoN6fe0ne0qrTQxeiu0P44hMWWbk
       10 hA6Ofhj75FPgqnCKEJ9g6pLSKapxxmGC
       10 Hq6uxRAkKPNLnH6eRSFDzXtvVt0CSsee
       10 I3fc578VLa7mOQ1t9zArPPOPY7aDVBcJ
       10 iIaOHQG7ZLdimomwMQaGIF7vib1RmXBh
       10 IkAAyqo1rCrxdY8qH0FfxXkRTTO2GNSf
       10 iKiMcQpNMn2ImOASX39XBUR8XfApdmsj
       10 InU7h0xhZh4SMMOMvlnsq03pz0k9J5FX
       10 iwE0KTeKQ8PWihqvjUnpu52YZeIO8Pqb
       10 J6Lzp6ZqTJsOuJRTXcvhwKfM0KK3Xtbl
       10 K9D1CLsVCdkodgvJJIt1oHIaiOY1h8hg
       10 KASHOxc1NxaM8caXUw5MHCkddANXOkCu
       10 khecG2RClunkhrgmq4UNB26N5F1yiUwL
       10 kJTBMD8k9OHyXwZ2aJMQkV23u0gyuoIO
       10 KLu6irnqFwhOKnVoTwuoT9e5t6oxYQwv
       10 KrDVVORXLPfRhfnRmmuP3OnVHWKDMSM8
       10 kUbOkhsIw6GSp0WI2YUo1Q3hDxFU0iQn
       10 l1I3Red7uSH9n30OylHP2hQDbOU0qGaq
       10 l2lECnJkQk8EBl6IO3gHUlnjoCTF1has
       10 LfrBHfAh0pP9bgGAZP4QrVkut3pysAYC
       10 Lg4vWWvEY7s0bG6BRiA35AHzo2gM6lHg
       10 mpgNGRH628hTQxajScbagkxaPKklUhjn
       10 mzOW32HQZi14kwrdeiquO1LCbyaOtbiT
       10 nJRb4MipHMdTmFylFc1NlqmywgxDSdoI
       10 NLWvtQvL7EaqBNx2x4eznRlQONULlCYZ
       10 NOdH1kFWibx4XnNaJoLFmghBn7oIs5hb
       10 ojGabNG5NJ9ppKUBXGr8lwMRRS5GuiA5
       10 OZ1wgx8bDI0vFOFxDQH32eMMcIPiIuPE
       10 PfbMe4Xb3mw5mJmabIbKAXKCU7zynDHl
       10 PQKOeIQwTw490Y8yobuxZAOL4cNmVo1D
       10 PSdVQSeUUBPRZD58WWP0OXLKxSgU3RxX
       10 ptb5ZW8TcgD3U6gOGCcN31xCDGIoQSEa
       10 qaWWAOOquC3yHnfJI4zvPWzCBdfHQ8wa
       10 RMiSPoAvF7WhgIcOdSQR2r6Zx0DNS5UW
       10 s1603Q2r4RPKqyoA8cspIRk0VdgEmFC3
       10 SA05uWMVCao2rzS8YRqUXh19SvnDpuOl
       10 SHMAMUEzQe4mV7SJpETTZFsyNRJsZE2k
       10 si952kS1y6pt4AFenmm0oIp8n7W5d3bd
       10 sYSokIATVvFUKU4sAHTtMarfjlZWWj5i
       10 SzwgS2ADSjP6ypOzp2bIvdqNyusRtrHj
       10 TKUtQbeYnEzzYIne7BinoBx2bHFLBXzG
       10 TThRArdF2ZEXMO47TIYkyPPLtvzzLcDf
       10 tVW9iY1Ml0uHPK4usZnN8oZXbjRt2ATY
       10 U0NYdD3wHZKpfEg9qGQOLJimAJy6qxhS
       10 UASW6CQwD6MRzftu6FAfyXBK0cVvnBLP
       10 UJiCNvDNfgb3fcCj8PjjnAXHqUM63Uyj
       10 UjsVbcqKeJqdCZQCDMkzv6A9X7hLbNE4
        1 UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
       10 UVnZvhiVQECraz5jl8U14sMVZQhjuXia
       10 V2d9umHiuPLYLIDsuHj0frOEmreCZMaA
       10 v9zaxkVAOdIOlITZY2uoCtB1fX2gmly9
       10 VkBAEWyIibVkeURZV5mowiGg6i3m7Be0
       10 w4zUWFGTUrAAh8lNkS8gH3WK2zowBEkA
       10 WBqr9xvf6mYTT5kLcTGCG6jb3ex94xWr
       10 wjNwumEX58RUQTrufHMciWz5Yx10GtTC
       10 X1JHOUkrb4KgugMXIzMWWIWvRkeZleTI
       10 XyeJdbrUJyGtdGx8cXLQST0pwu5cvpcA
       10 yo0HbSe2GM0jJNhRQLxwoPp7ayYEmRKY
       10 ySvsTwlMgnUF0n86Fgmn2TNjkSOlrV72
       10 Z9OC6DQpppreChPhwRJJV9YYTtrxNVcO
       10 zdd2ctVveROGeiS2WE3TeLZMeL5jL7iM
  bandit8@bandit:~$ cat data.txt | sort | uniq -c | grep -v "10" ##grep -v显示不包含匹配文本的所有行。
        1 UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
  ```



## level 9

- ### Level Goal

  The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.

  #### *Commands you may need to solve this level*

  grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

- ### problem solving process

  ```bash
  man strings
  NAME
         strings - print the strings of printable characters in files. ##strings命令在对象文件或二进制文件中查找可打印的字符串。
  
  bandit9@bandit:~$ cat data.txt | strings | grep =
  ========== the*2i"4
  =:G e
  ========== password
  <I=zsGi
  Z)========== is
  A=|t&E
  Zdb=
  c^ LAh=3G
  *SF=s
  &========== truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
  S=A.H&^
  ```



## level 10

- ### Level Goal

  The password for the next level is stored in the file **data.txt**, which contains base64 encoded data

  #### *Commands you may need to solve this level*

  grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

  #### *Helpful Reading Material*

  - [Base64 on Wikipedia](https://en.wikipedia.org/wiki/Base64)

- ### problem solving process

  ```bash
  bandit10@bandit:~$ ls
  data.txt
  bandit10@bandit:~$ cat data.txt
  VGhlIHBhc3N3b3JkIGlzIElGdWt3S0dzRlc4TU9xM0lSRnFyeEUxaHhUTkViVVBSCg==
  
  man base64
  -d, --decode
                decode data
  
  bandit10@bandit:~$ cat data.txt | base64 -d
  The password is IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
  ```



## level 11

- ### Level Goal

  The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

  #### *Commands you may need to solve this level*

  grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd

  #### *Helpful Reading Material*

  - [Rot13 on Wikipedia](https://en.wikipedia.org/wiki/Rot13)

- ### problem solving process

  ```bash
  bandit11@bandit:~$ ls
  data.txt
  bandit11@bandit:~$ cat data.txt
  Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh
  ##rot13编码，凯撒加密的一种
  ```

  <img src="/img/article/4.png"/>

  The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu



## level 12

- ### Level Goal

  The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

  #### *Commands you may need to solve this level*

  grep, sort, uniq, strings, base64, tr, tar, gzip, bzip2, xxd, mkdir, cp, mv, file

  #### *Helpful Reading Material*

  - [Hex dump on Wikipedia](https://en.wikipedia.org/wiki/Hex_dump)

- ### problem solving process

  ```bash
  bandit12@bandit:~$ mkdir /tmp/12    #创建新目录
  bandit12@bandit:~$ cp data.txt /tmp/12  #将数据文本复制到该目录中
  bandit12@bandit:~$ cd /tmp/12
  bandit12@bandit:/tmp/12$ ls
  data.txt
  
  man xxd
  NAME
         **xxd - make a hexdump or do the reverse**. #xxd - 做一个十六进制转储或做相反的事情
  # xxd 命令用于用二进制或十六进制显示文件的内容，如果没有指定outfile参数，则把结果显示在屏幕上，如果指定了outfile则把结果输出到 outfile中；如果infile参数为 – 或则没有指定infile参数，则默认从标准输入读入。
  ```
