# Git introduction

标签（空格分隔）： 版本控制 Git

本文是个人对Git版本控制系统的学习，Git相关知识的学习。介绍Git的基本知识，常用操作等等。

---
## 版本控制系统 ##
VCS：Version Control System
版本控制系统是记录文件的内容变化，在任何时候可以查看文件在特定版本的修订情况的系统。它可以对任何文件进行版本控制，不管是代码文件、图片文件、文档文件等等。所以有了VCS之后我们可以将某个文件回退到之前的某一个状态，甚至可以将整个项目都回退到过去某个时间点的状态。
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

