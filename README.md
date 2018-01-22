## 主要工具 

- 版本控制
- SVN
- Git
- Github

---

## 版本控制

### 问题1：历史记录

### 问题2：多人协作

### 解决问题：软件

```
版本  用户  说明                   日期
1     张三  删除了软件服务条款5    7/12 10:38
2     张三  增加了License人数限制  7/12 18:09
3     李四  财务部门调整了合同金额 7/13 9:51
4     张三  延长了免费升级周期     7/14 15:17
```

### 什么是版本控制？

版本管理就是管理更新的历史记录，
它给我们提供了一些在软件开发过程中必不可少的功能，例如：

- 记录一款软件添加或更改源代码的过程
- 回滚到特定阶段，恢复误删除的文件
- 合并多人协作的文件等
- 多人协同，文件传输

### 版本控制分类

- 集中式
  + SVN
- 分布式
  + Git

---

## SVN

SVN 全称 Apache Subversion，是一个开放源代码的集中式版本管理系统。
在 2000 年由 CollabNet 开发，现已发展成为 Apache 软件基金会的一个开源项目。

### 环境安装

### SVN 交互协作流程

![集中式版本管理 - SVN](./img/svn交互流程.png)

### 集中式

早期的版本管理就是以 `Apache Subversion` 为代表的集中式版本管理，
集中式版本管理将所有的数据集中存放在服务器中，这是有便于统一管理的优点。
但是一旦开发者所处的环境不能连接服务器，就无法获取最新源代码，开发也就无法进行。
服务器宕机时也是同样的道理，而且万一服务器故障导致数据丢失，
恐怕开发者就再也见不到最新的源代码了。

简而言之：

- 中央服务器好比是一个图书馆
- 你要改一本书，必须先从图书馆借出来（checkout）
- 然后回到家自己改，改完了，再放到图书馆（commit）

### 一些术语

- 源代码库（repository）：源代码统一存放的地方
- 检出（checkout）：当你手上没有源代码的时候，就需要从 responsive checkout 一份
- 提交（commit）：当你已经修改了代码，就需要 commit 到 repository
- 更新（update）：当你已经 checkout 了一份源代码，Update 一下就可以和 repository 上的源代码同步，你手上的代码就会有最新的变更

### 使用 VisualSVN 搭建 SVN 服务器

SVN 服务器：运行 Subversion 服务的计算机。

为了方便，我们这里使用比较流行的图形化工具 [VisualSVN](https://www.visualsvn.com/) 
来搭建我们的 SVN 服务。

安装完毕之后，基本使用流程如下：

- 创建用户
- 创建版本仓库
- 设定用户权限

### 使用 TortoiseSVN 作为 SVN 客户端

SVN 客户端：用户通过SVN客户端同SVN服务器交互

这里我们使用最流行的 [TortoiseSVN](https://tortoisesvn.net/)

https://DESKTOP-40UMEJI:8443/svn/jd

https://192.168.133.25:8443/svn/jd

### TortoiseSVN 客户端基本操作流程

- 检出项目：`checkout`
  + 在没有源代码的前提下，需要通过 tortoise-svn 客户端下载
- 提交修改：`commit`
  + 帮你记录当前开发的软件的状态
- 更新文件或目录：`update`（更新）
  + 别的开发人员在已有源代码的前提下可以通过 update 更新服务器上最新的版本
- 查看版本日志：`log`（日志）

### 关于冲突

假设 A、B 两个用户都在版本号为 100 的时候，更新了 kingtuns.txt 这个文件，
A 用户在修改完成之后提交 kingtuns.txt 到服务器， 这个时候提交成功，
这个时候 kingtuns.txt 文件的版本号已经变成 101 了。
同时B用户在版本号为 100 的 kingtuns.txt 文件上作修改， 修改完成之后提交到服务器时，
由于不是在当前最新的 101 版本上作的修改，所以导致提交失败。

良好的使用习惯就是，提交之前，先更新。

为了避免冲突，别人的文件你最好不要动，
万一你要修改公共的文件或者是别人的文件，
跟别人最好口头沟通好，就是你改动的时候，
别人最好不要去改动，这样才能最大程度上避免冲突的问题。

多人协作时，同个目录或同个文件需要不同成员共同开发，
这个时候 commit 和 update 就可能出现冲突。

- 两个程序员只要不是修改了同一行程序，SVN 可以通过 update 自动合并修改
- 但是如果两个程序员修改了同一行程序， SVN 会提示文件 conflict，需要手动确定

如何解决？

第一种解决方法：手动合并冲突的内容

第二种解决方法：每次修改某个文件的时候对文件上锁，这样你在修改的过程中别人就无法更新这个文件

建议：

- 一个文件最好同一时间只被一个人修改提交
- 多跟团队成员沟通
- 不要随便去修改别人的文件

### 版本管理使用建议

- 不要频繁的提交版本
  + 一般有比较成熟的功能模块的时候，再去提交
  + 修复了功能性 bug 的时候再去提交
  + 提交的代码最好无 bug
- 每次 commit 之前都要 update
  + 因为你在编辑这个文件的时候，可能比人已经编辑并提交了某个版本
  + 所以先 update，目的是为了检查一下服务器上有没有最新版，如果有，直接更新
    * 更新的过程中如果遇到冲突，不要慌，去手动解决
- 每次 commit 的时候都务必要写提交日志
  + 这个提交日志就好比你保存副本的时候加的一个标记
  + 目的是为了日后做版本的回退查找以及查看记录更新状态

### 使用总结

- 版本控制管理系统
- 源代码仓库 repository
- 检出代码 checkout
- 更新最新源代码 update
- 提交修改 commit

### 其它

- [清除svn保存的username用户名和paasword密码(windows和linux)](http://holy2010.blog.51cto.com/1086044/645944)
- [菜鸟教程 - SVN 教程](http://www.runoob.com/svn/svn-tutorial.html)

---

## Git

> [维基百科 - Git](https://zh.wikipedia.org/wiki/Git)

### 学习资源介绍

- [Git教程 - 廖雪峰](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/)
- [Pro Git](http://git.oschina.net/progit/)
- [git - 简明指南](http://rogerdudler.github.io/git-guide/index.zh.html)
- [猴子都能懂的GIT入门](http://backlogtool.com/git-guide/cn/)

### Git 简介

- 是什么
  + Git 也是一个版本控制管理软件
- 有什么用，可以解决什么问题
  + 保存历史记录
  + 多人协作
- 有了 SVN，为啥要学 Git
  + Git 分布式管理，适合多人协作
- 怎么用
- Git 的诞生
  + http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137402760310626208b4f695940a49e5348b689d095fc000

### Git 使用交互流程

![git交互模型](img/git交互模型.png)

### 安装和配置 Git 环境

- 下载地址：https://git-scm.com/

#### bash 常用命令
- pwd (print working dirstory) 显示当前路径
- ls 显示全部文件
- cd (change dirstory) 进入文件
- cd ..  进入上级目录
- mkdir (make dirstory) 创建目录
- touch 创建文件

- rm 
    + rm  文件名         删除文件 
    + rm -r  (remove recusion) 删除目录
- less 分页阅读; q 退出
- mv 
    + mv  [位置]      移动文件到
    + mv  [旧名] [新名]   重命名
- cp (copy) 复制 ,重命名方法与 rm 相同

- cat 查看文件全部内容
- head [-数字]   查看文件前"xx"行
- tail [-数字]   查看文件后"xx"行

- history 查看操作历史

#### 初始化配置

```bash
# 设置用户名
git config --global user.name "你的名字"
# 配置用户邮箱
git config --global user.email "你的常用邮箱"
# 设置 gitk 图形查看工具中文显示默认编码（防止乱码）
git config --global gui.encoding utf-8
# 查看配置列表项
git config --list
```

### 基本使用

- `git init`
  + 初始化一个 Git 仓库
- `git status`
  + 查看当前工作区、暂存区、本地仓库的状态
- `git clone [url] --depth=1`	下载仓库文件,并规定下载深度
- `git add`     将 工作区 文件提交到 暂存区
- `git commit`  将 暂存区 文件全部提交到 本地仓库
  + 示例：`git commit -m "日志说明" --author="操作者姓名 <邮箱>"`
  + 执行 `git commit` 的时候，Git 会要求具有用户名和邮箱的参数选项
  + 可以通过 `git config` 命令配置一下用户名和邮箱
- `git log`   查看记录
- `gitk`      图形化界面

总结：
```
操作 Git 的基本工作流程就是先修改文件，然后执行 `git add` 命令。
`git add` 命令会把文件加入到 暂存区，
暂存之后 拉取上级分支代码，然后合并到本地分支，（如果这时候有冲突可以手动解决冲突）
接着就可以执行 `git commit` 命令，将文件存入文档库，
从而形成一次历史记录。
```

- 问题1：关于 Git-bash 中文问题
- [Git for Windows Unicode Support](https://github.com/msysgit/msysgit/wiki/Git-for-Windows-Unicode-Support)
- 问题2：执行 commit 的时候一大堆的信息
- 问题3：配置 user.name 和 user.email 问题

### 工作区、暂存区、本地仓库

### 分支管理
```bash
# 列出所有分支，并用*标注目前所在分支
$ git branch 

# 查看所有分支 及 源
$ git branch -a 

# 基于当前分支新建一个分支，但依然停留在当前分支
$ git branch [branch-name]

# 基于当前分支新建一个分支，并切换到该分支
$ git checkout -b [branch-name]

# 切换到某个分支
$ git checkout [brach-name]

# 删除分支
$ git branch -d [branch-name]

# 将指定分支合并到当前分支(--no-ff表示为不使用fast-Forward合并模式)
$ git merge [--no-ff] [branch-name]

# 衍合 ：
  1. rebase命令将版本回到当前分支与branchName分支的共同祖先版本，
  2. 手动将当前分支的变化补丁在branchName的基础上重新打一遍
  3. 然后到branchName分支，进行快速合并）
  **！一旦分支中的提交对象发布到公共仓库，就千万不要对该分支进行衍合操作。**
$ git rebase [branch-name]

# 同步远程服务器上的数据到本地（ 找到origin并更新本地数据，然后同步版本 ）
$ git fetch origin  

# 把另一个服务器加为远程仓库
$ git fetch [服务器名]

# 跟踪远程分支（因为有时候想跟踪的远程分支是你在clone代码之后创建的，这种情况下在本地会切换不到该分支）
$ git checkout -b [branchName] [origin]/[branchName]

# 删除远程分支
$ git push origin :[branch-name]  // 推送一个空分支到远程分支，相当于删除
$ git push origin -d [tag <tagname>] [branch-name]  // 删除 tag 或 远程分支

```

### 版本回退

```gitbash

# 删除暂存区的文件
$git rm --cached <file>

# 恢复暂存区的指定文件到工作区
$ git checkout [file]

# 清空暂存区的修改
$ git checkout .

#重命名文件并且提交到暂存区(省略add)
$ git mv [oldFileName] [newFileName]

# 恢复某个commit的指定文件到暂存区和工作区
$ git checkout [commit] [file]

# 恢复暂存区的所有文件到工作区
$ git checkout .

# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
$ git reset [file]

--head:git log 中最新的版本

# 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
$ git reset [commit]

# 重置暂存区与工作区，与上一次commit保持一致
$ git reset --hard HEAD^

# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
$ git reset --hard [commit]

# 重置当前HEAD为指定commit，但保持暂存区和工作区不变
$ git reset --keep [commit]

# 新建一个commit，用来撤销指定commit
# 后者的所有变化都将被前者抵消，并且应用到当前分支
$ git revert [commit]

# 暂时将未提交的变化移除，稍后再移入
$ git stash
$ git stash pop
```

### 远程同步

```bash
# 下载一个远程仓库
$ git clone [url]

# 显示所有远程仓库
$ git remote -v

# 显示某个远程仓库的信息
$ git remote show [remote]

# 增加一个新的远程仓库，并命名
$ git remote add [shortname] [url]

# 取回远程仓库的变化，并与本地分支合并
$ git pull [remote] [branch]

# 上传本地指定分支到远程仓库
$ git push [remote] [branch]

# 强行推送当前分支到远程仓库，即使有冲突
$ git push [remote] --force
```

### 在线仓库托管服务

Git 工作流程:git flow / github flow /gitlab flow

- github
- 码云
- coding

---

## Github

> 可以社交化的方式进行编程协作、
>     - 点赞
>     - 评论
>     - 转发
>     - etc.
> 主要作用：可以免费在线托管代码仓库
> 可以实现多人协作
> 提供了一个可视化界面（Web Page）能直观清晰的了解你的项目源代码

### 与 Github 进行多人协作

#### Collaborators

#### Pull Request
