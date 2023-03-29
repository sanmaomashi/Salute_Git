## 1、工作使用git

> 项目经理:

(1)   项目经理搭建项目的框架。

(2)   搭建完项目框架之后，项目经理把项目框架代码放到服务器。

> 普通员工:

(1)  在自己的电脑上，生成ssh公钥，然后把公钥给项目经理，项目经理把它添加的服务器上面。

(2)  项目经理会给每个组员的项目代码的地址，组员把代码下载到自己的电脑上。

(3)  创建本地的分支dev,在dev分支中进行每天的开发。

(4)  每一个员工开发完自己的代码之后，都需要将代码发布远程的dev分支上。

3. 项目里通常会添加两个分支：

Master:用户保存发布的项目代码。V1.0,V2.0

Dev:保存开发过程中的代码。

## 2、Git分支

### 2.1 概念

几乎所有的版本控制系统都以某种形式支持分支。使用分支意味着你可以把你的工作从开发主线上分离开来，以免影响开发主线。Git的master分支并不是一个特殊分支。 它跟其它分支没有区别。 之所以几乎每一个仓库都有 master 分支，是因为git init 命令默认创建它，并且大多数人都懒得去改动它。

分支就是科幻电影里面的平行宇宙，当你正在电脑前努力学习Git的时候，另一个你正在另一个平行宇宙里努力学习SVN。

如果两个平行宇宙互不干扰，那对现在的你也没啥影响。不过，在某个时间点，两个平行宇宙合并了，结果，你既学会了git又学会了SVN！

![image002](https://gitee.com/zgf1366/pic_store/raw/master/img/20210107135614.png)

分支在实际中有什么用呢？假设你准备开发一个新功能，但是需要两周才能完成，第一周你写了50%的代码，如果立刻提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。如果等代码全部写完再一次提交，又存在丢失每天进度的巨大风险。

现在有了分支，就不用怕了。你创建了一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作。

### 2.2 创建分支

git把我们之前每次提交的版本串成一条时间线，这条时间线就是一个分支。截止到目前只有一条时间线，在git里，这个分支叫主分支，即master分支。HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。

(1) 一开始的时候，master分支是一条线，git用master指向最新的提交，再用HEAD指向master，就能确定当前分支，以及当前分支的提交点：

![image0012](https://gitee.com/zgf1366/pic_store/raw/master/img/20210107135736.png)

每次提交，master分支都会向前移动一步，这样，随着你不断提交，master分支的线也越来越长。

(2)当我们创建新的分支，例如dev时，git新建了一个指针叫dev，指向master相同的提交，再把HEAD指向dev，就表示当前分支在dev上：

![clip_image0014](https://gitee.com/zgf1366/pic_store/raw/master/img/20210107135806.png)

git创建一个分支很快，因为除了增加一个dev指针，改变HEAD的指向，工作区的文件都没有任何变化。

(3)不过，从现在开始，对工作区的修改和提交就是针对dev分支了，比如新提交一次后，dev指针往前移动一步，而master指针不变：

![clip_image0016](https://gitee.com/zgf1366/pic_store/raw/master/img/20210107135832.png)



(4)假如我们在dev上的工作完成了，就可以把dev合并到master上。git怎么合并呢？最简单的方法，就是直接把master指向dev的当前提交，就完成了合并：

![clip_image0018](https://gitee.com/zgf1366/pic_store/raw/master/img/20210107135847.png)

git合并分支也很快，就改改指针，工作区内容也不变。

(5)合并完分支后，甚至可以删除dev分支。删除dev分支就是把dev指针给删掉，删掉后，我们就剩下了一条master分支：

![clip_image0101](https://gitee.com/zgf1366/pic_store/raw/master/img/20210107135911.png)

创建分支命令：

```bash
$ git branch <name>
$ git branch 分支名称
```

### 2.3 查看分支 

执行 git branch 命令可以查看当前有几个分支并且看到在哪个分支下工作。

\# 列出所有本地分支 

```bash
$ git branch
```

`git branch`命令会列出所有分支，当前分支前面会标一个`*`号。

\# 列出所有远程分支

-r 参数相当于：remote

```bash
$ git branch -r
```

\# 列出所有本地分支和远程分支

-a 参数相当于：all

```bash
$ git branch -a
```

展示本地分支关联远程仓库的情况

```bash
$ git branch -vv
```

查看远程分支和本地分支的对应关系

```sh
$ git remote show origin
```



### 2.4 切换分支 

命令格式：

```bash
$ git checkout <name>
```

创建+切换本地分支

```bash
$ git checkout -b <branch-name>
```

从远程分支中创建并切换到本地分支

```bash
$ git checkout -b <branch-name> origin/<branch-name>
```

快速切换到上一个分支

```bash
$ git checkout -
```

### 2.5 合并分支

有时候合并操作不会如此顺利。 如果你在两个不同的分支中，对同一个文件的同一个部分进行了不同的修改，Git 就没办法合并它们，同时会提示文件冲突。git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容。此时需要我们打开冲突的文件并修复冲突内容，最后执行git add命令来标识冲突已解决

命令格式为：

```bash
$ git merge branchName 
$ git add 文件名称 
$ git push origin master #推送分支
```

通常，合并分支时，如果可能，git会用fast forward模式，但是有些快速合并不能成而且合并时没有冲突，这个时候会合并之后并做一次新的提交。但这种模式下，删除分支后，会丢掉分支信息。

### 2.6 推送分支

推送分支，就是把该分支上的所有本地提交推送到远程库，推送时要指定本地分支，这样，git就会把该分支推送到远程库对应的远程分支上

```bash
$ git push origin 分支名称 
例：
git push origin smart
```

### 2.7 从远程分支上拉取代码

```bash
git pull orgin 分支名称
例：
git pull orgin smart
```

使用上述命令会把远程分支smart上的代码下载并合并到本地所在分支。

### 2.8 将本地分支跟踪服务器分支

本地仓库中分支 A 与远程仓库中分支 B 建立连接方式：

1、git branch --set-upstream-to

```bash
git branch --set-upstream-to=origin/远程分支名称 本地分支名称
例：
git branch --set-upstream-to=origin/smart smart
```

2、git push -u

关联之后，`git branch -vv` 就可以展示关联的远程分支名了，同时推送到远程仓库直接：`git push`，不需要指定远程仓库了。

```bash
git branch -u origin/mybranch
```

或者在 push 时加上 `-u` 参数

```bash
git push origin/mybranch -u
```

### 2.9  删除分支

删除分支删除的是本地的分支，远程分支不会受到影响。

```bash
$ git branch -d <local-branchname> 
```

如果要删除的分支中进行了一些开发动作，此时执行上面的删除命令并不会删除分支，如果坚持要删除此分支，可以将命令中的-d参数改为-D

```bash
$ git branch -D branchName 
```

注：如果要删除远程仓库中的分支，可以使用命令git push


```bash
$ git push origin –d branchName

# or
$ git push origin --delete <remote-branchname>

# or
$ git push origin :<remote-branchname>
```

删除已经合并到 master 的分支

```bash
$ git branch --merged master | grep -v '^\*\|  master' | xargs -n 1 git branch -d
```

远程删除了分支本地也想删除

```bash
$ git remote prune origin
```

### 2.10 重命名本地分支

```bash
git branch -m <new-branch-name>
```

### 2.11 Bug分支 

软件开发中，bug就像家常便饭一样。有了bug就需要修复，在git中，由于分支是如此的强大，所以，每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。

(1)当你接到一个修复一个代号001的bug的任务时，很自然地，你想创建一个分支bug-001来修复它，但是，等等，当前正在dev上进行的工作还没有提交

并不是你不想提交，而是工作只进行到一半，还没法提交，预计完成还需1天时间。但是，必须在两个小时内修复该bug，怎么办？

(2)git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作：

```bash
$ git stash
```

![image-20201224153835244](https://gitee.com/zgf1366/pic_store/raw/master/img/20210107141643.png)

(3)首先确定要在哪个分支上修复bug，假定需要在master分支上修复，就从master创建临时分支：

![image-20201224153808155](https://gitee.com/zgf1366/pic_store/raw/master/img/20210107141704.png)

(4)现在修复bug,把 the new line删掉，然后提交。

![image-20201224153931463](https://gitee.com/zgf1366/pic_store/raw/master/img/20210107141724.png)

(5)修复完成后，切换到master分支，并完成合并，最后删除bug-001分支。

![clip_image00122](https://gitee.com/zgf1366/pic_store/raw/master/img/20210107141739.png)

(6)现在bug-001修复完成，是时候接着回到dev分支干活了！

![clip_image0044](https://gitee.com/zgf1366/pic_store/raw/master/img/20210107141757.png)

(7)工作区是干净的，刚才的工作现场存到哪去了？用git stash list命令看看：

![clip_image0406](https://gitee.com/zgf1366/pic_store/raw/master/img/20210107141809.png)

工作现场还在，git把stash内容存在某个地方了，但是需要恢复一下。修复后，再git stash pop，恢复工作现场。

![clip_image0048](https://gitee.com/zgf1366/pic_store/raw/master/img/20210107141830.png)

## 3、 冲突

- **提示**：多人协同开发时，避免不了会出现代码冲突的情况
- **原因**：多人同时修改了同一个文件
- **危害**：会影响正常的开发进度
- **注意**：一旦出现代码冲突，必须先解决再做后续开发

**代码冲突演练**

1.张三先编辑`login.py`文件代码

- 进入张三本地仓库：`cd Desktop/zhangsan/info`
- 拉取服务器最新代码：`git pull`
- 编辑代码：`num3 = 30`
- 本地仓库记录版本：`git commit -am '第三个变量'`
- 推送到服务器仓库：`git push`
- 张三本地仓库和远程仓库代码如下：

![img](https://gitee.com/zgf1366/pic_store/raw/master/img/20211006163657.png)

![img](https://gitee.com/zgf1366/pic_store/raw/master/img/20211006163703.png)

2.经理后编辑`login.py`文件代码

- 进入经理本地仓库：`cd Desktop/manager/info/`

- 编辑代码：`num3 = 300`

- 本地仓库记录版本：`git commit -am '第三个变量'`

- 推送到服务器仓库：`git push`

- **以上操作会出现代码冲突**

  - 提示需要先pull

  ![img](https://gitee.com/zgf1366/pic_store/raw/master/img/20211006163747.png)

  - 提示冲突文件

  ![img](https://gitee.com/zgf1366/pic_store/raw/master/img/20211006163752.png)

  - 冲突代码表现

![img](https://gitee.com/zgf1366/pic_store/raw/master/img/20211006163759.png)

3.解决冲突

- 原则：谁冲突谁解决，并且一定要协商解决
- 方案：保留所有代码 或者 保留某一人代码
- 解决完冲突代码后，依然需要`add`、`commit`、`push`

![img](https://gitee.com/zgf1366/pic_store/raw/master/img/20211006163815.png)

![img](https://gitee.com/zgf1366/pic_store/raw/master/img/20211006163822.png)

- 提示：如果张三执行`pull`没有影响，就算真正解决了冲突代码

**补充：**

- **容易冲突的操作方式**
  - 多个人同时操作了同一个文件
  - 一个人一直写不提交
  - 修改之前不更新最新代码
  - 提交之前不更新最新代码
  - 擅自修改同事代码
- **减少冲突的操作方式**
  - 养成良好的操作习惯,先`pull`在修改,修改完立即`commit`和`push`
  - 一定要确保自己正在修改的文件是最新版本的
  - 各自开发各自的模块
  - 如果要修改公共文件,一定要先确认有没有人正在修改
  - 下班前一定要提交代码,上班第一件事拉取最新代码
  - 一定不要擅自修改同事的代码