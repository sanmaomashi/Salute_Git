## Git代码托管服务

如何搭建Git远程仓库呢？我们可以借助互联网上提供的一些代码托管服务来实现，其中比较常用的有GitHub、码云、GitLab等。

> Gitee

- 地址： https://gitee.com/
- 是国内的一个代码托管平台，由于服务器在国内，所以相比于GitHub，码云速度会更快

> GitHub

- 地址：https://github.com/ 
- 是一个面向开源及私有软件项目的托管平台，因为只支持Git 作为唯一的版本库格式进行托管，故名gitHub

> GitLab

- 地址： https://about.gitlab.com/
- 是一个用于仓库管理系统的开源项目，使用Git作为代码管理工具，并在此基础上搭建起来的web服务

## SSH协议

### 10.1 什么是SSH协议

SSH 为 Secure Shell（安全外壳协议）的缩写，由 IETF 的网络小组（Network Working Group）所制定。SSH 是目前较可靠，专为远程登录会话和其他网络服务提供安全性的协议。利用 SSH 协议可以有效防止远程管理过程中的信息泄露问题。

由于本地Git仓库和远程仓库之间的传输是通过SSH加密的，所以必须要让远程仓库服务器认证你的SSH key，在此之前，必须要生成SSH key。

使用ssh协议通信时，推荐使用基于密钥的验证方式。你必须为自己创建一对密匙（公钥和私钥），并把公匙放在需要访问的服务器上。

### 10.2 Git支持的传输协议

由于Git的远程仓库并不在我们本地，当我们在使用远程仓库的时候（例如克隆、拉取、推送）就会涉及到数据的网络传输，Git支持多种数据传输协议

- 本地协议（Local）
- HTTPS 协议
- SSH（Secure Shell）协议
- Git 协议

![image-44](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/git/20211108144936.png)

### 10.3  配置SSH协议

可以使用Git提供的命令行工具Git Bash生成公钥和私钥，具体操作过程如下：

1、使用命令ssh-keygen –t rsa生成公钥和私钥，执行完成后在window本地用户.ssh目录C:\Users\用户名\.ssh下面生成如下名称的公钥和私钥

```bash
ssh-keygen –t rsa
ssh-keygen -t rsa -C "邮箱地址"
```

![image-22](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/git/20211108144943.png)

2、复制公钥文件内容至码云服务器

![image-11](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/git/20211108144949.png)





Git 并不像 SVN 那样有个中心服务器。

目前我们使用到的 Git 命令都是在本地执行，如果你想通过 Git 分享你的代码或者与其他开发人员合作。 你就需要将数据放到一台其他开发人员能够连接的服务器上。

![img](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210928095228.jpeg)



## Reference
