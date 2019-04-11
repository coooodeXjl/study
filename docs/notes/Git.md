# 一 Git 简介

Git 是目前世界上最先进的分布式版本控制系统（没有之一）

功能：不但能自动帮我记录每次文件的改动，还可以让同事协作编辑

# 二 安装 Git

## （1）在 Windows 上安装 Git

在 Windows 上使用 Git，可以从 Git 官网直接下载安装程序，（网速慢的同学请移步国内镜像），然后按默认选项安装即可。

安装完成后，在开始菜单里找到 “Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明 Git 安装成功！

安装完成后，还需要最后一步设置，在命令行输入：

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

# 三 创建本地仓库

## (1) 创建空目录

首先，选择一个合适的地方，创建一个空目录：

```
$ mkdir rep
$ cd rep
$ pwd
/Users/michael/rep
```

pwd 命令用于显示当前目录。在我的 windows 上，这个仓库位于 /Users/cl22/rep

> **如果你使用 Windows 系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文**
 
## (2) 通过 git init 命令把这个目录变成Git可以管理的仓库：
 
 ```
 $ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
 ```
 
 瞬间 Git 就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个 .git 的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把 Git 仓库给破坏了
 
> **使用 Windows 的童鞋要特别注意：
千万不要使用 Windows 自带的记事本编辑任何文本文件。原因是 Microsoft 开发记事本的团队使用了一个非常蠢的行为来保存 UTF-8 编码的文件，他们自作聪明地在每个文件开头添加了 0xefbbbf（十六进制）的字符，你会遇到很多不可思议的问题**

## (3) 创建并编辑一个文件

创建文件 readme.md
```
$ touch readme.md
```

或者直接通过编辑文件创建文件 readme.md
```
$ vi readme.md
```

进入编辑页面，按 i 开始编辑

按ESC键，以确保不在编辑模式，然后键入 :wq，保存并退出编辑

## (4) 添加至本地仓库

分两步：
第一先添加文件

```
 git add readme.txt
```

第二提交文件
```
 $ git commit -m "wrote a readme file"
[master (root-commit) eaadf4e] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```

-m后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。

1 file changed：1个文件被改动（我们新添加的readme.txt文件）；2 insertions：插入了两行内容（readme.txt有两行内容）

# 四 commit 版本退档

## (1)修改文件，查看 commit 信息，版本回退

通过 vi 指令多次修改文件并 commit 

像这样，你不断对文件进行修改，然后不断提交修改到版本库里，就好比玩RPG游戏时，每通过一关就会自动把游戏状态存盘，如果某一关没过去，你还可以选择读取前一关的状态。有些时候，在打Boss之前，你会手动存盘，以便万一打Boss失败了，可以从最近的地方重新开始。Git也是一样，每当你觉得文件修改到一定程度的时候，就可以“保存一个快照”，这个快照在Git中被称为commit。一旦你把文件改乱了，或者误删了文件，还可以从最近的一个commit恢复，然后继续工作，而不是把几个月的工作成果全部丢失。

在Git中，我们用git log命令查看 commit 版本历史记录
```
cl22@DESKTOP-7VCRQT0 MINGW64 /f/gitRep/rep (master)
$ git log
commit ab258c910f4b6c3862373fde0aec232bad9feab8 (HEAD -> master)
Author: xujilong <txjl0908@163.com>
Date:   Thu Apr 11 14:22:55 2019 +0800

    third commit

commit c25926125a1e96e20705b2a92f148b4eb7ccb6af
Author: xujilong <txjl0908@163.com>
Date:   Thu Apr 11 14:20:56 2019 +0800

    second commit

commit e52ce980436858e028aefd2fd0c322c02f025307
Author: xujilong <txjl0908@163.com>
Date:   Thu Apr 11 14:16:19 2019 +0800

    first commit

```

> 需要友情提示的是，你看到的一大串类似 1094adb... 的是 commit id（版本号）是一个 SHA1 计算出来的一个非常大的数字，用十六进制表示

首先，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交1094adb...（注意我的提交ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。
```
cl22@DESKTOP-7VCRQT0 MINGW64 /f/gitRep/rep (master)
$ git reset --hard HEAD^
HEAD is now at c259261 second commit
```

## (2) 工作区，暂存区和版本库

工作区（Working Directory）：
就是你在电脑里能看到的目录，比如我的 rep 文件夹就是一个工作区：

使用 vi 指令修改文件后，此时文件只在工作区进行了修改

使用 git add 指令将工作区文件添加到 暂存区

使用 git commit 指令将暂存区文件提交到版本库

使用 git status 指令可查看当前文件状态

## (3) 管理修改

Git跟踪并管理的是修改，而非文件

举个栗子，readme.md 文件，第一次修改并 git add，此时暂存区存放的不是文件，而是 readme.md 的修改操作，此时第二次修改  readme.md 文件不 git add，第二次修改完以后，暂存区仍然存放的是第一次修改的操作

## (4) 撤销工作区的修改

在工作区修改后发现有误想删除这次修改，可使用指令：

```
$ git checkout -- readme.md
```

命令 git checkout -- readme.md 意思就是，把 readme.md 文件在工作区的修改全部撤销，这里有两种情况：

一种是 readme.md 自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是 readme.md 已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

> git checkout -- file命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到 git checkout 命令

在工作区修改并 git add 后发现有误想删除这次 add 的修改，可使用指令把暂存区的修改撤销掉（unstage），重新放回工作区：

```
$ git reset HEAD readme.md
Unstaged changes after reset:
M    readme.md
```

## (5) 删除文件

使用指令删除文件：
```
$ git rm test.txt
rm 'test.txt'

$ git commit -m "remove test.txt"
[master d46f35e] remove test.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 test.txt
```



# 五 关联远程仓库

Git 是分布式版本控制系统，同一个 Git 仓库，可以分布到不同的机器上

GitHub 提供免费的 Git 仓库托管服务

由于你的本地 Git 仓库和 GitHub 仓库之间的传输是通过 SSH 加密的，所以，需要一点设置

## (1) 创建 SSH Key

在用户主目录下（在开始菜单打开 Git bash 当前路径就是主菜单，一般是 C 盘 user 里的 “yourUsername” 文件夹），看看有没有 .ssh 目录，如果有，再看看这个目录下有没有 id_rsa 和 id_rsa.pub 这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开 Shell（Windows 下打开 Git Bash），创建 SSH Key：

```
$ ssh-keygen -t rsa -C "youremail@example.com" 
```

你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可

如果一切顺利的话，可以在用户主目录里找到 .ssh 目录，里面有 id_rsa 和 id_rsa.pub 两个文件，这两个就是 SSH Key的秘钥对，id_rsa 是私钥，不能泄露出去，id_rsa.pub 是公钥，可以放心地告诉任何人

## (2) 在远程仓库添加 SSH 公钥

登陆 GitHub 或 GitLab，打开 “Account settings”，“SSH Keys” 页面

然后，点“Add SSH Key”，填上任意 Title，在 Key 文本框里粘贴 id_rsa.pub 文件的内容

为什么 GitHub 需要 SSH Key 呢？因为 GitHub 需要识别出你推送的提交确实是你推送的

## (3) 添加远程仓库

首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：

目前，在 GitHub 上的这个 rep 仓库还是空的，GitHub 告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到 GitHub 仓库。

```
cl22@DESKTOP-7VCRQT0 MINGW64 /f/gitRep/rep (master)
$ git remote add origin git@github.com:coooodeXjl/rep.git
```

```
cl22@DESKTOP-7VCRQT0 MINGW64 /f/gitRep/rep (master)
$ git push -u origin master
The authenticity of host 'github.com (52.74.223.119)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,52.74.223.119' (RSA) to the list of known hosts.
Enumerating objects: 14, done.
Counting objects: 100% (14/14), done.
Delta compression using up to 6 threads
Compressing objects: 100% (8/8), done.
Writing objects: 100% (14/14), 1013 bytes | 506.00 KiB/s, done.
Total 14 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), done.
To github.com:coooodeXjl/rep.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

把本地库的内容推送到远程，用 git push 命令，实际上是把当前分支 master 推送到远程。

由于远程库是空的，我们第一次推送 master 分支时，加上了-u参数，Git 不但会把本地的master分支内容推送的远程新的 master 分支，还会把本地的 master 分支和远程的 master 分支关联起来，在以后的推送或者拉取时就可以简化命令。

从现在起，只要本地作了提交，就可以通过命令提交到远程库：
```
$ git push origin master
```

# 参考资料

<a href="https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000" target="_blank">廖雪峰 : Git 教程</a>