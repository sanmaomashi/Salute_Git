  # GitHub托管平台使用

> 本篇基于macOS Monterey v12.4测试，win操作系统可借鉴。

  ## 一、注册账户

首先我们来到[GitHub](https://github.com/)的官网，点击右上角的sign up注册（sign in是登录），创建一个GitHub账户。

输入用户名、邮箱及密码，加入GitHub即可

![2](../../img/2.png)

  ## 二、创建仓库

**1. 注册github账户，登录后，点击"New respository "**

![image-20220411225816771](../../img/3.png)

**2. 在新页面中，输入项目的名称，选择自己仓库的相关配置**

![image-20220411230216856](../../img/4.png)

> 页面配置说明

（1）`Repository name`

输入框输入自己仓库的名字，建议填写一个与项目相关的名字，系统会自动检测名称是否重复。

（2）`Descriptioin（optional）`

对创建仓库的描述，当然，这个可以选填。

（3）`Public && Private`

Public即为公众的，选了Public即代表你的仓库代码为公开的，仓库内的所有内容都会被公开。

Private即为私有的，选了Private即代表你的仓库为私密的，当然你选了这个也可以自己设置访问权限。相比Public多了一些功能，并且是收费的。如果只是自己的练习或者不重要的信息，当然我们没必要去选择付费的这一项。

（4）`Initialize this repository with --- ADD a README file`

如果勾选了这个选项，那么它就代表着GitHub会自动初始化仓库并且设置README文件，可以让你立刻clone这个仓库。clone意思就是本地没有repository（仓库）时，将远程repository（仓库）整个下载过来。如果不勾选它，那么，你可以手动push。将已经有的Git仓库添加到GitHub。

（5）`Initialize this repository with --- Add .gitignore`

在使用git作版本控制时，git会默认把git控制的文件夹里面的所有文件都加入到版本控制。但是在实践中，我们经常会遇到不想某些文件或文件夹被git追踪的情况。比如logs文件、代码构建过程中产生的一些列文件，要解决这种问题,通常情况下我们需要创建一个文件格式后缀名为.gitignore的文件，来控制那些文件不被git追踪。

这里所说的git追踪，通俗一点来讲就是在我们push上传文件的时候，这些文件不会被上传。只会存在你本地的磁盘里，不会随你要上传的文件一起上传，它会被滤过。

下拉菜单中有多种语言及框架，看你的需要进行选择。

（6）``Initialize this repository with --- Choose a license``

这个下拉菜单意思是给你的代码仓库添加一个许可证，你可以根据需求进行选择。比如我添加一个开源许可证，当别人浏览我的代码仓库时，别人也可以进行修改我仓库中的项目。

随后会生成包含许可协议内容的LICENSE文件，用来表明你的仓库内容的许可协议。

**3. 添加成功后，点击Create repository按钮，即完成仓库的创建，并转到文件列表页面。**

![image-20220411231849776](../../img/5.png)

## 三、删除仓库

**1. 点击进入仓库主页，点击settings**

![image-20220412213548272](../../img/17.png)

**2. 进入设置界面后向下拉，拉到页面的最后，有一个delete选项，点击**

![image-20220412213659659](../../img/18.png)

**3. 将黑体字复制进下面空白框内，点击“I ubderstand the consequences, delete this repository”即可删除仓库。**

![image-20220412213805606](../../img/19.png)

## 四、删除某个文件夹

在github上只能删除仓库,却无法删除文件夹或文件, 所以只能通过命令来解决

**1. 将github的项目拉取到本地**

```bash
git pull origin master 
```

**2. 删除相应到文件夹**

```bash
git rm -r --cached xxx  # xxx指对应到文件夹名称
```

**3. 重新提交项目到本地仓库上**

```bash
git commit -m "注释内容"
```

**4. 将项目从本地提交到GitHub上**

```bash
git push origin master
```

  ## 五、下载项目

**1. 下载整个项目文件**

找到项目文件，然后点击右上角`Code`，选择`Download Zip`即可！

注：不登录账号也可以下载

![image-20220412002428026](../../img/7.png)

**2. 使用git检出**

找到该项目文件，点击右上角`Code`，选择`HTTPS`后点击复制

![image-20220412002758337](../../img/8.png)

打开终端，使用`git clone `命令拷贝一个 Git 仓库到本地，让自己能够查看该项目，或者进行修改。

拷贝项目命令格式如下，**[url]** 是你要拷贝的地址：

```bash
 git clone [url]
```

使用https url克隆对初学者来说会比较方便，复制https url 到终端里面直接用clone命令克隆到本地就好了。而使用 SSH url 克隆却需要在克隆之前先配置和添加好 SSH key 。因此，如果你想要使用 SSH url 克隆的话，你必须是这个项目的拥有者。否则你是无法添加 SSH key 的。

> https 和 SSH 的区别：

- 前者可以随意克隆github上的项目，而不管是谁的；而后者则是你必须是你要克隆的项目的拥有者或管理员，且需要先添加 SSH key ，否则无法克隆。
- https url 在push的时候是需要验证用户名和密码的；而 SSH 在push的时候，是不需要输入用户名的，如果配置SSH key的时候设置了密码，则需要输入密码的，否则直接是不需要输入密码的。

**3. 下载单个文件**

直接选择该文件，右键选择对应的下载工具即可！

![image-20220412003343070](../../img/9.png)

## 六、添加ssh账户

如果某台机器需要与github上的仓库交互，那么就要把这台机器的ssh公钥添加到这个github账户上。

而免密登陆直白的讲就是在远程 SSH访问的时候不用重复输入密码，例如：在使用 github 进行提交/拉取代码的时候，配置了免密登录后，就不用每次都输入密码啦。

**1. 打开命令行终端,验证是否有ssh keys,看下返回的结果中是否已经存在了.pub结尾的文件**

```bash
ls -alh ~/.ssh
```

如果有.pub结尾的文件直接打开，复制到github上的SSH keys，如果没有就继续执行

![image-20220412004958453](../../img/10.png)

**2. 使用如下命令生成ssh-keygen密钥,然后一路回车。其中，“邮箱地址”是你的github关联的邮箱。**

```bash
ssh-keygen -t rsa -C "邮箱地址"
```

![image-20220412005459525](../../img/11.png)

这个时候在默认路径下就生成了两个文件，公钥和私钥。进入主目录下的.ssh文件夹，公钥为id_rsa.pub，私钥为id_rsa。

![image-20220412005759912](../../img/12.png)

执行以下命令查看公钥内容，复制此内容

```bash
# 打开id_rsa.pub文件
cat ~/.ssh/id_rsa.pub
```

![image-20220412010049113](../../img/13.png)

**3. 点击账户头像后的下拉三角，选择'settings'。**

![20210107013156](../../img/14.png)

**4. 点击'SSH and GPG keys'，添加ssh公钥。**

![15](../../img/15.png)

**5. 填写标题，粘贴公钥**

![20210107013547](../../img/16.png)

**6. 验证github是否链接**

```bash
ssh -T git@github.com
```

这样github的ssh就可以链接mac了，可以上传和下载代码了~~

## 七、更改远程跟踪链接

当一个项目拉下来，只是想看看的时候，都是用 HTTP 的方式 clone，但当自己想修改了，改完了需要推送到其他地址，就需要修改远程跟踪链接。

- 打开终端
- 将当前的工作目录/项目更改为本地项目

- 查看当前 Git 跟踪情况

```bash
git remote -v
> origin  https://github.com/user/repo.git (fetch)
> origin  https://github.com/user/repo.git (push)
```

- 设置远程跟踪链接

```bash
git remote set-url origin https://github.com/USERNAME/REPOSITORY.git
git remote set-url origin https://github.com/Nicolas-gaofeng/Salute_Operation_System.git
```

然后再查看跟踪情况，会发现改为了设置的远程地址，此时再推送即可。



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

## 

## githubpages

## 图床配合上传图片

## 探索

### 1. 如何写属于自己的 license（软件协议）？

 **（1）最为方便的license创建方式：**

当你在 GitHub 上你创建新的 repository 的时候，你可以直接选择一些比较好的 license：

![image-20220411232540993](../../img/1.png)

随着你项目做得多了代码写得多了，你会发现编码过程中会不时用到其他人的成果，一个项目下来多少会引入一些优秀的库，别人放在公网上开源的 DLL，以及一些算法等等。细心的你会注意到即使只是一小段代码，优秀的作者都在最开始会简单地附上一段关于许可的声明，或者说是协议比如"Licensed under the MIT license"，并且一些博客也会标明"此文章发表在 CC 协议下"。而如果我们 Copy 了别人的代码或者文字同时没注意这些的话，在国外法律意识特别强的环境下，我们的作品会因触犯别人的权益而违法。因为好多开源协议最低要求是使用者需要保留原作者对代码的声明，不声不响地就拿来用了必然导致恶果。**所以开源不等于免费，开源也不等于没有约束。**

**（2）何为License？**

License 是软件的授权许可，里面详尽表述了你获得代码后拥有的权利，可以对别人的作品进行何种操作，何种操作又是被禁止的。软件协议可分为开源和商业。当然我们要讨论的当然是开源协议。

对于商业协议，或者叫法律声明、许可协议，每个软件会有自己的一套行文，由软件作者或专门律师撰写。这是什么惊为天人的东西嘛还得请专门的律师。因为涉及到以后侵权打官司这种事情，这种商业条款的行文是非常严谨而讲究的，记得以前看到句调侃的话：'如果法律文件不写得那么生涩难懂，律师们就没饭吃了'，就是说任何文字一旦上升到法律的层次，不要说你接受完了九年义务教育，就是考了个专八也会觉得英语白学了，直接的法律协议什么的那不是给常人看的。

所以对于大多数人来说，不用自己花大把时间去写许可协议，选择一份广为流传的开源协议是个不错的选择，如果你的作品是开源的话，这样省时又省心。

**（3）选择一分协议的好处**

你的作品如果不是定性为全商业性质，可以考虑选择一份流行度比较高的开源协议。具体来说的话，你肯定希望作品能够被多数人分享查阅吧，不但提高自己业界的知名度，同时也方便了需要的人为开源做出了贡献。换句话说，你不分享出来的话你的作品的意义何在呢（当然，自己捣腾的私人东西还是自己保留吧）？可是一旦你把你的代码贴出来，这就表示任何人都可以看到并获取，之后发生的事情你无法控制，有的人或许稍微修改一下放进自己的代码中，有的把你的软件改个名字拿去贩卖，有的甚至会拿去把作者名字改为自己然后拿去找工作什么的，而不会有人知道这个作品的原作者，背后辛勤付出了的人。所以为了公开分享你的代码，同时又让你对代码保留一定权利，在作品中声明一个许可协议是非常有必要的，这是很多新人所忽略的问题，同时很多人在使用别人的劳动成果时也会忽视协议的存在，这样不好。

多说一句，一个事实让你了解国外开发者在尊重他人劳动成果方面做得是如何的到位，如果 A 的作品是因为 B 的作品的启发而来，A 甚至都没有使用 B 任何一句代码，但 A 会在他的作品里面指明是受到了 B 的启发 "Inspired by XXX link：[http://www.blah.com](http://www.blah.com/)"。

当然有人会觉得，有了一分协议声明在那里，我就需要鸟你么，我拿来用了把作者名字去掉同时还要加上我的名字，你咬我？！这是后话，只是在利益很小的情况下，或者作者不知情的情况下，作者不会追究什么责任，但如果你的产品做成功了，那就不一定了。另外就是，有协议和没声明协议的裸代码是有非常重要区别的，一般作品当中没声明协议的默认为 Copy right 的，也就是版权保留。此种情况表明他人没有任何授权，不得复制分发修改使用等等，但一如上面所讨论的，这样的话还何来开源，何来分享呢。有了协议的声明，在未来你的维权上面会方便很多，让你的作品在分享的同时保留了自身的一些权利。

**（4）快速选择**

目前流行的开源协议有很多，并且同一款协议有很多变种，比如你或许看到过 ' CC Attribution-NoDerivs'，' CC Attribution-NonCommercial' 同属 CC协议（后面会有介绍）。如此纷繁的协议该如何选择？协议太宽松会导致作者丧失对作品的很多权利，太严格又不便于使用者使用及作品的传播。所以除了协议多之外，你还要考虑你对作品想保留哪些权利，放开哪些限制。

如果你不想了解太多，只是想要一个简直直接的答案，下面给出的建议或许适合你。下方关于协议的选择及表格来自GitHub [choosealicence](http://choosealicense.com/)项目。

**（5）简单宽松的协议**

如果你只想要一个简单点的协议不想太麻烦的话。[MIT协议](http://choosealicense.com/licenses/mit)相对宽松但还是抓住了要点的。此协议允许别人以任何方式使用你的代码同时署名原作者，但原作者不承担代码使用后的风险，当然也没有技术支持的义务。jQuery 和 Rails 就是 MIT 协议。

**（6）考虑有专利的情况**

如果你的作品中涉及到专利相关。[Apache协议](http://choosealicense.com/licenses/apache/) 也是个相对宽松与 MIT 类似的协议，但它简单指明了作品归属者对用户专利上的一些授权（我的理解是软件作品中含有专利，但它授权你可以免费使用）。Apache 服务器，SVN 还有 NuGet 等是使用的 Apache 协议。

**（7）代码分享与促进**

如果你在乎作品的传播和别人的修改，希望别人也以相同的协议分享出来。

GPL（[V2](http://choosealicense.com/licenses/gpl-v2)或[V3](http://choosealicense.com/licenses/gpl-v3)）是一种版本自由的协议（可以参照 copy right 来理解，后者是版本保留，那 copyleft 便是版权自由，或者无版权，但无版权不代表你可以不遵守软件中声明的协议）。此协议要求代码分发者或者以此代码为基础开发出来的衍生作品需要以同样的协议来发布。此协议的版本 3 与版本 2 相近，只是多 3 中加了条对于不支持修改后代码运行的硬件的限制。

**（8）各协议授权的名词解释**

- 协议和版权信息(License and copyright notice)：在代码中保留作者提供的协议和版权信息
- 声明变更(State Changes)：在代码中声明对原来代码的重大修改及变更
- 公开源码(Disclose Source)：代码必需公开。如果是基于[LGPL协议](https://www.gnu.org/licenses/lgpl.html)  下，则只需使用的开源代码公开，不必将整个软件源码公开
- 库引用(Library usage)：该库可以用于商业软件中
- 责任承担(Hold Liable)：代码的作者承担代码使用后的风险及产生的后果
- 商标使用(Use Trademark)：可以使用作者的姓名，作品的Logo，或商标
- 附加协议(Sublicensing)：允许在软件分发传播过程中附加上原来没有的协议条款等

<table>
<thead>
<tr>
<th style="text-align:left">协议</th>
<th style="text-align:left">描述</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left"><a href="http://choosealicense.com/licenses/apache/" target="_blank" rel="nofollow">Apache</a></td>
<td style="text-align:left">一个较宽松且简明地指出了专利授权的协议。</td>
</tr>
<tr>
<td style="text-align:left"><a href="http://choosealicense.com/licenses/gpl-v2/" target="_blank" rel="nofollow">GPL</a></td>
<td style="text-align:left">此协议是应用最为广泛的开源协议，拥有较强的版权自由( copyleft )要求。衍生代码的分发需开源并且也要遵守此协议。此协议有许多变种，不同变种的要求略有不同。</td>
</tr>
<tr>
<td style="text-align:left"><a href="http://choosealicense.com/licenses/mit/" target="_blank" rel="nofollow">MIT</a></td>
<td style="text-align:left">宽松简单且精要的一个协议。在适当标明来源及免责的情况下，它允许你对代码进行任何形式的使用。</td>
</tr>
<tr>
<td style="text-align:left"><a href="http://choosealicense.com/licenses/artistic/" target="_blank" rel="nofollow">Artistic</a></td>
<td style="text-align:left">Perl 区尤为钟爱此协议。要求更改后的软件不能影响原软件的使用。</td>
</tr>
<tr>
<td style="text-align:left"><a href="http://choosealicense.com/licenses/bsd/" target="_blank" rel="nofollow">BSD</a></td>
<td style="text-align:left">较为宽松的协议，包含两个变种<a href="http://choosealicense.com/licenses/bsd" target="_blank" rel="nofollow"><strong>BSD 2-Clause</strong></a> 和<a href="http://choosealicense.com/licenses/bsd-3-clause" target="_blank" rel="nofollow"><strong>BSD 3-Clause</strong></a>，两者都与MIT协议只存在细微差异。</td>
</tr>
<tr>
<td style="text-align:left"><a href="http://choosealicense.com/licenses/eclipse/" target="_blank" rel="nofollow">Eclipse</a></td>
<td style="text-align:left">对商用非常友好的一种协议，可以用于软件的商业授权。包含对专利的优雅授权，并且也可以对相关代码应用商业协议。</td>
</tr>
<tr>
<td style="text-align:left"><a href="http://choosealicense.com/licenses/lgpl-v2.1/" target="_blank" rel="nofollow">LGPL</a></td>
<td style="text-align:left">主要用于一些代码库。衍生代码可以以此协议发布（言下之意你可以用其他协议），但与此协议相关的代码必需遵循此协议。</td>
</tr>
<tr>
<td style="text-align:left"><a href="http://choosealicense.com/licenses/mozilla/" target="_blank" rel="nofollow">Mozilla</a></td>
<td style="text-align:left">Mozilla Public License(MPL 2.0)是由Mozilla基金创建维护的。此协议旨在较为宽松的BSD协议和更加互惠的GPL协议中寻找一个折衷点。</td>
</tr>
<tr>
<td style="text-align:left"><a href="http://choosealicense.com/licenses/no-license/" target="_blank" rel="nofollow">No license</a></td>
<td style="text-align:left">你保留所有权利，不允许他人分发，复制或者创造衍生物。当你将代码发表在一些网站上时需要遵守该网站的协议，此协议可能包含了一些对你劳动成果的授权许可。比如你将代码发布到GitHub，那么你就必需同意别人可以查看和 Fork你的代码。</td>
</tr>
<tr>
<td style="text-align:left"><a href="http://choosealicense.com/licenses/unlicense/" target="_blank" rel="nofollow">Public domain dedication</a></td>
<td style="text-align:left">在许多国家，默认版权归作者自动拥有，所以<a href="http://unlicense.org/" target="_blank" rel="nofollow">Unlicense</a>协议提供了一种通用的模板，此协议表明你放弃版权，将劳动成果无私贡献出来。你将丧失对作品的全部权利，包括在MIT/X11中定义的无担保权利。</td>
</tr>
</tbody>
</table>

**（9）非代码类作品的协议**

上面各协议只是针对软件或代码作品，如果你的作品不是代码，比如视频，音乐，图片，文章等，共享于公众之前，也最好声明一下协议以保证自己的权益不被侵犯。针对非代码的数字作品的协议，最通用的莫过于[**Creative Commons**](http://creativecommons.org/choose/)(也是你经常在别人博客下面可以看到的CC协议)协议。所以现在你见到博客园别人文章下面的签名就不会感到陌生了。

**（10）无协议**

你没有义务也没人非要你必需在自己的代码作品里面加上一个开源协议。但一如上文所讨论过的优点，如果你想把代码分享出来，最好还是选择一个适合的开源协议，这样别人用着放心。

### 2.github下载加速

Github就像是一个巨大的宝藏库，内涵丰富的开源免费软件和优质的项目。但是，当想从Github下载自己喜欢的项目或软件时，会发现它的速度无比感人。1k、2k、1k、2k....就这样让人充满绝望。今天，就来给大家介绍**3种**方法，教你快速从Github下载想要的内容。



## Reference

1. https://blog.csdn.net/weixin_43729943/article/details/103915046
2. https://github.com/github/choosealicense.com
3. http://choosealicense.com/
4. http://www.smashingmagazine.com/2011/06/14/understanding-copyright-and-licenses/
5. https://www.jianshu.com/p/fabcf532ecd6
6. https://blog.csdn.net/weixin_42072280/article/details/122540366
7. https://www.jianshu.com/p/26176884e077
7. [Managing remote repositories](https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories)
