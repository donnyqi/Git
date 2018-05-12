# Git introduction

标签（空格分隔）： 版本控制 Git

本文是个人对Git版本控制系统的学习，Git相关知识的学习。介绍Git的基本知识，常用操作等等。

---
## 版本控制系统 ##
VCS：Version Control System
版本控制系统是记录文件的内容变化，以便在任何时候可以查看文件在特定版本修订情况的系统。它可以对任何文件进行版本控制，不管是代码文件、图片文件、文档文件等等。所以有了VCS之后我们可以将某个文件回退到之前的某一个状态，甚至可以将整个项目都回退到过去某个时间点的状态。
当然通过VCS可以比较文件具体的变化细节：
```javascript
    + var a = 5                                          - var a = 3
```
```javascript
-        console.log(JSON.stringify(data))
-        console.log('isVcardUsing====', self.freeUse)
-        console.log(typeof self.freeUse)
+        // console.log(JSON.stringify(data))
+        // console.log('isVcardUsing====', self.freeUse)
+        // console.log(typeof self.freeUse)
```
这样在出现一些bugs的时候我们可以去分析出最后是谁修改了哪个地方，从而发现导致bugs的原因，从而可以快速修复问题。通过VCS的目的并不是说要去追踪是谁导致出现问题的人，而是帮助我们快速的去解决问题。
不过目前很多公司有着一套版本发布或持续集成系统，如果发布上线之后发现有问题出现，可以快速的回退到上一个指定没有问题的版本，然后在通过分析导致bugs的原因重新上线。
另外假设再开发过程中不小心把项目中的文件改的改删的删，我们也可以轻松的恢复到原来的状态。

**版本控制系统历史分类：**
 1. 本地版本控制系统
 2. 集中化版本控制系统CVCS:CVS,subversion……
 3. 分布式版本控制系统DVCS:Git,Mercurial,Bazaar……

## Git历史 ##
Linux内核开源项目有很多的参与者，但是绝大多数的Linux内核维护工作都花在提交补丁和保存归档的繁琐事务上面(1991-2002)，到 2002 年，整个项目组开始启用分布式版本控制系统 BitKeeper 来管理和维护代码。到了2005年，开发 BitKeeper 的商业公司同 Linux 内核开源社区的合作关系结束，他们收回了免费使用 BitKeeper 的权力。自此Git分布式版本控制系统就诞生了。

Git当初设定的目标：

* 速度
* 简单的设计
* 对非线性开发模式的强力支持（允许上千个并行开发的分支）
* 完全分布式
* 有能力高效管理类似 Linux 内核一样的超大规模项目（速度和数据量）


## Git基础 ##
理解Git的思想和基本工作原理，用起来就会之其所以然，游刃有余。

- Git的原理是直接记录快照，并非差异比较：Git并不保存文件前后变化的差异数据，实际上是把变化的文件做快照后，记录在一个微型的文件系统中；
- Git所有的操作都是本地执行；
- 时刻保持数据的完整性：在保存到Git之前，所有的数据都会进行内容的校验和(checksum)计算，并将此结果作为数据的唯一标识和索引。Git- 使用SHA-1算法计算数据的校验和，此SHA-1 哈希值作为指纹字符串，该字串由 40 个十六进制字符（0-9 及 a-f）组成；
- 多数操作仅添加数据：常用的 Git 操作大多仅仅是把数据添加到数据库；
- 文件的三种状态：
    1.已提交 commited 表示该文件已经被安全地保存在本地数据库中了
    2.已修改 modified 表示修改了某个文件，但还没有提交保存
    3.已暂存 staged   表示把已修改的文件放在下次提交时要保存的清单中

    Git管理项目时，文件流转的三个工作区域：Git工作目录，暂存区域，本地仓库(Git目录.git)。
    **基本的 Git 工作流程如下：**
        1.在工作目录中修改某些文件。
        2.对修改后的文件进行快照，然后保存到暂存区域。
        3.提交更新，将保存在暂存区域的文件快照永久转储到Git目录中。

## Git初始设置 ##
- git config --list
- git config --global user.name 'username'
- git config --global user.email 'useremail'
`如果用了 --global 选项，那么更改的配置文件就是位于你用户主目录下的那个，以后你所有的项目都会默认使用这里配置的用户信息。如果要在某个特定的项目中使用其他名字或者电邮，只要去掉 --global 选项重新配置即可，新的设定保存在当前项目的 .git/config 文件里。`

### 初始Git respository ###
- git init        当前目录创建git仓库
- git init `name`   创建目录为name的git仓库
- git clone `https://github.com/donnyqi/Html.git`  拷贝远程git仓库,目录为Html
- git clone `https://github.com/donnyqi/Html.git HtmlTest`  拷贝远程git仓库,目录为自定义的HtmlTest

### 记录每次更新到仓库 ###
文件的状态变化周期：
工作目录下的所有文件都不外乎两种状态：已跟踪 、 未跟踪
`已跟踪的文件是指本来就被纳入版本控制管理的文件，在上次快照中有它们的记录，工作一段时间后，它们的状态可能是未更新，已修改或者已放入暂存区。而所有其他文件都属于未跟踪文件。它们既没有上次更新时的快照，也不在当前的暂存区域。初次克隆某个仓库时，工作目录中的所有文件都属于已跟踪文件，且状态为未修改。`

状态的提示语：
untracked `Untracked files`
unmodified
modified `Changes not staged for commit`
staged  `Changes to be committed`

```Git
bogon:static vivo$ git status
On branch branch_point_20180426_v3_2_1
Your branch is up-to-date with 'origin/branch_point_20180426_v3_2_1'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   src/api/test.js

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   src/api/index.js
        modified:   src/router/index.js

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        src/views/Test/
```


git status 检查当前文件状态
git log 查看提交历史
git add `filename` 跟踪新文件，已跟踪文件放到暂存区
git add . 跟踪所有文件
git checkout `filename` 放弃更改工作目录中当前修改的文件
git reset `filename` 放弃工作目录中当前暂存的文件到未暂存或未追踪
git diff 查看已暂存和未暂存的更新
git diff 查看工作目录中当前文件未暂存的文件与暂存区域快照直接的差异，也就是修改之后还没有暂存起来的变化内容。**如果未暂存的文件全部都add到暂存区域，git diff是没有变化的**
git diff --cached || --staged 当前工作目录中已暂存文件与上次提交时的快照之间的差异    **或者通过开发工具比较**
git commit 进入Vim输入本次提交的说明(默认的提交消息包含最后一次运行 git status 的输出)->i->input commit message->esc-> : ->wq->enter
git commit -v 进入Vim输入本次提交的说明(将修改差异的每一行都包含到注释中来)
git commit -m "commit message" 直接提交说明
git commit -a -m "commit message" Git会自动把所有已经跟踪过的文件暂存起来一并提交直接加到staged区域，从而跳过 git add 步骤，但是不能添加untracked文件
git commit -a 进入Vim输入本次提交的说明，把已经跟踪过的文件暂存到暂存区域，但是不能添加untracked文件



**`注：如果在新跟踪了某个untracked文件或者在跟踪了某个已修改后的文件，添加到staged区域(Changes to be committed)之后，再次对该跟踪的文件进行了修改，这个时候如果现在提交，那么提交的是之前add的版本，而非当前工作目录中的版本。所以，运行了 git add 之后又作了修订的文件，需要重新运行 git add 把最新版本重新暂存起来`**




