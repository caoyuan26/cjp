#Git教程
 
###一、Git简介

1.1. Git的诞生
1.2.集中式的vs分布式
###二、安装Git

###三、创建版本库
	
###四、时光穿梭机	
4.1版本回退
4.2工作区和暂存区
4.3管理修改
4.4撤销修改
4.5删除文件
###五、远程仓库
5.1添加远程仓库
5.2从远程库中克隆

###六、分支管理
6.1创建与合并分支
6.2解决冲突
6.3分支管理策略
6.4Bug分支
6.5Feature分支
6.6多人协作
###七、标签管理
7.1创建标签
7.2操作标签
###八、使用GitHub
###九、自定义Git
9.1忽略特殊定义符
9.2配置别名
9.3搭建Git服务器
  ##十、总结

###一、Git简介
Git是什么？

Git是目前世界上最先进的分布式版本控制系统（没有之一）。

Git有什么特点？简单来说就是：高端大气上档次！

那什么是版本控制系统？

####1.1 Git的诞生

你也许会想，为什么Linus不把Linux代码放到版本控制系统里呢？不是有CVS、SVN这些免费的版本控制系统吗？因为Linus坚定地反对CVS和SVN，这些集中式的版本控制系统不但速度慢，而且必须联网才能使用。有一些商用的版本控制系统，虽然比CVS、SVN好用，但那是付费的，和Linux的开源精神不符。

不过，到了2002年，Linux系统已经发展了十年了，代码库之大让Linus很难继续通过手工方式管理了，社区的弟兄们也对这种方式表达了强烈不满，于是Linus选择了一个商业的版本控制系统BitKeeper，BitKeeper的东家BitMover公司出于人道主义精神，授权Linux社区免费使用这个版本控制系统。

安定团结的大好局面在2005年就被打破了，原因是Linux社区牛人聚集，不免沾染了一些梁山好汉的江湖习气。开发Samba的Andrew试图破解BitKeeper的协议（这么干的其实也不只他一个），被BitMover公司发现了（监控工作做得不错！），于是BitMover公司怒了，要收回Linux社区的免费使用权。

Linus可以向BitMover公司道个歉，保证以后严格管教弟兄们，嗯，这是不可能的。实际情况是这样的：

Linus花了两周时间自己用C写了一个分布式版本控制系统，这就是Git！一个月之内，Linux系统的源码已经由Git管理了！牛是怎么定义的呢？大家可以体会一下。

分布式 VS 集中式
* 集中式
SVN - CVS - ClearCase(IBM 收费) - VSS(微软)

* 分布式
git - BitKeeper(促使git诞生) - Mercurial - Bazaar

目前集中式常用的SVN, 分布式常用git

集中式

集中式版本控制系统, 版本库需要集中的放到一台服务器上, 在工作时, 用自己的电脑从中央服务器上将目前最新内容下载到本地, 实现效果后再讲内容推送到中央服务器.

* 缺点

1.中央服务器崩溃, 所有人都干不了活
2.网络带宽会影响文件下载和上传速度

分布式

分布式版本控制系统压根没有”中央服务器”这个东西, 每个人的电脑都是一个完整的版本库, 这样工作的时候并不需要网络. 多人协作, 在合并作品的时候, 只需将自己的内容传给对方, 对方既可以看到你修改的内容. 同时, git提供强大的分支, 可以将项目拆分, 使项目更加安全.

**注意** 

git虽然没有”中央服务器”, 但常常找出一台电脑来充当”中央服务器”, 不过其作用是为了方便交换, 因为, 协作的两个人不在同一个局域网, 或者其中一人电脑未开启等特殊情况.

* 优点

安全性极高, 即便自己的电脑坏了, 只需要从别人的电脑上重新clone一个版本库即可
强大的分支, 可以将一个大项目拆分成若干小功能来实现, 实现后再合并

###安装git(Linux)

1.在终端输入 git 查看git信息(如果没有安装会有下方的友好提示)
$ git
The program 'git' is currently not installed. You can install it by typing:sudo apt-get install git

2.如果没有安装, 在终端输入 **sudo apt-get install git** 安装

**注意:** 

老一点的Debian或Ubuntu Linux，要把命令改为sudo apt-get install git-core，因为以前有个软件也叫GIT（GNU Interactive Tools），结果Git就只能叫git-core了。由于Git名气实在太大，后来就把GNU Interactive Tools改成gnuit，git-core正式改为git。

###创建版本库

版本库又名仓库，英文名repository，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。
在一个有足够权限的地方创建空文件夹
在终端使用命令: 
```
$git init
git initInitialized empty Git repository in /Users/michael/learngit/.git/
```
这时git参考就建立好了, 而且是一个空仓库, 此时文件夹下会多一个.git隐藏文件, 它是来跟踪仓库变化的, 不要随意改动这个文件.
将内容放到版本库

1.git add fileName
2.git commit -m ‘info’
```
$ git add readme.md
$ git add git_study.md
$ git commit -m "add 2 files."
```

**说明:** 

git add 告诉 git 我要加入某个文件, git commit告诉 git 内容可以放入版本库了, git commit后的 -m ‘xxx’ 参数的意思是这次提交做了哪些改动, 强烈建议写上, 因为用不了多久你就会忘了曾经做了什么. 因为git commit 一次可以提交多个文件, 所以可以先通过add多个文件, 然后commit一次提交.