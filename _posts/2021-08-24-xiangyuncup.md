---
layout: post
title: 2021祥云杯部分wp
date: 2021-08-24
categories: blog
tags: [wp篇]
description: 文章。


---

# MISC

### 层层取证

#### 题目描述

题目提供两个压缩包一个内存镜像一个磁盘镜像

内存镜像名为memdump.mem可用volatility分析，filescan可发现使用FTK的痕迹

磁盘镜像为Forensic_image，用FTK挂载后，在其桌面上看到flag.txt

<img src="/img/article/xiangyuncup/1.png"/>

可用DiskGenius打开磁盘文件，有条件用取证大师也可，打开后发现有个BitLocker加密分区

<img src="/img/article/xiangyuncup/2.png"/>

用vmware仿真起来，这里用替换SAM表的方法绕开密码，看到桌面上有便条

<img src="/img/article/xiangyuncup/3.png"/>

在磁盘中\Users\XiaoMing\AppData\Local\Temp中找到两个流量包其中wireshark_4D9DE10B-B9DF-4EFF-93CB-50C8BB2AF217_20200813223005_a03980.pcapng通过搜索flag追踪udp流可导出一个压缩包（头也为rar），显示和保存数据为选择原始数据，save as为rar

<img src="/img/article/xiangyuncup/6.png"/>

看到另一篇wp解出了Bitlocker密钥，在加密盘中发现有名为2.pcapng流量包即wireshark_4D9DE10B-B9DF-4EFF-93CB-50C8BB2AF217_20200813223005_a03980.pcapng，如上导出rar(解压需密码，提示和开机密码一样)

<img src="/img/article/xiangyuncup/7.png"/>

<img src="/img/article/xiangyuncup/8.png"/>

回到内存取证(找开机密码)

<img src="/img/article/xiangyuncup/4.png"/>

```bash
E:\volatility>volatility.exe -f E:\祥云杯\Forensic_9b23172e1dba502daa656b8d4234897f\memdump\memdump.mem --profile=Win7SP1x64 hivelist
Volatility Foundation Volatility Framework 2.6
Virtual            Physical           Name
------------------ ------------------ ----
0xfffff8a000ce7410 0x000000001a045410 \SystemRoot\System32\Config\SAM
0xfffff8a000dcb010 0x0000000019482010 \??\C:\Windows\ServiceProfiles\NetworkService\NTUSER.DAT
0xfffff8a000e5f010 0x00000000199c9010 \??\C:\Windows\ServiceProfiles\LocalService\NTUSER.DAT
0xfffff8a0013f1010 0x000000000a8d3010 \??\C:\Users\XiaoMing\ntuser.dat
0xfffff8a001409010 0x000000000a56e010 \??\C:\Users\XiaoMing\AppData\Local\Microsoft\Windows\UsrClass.dat
0xfffff8a00605c010 0x000000003c087010 \SystemRoot\System32\Config\DEFAULT
0xfffff8a00000f010 0x0000000022787010 [no name]
0xfffff8a000024010 0x0000000023512010 \REGISTRY\MACHINE\SYSTEM
0xfffff8a000060410 0x00000000211d0410 \REGISTRY\MACHINE\HARDWARE
0xfffff8a0002bb010 0x000000003c017010 \Device\HarddiskVolume3\Boot\BCD
0xfffff8a000334010 0x0000000000b83010 \SystemRoot\System32\Config\SOFTWARE
0xfffff8a000c96010 0x0000000017104010 \SystemRoot\System32\Config\SECURITY
```

```bash
E:\volatility>volatility.exe -f E:\祥云杯\Forensic_9b23172e1dba502daa656b8d4234897f\memdump\memdump.mem --profile=Win7SP1x64 hashdump -y 0xfffff8a000024010 -s
0xfffff8a000ce7410
Volatility Foundation Volatility Framework 2.6
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
XinSai:1000:aad3b435b51404eeaad3b435b51404ee:27caa41e7118fd4429d9b9cbd87aaa40:::
XiaoMing:1001:aad3b435b51404eeaad3b435b51404ee:92efa7f9f2740956d51157f46521f941:::
```

把用户xiaoming的92efa7f9f2740956d51157f46521f941放到[cmd5](https://link.zhihu.com/?target=https%3A//www.cmd5.com/)尝试查询NTLM Hash显示为付费，看别人wp已解出密码为xiaoming_handsome

<img src="/img/article/xiangyuncup/5.png"/>

解密压缩包(xiaoming_handsome)，里面的flag.docx密码为xiaoming1314得到flag

<img src="/img/article/xiangyuncup/9.png"/>

