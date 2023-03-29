## 1、Git的前世今生

> 今生：

到目前为止，git是世界上使用最为广泛的分布式版本控制系统。大量软件项目依赖 Git 进行版本管理，其中既有开源软件，也有商业软件。Git 在很多操作系统和集成开发环境（IDE）上都表现良好。绝大多数软件开发者或多或少都使用过 Git。

> 前世：

Git 诞生于一个极富纷争大举创新的年代。Linus Torvalds 在1991年创建了开源的Linux，从此，Linux系统不断发展，已经成为最大的服务器系统软件了。Linus虽然创建了Linux，但Linux的壮大是靠全世界热心的志愿者参与的，这么多人在世界各地为Linux编写代码，那Linux的代码是如何管理的呢？事实是，在2002年以前，世界各地的志愿者把源代码文件通过diff的方式发给Linus，然后由Linus本人通过手工方式合并代码！

你也许会想，为什么Linus不把Linux代码放到版本控制系统里呢？不是有CVS、SVN这些免费的版本控制系统吗？因为Linus坚定地反对CVS和SVN，这些集中式的版本控制系统不但速度慢，而且必须联网才能使用。有一些商用的版本控制系统，虽然比CVS、SVN好用，但那是付费的，和Linux的开源精神不符。不过，到了2002年，Linux系统已经发展了十年了， 绝大多数的 Linux 内核维护工作都花在了提交补丁和保存归档的繁琐事务上（1991－2002年间）。 代码库之大让Linus很难继续通过手工方式管理了，社区的弟兄们也对这种方式表达了强烈不满，于是Linus选择了一个商业的版本控制系统BitKeeper，BitKeeper的东家BitMover公司出于人道主义精神，授权Linux社区免费使用这个版本控制系统。

安定团结的大好局面在2005年就被打破了，原因是Linux社区牛人聚集，不免沾染了一些梁山好汉的江湖习气。开发Samba的Andrew试图破解BitKeeper的协议(这么干的其实也不只他一个)，被BitMover公司发现了(监控工作做得不错！)，于是BitMover公司怒了，要收回Linux社区的免费使用权。Linus可以向BitMover公司道个歉，保证以后严格管教弟兄们，嗯，这是不可能的，在2005年，开发 BitKeeper 的商业公司同 Linux 内核开源社区的合作关系结束，他们收回了 Linux 内核社区免费使用 BitKeeper 的权力。

实际情况是这样的：Linus花了两周时间自己用C写了一个分布式版本控制系统，Linus对新的系统制订了若干目标：速度;简单的设计;对非线性开发模式的强力支持（允许成千上万个并行开发的分支）;完全分布式;有能力高效管理类似 Linux 内核一样的超大规模项目（速度和数据量）等，这就是Git！一个月之内，Linux系统的源码已经由Git管理了！牛是怎么定义的呢？大家可以体会一下。Git迅速成为最流行的分布式版本控制系统，尤其是2008年，GitHub网站上线了，它为开源项目免费提供Git存储，无数开源项目开始迁移至GitHub，包括jQuery，PHP，Ruby等等。历史就是这么偶然，如果不是当年BitMover公司威胁Linux社区，可能现在我们就没有免费而超级好用的Git了。

## 2、Git特点

> 版本控制：

可以解决多人同时开发的代码问题，也可以解决找回历史代码的问题。

> 分布式：

Git是分布式版本控制系统，同一个Git仓库，可以分布到不同的机器上。首先找一台电脑充当服务器的角色，每天24小时开机，其他每个人都从这个“服务器”仓库克隆一份到自己的电脑上，并且各自把各自的提交推送到服务器仓库里，也从服务器仓库中拉取别人的提交。可以自己搭建这台服务器，也可以使用GitHub网站。

> 高性能

Git 的底层性能相较于其他版本管理软件有强大的优势。提交修改、创建分支、合并分支和比较版本都针对性能进行了优化。Git 中实现的算法利用了现实中代码树的特点以及它们被修改和访问的常见模式。

不同于某些版本管理软件，Git 在决定文件树的储存和版本历史时，不会被文件名的变化所愚弄——Git 关注的是文件的内容本身。毕竟，代码文件经常会被重命名、拆分和重新编排。Git 仓库中的文件对象通过差分编码（delta encoding，仅保存代码修改的差分）和压缩技术储存，并且直接保存文件夹中的内容和版本控制元数据。

分布式架构也给 Git 带来了巨大的性能优势。

比如说，有一名开发成员 Alice 修改了代码，添加了一些准备在 2.0 版本中发布的功能，然后提交了这些修改及其描述。随后，她又编写并提交了另一个新功能。很自然地，这两次修改是版本历史中两份独立的工作。Alice 又切换到了 1.3 版本的分支，修复了一个只影响这个旧版本的 bug。这次修复的目的是为了让团队在 2.0 版本还没有完成之前，发布一个 1.3.1 版本来解决旧版本中的一些 bug。Alice 可以立刻回到 2.0 版本分支，继续新功能开发。这一切都不需要网络连接，非常快速可靠，甚至可以在飞机中完成。当她准备好将这些单独提交的更改发送到远程仓库时，她只需要一个“推送”（push）命令。

> 安全

Git 设计时就把托管代码的完好性作为重中之重。文件内容以及文件、目录、版本、标签和提交的关联，都通过安全的加密哈希校验算法（SHA1）保护。这可以避免代码和修改历史被不小心或者恶意改变，并且保证修改历史完全可追迹。

你可以相信在 Git 中源代码的修改历史是真实可靠的。

有一些版本管理软件无法防止版本历史之后被篡改。这对于任何依赖软件开发的团队来说都是严重的安全漏洞。

> 灵活

Git 的关键设计目标之一就是灵活。Git 在很多方面都展现出了其灵活性：支持多种非线性的工作流，对不同规模的项目来说都很高效，并且兼容多个操作系统和协议。

Git 在设计时最重要的功能便是分支和标签（不同于 SVN），因此所有影响分支和标签的操作也都会被保存到修改历史中。不是所有的版本管理软件关注的都是这个层面的版本追踪。

## 3、Git与SVN对比

> SVN

是集中式版本控制系统，版本库是集中放在中央服务器的，而开发人员工作的时候，用的都是自己的电脑，所以首先要从中央服务器下载最新的版本，然后开发，开发完后，需要把自己开发的代码提交到中央服务器。

集中式版本控制工具缺点：

- ​	服务器单点故障

- ​	容错性差

![SVN](https://gitee.com/nicolas-gaofeng/pic_store/raw/master/img/git/20211108144744.png)

> Git

是分布式版本控制系统（Distributed Version Control System，简称 DVCS） ，分为两种类型的仓库：本地仓库和远程仓库。

- 本地仓库：是在开发人员自己电脑上的Git仓库
- 远程仓库：是在远程服务器上的Git仓库
- Clone：克隆，就是将远程仓库复制到本地
- Push：推送，就是将本地仓库代码上传到远程仓库
- Pull：拉取，就是将远程仓库代码下载到本地仓库

![git_ll](https://gitee.com/nicolas-gaofeng/pic_store/raw/master/img/git/20211108144800.png)

## 4、Git基本概念

![img](https://gitee.com/nicolas-gaofeng/pic_store/raw/master/img/git/20211109100049.png)

> 版本库

- 前面看到的.git隐藏文件夹就是版本库，版本库中存储了很多配置信息、日志信息和文件版本信息等

- 工作目录（工作区）
  - 包含.git文件夹的目录就是工作目录，主要用于存放开发的代码
  - 对于`添加`、`修改`、`删除`文件的操作，都发生在工作区中

> 暂存区

- .git文件夹中有很多文件，其中有一个index文件就是暂存区，也可以叫做stage。暂存区是一个临时保存修改文件的地方，还有git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。因为我们创建git版本库时，git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

Git工作目录下的文件存在两种状态：

- untracked 
  - 未跟踪（未被纳入版本控制）


- tracked 
  - 已跟踪（被纳入版本控制）
    - Unmodified 未修改状态
    - Modified 已修改状态
    - Staged 已暂存状态


这些文件的状态会随着我们执行Git的命令发生变化

> 仓库区

- 仓库区表示个人开发的一个小阶段的完成
  - 仓库区中记录的各版本是可以查看并回退的
  - 但是在暂存区的版本一旦提交就再也没有了




## 5、Git工作流程

工作流程如下：

1．从远程仓库中克隆代码到本地仓库

2．从本地仓库中checkout代码然后进行代码修改

3．在提交前先将代码提交到暂存区

4．提交到本地仓库。本地仓库中保存修改的各个历史版本

5．修改完成后，需要和团队成员共享代码时，将代码push到远程仓库

![工作流程](https://gitee.com/nicolas-gaofeng/pic_store/raw/master/img/git/20211108144821.png)

Git 的工作就是创建和保存你项目的快照及与之后的快照进行对比。

## 6、Git安装

### 6.1 windows安装

​	[Git](https://git-scm.com/download/win)

- 对于 Windows 用户，安装后如果希望在全局的 cmd 中使用 Git，需要把 git.exe 加入 PATH 环境变量中，或在 Git Bash 中使用 Git。

### 6.2 Centos安装

如果你使用的系统是 Centos 安装命令为：

```shell
sudo yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel

sudo yum -y install git-core
```

### 6.3 Mac安装

Xcode Command Line Tools 自带 Git（`xcode-select --install`）

### 6.4 查看版本 

```shell
git --version
```

## 7、Git配置

当安装Git后首先要做的事情是设置用户名称和email地址。这是非常重要的，因为每次Git提交都会使用该用户信息。

Git 将配置项保存在三个单独的文件中，允许你分别对单个仓库、用户和整个系统设置。

- <repo>/.git/config – 特定仓库的设置。


- ~/.gitconfig – 特定用户的设置。这也是 `--global` 标记的设置项存放的位置。


- $(prefix)/etc/gitconfig – 系统层面的设置。

当这些文件中的配置项冲突时，本地仓库设置覆盖用户设置，用户设置覆盖系统设置。如果你打开期中一份文件，你会看到下面这些：

``` shell
[user]

name = John Smith

email = john@example.com

[alias]

st = status

co = checkout

br = branch

up = rebase

ci = commit

[core]

editor = vim
```

你可以用 `git config` 手动编辑这些值。

`git config` 命令允许你在命令行中配置你的 Git 安装（或是一个独立仓库）。这个命令定义了所有配置，从用户信息到仓库行为等等。一些常见的配置命令如下所列。

### 7.1 查看配置信息

```shell
########## 查看设置列表 ##########
git config --list

########## 查看用户名 ##########
git config user.name

########## 查看邮箱 ##########
git config user.email
```

### 7.2 设置用户信息 

```shell
git config user.name “***”
```

定义当前仓库所有提交使用的作者姓名。

```shell
git config user.email “*******@qq.cn”
```

定义当前用户所有提交使用的作者邮箱。

``` shell
git config --global user.name <name>

git config --global user.email <email>
```

如果用了 **--global** 选项，那么更改的配置文件就是位于你用户主目录下的那个，以后你所有的项目都会默认使用这里配置的用户信息。

如果要在某个特定的项目中使用其他名字或者电邮，只要去掉 --global 选项重新配置即可，新的设定保存在当前项目的 .git/config 文件里。

### 7.3 为git命令创建快捷方式（别名）

``` shell
git config alias.<shortcut> <command>

# 这种方式仅在当前Git存储库中配置快捷方式。 为了无论存储库如何都可以调用它，请使用通常的--global选项：
git config--global alias.amend 'commit --amend --no-edit'
```

> 栗子

例如，这种方法用于以下快捷方式：

```shell
git config alias.amend'commit --amend --no-edit'
```

现在可以简单地调用：

```shell
git amend
```

### 7.4 文本编辑器

设置Git默认使用的文本编辑器, 一般可能会是 Vi 或者 Vim。如果你有其他偏好，比如 Emacs 的话，可以重新设置：

```shell
git config --global core.editor emacs

# 选择你喜欢的文本编辑器

git config --global core.editor vim
```

### 7.5 差异分析工具

还有一个比较常用的是，在解决合并冲突时使用哪种差异分析工具。比如要改用 vimdiff 的话：

```shell
git config --global merge.tool vimdiff
```

Git 可以理解 kdiff3，tkdiff，meld，xxdiff，emerge，vimdiff，gvimdiff，ecmerge，和 opendiff 等合并工具的输出信息。

## 8、展示帮助信息

```shell
git help -g
```

The command output as below:

```text
The common Git guides are:
   attributes          Defining attributes per path
   cli                 Git command-line interface and conventions
   core-tutorial       A Git core tutorial for developers
   cvs-migration       Git for CVS users
   diffcore            Tweaking diff output
   everyday            A useful minimum set of commands for Everyday Git
   glossary            A Git Glossary
   hooks               Hooks used by Git
   ignore              Specifies intentionally untracked files to ignore
   modules             Defining submodule properties
   namespaces          Git namespaces
   repository-layout    Git Repository Layout
   revisions           Specifying revisions and ranges for Git
   tutorial            A tutorial introduction to Git
   tutorial-2          A tutorial introduction to Git: part two
   workflows           An overview of recommended workflows with Git

'git help -a' and 'git help -g' list available subcommands and some concept guides. See 'git help <command>' or 'git help <concept>' to read about a specific subcommand or concept.
```

## 9、在IDEA中配置Git

安装好IntelliJ IDEA后，如果Git安装在默认路径下，那么idea会自动找到git的位置，如果更改了Git的安装位置则需要手动配置下Git的路径。

选择File→Settings打开设置窗口，找到Version Control下的git选项：

![图片41](https://gitee.com/nicolas-gaofeng/pic_store/raw/master/img/git/20211108144919.png)

选择git的安装目录后可以点击“Test”按钮测试是否正确配置

![图片42](https://gitee.com/nicolas-gaofeng/pic_store/raw/master/img/git/20211108144925.png)

### 
