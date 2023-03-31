  # GitHub托管平台使用

GitHub是一个代码托管平台，开发者可以在上面创建自己的代码仓库，并将代码上传到这些仓库中，以便与其他开发者进行协作、版本控制、代码共享和代码存档等操作。

  ## 一、注册账户

首先我们来到[GitHub](https://github.com/)的官网，点击右上角的sign up注册（sign in是登录），创建一个GitHub账户。

输入用户名、邮箱及密码等信息，并完成验证过程，加入GitHub即可。

  ## 二、创建仓库

注册github账户，登录后，点击"New respository "，在新页面中，输入项目的名称，选择自己仓库的相关配置。

> 页面配置说明

### 1. `Repository name`

输入框输入自己仓库的名字，建议填写一个与项目相关的名字，系统会自动检测名称是否重复。

### 2. `Descriptioin（optional）`

对创建仓库的描述，当然，这个可以选填。

### 3. `Public && Private`

Public即为公众的，选了Public即代表你的仓库代码为公开的，仓库内的所有内容都会被公开。

Private即为私有的，选了Private即代表你的仓库为私密的，当然你选了这个也可以自己设置访问权限。相比Public多了一些功能，并且是收费的。如果只是自己的练习或者不重要的信息，当然我们没必要去选择付费的这一项。

### 4. `Initialize this repository with --- ADD a README file`

如果勾选了这个选项，那么它就代表着GitHub会自动初始化仓库并且设置README文件，可以让你立刻clone这个仓库。clone意思就是本地没有repository（仓库）时，将远程repository（仓库）整个下载过来。如果不勾选它，那么，你可以手动push。将已经有的Git仓库添加到GitHub。

### 5. `Initialize this repository with --- Add .gitignore`

在使用git作版本控制时，git会默认把git控制的文件夹里面的所有文件都加入到版本控制。但是在实践中，我们经常会遇到不想某些文件或文件夹被git追踪的情况。比如logs文件、代码构建过程中产生的一些列文件，要解决这种问题,通常情况下我们需要创建一个文件格式后缀名为.gitignore的文件，来控制那些文件不被git追踪。

这里所说的git追踪，通俗一点来讲就是在我们push上传文件的时候，这些文件不会被上传。只会存在你本地的磁盘里，不会随你要上传的文件一起上传，它会被滤过。

下拉菜单中有多种语言及框架，看你的需要进行选择。

### 6. `Initialize this repository with --- Choose a license`

这个下拉菜单意思是给你的代码仓库添加一个许可证，你可以根据需求进行选择。比如我添加一个开源许可证，当别人浏览我的代码仓库时，别人也可以进行修改我仓库中的项目。

随后会生成包含许可协议内容的LICENSE文件，用来表明你的仓库内容的许可协议。

### 7. Create repository

添加成功后，点击Create repository按钮，即完成仓库的创建，并转到文件列表页面。

## 三、删除仓库

如果你需要删除GitHub上的某个仓库，可以按照以下步骤进行操作：

1. 登录GitHub账户，并进入需要删除的仓库所在的页面。
2. 点击页面右上角的“Settings”按钮，进入仓库设置页面。
3. 在设置页面的下方，找到“Danger Zone”区域。
4. 点击“Delete this repository”按钮，弹出确认框。
5. 在确认框中输入仓库名称，确认删除操作，仓库将被永久删除。

注意：删除仓库是不可逆的操作，一旦删除，将无法恢复。在删除仓库之前，请确保你已经备份好仓库中的所有数据，以免造成不必要的损失。

另外，如果你是仓库的拥有者，还可以将仓库转移给其他用户或者组织，以便他们继续维护该仓库。

## 四、删除某个文件夹

要从GitHub仓库中删除一个文件夹，可以按照以下步骤进行操作：

1. 打开需要删除文件夹的仓库，进入仓库主页。
2. 点击要删除的文件夹进入该文件夹，确保你要删除的是正确的文件夹。
3. 点击文件夹右上角的“Delete”按钮。
4. 弹出确认框，输入要删除文件夹的名称，并点击“Delete”按钮。
5. 文件夹将被永久删除。

需要注意的是，删除文件夹也是不可逆的操作，删除之前请务必确认你要删除的文件夹是正确的，并且已经备份了所有需要保留的文件。另外，删除文件夹可能会影响到该文件夹下面的所有文件，如果不确定是否需要删除，请谨慎考虑。

  ## 五、下载项目

要下载GitHub上的一个项目，可以按照以下步骤进行操作：

1. 打开需要下载的GitHub项目的仓库页面。
2. 点击页面右上角的“Code”按钮。
3. 选择“Download ZIP”选项，开始下载项目压缩包。
4. 下载完成后，解压压缩包，即可获取项目的所有文件。

另外，如果你已经安装了git客户端，也可以通过git clone命令来下载GitHub上的项目。具体操作步骤如下：

1. 打开需要下载的GitHub项目的仓库页面。
2. 点击页面右上角的“Code”按钮。
3. 复制仓库的URL地址。
4. 在本地打开终端或命令行工具，使用cd命令进入你要保存项目的目录。
5. 执行以下命令：git clone [仓库URL地址]，其中[仓库URL地址]替换为你刚才复制的仓库URL地址。
6. 等待下载完成后，即可在本地获取项目的所有文件。

通过以上方法，你可以很方便地从GitHub上下载任何你需要的开源项目或代码仓库。

## 六、更改远程跟踪链接

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

需要注意的是，更改远程跟踪链接将会影响到所有本地分支与该远程仓库的关联。如果不确定操作，请谨慎考虑，并确保备份所有数据。

## 七、githubpages

GitHub Pages是GitHub提供的一项免费服务，允许用户将自己的网站或静态页面托管在GitHub上，并通过特定的URL地址进行访问。以下是使用GitHub Pages的一些步骤：

1. 创建仓库：首先，你需要在GitHub上创建一个新的仓库，用于托管你的网站或静态页面。
2. 选择主题：在仓库中，你可以选择一个适合你网站主题的Jekyll主题或者直接上传HTML、CSS等静态页面。
3. 配置设置：在仓库的“Settings”页面中，找到“GitHub Pages”选项，选择你要托管的分支和文件夹。
4. 访问网站：完成以上设置后，你的网站就可以通过类似于https://username.github.io/repository的URL地址进行访问了。
5. 自定义域名：如果你想使用自己的域名访问网站，可以在“Custom domain”选项中设置自定义域名，并在域名管理后台中添加相应的DNS记录。

总之，GitHub Pages是一个非常方便的托管静态网站和页面的服务，使用起来也比较简单。如果你需要搭建一个简单的个人网站或者展示静态页面，可以尝试使用GitHub Pages来实现。

## 八、探索

### 1. 如何写属于自己的 license（软件协议）？

 **（1）最为方便的license创建方式：**

当你在 GitHub 上你创建新的 repository 的时候，你可以直接选择一些比较好的 license

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



