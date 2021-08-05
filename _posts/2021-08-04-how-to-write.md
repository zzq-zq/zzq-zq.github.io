---
layout: post
title: 如何搭建属于自己的博客 小白篇
date: 2021-08-04
categories: blog
tags: [hello,xixi]
description: 文章。
---





摘要：本文仅供大家参考学习，里面介绍了域名注册、DNS 设置、GitHub 和 Jekyll 设置等过程，以下教程主要参考https://www.cnfeat.com/blog/2014/05/11/how-to-build-a-blog/写成。

选择[GitHub Pages](https://link.zhihu.com/?target=https%3A//pages.github.com/)的理由

- 1、GitHub Pages 有 300M 免费空间，资料自己管理，保存可靠；
- 2、学着用 GitHub，享受 GitHub 的便利，上面有很多大牛，眼界会开阔很多；
- 3、顺便看看 GitHub 工作原理，最好的团队协作流程；
- 4、GitHub 是趋势；

### 什么是 GitHub Pages

`GitHub Pages` 是一个静态站点托管服务。
`Github` 页面旨在直接从 `GitHub` 仓库中直接托管您的个人、组织或项目页面。了解关于 `GitHub Pages` 网站不同类型的更多信息，请参阅[用户、组织和项目页面](https://help.github.com/articles/user-organization-and-project-pages/)。

你可以使用 [Jekyll Theme Chooser](https://help.github.com/articles/creating-a-github-pages-site-with-the-jekyll-theme-chooser/) 在线创建和发布 `GitHub Pages`。如果你希望在本地使用，可以使用 [GitHub Desktop](https://desktop.github.com/) 或者[命令行](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/)。

`GitHub Pages` 是静态站点托管服务器，不支持 `PHP` ，`Ruby` 或 `Python` 等服务器端代码。

### 按需注册购买域名

1、域名例如qzqzhang.com，例如 狗爹[http://godaddy.com](https://link.zhihu.com/?target=http%3A//godaddy.com) ，（此网站支持支付宝支付），实名认证通过后输入想要的域名

<img src="/img/article/5.png"/>

2、选择喜欢的加入购物车

<img src="/img/article/6.png"/>

3、进入此页面，按需索取，建议选择不用了，谢谢，免费的也可以不要，点击继续进入购物车

<img src="/img/article/7.png"/>

4、跳转到的页面按指示选择购买期限后，登陆后即可购买。

细心的小伙伴会发现有促销码，需要的自行网上搜索，一般优惠幅度是 20%~ 30% 不等，当发现使用促销码后支付失败，可能是地域的原因使得支付条件不支持，此时就需要换一个促销码试试。

5、信息确认后点击前去付款，登录或注册界面，填完必要的信息之后，选择用支付宝或银行卡结算。

6、结算成功后，重新登陆点击用户处出现下拉框，在账户-我的产品中可以发现域名已经存在。

- 输入优惠码没有优惠或者优惠幅度较低，请清除浏览器 cookies 再尝试；
- 如果没有支付宝支付选项，有可能是使用的优惠码不支持支付宝，请重新清除浏览器 cookies 再尝试；
- 注册时用户填写信息时一定要输入正确的邮箱名字，否则修改十分麻烦。
- 买完域名之后一定要记得去自己的邮箱查看激活邮件，否则域名激活不了。

### 安装准备软件

下载安装

- 1、[Node.js](http://nodejs.org/)
- 2、[Git](http://git-scm.com/)

在下载完成后的Git中，有个git-bash.exe，双击就能打开(windows)，其他系统下面则打开终端（Terminal）。

<img src="/img/article/8.png"/>

### **注册 GitHub**

访问：[http://www.GitHub.com/](https://link.zhihu.com/?target=http%3A//www.github.com/)s

注册你的 username 和邮箱，邮箱十分重要，GitHub 上很多通知都是通过邮箱发送。

具体注册事项在网上搜索即可，在github上也有具体教程，注册完后就可以在自己的github上建立仓库了，详情请参见https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site

### **配置 SSH keys**

我们需要让本地git项目与远程Github建立联系，打开git-bash.exe，在命令行中输入以下命令。

### 检查 SSH keys的设置

首先我们需要检查你电脑上现有的 ssh key：

```bash
$ cd ~/.ssh 检查本机的ssh密钥
```

如果提示：No such file or directory 说明你是第一次使用 git。

### 生成新的 SSH Key：

```bash
$ ssh-keygen -t rsa -C "邮件地址@youremail.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/your_user_directory/.ssh/id_rsa):<回车就好>
```

- 注意 1: 此处的邮箱地址，你可以输入自己的邮箱地址；
- 注意2: 此处的「-C」的是大写的「C」

然后系统会要你输入密码(输入密码时是不显示的，直接输入即可)：

```bash
Enter passphrase (empty for no passphrase):<输入加密串>
Enter same passphrase again:<再次输入加密串>
```

在回车中会提示你输入一个密码，这个密码会在你提交项目时使用，如果为空的话提交项目时则不用输入。这个设置是防止别人往你的项目里提交内容。

最后看到这样的界面，就成功设置ssh key了：

<img src="/img/article/9.png"/>

### **添加 SSH Key 到 GitHub**

在本机设置SSH Key之后，需要添加到GitHub上，以完成SSH链接的设置。

用文本编辑工具打开id_rsa.pub文件，如果看不到这个文件，你需要设置显示隐藏文件。准确的复制这个文件的内容，才能保证设置的成功。

<img src="/img/article/12.png"/>

点击github主页上的settings

<img src="/img/article/10.png"/>

在左侧选择栏中选择SSH and GPG keys，看向第一个SSH keys，此处因为我之前已经添加过了，这边不做重复添加了，第一次用应该是没有的，点击New SSH key，把刚刚复制的id_rsa.pub文件的内容粘贴完成添加即可。

<img src="/img/article/11.png"/>

<img src="/img/article/13.png"/>

### 测试一下

可以输入下面的命令，看看设置是否成功，`git@github.com`的部分不要修改：

```
$ ssh -T git@github.com
```

输入密码后，如果是下面的反应：

```
The authenticity of host 'github.com (207.97.227.239)' can't be established.RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.Are you sure you want to continue connecting (yes/no)?
```

不要紧张，输入`yes`就好，然后会看到：

```
Hi <em>username</em>! You've successfully authenticated, but GitHub does not provide shell access.
```

若有问题，请重新设置。常见错误请参考：

- [GitHub Help - Generating SSH Keys](http://help.github.com/articles/generating-ssh-keys)
- [GitHub Help - Error Permission denied (publickey)](http://help.github.com/articles/error-permission-denied-publickey)

### 设置你的账号信息

现在你已经可以通过SSH链接到GitHub了，还有一些个人信息需要完善的。

Git会根据用户的名字和邮箱来记录提交。GitHub也是用这些信息来做权限的处理，输入下面的代码进行个人信息的设置，把名称和邮箱替换成你自己的，名字必须是你的真名，而不是GitHub的昵称。

```
$ git config --global user.name "你的名字"$ git config --global user.email "your_email@youremail.com"
```

好了，现在你已经可以成功连接GitHub了。

### 使用GitHub Pages建立博客

与GitHub建立好链接之后，就可以方便的使用它提供的Pages服务，GitHub Pages分两种，一种是你的GitHub用户名建立的`username.github.io`这样的用户&组织页（站），另一种是依附项目的pages。

### User & Organization Pages

想建立个人博客是用的第一种，形如`beiyuu.github.io`这样的可访问的站，如下点击建立新仓库。

<img src="/img/article/14.png"/>

输入想要的名字，选择权限等，这里警示标红是因为我已经建立过这个名字的仓库，第一次用的命名应该显示绿色通过，详细创建过程可以参见GitHub文档https://docs.github.com/en

<img src="/img/article/15.png"/>

### 将独立域名与 GitHub Pages 的空间绑定

#### DNS 设置

用 DNSpod，快，免费，稳定。

注册[DNSpod](https://www.cnfeat.com/blog/2014/05/11/how-to-build-a-blog/www.dnspod.cn)，添加域名，可以自动检测，也可以手动设置如下图设置。

<img src="/img/article/16.png"/>

其中 A 的两条记录指向的ip地址是 GitHub Pages 的提供的 ip

- 192.30.252.153
- 192.30.252.154

如博客不能登录，有可能是 GitHub 更改了空间服务的 ip 地址，记得及时到在[GitHub Pages](https://help.github.com/articles/setting-up-a-custom-domain-with-GitHub-Pages)查看最新的 ip 即可

www 指定的记录是你在 GitHub 注册的仓库。

### 去 GoDaddy 修改 DNS 地址

更改 [GoDaddy](https://mya.godaddy.com/) 的 Nameservers 为 DNSpod 的 NameServers。

1、点击你的账户，DNS管理。

<img src="/img/article/17.png"/>

将其更改成[f1g1ns1.dnspod.net](https://link.zhihu.com/?target=http%3A//f1g1ns1.dnspod.net) 和 [http://f1g1ns2.dnspod.net](https://link.zhihu.com/?target=http%3A//f1g1ns2.dnspod.net)，也就是DNSpod页面记录类型为NS的对应的两条记录

<img src="/img/article/18.png"/>

### 到Github **Fork 已设置好的仓库**

点击 [cnfeat/blog.io](https://github.com/cnfeat/blog.io/tree/master)

<img src="/img/article/19.png"/>

得到现成可使用的仓库，若在你新建的自己的仓库下没有看到fork到的文件，也可以下载其文件，解压后通过添加文件手动拖拽得到。

此时你的 GitHub 用户名.[http://GitHub.io](https://link.zhihu.com/?target=http%3A//GitHub.io)已经可以访问了。

### 将独立域名与 GitHub Pages 的空间绑定

#### GitHub Pages 的设置

去到你的 blog.io 仓库，点击 CNAME ,再点击右下角的 铅笔 编辑，将 cnfeat.com 改成你的域名

<img src="/img/article/20.png"/>

这样，你再去你绑定的域名看看，估计已经导向到 你的 GitHub 用户名.[http://GitHub.io](https://link.zhihu.com/?target=http%3A//GitHub.io)了。

### **搭建完成**

### 如何更新博文

#### 安装 GitHub desktop

下载地址：[GitHub Desktop](https://desktop.github.com/)

将你的仓库clone到本地，若想新增文章，直接在_posts文件夹中新增.md文件即可

注意：此处.md文件有命名格式需按年-月-日-**来命名，若要更新图片建议在img文件中添加想要显示的图片，在md文件相应位置处标注路径，如：<img src="/img/article/21.png"/>

