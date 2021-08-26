---
layout: post
title: 2021祥云杯部分wp misc篇
date: 2021-08-24
categories: blog
tags: [wp篇]
description: 文章。


---

## 层层取证

#### 题目描述

题目提供两个压缩包一个内存镜像一个磁盘镜像

内存镜像名为`memdump.mem`可用volatility分析，filescan可发现使用FTK的痕迹

磁盘镜像为`Forensic_image`，用FTK挂载后，在其桌面上看到flag.txt

<img src="/img/article/xiangyuncup/1.png"/>

可用DiskGenius打开磁盘文件，有条件用取证大师也可，打开后发现有个BitLocker加密分区

<img src="/img/article/xiangyuncup/2.png"/>

用vmware仿真起来，这里用替换SAM表的方法绕开密码，看到桌面上有便条

<img src="/img/article/xiangyuncup/3.png"/>

在磁盘中\Users\XiaoMing\AppData\Local\Temp中找到两个流量包其中`wireshark_4D9DE10B-B9DF-4EFF-93CB-50C8BB2AF217_20200813223005_a03980.pcapng`通过搜索flag追踪udp流可导出一个压缩包（头也为rar），显示和保存数据为选择原始数据，save as为rar

<img src="/img/article/xiangyuncup/6.png"/>

看到另一篇wp解出了Bitlocker密钥，在加密盘中发现有名为2.pcapng流量包即`wireshark_4D9DE10B-B9DF-4EFF-93CB-50C8BB2AF217_20200813223005_a03980.pcapng`，如上导出rar(解压需密码，提示和开机密码一样)

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

把用户`xiaoming`的92efa7f9f2740956d51157f46521f941放到[cmd5](https://link.zhihu.com/?target=https%3A//www.cmd5.com/)尝试查询NTLM Hash显示为付费，看别人wp已解出密码为`xiaoming_handsome`

<img src="/img/article/xiangyuncup/5.png"/>

解密压缩包(xiaoming_handsome)，里面的flag.docx密码为xiaoming1314得到flag

<img src="/img/article/xiangyuncup/9.png"/>



## 鸣雏恋

此题给了一个.docx文档

<img src="/img/article/xiangyuncup/10.png"/>

放kali里binwalk一下发现zip，直接改后缀为zip得到一个压缩包

<img src="/img/article/xiangyuncup/11.png"/>

解压后发现`_rels`文件夹下有东西：`key.txt`和一个ZIP压缩包。

<img src="/img/article/xiangyuncup/12.png"/>

`key.txt`放入010Editor发现是[零宽隐写]([(43条消息) misc学习笔记1-txt零宽度字符隐写_Amherstieae的博客-CSDN博客_零宽隐写](https://blog.csdn.net/Amherstieae/article/details/108909743))在‌‌‌‌‌‌‍‌‌‌‌‌kali中用`vim key.txt`也可发现‬(‌‌‌‌‌‌‍蓝色的就是零宽度字符)

<img src="/img/article/xiangyuncup/13.png"/>

‌‌‌‌‌‍‌‌‌‌<img src="/img/article/xiangyuncup/14.png"/>‬‌‌‌‌‌‌‍‌‌‌‌‌‬‌‌‌‌‌‌‍‍‌‌‌‌

[在线解密]([Unicode Steganography with Zero-Width Characters (330k.github.io)](https://330k.github.io/misc_tools/unicode_steganography.html))密码为 

``` text
Because I like naruto best
```

<img src="/img/article/xiangyuncup/15.png"/>

解密后发现里面很多鸣人和雏田的头像，按照数字顺序，每8个一byte，雏田0，鸣人1，用脚本解得base64

<img src="/img/article/xiangyuncup/16.png"/>

```python
from PIL import Image
from tqdm import tqdm
path = '鸣雏恋\\_rels\\love\\out\\'
flag = ''

for i in tqdm(range(129488)):
    img = Image.open(path+str(i)+'.png')
    s = img.getpixel((10,10))
    if(str(s) == '1'):
        flag += '0'
    elif(str(s) == '3'):
        flag += '1'
    else:
        print('wrong!')
        exit()
s = ''
rflag = ''
for i in flag:
    s+=i
    if len(s)==8:
        rflag += chr(int(s,2))
        s=''
print(rflag)
```

base64转图片后在图片下方看到flag

<img src="/img/article/xiangyuncup/17.png"/>

```text
flag{57dd74fb21bb1aee50f19421bf836f23}
```

下方脚本可直接恢复出图片

```python
from tqdm import tqdm
from Crypto.Util.number import *
import base64

with open('鸣雏恋/_rels/love/out/0.png', 'rb') as f:
    zero = f.read()

ans = ''
for i in tqdm(range(129488)):
    with open(f'鸣雏恋/_rels/love/out/{i}.png', 'rb') as f:
        s = f.read()
    if (s == zero):
        ans += '0'
    else:
        ans += '1'

s = (long_to_bytes(int(ans, 2))).decode()
s = base64.b64decode(s[22:])
with open('gao_3.png', 'wb') as f:
    f.write(s)
```



