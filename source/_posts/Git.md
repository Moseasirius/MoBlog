---
title: Git
date: 2021-09-29 15:08:22
tags: Git
categories: CodeTool
---

Git基本命令<!--more--> 

## Linux 平台上安装

Ubuntu Git 安装命令为：

```
apt-get install libcurl4-gnutls-dev libexpat1-dev gettext  libz-dev libssl-dev
apt-get install git	
git --version
```

用户信息

```
git config --global user.name "mo"
git config --global user.email test@mo.com
```

查看配置信息

```
git config --list
windows
....
user.name=Moseasirius
user.email=moseasirius@gmail,com
...
init.defaultbranch=main
http.version=HTTP/1.1
```

##  Git 工作流程

克隆 Git 资源作为工作目录。

在克隆的资源上添加或修改文件。

如果其他人修改了，你可以更新资源。

在提交前查看修改。

提交修改。

在修改完成后，如果发现错误，可以撤回提交并再次修改并提交。

## 基本概念

- **工作区：**就是你在电脑里能看到的目录。
- **暂存区：**英文叫 stage 或 index。一般存放在 **.git** 目录下的 index 文件（.git/index）中，所以我们把暂存区有时也叫作索引（index）。
- **版本库：**工作区有一个隐藏目录 **.git**，这个不算工作区，而是 Git 的版本库。

{%asset_img Git.jpg%}



- 图中左侧为工作区，右侧为版本库。在版本库中标记为 "index" 的区域是暂存区（stage/index），标记为 "master" 的是 master 分支所代表的目录树。
- 图中我们可以看出此时 "HEAD" 实际是指向 master 分支的一个"游标"。所以图示的命令中出现 HEAD 的地方可以用 master 来替换。
- 图中的 objects 标识的区域为 Git 的对象库，实际位于 ".git/objects" 目录下，里面包含了创建的各种对象及内容。
- 当对工作区修改（或新增）的文件执行 **git add** 命令时，暂存区的目录树被更新，同时工作区修改（或新增）的文件内容被写入到对象库中的一个新的对象中，而该对象的ID被记录在暂存区的文件索引中。
- 当执行提交操作（git commit）时，暂存区的目录树写到版本库（对象库）中，master 分支会做相应的更新。即 master 指向的目录树就是提交时暂存区的目录树。
- 当执行 **git reset HEAD** 命令时，暂存区的目录树会被重写，被 master 分支指向的目录树所替换，但是工作区不受影响。
- 当执行 **git rm --cached <file>** 命令时，会直接从暂存区删除文件，工作区则不做出改变。
- 当执行 **git checkout .** 或者 **git checkout -- <file>** 命令时，会用暂存区全部或指定的文件替换工作区的文件。这个操作很危险，会清除工作区中未添加到暂存区中的改动。
- 当执行 **git checkout HEAD .** 或者 **git checkout HEAD <file>** 命令时，会用 HEAD 指向的 master 分支中的全部或者部分文件替换暂存区和以及工作区中的文件。这个命令也是极具危险性的，因为不但会清除工作区中未提交的改动，也会清除暂存区中未提交的改动。

## Git 的基本操作

- workspace：工作区
- staging area：暂存区/缓存区
- local repository：版本库或本地仓库
- remote repository：远程仓库

```
git init    
git add .    
git commit
git init - 初始化仓库。
git add . - 添加文件到暂存区。
git commit - 将暂存区内容添加到仓库中。
```

## 创建仓库命令

```
git init	初始化仓库 

mkdir gittest 
cd gittest
git init

git clone 
git clone [url]
cd gittest
git clone https://github.com/Moseasirius/Moseasirius.github.io.git
```

## 提交与修改

Git 的工作就是创建和保存你的项目的快照及与之后的快照进行对比。

下表列出了有关创建与提交你的项目的快照的命令：

| 命令         | 说明                                     |
| :----------- | :--------------------------------------- |
| `git add`    | 添加文件到仓库                           |
| `git status` | 查看仓库当前的状态，显示有变更的文件。   |
| `git diff`   | 比较文件的不同，即暂存区和工作区的差异。 |
| `git commit` | 提交暂存区到本地仓库。                   |
| `git reset`  | 回退版本。                               |
| `git rm`     | 删除工作区文件。                         |
| `git mv`     | 移动或重命名工作区文件。                 |

## 提交日志

| 命令               | 说明                                 |
| :----------------- | :----------------------------------- |
| `git log`          | 查看历史提交记录                     |
| `git blame <file>` | 以列表形式查看指定文件的历史修改记录 |



## 远程操作

| 命令         | 说明               |
| :----------- | :----------------- |
| `git remote` | 远程仓库操作       |
| `git fetch`  | 从远程获取代码库   |
| `git pull`   | 下载远程代码并合并 |
| `git push`   | 上传远程代码并合并 |



## Git 分支管理

几乎每一种版本控制系统都以某种形式支持分支。使用分支意味着你可以从开发主线上分离开来，然后在不影响主线的同时继续工作。

有人把 Git 的分支模型称为**必杀技特性**，而正是因为它，将 **Git** 从版本控制系统家族里区分出来。



```
创建分支命令
git branch (branchname)
切换分支命令:

git checkout (branchname)
当你切换分支的时候，Git 会用该分支的最后提交的快照替换你的工作目录的内容， 所以多个分支不需要多个目录。

合并分支命令:
git merge 

列出分支基本命令：
git branch
没有参数时，git branch 会列出你在本地的分支。
mo@Mosea-PC MINGW64 /e/AlgorithmAndDataStructure (main)
git branch
* main
现在默认分支为main
当你执行 git init 的时候，默认情况下 Git 就会为你创建 main 分支。

如果我们要手动创建一个分支。执行 git branch (branchname) 即可。
git branch testing
git branch
* master
  testing
  
删除分支命令：
git branch -d (branchname)



```







































Git 是林纳斯·托瓦兹一堆大佬聚集以后（Linux社群），觉得使用分布式版本控制的软件性能不佳，然后林纳斯·托瓦兹大佬现将其创作出来，然后一些大佬和他一起将其完善。

## 历史

git（/ɡɪt/）是一个分布式版本控制软件，最初由林纳斯·托瓦兹创作，于2005年以GPL发布。最初目的是为更好地管理Linux内核开发而设计。应注意的是，这与GNU Interactive Tools（一个类似Norton Commander界面的文件管理器）不同。

git最初的开发动力来自于BitKeeper和Monotone。git最初只是作为一个可以被其他前端（比如Cogito或Stgit）包装的后端而开发的，但后来git内核已经成熟到可以独立地用作版本控制。很多著名的软件都使用git进行版本控制，其中包括Linux内核、X.Org服务器和OLPC内核等项目的开发流程。

自2002年开始，林纳斯·托瓦兹决定使用BitKeeper作为Linux内核主要的版本控制系统用以维护代码。因为BitKeeper为专有软件，这个决定在社群中长期遭受质疑。在Linux社群中，特别是理查德·斯托曼与自由软件基金会的成员，主张应该使用开放源代码的软件来作为Linux内核的版本控制系统。林纳斯·托瓦兹曾考虑过采用现成软件作为版本控制系统（例如Monotone），但这些软件都存在一些问题，特别是性能不佳。现成的方案，如CVS的架构，受到林纳斯·托瓦兹的批评。

2005年，安德鲁·垂鸠写了一个简单程序，可以连接BitKeeper的存储库，BitKeeper著作权拥有者拉里·麦沃伊认为安德鲁·垂鸠对BitKeeper内部使用的协议进行逆向工程，决定收回无偿使用BitKeeper的许可。Linux内核开发团队与BitMover公司进行磋商，但无法解决他们之间的歧见。林纳斯·托瓦兹决定自行开发版本控制系统替代BitKeeper，以十天的时间编写出git第一个版本

## 命名

林纳斯·托瓦兹讽刺地嘲笑git这个名字（在英式英语俚语中表示“不愉快的人”）

源代码的自述文件进一步阐述了：

The name "git" was given by Linus Torvalds when he wrote the very first version. He described the tool as "the stupid content tracker" and the name as (depending on your way):

random three-letter combination that is pronounceable, and not actually used by any common UNIX command. The fact that it is a mispronunciation of "get" may or may not be relevant.
"global information tracker": you're in a good mood, and it actually works for you. Angels sing, and a light suddenly fills the room.
stupid. contemptible and despicable. simple. Take your pick from the dictionary of slang.
林纳斯·托瓦兹在编写第一个版本时就使用了“git”这个名称。 他将工具描述为“愚蠢的内容跟踪器”，并将其描述为（取决于您的方式）：

可以发音念出的随机三个字母组合，而且并未被实际用在任何 UNIX 指令上。它是“get”的错误发音，这点可能相关也可能无关。
“全球信息跟踪器”：您的心情不错，对你而言它也确实说得通。天使唱歌，房间突然充满光明。
愚蠢的。鄙视和卑鄙的。简单。从俚语字典中选择。

## 实现原理

git和其他版本控制系统（如CVS）有不小的差别，git本身关心文件的整体性是否有改变，但多数的版本控制系统如CVS或Subversion系统则在乎文件内容的差异。git拒绝保持每个文件的版本修订关系。因此查看一个文件的历史需要遍历各个history快照；git隐式处理文件更名，即同名文件默认为其前身，如果没有同名文件则在前一个版本中搜索具有类似内容的文件。

git更像一个文件系统，直接在本机上获取资料，不必连线到主机端获取资料。 每个开发者都可有全部开发历史的本地副本，changes从这种本地repository复制给其他开发者。这些changes作为新增的开发分支被导入，可以与本地开发分支合并。

分支是非常轻量级的，一个分支仅是对一个commit的引用。

git是用C语言开发的，以追求最高的性能。git自动完成垃圾回收，也可以用命令git gc --prune直接调用。

git存储每个新创建的object作为一个单独文件。为了压缩存储空间占用， packs操作把很多文件（启发式类似名字的文件往往具有类似内容）使用差分压缩入一个文件中（packfile），并创建一个对应的索引文件，指明object在packfile中的偏移值。新创建的对象仍然作为单独文件存在。repacks操作非常费时间，git会在空闲时间自动做此操作。也可用命令git gc来直接启动repack。packfile与索引文件都用SHA-1作为校验和并作为文件名。git fsck命令做校验和的完整性验证。

Git服务器典型的TCP监听端口为9418。

## 数据结构

Git有两种数据结构：可变的索引（index或stage或cache)用于缓冲工作目录信息与下一次提交的版本信息；不变的、仅追加的对象数据库。

对象数据库包含4类对象：

blob (二进制大对象)是使用zlib压缩算法对一个文件的内容压缩后的结果。Blobs没有保存文件名、时间戳或其他元数据。Git将其存储在位于隐藏的.git/objects文件夹中。文件的名称为使用SHA-1哈希函数对原文件内容生成的哈希值。这些对象文件称为Blob，每次将新文件添加到存储库时会创建Blob对象。
tree对象对应于文件目录。包含文件名列表以及文件的类型比特（包含许可权）、到blob（对应于文件）或tree对象的引用。tree对象是源树(source tree)的快照。用默克尔树实现。
commit对象链接tree对象在一起而成为history，包含顶层源目录的tree对象名字、一个时间戳、log信息、0个或多个父commit对象的名字。用于保存特定版本的树型文件夹结构以及提交作者，电子邮件地址，日期和描述性提交消息。
tag对象是一个容器，包含了到另一个对象的引用，也可以增加关于另外对象的元数据。通常它保存需要追溯的特定版本数据的一个commit对象的数字签名。
以上4类的对象用其内容的SHA-1 hash值标识：hash值的前两个字符作为存放的目录名字，其余hash字符作为这个对象的文件名。

Git数据库中不变引用的对象将会被垃圾回收清除。Git命令可以创建、移动、删除引用。"git show-ref"列出所有引用。某些引用类型：

heads: 引用一个本地对象，是commit的指针。每个head可以指任意一个这样的指针。可以包含任意数量的heads。而"HEAD"（全部大写），仅仅指的是当前有效的head。默认情况下，在每个仓库下都有一个head，叫做master。
remotes: 引用远程repository中的一个对象
stash: 引用一个还没有committed的一个对象
meta: 例如一个bare repository中的一个配置, 用户权限; refs/meta/config名字空间等[19]
tags:
某些操作（例如，将提交推送到远程存储库，存储太多对象或手动运行Git的垃圾收集命令）可能会导致Git将对象重新打包为打包文件，在打包过程中，采用反向差异并进行压缩以消除多余的内容并减小尺寸。该过程将生成包含对象内容的.pack文件，每个文件都有一个对应的.idx索引文件，其中包含对打包对象及其在打包文件中位置的引用。当将分支推送到远程存储库或从远程存储库拉出分支时，这些打包文件将通过网络传输。提取或获取分支时，将打包文件解压缩以在对象存储库中创建松散对象。

{%asset_img Git_operations.svg%}               

图片来源：https://commons.wikimedia.org/wiki/User:Duesentrieb

