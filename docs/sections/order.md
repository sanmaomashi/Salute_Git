## 1、获取Git仓库

要使用Git对我们的代码进行版本控制，首先需要获得Git仓库。获取Git仓库通常有两种方式：

### 1.1 在本地初始化一个Git仓库

`git init` 命令创建一个新的 Git 仓库。它用来将已存在但还没有版本控制的项目转换成一个 Git 仓库，或者创建一个空的新仓库。大多数Git命令在未初始化的仓库中都是无法使用的，所以这就是你运行新项目的第一个命令了。

和 SVN 相比，`git init` 命令是一个创建新的版本控制项目非常简单的途径。Git 不需要你创建仓库，导入文件，检查正在修改的拷贝。你只需要 `cd` 到你的项目目录下，运行 `git init`，你就有了一个功能强大的 Git 仓库。

运行 `git init` 命令会在你项目的根目录下创建一个新的 `.git` 目录，其中包含了你项目必需的所有元数据。除了 `.git` 目录之外，已经存在的项目不会被改变（就像 SVN 一样，Git 不强制每个子目录中都有一个 `.git` 目录）。

执行命令：

```shell
git init
```

如果在当前目录中看到.git文件夹（此文件夹为隐藏文件夹）则说明Git仓库创建成功，通常，我们初始化本地仓库时，使用`git init`：建立一个标准的**Git仓库**。

![图片13](https://gitee.com/nicolas-gaofeng/pic_store/raw/master/img/git/20211106102359.png)

我们初始化远程服务器仓库时，使用`git init --bare`：建立一个“裸”的**Git仓库**。

这样的仓库初始化后，其项目目录下就是标准仓库`.git`目录里的内容，**没有工作空间**。

这个仓库只保存git历史提交的版本信息，而不允许用户在上面进行各种git操作（如：`push`、`commit`操作）。但是，你依旧可以使用`git show`命令查看提交内容：

``` shell
git init --bare <directory>
```

初始化一个裸的 Git 仓库，但是忽略工作目录。共享的仓库应该总是用 `--bare` 标记创建。一般来说，用 `—bare` 标记初始化的仓库以 `.git` 结尾。比如，一个叫`my-project`的仓库，它的空版本应该保存在 `my-project.git` 目录下。

> 裸仓库

`-—bare` 标记创建了一个没有工作目录的仓库，这样我们在仓库中更改文件并且提交了。中央仓库应该总是创建成裸仓库，因为向非裸仓库推送分支有可能会覆盖已有的代码变动。将`-—bare`看成是用来将仓库标记为储存设施，而不是一个开发环境。也就是说，对于所有的 Git 工作流，中央仓库是裸仓库，开发者的本地仓库是非裸仓库。

![](https://gitee.com/nicolas-gaofeng/pic_store/raw/master/img/git/20211108155034.svg)

> 栗子

因为 `git clone` 创建项目的本地拷贝更为方便，`git init` 最常见的使用情景就是用于创建中央仓库：

``` shell
ssh <user>@<host>

cd path/above/repo

git init --bare my-project.git
```

首先，你用SSH连入存放中央仓库的服务器。然后，来到任何你想存放项目的地方，最后，使用 `-—bare` 标记来创建一个中央存储仓库。开发者会将 `my-project.git` 克隆到本地的开发环境中。

### 1.2 从远程仓库克隆

对大多数项目来说，`git init` 只需要在创建中央仓库时执行一次——开发者通常不会使用 `git init` 来创建他们的本地仓库。他们往往使用 `git clone` 来将已存在的仓库拷贝到他们的机器中去。

如果你想获得一份已经存在了的 Git 仓库的拷贝，这时就要用到 git clone 命令。 Git 克隆的是该 Git 仓库服务器上的几乎所有数据（包括日志信息、历史记录等），而不仅仅是复制工作所需要的文件。 当你执行 git clone 命令的时候，默认配置下远程 Git 仓库中的每一个文件的每一个版本都将被拉取下来。

可以通过Git提供的命令从远程仓库进行克隆，将远程仓库克隆到本地，命令形式为：

```shell
git clone 远程仓库地址 
```

## 2、本地仓库操作

“保存”这个概念在 Git 等版本控制系统和 Word 等文本编辑应用中不太一样。传统软件里的“保存”在 Git 里被叫做“提交”（commit）。 我们常说的的保存可以理解成在文件系统中覆盖一个已有的文件或者创建一个新的文件。而在 Git 中，提交这个操作作用于若干个文件和目录。

在 Git 和 SVN 里保存更改也不一样。SVN 提交或检入（check-in）将会推送到远端的中央服务器。也就是说 SVN 的提交需要联网才能完全“保存”项目更改。Git 提交可以在本地完成，然后再使用`git push -u origin master`命令推送到远端服务器。这两种方法的区别体现了两种架构设计的本质区别。Git 是一个分布式的应用，而 SVN 是一个中心化的应用。分布式应用一般来说更可靠，因为它们不存在中央服务器这样的单点故障。

`git add`、`git status`和`git commit`这三个命令通常一起使用，将 Git 项目当前的状态保存成一份快照。

### 2.1 查看仓库状态

`git status` 命令显示工作目录和缓存区的状态。你可以看到哪些更改被缓存了，哪些还没有，以及哪些还未被 Git 追踪。status 的输出 *不会* 告诉你任何已提交到项目历史的信息。命令形式为：

```shell
########## 列出已缓存、未缓存、未追踪的文件 ##########
git status 

########## 使输出信息更加简洁 ##########
git status –s

########## 展示所有 stashes ##########
git stash list
```

### 2.2  文件加入暂存区

`git add` 命令将工作目录中的变化添加到暂存区。它告诉 Git 你想要在下一次提交时包含这个文件的更新。但是，`git add` 不会实质上地影响你的仓库——在你运行 `git commit` 前更改都还没有真正被记录。

将文件添加到暂存区

```shell
git add <file>
```

将 `<file>` 中的更改加入下次提交的缓存。

```shell
git add .
```

添加项目中所有文件 

```shell
git add <directory>
```

将 `<directory>` 下的更改加入下次提交的缓存。

```shell
git add -i
```

开始交互式的缓存，你可以选择文件的一部分加入到下次提交缓存。它会向你展示一堆更改，等待你输入一个命令。`y` 将这块更改加入缓存，`n` 忽略这块更改，`s` 将它分割成更小的块，`e` 手动编辑这块更改，以及 `q` 退出。

### 2.3 回滚修改

#### 2.3.1 checkout

版本控制系统背后的思想就是「安全」地储存项目的拷贝，这样你永远不用担心什么时候不可复原地破坏了你的代码库。当你建立了项目历史之后，`git checkout` 是一种便捷的方式，来将保存的快照「加载」到你的开发机器上去。

检出之前的提交是一个只读操作。在查看旧版本的时候绝不会损坏你的仓库。你项目「当前」的状态在	`master` 上不会变化。在开发的正常阶段，`HEAD` 一般指向 master 或是其他的本地分支，但当你检出之前提交的时候，`HEAD` 就不再指向一个分支了——它直接指向一个提交。

`git checkout` 这个命令有三个不同的作用：检出文件、检出提交和检出分支。

检出提交会使工作目录和这个提交完全匹配。你可以用它来查看项目之前的状态，而不改变当前的状态。检出文件使你能够查看某个特定文件的旧版本，而工作目录中剩下的文件不变。

回到 master 分支。你只需要将它视为回到项目「当前」状态的一种方式。

```shell
git checkout master
```

查看文件之前的版本。它将工作目录中的 `<file>` 文件变成 `<commit>` 中那个文件的拷贝，并将它加入缓存区。

```shell
git checkout <commit> <file>
```

更新工作目录中的所有文件，使得和某个特定提交中的文件一致。你可以将提交的哈希字串，或是标签作为 `<commit>` 参数。这会使你处在分离 HEAD 的状态。

```shell
git checkout <commit>
```

放弃所有修改：

```shell
git checkout .
```

> 栗子

查看之前的版本

这个栗子假定你开始了一个疯狂的实验，但你不确定你是否想要保留它。为了帮助你决定，你想看一看你开始实验之前的项目状态。首先，你需要找到你想要看的那个版本的 ID。

```shell
git log --oneline
```

假设你的项目历史看上去和下面一样：

```text
b7119f2 继续做些丧心病狂的事
872fa7e 做些丧心病狂的事
a1e8fb5 对 hello.py 做了一些修改
435b61d 创建 hello.py
9773e52 初始导入
```

你可以这样使用 `git checkout` 来查看「对 hello.py 做了一些修改」这个提交：

```shell
git checkout a1e8fb5
```

这让你的工作目录和 `a1e8fb5` 提交所处的状态完全一致。你可以查看文件，编译项目，运行测试，甚至编辑文件而不需要考虑是否会影响项目的当前状态。你所做的一切 *都不会* 被保存到仓库中。为了继续开发，你需要回到你项目的「当前」状态：

```shell
git checkout master
```

这里假定了你默认在 master 分支上开发，我们会在以后的分支模型中详细讨论。

一旦你回到 master 分支之后，你可以使用 `git revert` 或 `git reset` 来回滚任何不想要的更改。

> 检出文件

如果你只对某个文件感兴趣，你也可以用 `git checkout` 来获取它的一个旧版本。比如说，如果你只想从之前的提交中查看 `hello.py` 文件，你可以使用下面的命令：

```shell
git checkout a1e8fb5 hello.py
```

记住，和检出提交不同，这里 *确实* 会影响你项目的当前状态。旧的文件版本会显示为「需要提交的更改」，允许你回滚到文件之前的版本。如果你不想保留旧的版本，你可以用下面的命令检出到最近的版本：

```shell
git checkout HEAD hello.py
```

#### 2.3.2  revert

`git revert` 命令用来撤销一个已经提交的快照。但是，它是通过搞清楚如何撤销这个提交引入的更改，然后在最后加上一个撤销了更改的新提交，而不是从项目历史中移除这个提交。这避免了Git丢失项目历史，这一点对于你的版本历史和协作的可靠性来说是很重要的。

![Git Tutorial: git revert](https://wac-cdn.atlassian.com/dam/jcr:b6fcf82b-5b15-4569-8f4f-a76454f9ca5b/03%20(7).svg)

> 用法

```shell
git revert <commit>
```

生成一个撤消了 `<commit>` 引入的修改的新提交，然后应用到当前分支。

> 讨论

撤销（revert）应该用在你想要在项目历史中移除一整个提交的时候。比如说，你在追踪一个 bug，然后你发现它是由一个提交造成的，这时候撤销就很有用。与其说自己去修复它，然后提交一个新的快照，不如用 `git revert`，它帮你做了所有的事情。

> 撤销（revert）和重设（reset）对比

理解这一点很重要。`git revert` 回滚了「单独一个提交」，它没有移除后面的提交，然后回到项目之前的状态。在 Git 中，后者实际上被称为 `reset`，而不是 `revert`。

![Git Tutorial: Revert vs Reset](https://gitee.com/nicolas-gaofeng/pic_store/raw/master/img/git/20211109103015.svg)

撤销和重设相比有两个重要的优点。首先，它不会改变项目历史，对那些已经发布到共享仓库的提交来说这是一个安全的操作。

其次，`git revert` 可以针对历史中任何一个提交，而 `git reset` 只能从当前提交向前回溯。比如，你想用 `git reset` 重设一个旧的提交，你不得不移除那个提交后的所有提交，再移除那个提交，然后重新提交后面的所有提交。不用说，这并不是一个优雅的回滚方案。

> 栗子

下面的这个栗子是 `git revert` 一个简单的演示。它提交了一个快照，然后立即撤销这个操作。

```shell
# 编辑一些跟踪的文件

# 提交一份快照
git commit -m "Make some changes that will be undone"

# 撤销刚刚的提交
git revert HEAD
```

#### 2.3.3 reset

如果说 `git revert` 是一个撤销更改安全的方式，你可以将 `git reset` 看做一个 *危险* 的方式。当你用 `git reset` 来重设更改时(提交不再被任何引用或引用日志所引用)，我们无法获得原来的样子——这个撤销是永远的。使用这个工具的时候务必要小心，因为这是少数几个可能会造成工作丢失的命令之一。

和 `git checkout` 一样，`git reset` 有很多种用法。它可以被用来移除提交快照，尽管它通常被用来撤销缓存区和工作目录的修改。不管是哪种情况，它应该只被用于 *本地* 修改——你永远不应该重设和其他开发者共享的快照。

> 用法

```shell
git reset <file>
```

从缓存区移除特定文件，但不改变工作目录。它会取消这个文件的缓存，而不覆盖任何更改。

```shell
git reset
```

重设缓冲区，匹配最近的一次提交，但工作目录不变。它会取消 *所有* 文件的缓存，而不会覆盖任何修改，给你了一个重设缓存快照的机会。

```shell
git reset --hard
```

重设缓冲区和工作目录，匹配最近的一次提交。除了取消缓存之外，`--hard` 标记告诉 Git 还要重写所有工作目录中的更改。换句话说：它清除了所有未提交的更改，所以在使用前确定你想扔掉你所有本地的开发。

```shell
git reset <commit>
```

将当前分支的末端移到 `<commit>`，将缓存区重设到这个提交，但不改变工作目录。所有 `<commit>` 之后的更改会保留在工作目录中，这允许你用更干净、原子性的快照重新提交项目历史。

```shell
git reset --hard <commit>
```

将当前分支的末端移到 `<commit>`，将缓存区和工作目录都重设到这个提交。它不仅清除了未提交的更改，同时还清除了 `<commit>` 之后的所有提交。

> 讨论

上面所有的调用都是用来移除仓库中的修改。没有 `--hard` 标记时 `git reset` 通过取消缓存或取消一系列的提交，然后重新构建提交来清理仓库。而加上 `--hard` 标记对于作了大死之后想要重头再来尤其方便。

撤销(revert)被设计为撤销 *公开* 的提交的安全方式，`git reset`被设计为重设 *本地* 更改。因为两个命令的目的不同，它们的实现也不一样：重设完全地移除了一堆更改，而撤销保留了原来的更改，用一个新的提交来实现撤销。

> 不要重设公共历史

当有 `<commit>` 之后的提交被推送到公共仓库后，你绝不应该使用 `git reset`。发布一个提交之后，你必须假设其他开发者会依赖于它。

移除一个其他团队成员在上面继续开发的提交在协作时会引发严重的问题。当他们试着和你的仓库同步时，他们会发现项目历史的一部分突然消失了。下面的序列展示了如果你尝试重设公共提交时会发生什么。`origin/master` 是你本地 `master` 分支对应的中央仓库中的分支。

![Git Tutorial: Resetting an Public Commit](https://gitee.com/nicolas-gaofeng/pic_store/raw/master/img/git/20211109103204.svg)

一旦你在重设之后又增加了新的提交，Git 会认为你的本地历史已经和 `origin/master` 分叉了，同步你的仓库时的合并提交（merge commit）会使你的同事困惑。

重点是，确保你只对本地的修改使用 `git reset`，而不是公共更改。如果你需要修复一个公共提交，`git revert` 命令正是被设计来做这个的。

> 栗子

> 取消文件缓存

`git reset` 命令在准备缓存快照时经常被用到。下面的例子假设你有两个文件，`hello.py` 和 `main.py`它们已经被加入了仓库中。

```shell
# 编辑了hello.py和main.py

# 缓存了目录下所有文件
git add .

# 意识到hello.py和main.py中的修改
# 应该在不同的快照中提交

# 取消main.py缓存
git reset main.py

# 只提交hello.py
git commit -m "Make some changes to hello.py"

# 在另一份快照中提交main.py
git add main.py
git commit -m "Edit main.py"
```

如你所见，`git reset` 帮助你取消和这次提交无关的修改，让提交能够专注于某一特定的范围。

> 移除本地修改

下面的这个栗子显示了一个更高端的用法。它展示了你作了大死之后应该如何扔掉那几个更新。

```shell
# 创建一个叫`foo.py`的新文件，增加代码

# 提交到项目历史
git add foo.py
git commit -m "Start developing a crazy feature"

# 再次编辑`foo.py`，修改其他文件

# 提交另一份快照
git commit -a -m "Continue my crazy feature"

# 决定废弃这个功能，并删除相关的更改
git reset --hard HEAD~2
```

`git reset HEAD~2` 命令将当前分支向前倒退两个提交，相当于在项目历史中移除刚创建的这两个提交。记住，这种重设只能用在 *非公开* 的提交中。绝不要在将提交推送到共享仓库之后执行上面的操作。

#### 2.3.4 clean

`git clean` 命令将未跟踪的文件从你的工作目录中移除。它只是提供了一条捷径，因为用 `git status` 查看哪些文件还未跟踪然后手动移除它们也很方便。和一般的 `rm` 命令一样，`git clean` 是无法撤消的，所以在删除未跟踪的文件之前想清楚，你是否真的要这么做。

`git clean` 命令经常和 `git reset --hard` 一起使用。记住，reset 只影响被跟踪的文件，所以还需要一个单独的命令来清理未被跟踪的文件。这个两个命令相结合，你就可以将工作目录回到之前特定提交时的状态。

> 用法

```shell
git clean -n
```

执行一次git clean的『演习』。它会告诉你那些文件在命令执行后会被移除，而不是真的删除它。

```shell
git clean -f
```

移除当前目录下未被跟踪的文件。`-f`（强制）标记是必需的，除非 `clean.requireForce` 配置项被设为了 `false`（默认为 `true`）。它 *不会* 删除 `.gitignore` 中指定的未跟踪的文件。

```shell
git clean -f <path>
```

移除未跟踪的文件，但限制在某个路径下。

```shell
git clean -df
```

移除未跟踪的文件，以及目录。

```shell
git clean -xf
```

移除当前目录下未跟踪的文件，以及 Git 一般忽略的文件。

> 讨论

如果你在本地仓库中作死之后想要毁尸灭迹，`git reset --hard` 和 `git clean -f` 是你最好的选择。运行这两个命令使工作目录和最近的提交相匹配，让你在干净的状态下继续工作。

`git clean` 命令对于 build 后清理工作目录十分有用。比如，它可以轻易地删除 C 编译器生成的 `.o` 和 `.exe` 二进制文件。这通常是打包发布前需要的一步。`-x` 命令在这种情况下特别方便。

请牢记，和 `git reset` 一样， `git clean` 是仅有的几个可以永久删除提交的命令之一，所以要小心使用。事实上，它太容易丢掉重要的修改了，以至于 Git 厂商 *强制* 你用 `-f` 标志来进行最基本的操作。这可以避免你用一个 `git clean` 就不小心删除了所有东西。

> 栗子

下面的栗子清除了工作目录中的所有更改，包括新建还没加入缓存的文件。它假设你已经提交了一些快照，准备开始一些新的实验。

```shell
# 编辑了一些文件
# 新增了一些文件
# 『糟糕』

# 将跟踪的文件回滚回去
git reset --hard

# 移除未跟踪的文件
git clean -df
```

在执行了 reset/clean 的流程之后，工作目录和缓存区和最近一次提交看上去一模一样，而  `git status`会认为这是一个干净的工作目录。你可以重新来过了。

注意，不像 `git reset` 的第二个栗子，新的文件没有被加入到仓库中。因此，它们不会受到 `git reset --hard` 的影响，需要 `git clean` 来删除它们。

### 2.4  将暂存区的文件提交到本地仓库

```shell
git commit
```

提交已经缓存的快照。它会运行文本编辑器，等待你输入提交信息。当你输入信息之后，保存文件，关闭编辑器，创建实际的提交。输入 i 变成插入模式，然后按esc  输入：wq 退出

```shell
git commit -m "随便的日志信息str"
```

提交已经缓存的快照。但将 `<message>` 作为提交信息，而不是运行文本编辑器。

```shell
git commit -a
```

提交一份包含工作目录所有更改的快照。它只包含跟踪过的文件的更改（那些之前已经通过 `git add` 添加过的文件）。

添加和提交合并命令:

```shell
git commit -am "版本描述"
```

- 提交两次代码，会有两个版本记录

> 优雅的Commit信息

使用[Angular团队提交规范](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#-git-commit-guidelines)

主要有以下组成

* 标题行: 必填, 描述主要修改类型和内容
* 主题内容: 描述为什么修改, 做了什么样的修改, 以及开发的思路等等
* 页脚注释: 放 Breaking Changes 或 Closed Issues

常用的修改项

* type: commit 的类型
* feat: 新特性
* fix: 修改问题
* refactor: 代码重构
* docs: 文档修改
* style: 代码格式修改, 注意不是 css 修改
* test: 测试用例修改
* chore: 其他修改, 比如构建流程, 依赖管理.
* scope: commit 影响的范围, 比如: route, component, utils, build...
* subject: commit 的概述
* body: commit 具体修改内容, 可以分为多行
* footer: 一些备注, 通常是 BREAKING CHANGE 或修复的 bug 的链接.

> commit工具

可以使用[cz-cli](https://github.com/commitizen/cz-cli)工具代替 `git commit`

全局安装

```shell
npm install -g commitizen cz-conventional-changelog

echo '{ "path": "cz-conventional-changelog" }' > ~/.czrc
```

全局安装后使用 `git cz` 代替 `git commit`就可以了,如下图

![](https://gitee.com/nicolas-gaofeng/pic_store/raw/master/img/git/20211108143319.png)



### 3.4  删除文件

```shell
git rm 文件名
git commit -m "str"
```

上面删除的只是工作区的文件，需要提交到本地仓库（git commit -m "str"）,rm命令默认将文件添加到暂存区，而直接通过右键删除的方式没有将文件添加到暂存区，需要手动添加文件到暂存区之后（git add 文件名）才能commit。

命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。

找回删错的文件

```shell
git checkout – 文件名
```

### 3.5 将文件添加至忽略列表

一般我们总会有些文件无需纳入Git 的管理，也不希望它们总出现在未跟踪文件列表。 通常都是些自动生成的文件，比如日志文件，或者编译过程中创建的临时文件等。 在这种情况下，我们可以在工作目录中创建一个名为 .gitignore 的文件（文件名称固定），列出要忽略的文件模式。下面是一个示例：

windows下 .gitignore文件的创建方式，右键Git bush here里输入touch .gitignore 

```text
# no .a files
*.a
# but do track lib.a, even though you're ignoring .a files above
!lib.a
# only ignore the TODO file in the current directory, not subdir/TODO
/TODO
# ignore all files in the build/ directory
build/
# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt
# ignore all .pdf files in the doc/ directory
doc/**/*.pdf
```

### 3.6 查看日志记录

`git log` 命令显示已提交的快照。你可以列出项目历史，筛选，以及搜索特定更改。`git status` 允许你查看工作目录和缓存区，而 `git log` 只作用于提交的项目历史。

log 输出可以有很多种自定义的方式，从简单地筛选提交，到用完全自定义的格式显示。其中一些最常用的 `git log` 配置如下所示。

```shell
git log 
```

按回车查看信息，出现end代表显示完毕。按q可以退出log页面

![image-20211106101822381](https://gitee.com/nicolas-gaofeng/pic_store/raw/master/img/git/20211106101827.png)



git reflog命令可以查看我们的操作记录。

```shell
git reflog
```

![image-20211106101942974](https://gitee.com/nicolas-gaofeng/pic_store/raw/master/img/git/20211106101943.png)



查看某段代码是谁写的,blame 的意思为‘责怪’，你懂的。

```shell
git blame <file-name>
```

`git log` 命令是 Git 查看项目历史的基本工具。当你要寻找项目特定的一个版本或者弄明白合并功能分支时引入了哪些变化，你就会用到这个命令。

```
commit 3157ee3718e180a9476bf2e5cab8e3f1e78a73b7
Author: John Smith
```

> 讨论

大多数时候都很简单直接。但是，第一行需要解释下。`commit` 后面 40 个字的字符串是提交内容的 SHA-1 校验总和（checksum）。它有两个作用。一是保证提交的正确性——如果它被损坏了，提交会生成一个不同的校验总和。第二，它是提交唯一的标识 ID。

这个 ID 可以用于 `git log` 这样的命令中来引用具体的提交。比如，`git log 3157e..5ab91` 会显示所有ID在 `3157e` 和 `5ab91` 之间的提交。除了校验总和之外，分支名、HEAD 关键字也是常用的引用提交的方法。`HEAD` 总是指向当前的提交，无论是分支还是特定提交也好。

~字符用于表示提交的父节点的相对引用。比如，`3157e~1` 指向 `3157e` 前一个提交,`HEAD~3` 是当前提交的回溯3个节点的提交。

所有这些标识方法的背后都是为了让你对特定提交进行操作。`git log` 命令一般是这些交互的起点，因为它让你找到你想要的提交。

### 3.7 回退到某个版本

其中HEAD表示当前最新版本，HEAD^表示当前版本的前一个版本,HEAD^^表示当前版本的前前个版本，也可以使用HEAD~1表示当前版本的前一个版本,HEAD~100表示当前版本的前100版本。

```shell
git reset --hard HEAD^
git reset --hard 指定版本号
```

![image-20211106102103350](https://gitee.com/nicolas-gaofeng/pic_store/raw/master/img/git/20211106102103.png)

### 3.8 查看冲突文件列表

展示工作区的冲突文件列表

```bash
git diff --name-only --diff-filter=U
```

### 3.9 展示工作区和暂存区的不同

输出**工作区**和**暂存区**的 different (不同)。

```bash
git diff
```

还可以展示本地仓库中任意两个 commit 之间的文件变动：

```bash
git diff <commit-id> <commit-id>
```

### 3.10 展示暂存区和最近版本的不同

输出**暂存区**和本地最近的版本 (commit) 的 different (不同)。

```bash
git diff --cached
```

### 3.11 展示暂存区、工作区和最近版本的不同

输出**工作区**、**暂存区** 和本地最近的版本 (commit) 的 different (不同)。

```bash
git diff HEAD
```



## 3、远程仓库操作

### 4.1 查看远程仓库

如果想查看已经配置的远程仓库服务器，可以运行 git remote 命令。 它会列出指定的每一个远程服务器的简写。 如果已经克隆了远程仓库，那么至少应该能看到 origin ，这是 Git 克隆的仓库服务器的默认名字

```bash
 git remote 
 
 ########## 显示远程地址 fetch代表抓取 push代表推送 ##########
 git remote -v
 
 ########## 显示更详细的信息 ##########
 git remote show origin
```

![image-20211106102616126](https://gitee.com/nicolas-gaofeng/pic_store/raw/master/img/git/20211106102616.png)

### 4.2  添加远程仓库

运行以下命令添加一个新的远程 Git 仓库，同时指定一个可以引用的简写。远程仓库的名称跟本地仓库名称可以不一致，但最好一致。一个本地仓库可以添加多个远程地址。

```bash
git remote add <shortname> <url>      
git remote add origin <url>   
```

### 4.3 移除无效的远程仓库 

如果因为一些原因想要移除一个远程仓库 ，可以使用

```bash
git remote rm 名称
```

注意：此命令只是从本地移除远程仓库的记录，并不会真正影响到远程仓库，远程仓库还是存在的

### 4.4 从远程仓库中抓取与拉取 

git fetch 是从远程仓库获取最新版本到本地仓库，不会自动merge

```bash
git fetch

########## 从origin仓库抓取master分支数据 ##########
git fetch origin master

########## 通过git merge手动合并 ##########
git merge origin master
```

git pull 是从远程仓库获取最新版本并merge到本地仓库

```bash
git pull
```

注意：如果当前本地仓库不是从远程仓库克隆，而是本地创建的仓库，并且仓库中存在文件，此时再从远程仓库拉取文件的时候会报错（fatal: refusing to merge unrelated histories ），解决此问题可以在git pull命令后加入参数--allow-unrelated-histories

```bash
git pull --allow-unrelated-histories
```

要求输入日志时直接输入 :wq！退出即可。

### 4.5 推送到远程仓库 

当你想分享你的代码时，可以将其推送到远程仓库。

 命令形式：

```bash
git push [remote-name][branch-name]


########## 强制推送 ##########
git push -f <remote-name> <branch-name>
```

### 4.6 回到远程仓库的状态

抛弃本地所有的修改，回到远程仓库的状态。

```bash
git fetch --all && git reset --hard origin/master
```

### 4.7 修改远程仓库的 url

```bash
git remote set-url origin <URL>
```



## 4、Git标签

像其他版本控制系统（VCS）一样，Git 可以给历史中的某一个提交打上标签，以示重要。 比较有代表性的是人们会使用这个功能来标记发布结点（v1.0 、v1.2等）。标签指的是某个分支某个特定时间点的状态。通过标签，可以很方便的切换到标记时的状态。

### 5.1 列出已有的标签

```bash
git tag
```

展示当前分支的最近的 tag

```bash
git describe --tags --abbrev=0
```

### 5.2 查看tag信息

```bash
git show [tag]

########## 查看标签详细信息 ##########
git tag -ln
```

### 5.3 创建新标签

```bash
git tag [tagName]
```

默认 tag 是打在最近的一次 commit 上，如果需要指定 commit 打 tag：

```bash
git tag -a <version-number> -m "v1.0 发布(描述)" <commit-id>
```

### 5.4 将标签推送至远程仓库

首先要保证本地创建好了标签才可以推送标签到远程仓库：

```bash
git push [remote] [tag] # 提交指定tag
git push origin v0.1
```

一次性推送所有标签，同步到远程仓库：

```bash
git push origin --tags
```

### 5.5 检出标签

```bash
git checkout -b [branch] [tag] # 新建一个分支，指向某个tag
```

### 5.6 删除标签

> 删除本地tag

```bash
git tag -d [tag] 
```

> 删除远程标签

```bash
git push origin :refs/tags/[tag] 

# or
git push origin --delete tag <tagname>
```

### 5.7 切回到某个标签

一般上线之前都会打 tag，就是为了防止上线后出现问题，方便快速回退到上一版本。下面的命令是回到某一标签下的状态：

```bash
git checkout -b branch_name tag_name
```

