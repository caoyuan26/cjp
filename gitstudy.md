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

###时光机穿梭

* 在终端使用命令git status查看那些文件被改动, 以及那些文件将要被commit提交

* 在终端使用命令git diff查看文件被改动了什么

版本回退

如果在修改文件过程中出现了什么错误, 需要回退到就版本, 怎么办呢?

在终端使用命令git log查看提交历史
```
commit f384b35e6c614ac5444efd0167e29fee66c9c37d
Merge: c65e7a0 2a0f55c
Author: caoyuan <2675142924@qq.com>
Date:   Wed Sep 21 15:46:03 2016 +0800

    merge with no-ff

commit 2a0f55c64f68abb7cb69547063330821a3a0df39
Author: caoyuan <2675142924@qq.com>
Date:   Wed Sep 21 15:35:31 2016 +0800

    add merge

commit c65e7a0f684587adce36c2f972de7fb4ce53cd69
Merge: 28d8785 71dbe9d
Author: caoyuan <2675142924@qq.com>
Date:   Wed Sep 21 14:58:04 2016 +0800

```
如果觉得内容太多, 可以使用命令git log --graph --pretty=oneline --abbrev-commit 查看
```
yuan@yuan:~/learngit$ git log --pretty=oneline --abbrev-commit
f384b35 merge with no-ff
2a0f55c add merge
c65e7a0 conflict fixed
28d8785 & simple
71dbe9d AND simple
fc62eb2 brach test
4c51d94 remove test.txt
1ee3747 add test.text
5895409 add cao
9a97047 git track changes
440c6b3 understand how stage works
5396aed append GPL
21c867f add 3 file
9c6ce9f add 1 file
```
**说明:** 
前面的一大串数字是commit id, 和SVN不一样，Git的commit id不是1，2，3……递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示.

上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。
```
yuan@yuan:~/learngit$ git reset --hard HEAD^
HEAD is now at c65e7a0 conflict fixed
```
**注意:**
 要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。
工作区和暂存区

Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念。

工作区

工作区可以简单的理解为是git仓库目录下内容.

暂存区

回顾一下, 在将内容提交到仓库时候, 需要先使用git add一下, 此时这个add其实是吧内容提交到stage暂存区, 在执行commit的使用才会将stage暂存区中的内容提交到工作区.

git add命令将文件提交到缓存区
![20160921133228815.jpg](http://upload-images.jianshu.io/upload_images/2665727-48cc6f11eb90f748.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念。

先来看名词解释。

##工作区（Working Directory）

就是你在电脑里能看到的目录，比如我的learngit文件夹就是一个工作区：

working-dir


##版本库（Repository）

工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。

Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。

**git-repo**

分支和HEAD的概念我们以后再讲。

前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：**

第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。

**因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。**

**你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。**

**俗话说，实践出真知。现在，我们再练习一遍，先对readme.txt做个修改，比如加上一行内容：
**
```
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
```

然后，在工作区新增一个LICENSE文本文件（内容随便写）。

先用git status查看一下状态：
```
$ git status
On branch master
Changes not staged for commit:
 (use "git add <file>..." to update what will be committed)
(use "git checkout -- <file>..." to discard changes in working directory)

   modified:   readme.txt

 Untracked files:
   (use "git add <file>..." to include in what will be committed)

   LICENSE
no changes added to commit (use "git add" and/or "git commit -a")
```
Git非常清楚地告诉我们，readme.txt被修改了，而LICENSE还从来没有被添加过，所以它的状态是Untracked。

现在，使用两次命令git add，把readme.txt和LICENSE都添加后，用git status再查看一下：
```
$ git status
On branch master
Changes to be committed:
(use "git reset HEAD <file>..." to unstage)

 new file:   LICENSE
 modified:   readme.txt

```
现在，暂存区的状态就变成这样了：

git-stage

所以，git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行git commit就可以一次性把暂存区的所有修改提交到分支。

$ git commit -m "understand how stage works"
[master 27c9860] understand how stage works
 2 files changed, 675 insertions(+)
 create mode 100644 LICENSE

一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的：

$ git status
# On branch master
nothing to commit (working directory clean)

现在版本库变成了这样，暂存区就没有任何内容了：

git-stage-after-commit

###小结

**暂存区是Git非常重要的概念，弄明白了暂存区，就弄明白了Git的很多操作到底干了什么。**

**没弄明白暂存区是怎么回事的童鞋，请向上滚动页面，再看一次。**

###4.3git撤销修改

  如果在reqdme.txt中多加了一行，在提交前，我们要撤销修改

  删除添加的行，返回到上一个历史版本。

  例1：
```
  yuan@yuan:~/learngit$ git status
	On branch master
	Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)
	modified:   readme.txt
    no changes added to commit (use "git add" and/or "git commit -a")
```

  执行git status后git会提醒git checkout -- file

  git checkout -- file  可以丢弃工作区的修改

  文件在工作区的修改全部撤销

  修改后还没被放到暂存区

  撤销修改就回到和版本库一模一样状态

  修改后已经添加到暂存区

又作了修改，现在，撤销修改就回到添加到暂存区后的状态
```
git commit  
git add
git checkout -- file 
```
命令中的 --的作用

没用-- 就变成切换到另一分支命令

git checkout命令

在commit之前发现这个问题，git status 修改只是添加到了暂存区，还没有提交：

	```
	yuan@yuan:~/learngit$ vim readme.txt
	Git is a distributed version control system.
	Git is free software distributed under the GPL.
	Git has a mutable index called stage.
	Git tracks changes.
	dddd cao yuan
	i love you
	```

通过`git diff`可以看到里面添加了一个 I love you的内容

```	
	yuan@yuan:~/learngit$ git diff
	diff --git a/readme.txt b/readme.txt
	index 5d1ed32..fcb9573 100644
	--- a/readme.txt
	+++ b/readme.txt
	@@ -3,3 +3,4 @@ Git is free software distributed under the GPL.
	 Git has a mutable index called stage.
	 Git tracks changes.
	 dddd cao yuan
	+i love you^M   //此行是添加的内容，可以看到前面有一个+号
```
2、我们现在把readme.txt添加到暂存区

```
	yuan@yuan:~/learngit$ git add readme.txt  //把readme.txt添加到暂存区
	yuan@yuan:~/learngit$ git status          //查看状态
	On branch master
	Changes to be committed: 
  	(use "git reset HEAD <file>..." to unstage) //提示撤销暂存区修改
	modified:   readme.txt    				 //提示修改reqdme.txt

	yuan@yuan:~/learngit$ git reset HEAD readme.txt //撤销暂存区修改，重新放回工作区
	Unstaged changes after reset:
	M	readme.txt
```
  
###查看状态,当前已前暂存区回到的工作区

```
 yuan@yuan:~/learngit$ git status     //查看状态 
	On branch master  
	Changes not staged for commit:
  	(use "git add <file>..." to update what will be committed)
  	(use "git checkout -- <file>..." to discard changes in working directory)
	modified:   readme.txt
	no changes added to commit (use "git add" and/or "git commit -a") //
```

###再从工作区撤销命令，看到结果中没有i love you字母了

```
	yuan@yuan:~/learngit$ git checkout -- readme.txt   //撤销工作区修改
	yuan@yuan:~/learngit$ cat readme.txt               //查看readme.txt
	Git is a distributed version control system.
	Git is free software distributed under the GPL.
	Git has a mutable index called stage.
	Git tracks changes.
	cao                                           

```

3、如果从暂存区提交到了版本库，只能用前面讲到的版本回退操作
	
	前提是没有把本地版本库推送到远程，否则无法撤销。

总结；

1、修改内容有误时了，但没有提交到暂存区 直接使用 git checkout -- file

2、修改某文件内容有误后，提交到暂存区想撤销修改分如下2步

	   第一步: 先让文件回到工作区  git rest HEAD file

	   第二步：从工作区撤销修改  git checkout -- file

3、已经提交了修改内容到版本库时，想要撤销本次提交只能用版本回退，前提没有推送到远程库

##删除文件

1、添加一个test.txt新文件

	```
	yuan@yuan:~/learngit$ vim test.txt
	yuan@yuan:~/learngit$ ls      //ls查看到当前目录下多了一个test.txt文件
	LICENSE.txt  readme.txt  test.txt
	```
2、把test文件提交到暂存区

	```
	yuan@yuan:~/learngit$ git add test.txt               //把test添加到暂存区
	yuan@yuan:~/learngit$ git commit -m "add test.text"  //把test添加到本地库
	[master 1ee3747] add test.text
	 1 file changed, 0 insertions(+), 0 deletions(-)
	 create mode 100644 test.txt
	```
3、删除test.txt文件

```
yuan@yuan:~/learngit$ rm test.txt
```

删除后Git知道你删除了文件，因此，工作区和版本库就不一致了

 4、git status查看状态

 ```
	 yuan@yuan:~/learngit$ git status
	 On branch master
	 Changes not staged for commit:
	 (use "git add/rm <file>..." to update what will be committed)
	 (use "git checkout -- <file>..." to discard changes in working directory)
	 deleted:    test.txt                        //提示文件被删除
	 no changes added to commit (use "git add" and/or "git commit -a")
```
5、是否确认删除文件

如果删除文件执行git rm test.txt 删掉，并且git commit

 ```
	 yuan@yuan:~/learngit$ git rm test.txt
	rm 'test.txt'
	yuan@yuan:~/learngit$ git commit -m "remove test.txt"
	[master 4c51d94] remove test.txt
	 1 file changed, 0 insertions(+), 0 deletions(-)
	 delete mode 100644 test.txt
```

如果不小心删错了用git checkout -- test.txt 就可以找回来

    git checkout用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

总结：
  
   	1、执行git rm file 删除文件

   	2、只要提交到版本库不用提心误删除，但只能恢复最版本。

##添加远程库

1、创建本地Git仓库，GitHub创建一个Git仓库

2、让本地仓库与远程仓库进行远程同步，可以作为备份

3、登录GitHub右上角Create a new repo创建一个新库

Respository name 填learngit 点击Create repository

4、本地库与远程库关联

```
yuan@yuan:~/learngit$ git remote add origin 2675142924@qq.com:michaelliao/learngit.git
```
5、本地所有内容添加到远程库上
```
yuan@yuan:~/learngit$ git push -u origin master
```
用git push命令，实际上是把当前分支master推送到远程

第一次推送master加上-u参数

本地master分支内容添加到远程新的master分支内容
还会把本地的master分支与远程master分支关联起来，方便以后推送

以后推送就可以通过以下命令
 ```
	 git push origin master
 ```
	第一次使用Git的clone或者push命令连接GitHub时会有警告

```
The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?
```
提示确认GitHub的Key的指纹信服务息是否真的来自GitHub服务器,输入Yes即可

```
Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
```

	**警告出现一次，后面的操作就不会有任何警告了

总结；
 1、关联远程库使用命令
```
git remote add origin 2675142924@qq.com:path/repo-name.git
```
 2、第一次推送分支所有内容：git push -u origin master

 3、以后每次提次只需输入命令:git push origin master 推送最新修改

##远程仓库

1、时光穿梭可恢复历史版本

2、git分布式版本控制系统

同一个Git仓库，可以分布到不同的机器上。

从版本库机器上克隆原始版本库，每台机器都一样

3、通过一台电脑玩远程库
一台电脑上可以克隆多个版本库，只要不在同一个目录下

4、多台电脑玩远程库

一台电脑当服务器用，其它的电脑从服务器中克隆一份到电脑上，并把各自的提交到服务器仓库，也

可从服务器拉取最新版本

5、GitHub网站提供版本托管服务
只要注册一个GitHub帐号，就可免费获得Git远程仓库,GitHub通过SSH加密传输
			
第一步：创建SSH Key

	查看用户主目录下是否有.ssh目录，有再看看有没有id_rsa和id_rsa.pub这两个文件如果有跳过

	没有就创建SSH Key,执行完.ssh目录下生成 id_rsa和id_rsa.pub两个密钥文件，

id_rsa私钥，不可泄露，id_rsa.pub是公钥可以告诉别人
```
ssh-keygen -t rsa -C "2675142924@qq.com"  //更换自己的邮件地址
```

第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：
点“Add Key”，你就应该看到已经添加的Key：

总结：

1、Github 有公钥就可以确认只有你自己推送

2、允许添加多个key，多台电脑，只要把每台要访问的电脑都加到GitHub中，就可以每台推送到Github中

3、GitHub免费托管的Git仓库，任何人都可以看到，但只有自己可以修改，所以重要信息不能放进去

4、如果不想让别人看到放在GitHub中第一交点钱，把公开的变成私有的，别人就看不见了，再一个就是自己

 搭建一个Git服务器，自己的服务器别人就看不到


##分支管理策略

合并分支时，Git会用Fast forwards模式，这种模式，删除分支后会丢掉信息

强制禁用Fast forward模式,Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息

--no--ff方式的git merge

####1、创建并切换dev分支：

```
yuan@yuan:~/learngit$ git checkout -b dev
Switched to a new branch 'dev'
```

####2、修改readme.txt，提交一个新的add commit

```
yuan@yuan:~/learngit$ git add readme.txt
yuan@yuan:~/learngit$ git commit -m "add merge"
[dev 2a0f55c] add merge
 1 file changed, 1 insertion(+), 5 deletions(-)
```
####3、切换回master分支

```
yuan@yuan:~/learngit$ git branch
* dev
  master
yuan@yuan:~/learngit$ git checkout master
Switched to branch 'master'
yuan@yuan:~/learngit$ git branch
  dev
* master
```

####4、合并dev分支，请注意--no-ff参数，表示禁用Fast forward:

```
yuan@yuan:~/learngit$ git merge --no-ff -m "merge with no-ff" dev
Merge made by the 'recursive' strategy.
 readme.txt | 6 +-----
 1 file changed, 1 insertion(+), 5 deletions(-)
```

####因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。

####5、查看分支历史git log：

```
yuan@yuan:~/learngit$ git log --graph --pretty=oneline --abbrev-commit  //查看分支

*   f384b35 merge with no-ff
|\  
| * 2a0f55c add merge
|/  
*   c65e7a0 conflict fixed
|\  
| * 71dbe9d AND simple
* | 28d8785 & simple
|/  
* fc62eb2 brach test
* 4c51d94 remove test.txt
……
```

####可以看到，不使用Fast forward模式，merge后就像这样：

####6、分支策略

####管理分支原则

master分支非常稳定，仅用来发布新版本，平时不在上面干活

干活一般都在dev分支上，dev分支是不稳定的，到某个时候，比如1.0版本发布，再把dev分支合并到master上，在master分支发布1.0版本

每个人都在dev分支上干活，每个人都可以有自己的分支，时不时地往dev分支上合并就可以了

团队合作的支支看起来就像这样

###总结

1、合并分支时，加上--no-ff参数就可以用普通模式合并

2、合并后的历史有分支，能看出来曾经做过合并

3、fast forward合并就看不出来曾经做过合并。

##Bug分支

####开发中Bug修复办法

```
yuan@yuan:~/learngit$ git status
On branch master
nothing to commit, working directory clean
```
在Git中分支功能比较强大，每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。

并不是你不想提交，而是工作只进行到一半，还没法提交，预计完成还需1天时间。但是，必须在两个小时内修复该bug，怎么办？

幸好，Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作：

```
yuan@yuan:~/learngit$ git stash
Saved working directory and index state WIP on dev: f384b35 merge with no-ff
HEAD is now at f384b35 merge with no-ff
```


现在，用git status查看工作区，就是干净的（除非有没有被Git管理的文件），因此可以放心地创建分支来修复bug。

首先确定要在哪个分支上修复bug，假定需要在master分支上修复，就从master创建临时分支：

```
$ git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 6 commits.
$ git checkout -b issue-101
Switched to a new branch 'issue-101'
```

现在修复bug，需要把“Git is free software ...”改为“Git is a free software ...”，然后提交：

```
yuan@yuan:~/learngit$ git commit -m "fix bug 101"
On branch master
nothing to commit, working directory clean

yuan@yuan:~/learngit$ git commit -m "fix bug 101"
[master 32614a1] fix bug 101
 1 file changed, 1 insertion(+), 1 deletion(-)

```

修复完成后，切换到master分支，并完成合并，最后删除issue-101分支：

```
$ git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 2 commits.
$ git merge --no-ff -m "merged bug fix 101" issue-101
Merge made by the 'recursive' strategy.
 readme.txt |    2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
$ git branch -d issue-101
Deleted branch issue-101 (was cc17032).
```

太棒了，原计划两个小时的bug修复只花了5分钟！现在，是时候接着回到dev分支干活了！

```
$ git checkout dev
Switched to branch 'dev'
$ git status
# On branch dev
nothing to commit (working directory clean)
```

工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：

1、是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；

2、另一种方式是用git stash pop，恢复的同时把stash内容也删了：

```
yuan@yuan:~/learngit$ git stash pop
On branch issue-101
Changes not staged for commit:
(use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (a3c15cae9ce0df80247abf06a3462f3d7a44a1d0)
```

3、再用git stash list查看，就看不到任何stash内容了

```
yuan@yuan:~/learngit$ git stash list
```

4、你可以多次stash，恢复的时候，先用git stash list查看，然后恢复指定的stash，用命令：

```
git stash apply stash@{0}
```
总结

修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。
##Feature分支

软件开发中，总要不断添加进来,添加新功能时。

你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。

现在，你终于接到了一个新任务：开发代号为Vulcan的新功能，该功能计划用于下一代星际飞船。于是准备开发：
```
yuan@yuan:~/learngit$ git checkout -b feature-vulcan
M	readme.txt
Switched to a new branch 'feature-vulcan'
```
5分钟后，开发完毕：
```
yuan@yuan:~/learngit$ git add vulcan.py
yuan@yuan:~/learngit$ git commit -m "add feature vulcan"
[feature-vulcan afb809a] add feature vulcan
 1 file changed, 1 insertion(+)
 create mode 100644 vulcan.py
```

切回dev
###准备合并：
```
yuan@yuan:~/learngit$ git checkout dev
```
####feature分支和bug分支合并，然后删除。
但是，
就在此时，接到上级命令，因经费不足，新功能必须取消！
虽然白干了，但是这个分支还是必须就地销毁：
```
yuan@yuan:~/learngit$ git branch -d feature-vulcan
error: The branch 'feature-vulcan' is not fully merged.
If you are sure you want to delete it, run 'git branch -D feature-vulcan'.
```
销毁失败。Git友情提醒，feature-vulcan
分支还没有被合并，如果删除，将丢失掉修改，如果要强行删除，需要使用命令git branch -D feature-vulcan
。
现在我们强行删除：
```
yuan@yuan:~/learngit$ git branch -d feature-vulcan
error: The branch 'feature-vulcan' is not fully merged.
If you are sure you want to delete it, run 'git branch -D feature-vulcan'.
```

终于删除成功！
