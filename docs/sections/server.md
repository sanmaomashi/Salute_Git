## 9、Git代码托管服务

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

## 10、SSH协议

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



  ## 1、GitHub

Git 并不像 SVN 那样有个中心服务器。

目前我们使用到的 Git 命令都是在本地执行，如果你想通过 Git 分享你的代码或者与其他开发人员合作。 你就需要将数据放到一台其他开发人员能够连接的服务器上。

![img](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210928095228.jpeg)

  ### 1.1  创建仓库

(1)注册github账户，登录后，点击"New respository "

![clip_image002](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210107013026.png)

(2)在新页面中，输入项目的名称，勾选'README.md'，点击'create repository'

![clip_image004](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210107013046.png)

(3)添加成功后，转到文件列表页面.

![img](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210107012943.png)

### 1.2 添加ssh账户

1. 如果某台机器需要与github上的仓库交互，那么就要把这台机器的ssh公钥添加到这个github账户上。点击账户头像后的下拉三角，选择'settings'。

   ![clip_image008](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210107013156.png)

2. 点击'SSH and GPG keys'，添加ssh公钥。

![clip_image010](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210107013228.png)

3. 在ubuntu的命令行中，回到用户的主目录下，编辑文件.gitconfig，修改某台机器的git配置。

![clip_image012](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210107013329.png)

4. 修改为注册github时的邮箱，填写用户名。

![clip_image014](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210107013407.png)

5. 使用如下命令生成ssh密钥。

```bash
ssh-keygen -t rsa -C "邮箱地址"
```

![clip_image016](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210107013448.png)

6. 进入主目录下的.ssh文件件，下面有两个文件。

   公钥为id_rsa.pub

   私钥为id_rsa

   查看公钥内容，复制此内容

   ![clip_image018](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210107013522.png)

7. 回到浏览器中，填写标题，粘贴公钥

![clip_image020](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210107013547.png)

### 1.3 自动生成README.md目录

由于码云和github的markdown解析器，都不支持 [TOC]，码云官方推荐的是使用<a>标签来生成目录，但是如果文档目录过多，这种方式显然很不现实。

因此我们使用神器[gh-md-toc](https://github.com/ekalinin/github-markdown-toc.go/releases)

首先将README.md文档复制到gh-md-toc.exe的根目录下。

接着按住shift键同时右击。

![image-20201224155327338](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210107012509.png)

打开Powershell窗口后，直接键入。

```bash
./gh-md-toc.exe README.md
```

然后将生成的这一大段内容粘贴到你的md文件中，上传到码云或github即可显示目录

### 1.4 github删除某个文件夹

在github上只能删除仓库,却无法删除文件夹或文件, 所以只能通过命令来解决

首先进入你的master文件夹下, Git Bash Here ,打开命令窗口

```bash
$ git --help                                      # 帮助命令
$ git pull origin master                    # 将远程仓库里面的项目拉下来
$ dir                                                # 查看有哪些文件夹
$ git rm -r --cached target              # 删除target文件夹
$ git commit -m '删除了target'        # 提交,添加操作说明
$ git push -u origin master # 将本次更改更新到github项目上去
```

注:本地项目中的target文件夹不收操作影响,删除的只是远程仓库中的target, 可放心删除
每次增加文件或删除文件，都要commit 然后直接 git push -u origin master，就可以同步到github上了

### 1.5 给README文件添加icon

![license-Apache 2-green](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210107012640.svg)

实际上分别是由三个不同的第三方生成的图:

https://shields.io

这个网站可以自定义一些徽章，并且还提供了从github上读取状态的功能。

https://travis-ci.org

这个是一个持续集成网站，他会对项目持续编译，然后给出一个徽章显示实时的状态。

https://bintray.com

这个是一个代码仓库，说到jcenter应该就比较熟悉了，他就是jcenter，项目传到jcenter后会给个徽章实时显示当前的最新版本。



添加Github中的star/fork/watch按钮,详见文档：https://ghbtns.com/

所需参数

您必须为以下每个 URL 参数声明一个值：

| 选项   | 描述                                                         |
| ------ | :----------------------------------------------------------- |
| `user` | 拥有仓库的 GitHub 用户名                                     |
| `repo` | GitHub 仓库名称                                              |
| `type` | 要显示的按钮类型: `star`、`watch`、`fork`、`sponsor`、`follow` |

可选参数

不需要以下 URL参数。根据需要添加它们。

| 选项    | 描述                                                  |
| ------- | :---------------------------------------------------- |
| `count` | 显示可选的观察器或分叉计数：*默认情况下*没有或`true`  |
| `size`  | 用于使用较大按钮的可选标志：*默认情况下*没有或`large` |

- Star

```html
<iframe src="https://ghbtns.com/github-btn.html?user=twbs&repo=bootstrap&type=star&count=true&size=large" frameborder="0" scrolling="0" width="170" height="30" title="GitHub"></iframe>
 
<iframe src="https://ghbtns.com/github-btn.html?user=twbs&repo=bootstrap&type=star&count=true" frameborder="0" scrolling="0" width="150" height="20" title="GitHub"></iframe>
```

- Watch

```html
<iframe src="https://ghbtns.com/github-btn.html?user=twbs&repo=bootstrap&type=watch&count=true&size=large&v=2" frameborder="0" scrolling="0" width="170" height="30" title="GitHub"></iframe>
 
<iframe src="https://ghbtns.com/github-btn.html?user=twbs&repo=bootstrap&type=watch&count=true&v=2" frameborder="0" scrolling="0" width="150" height="20" title="GitHub"></iframe>
```

- Fork

```html
<iframe src="https://ghbtns.com/github-btn.html?user=twbs&repo=bootstrap&type=fork&count=true&size=large" frameborder="0" scrolling="0" width="170" height="30" title="GitHub"></iframe>
 
<iframe src="https://ghbtns.com/github-btn.html?user=twbs&repo=bootstrap&type=fork&count=true" frameborder="0" scrolling="0" width="150" height="20" title="GitHub"></iframe>
```

可用选项

SSL 支持

示例按钮与 URL 一起显示。当 SSL 选项托管在 GitHub 页面上时，SSL 选项通过[CloudFlare 的免费通用 SSL 产品](https://blog.cloudflare.com/introducing-universal-ssl/)提供。如果您愿意，您仍然可以使用 。`https://` `http://`

语法格式

```html
// markdown语法
[![Travis](https://img.shields.io/badge/CSDN-阿钟-brightgreen.svg)](http://blog.csdn.net/a_zhon)

//html语法
<a target="_blank" href="http://blog.csdn.net/a_zhon"><img
        src="https://img.shields.io/badge/CSDN-%E9%98%BF%E9%92%9F-brightgreen.svg"></a>
```

## 2、Gitee

国内访问 Github 速度比较慢，很影响我们的使用。

如果希望体验到 Git 飞一般的速度，可以使用国内的 Git 托管服务——[Gitee（gitee.com）](https://gitee.com/?utm_source=remote_blog_cnjc)。

Gitee 提供免费的 Git 仓库，还集成了代码质量检测、项目演示等功能。对于团队协作开发，Gitee 还提供了项目管理、代码托管、文档管理的服务，5 人以下小团队免费。

由于我们的本地 Git 仓库和 Gitee 仓库之间的传输是通过SSH加密的，所以我们需要配置验证信息。

**1、我们先在 [Gitee](https://gitee.com/?utm_source=remote_blog_cnjc) 上注册账号并登录后，然后上传自己的 SSH 公钥。**

首先生成自己的 SSH 公钥，然后将用户主目录下的 ~/.ssh/id_rsa.pub 文件的内容粘贴 Gitee 上。

选择右上角用户头像 -> 设置，然后选择 "SSH公钥"，填写一个便于识别的标题，然后把用户主目录下的 .ssh/id_rsa.pub 文件的内容粘贴进去：

![img](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210928095705.png)

![img](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210928095716.png)

成功添加后如下图所示：

![img](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210928095730.png)

接下来我们创建一个项目。

点击右上角的 **+** 号，新建仓库：

![img](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210928095744.png)

然后添加仓库信息：

![img](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210928095755.png)

创建成功后看到如下信息：

![img](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210928095807.png)

接下来我们看下连接信息：

![img](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210928095824.png)

项目名称最好与本地库保持一致。

然后，我们在本地库上使用命令 **git remote add** 把它和 Gitee 的远程库关联：

```
git remote add origin git@gitee.com:imnoob/runoob-test.git
```

之后，就可以正常地用 git push 和 git pull 推送了！

如果在使用命令 git remote add 时报错：

```
git remote add origin git@gitee.com:imnoob/runoob-test.git
fatal: remote origin already exists.
```

这说明本地库已经关联了一个名叫 origin 的远程库，此时，可以先用 **git remote -v** 查看远程库信息：

```
git remote -v
origin    git@github.com:tianqixin/runoob.git (fetch)
origin    git@github.com:tianqixin/runoob.git (push)
```

可以看到，本地库已经关联了 origin 的远程库，并且，该远程库指向 GitHub。

我们可以删除已有的 GitHub 远程库：

```
git remote rm origin
```

再关联 Gitee 的远程库（注意路径中需要填写正确的用户名）：

```
git remote add origin git@gitee.com:imnoob/runoob-test.git
```

此时，我们再查看远程库信息：

```
git remote -v
origin    git@gitee.com:imnoob/runoob-test.git (fetch)
origin    git@gitee.com:imnoob/runoob-test.git (push)
```

现在可以看到，origin 已经被关联到 Gitee 的远程库了。

通过 git push 命令就可以把本地库推送到 Gitee 上。

有的小伙伴又要问了，一个本地库能不能既关联 GitHub，又关联 Gitee 呢？

答案是肯定的，因为 git 本身是分布式版本控制系统，可以同步到另外一个远程库，当然也可以同步到另外两个远程库。

使用多个远程库时，我们要注意，git 给远程库起的默认名称是 origin，如果有多个远程库，我们需要用不同的名称来标识不同的远程库。

仍然以 runoob-test 本地库为例，我们先删除已关联的名为 origin 的远程库：

```
git remote rm origin
```

然后，先关联 GitHub 的远程库：

```
git remote add github git@github.com:tianqixin/runoob-git-test.git
```

注意，远程库的名称叫 github，不叫 origin 了。

接着，再关联 Gitee 的远程库：

```
git remote add gitee git@gitee.com:imnoob/runoob-test.git
```

同样注意，远程库的名称叫 gitee，不叫 origin。

现在，我们用 git remote -v 查看远程库信息，可以看到两个远程库：

```
git remote -v
gitee    git@gitee.com:imnoob/runoob-test.git (fetch)
gitee    git@gitee.com:imnoob/runoob-test.git (push)
github    git@github.com:tianqixin/runoob.git (fetch)
github    git@github.com:tianqixin/runoob.git (push)
```

如果要推送到 GitHub，使用命令：

```
git push github master
```

如果要推送到 Gitee，使用命令：

```
git push gitee master
```

这样一来，我们的本地库就可以同时与多个远程库互相同步：

![img](https://gitee.com/Nicolas-gaofeng/pic_store/raw/master/img/20210928095855.png)
