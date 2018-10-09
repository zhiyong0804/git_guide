# 3.4 git基础常用命令

### 3.4.1 add命令
添加工作区的文件到暂存区。
例如git add file[*]，使用*可以添加该目录下所有的文件包含子目录下的文件。

### 3.4.2 status命令
git status：显示工作树的状态，一般有三种状态
* Untracked files：未被跟踪的文件，表示是工作目录新增加的文件
* Changes not staged for commit：工作目录中修改了文件，但是没有被添加到暂存区
* Changes to be committed：添加到暂存区的文件，等待提交

### 3.4.3 commit命令
git commit后，会生成一个commit-id，这是一个能唯一标识一个版本的序列号。 在使用git push后，这个序列号还会同步到远程仓库。
* git commit -m "提交消息"：提交暂存区的文件，带有提交消息
* git commit -a -m "提交消息"：跳过暂存区，直接提交工作目录中所有改变的文件，但是不能提交工作目录中新增的文件
* git commit --author=lavor -m "提交消息"：提交暂存区的文件，并重写提交作者
* git commit --date=06.13.2016T09:00:00 -m "提交消息"：提交暂存区的文件，并重写提交日期
* git commit --amend -m "提交消息"：通过创建一个新的提交，以替换当前分支的前端。所代表的含义就是在最新一次提交的基础上进行提交。比如我们完成了最新一次提交，并且这次提交完成后我们对工作目录进行了一些修改，但是我们发现某个文件忘了添加到暂存区并提交，我们可以先添加该文件到暂存区，然后利用该命令进行提交。

### 3.4.4 reset命令
* git reset：将暂存区的所有文件重置到当前分支的HEAD
* git reset <commit> files：将暂存区的指定文件重置到指定的<commit>,<commit>既可以是commit的hash（或者hash前7位）也可以是HEAD及其祖先，HEAD~1表示HEAD的父亲，是HEAD的前一次提交，没有<commit>时默认是HEAD。
* git reset [--hard|soft|mixed|merge|keep] [<commit>]：将当前的分支重设到指定的<commit>，并且根据mode有可能更新暂存区和工作目录。mode的取值可以是hard、soft、mixed、merged、keep。
    hard：重置暂存区与工作目录到指定提交，删除<commit>之后的所有提交并将HEAD指向该提交，此操作危险指数较大（应慎用）
    soft：暂存区与工作目录不会变化，仅仅删除<commit>之后的所有提交并将HEAD指向该提交
    mixed：默认的，重置暂存区到指定提交，删除<commit>之后的所有提交并将HEAD指向该提交
    merge与keep用的比较少，暂时不讨论

HEAD是指向当前分支引用的指针，该指针指向在该分支上的最后一个提交的指针。这意味着HEAD将是下一个创建的提交的父亲。一般来说，把你的HEAD作为你最后一次提交的快照，是最简单的。HEAD~1表示HEAD的前一次提交，HEAD~2表示HEAD的前两次提交，以此类推。

### 3.4.5 rm命令
* git rm files：删除工作目录的文件
* git rm -f files：强制删除工作目录的文件，不做更新检查
* git rm --cached files：删除暂存区的文件

### 3.4.6 mv命令
* git mv oldfile newfile：为文件重命名
* git mv files dir：移动文件到指定目录
* git mv -f oldfile newfile：强制为文件重命名，即使目标文件已存在
* git mv -f files dir：强制移动文件到指定目录名，即使目标文件已存在

### 3.4.7 fetch命令
* git fetch：下载远程仓库“origin”到本地
* git fetch remote repository：下载指定远程仓库到本地
* git fetch remote repository branchname：下载指定远程仓库指定分支到本地

### 3.4.8 pull命令
git pull remote repository branchname[:localbranch]：拉取指定远程仓库指定分支到本地仓库指定分支（默认是当前分支）.
git fetch和git pull的区别是当从远程仓库拉取信息到本地，前者不会自动与本地的修改做merge，而后者会。

### 3.4.9 push命令

git push remoterepository localbranch[:remotebranch] [--tags]：推送本地仓库指定分支到远程仓库指定分支（默认是与本地分支同名的远程分支），默认是不推送标签到远程仓库的，加上--tags就会推送标签

### 3.4.10 submodule命令
* git submodule add repository-url dir：添加仓库到指定目录，使之成为本仓库的子模块
* git submodule init：初始化子模块
* git submodule update：更新子模块

子模块是本仓库依赖的另一个仓库，但是我们不会对所依赖的仓库（子模块）进行修改，只会在必要的时候进行更新操作。

### 3.4.11 show命令
* git show [-times]：显示最近times次（默认是一次）提交的所有对象信息

### 3.4.12 log命令
* git log：查看提交记录
* git log --all：查看所有提交记录
* git log --oneline：查看提交记录，以oneline形式显示，只显示一行，显示的内容时提交hash的前7位与提交消息
* git log -p -times：表示查看最近times次提交改变的内容
* git log -stat [-times]：查看最近times次（默认是所有）提交记录，并显示文件的差异分析

### 3.4.13 diff命令
* git diff：查看工作目录与暂存区的差异
* git diff --cached [<commit>]：查看暂存区与指定提交（默认是HEAD）的差异
* git diff <commit>：查看工作目录与指定提交的差异
* git diff <commit>：查看工作目录与指定提交的差异
* git diff <commit> <commit>：查看两次指定提交的差异
* git diff branchname：查看工作目录与指定分支的差异
* git diff branchname branchname：查看两个指定分支间的差异
上面的所有操作后面都可以加上-- dir表示查看该目录下面的差异，在后面加上>patchname.patch表示将差异生成补丁，patchname是补丁的名字。

### 3.4.14 shortlog命令

git shortlog：显示总提交次数与每次提交的提交消息

### 3.4.15 describe命令
* git describe [<commit>|<tag>]：查看指定提交或者指定标签（默认是最近一次提交）的注解标签信息
* git desribe --tags [<commit>|<tag>]：查看指定提交或者指定标签（默认是最近一次提交）的标签信息
* git desribe --all [<commit>|<tag>]：查看指定提交或者指定标签（默认是最近一次提交）的引用信息

### 3.4.16 reflog命令
* git reflog：显示所有提交，下拉，推送，与切换分支操作
* git reflog --all：显示所有提交，下拉，推送操作

### 3.4.17 apply命令
* git apply [--index|--cached] patchname.patch：在暂存区与工作目录或者暂存区（默认是工作目录）打补丁
* git apply --reverse|-R patchname.patch：反向打补丁
* git apply --reject patchname.patch：打补丁，将没有冲突的文件合并，将有冲突的文件标记出来，并生成对应的.rej文件

### 3.4.18 cherry-pick命令
* git cherry-pick <commit>：将另一个分支上面的指定提交应用到当前分支上
* git cherry-pick banchname：将指定分支上面的最后一次提交应用到当前分支上

### 3.4.19 rebase命令
* git rebase branchname：将指定分支上所有修改应用到当前分支上
* git rebase branchname branchname：将第一个指定分支上所有修改应用到第二个分支上
在rebase加上-i会提供交互式的变基操作，在交互式操作中常用命令：

### 3.4.20 revert命令
* git revert <commit>：恢复一个指定提交

### 3.4.21 bisect命令
使用二分查找，找到引入bug的提交
* git bisect start：开始二分查找
* git bisect bad [<commit>]：设置指定提交（默认是当前分支）为bad
* git bisect good [<commit>]：设置指定提交（默认是当前分支）为good
输入了上面三个命令后就会自动开始二分查找，我们之后只需要标记当前提交时bad还是good就行了，如果当前找的的提交时bad就输入git bisect bad，否则输入git bisect good直到找到有bug的提交。

### 3.4.22 blame命令

显示修改和作者最后修改的文件的每一行，这就是一个“问责”的命令，如果哪里有问题，我们可以很快地找到该问题是谁导致的。

git blame filename：查看指定文件所有的操作者，看看是谁错误地修改了该文件

### 3.4.23 grep命令
git grep keys：在工作目录中所有文件中搜索keys
git grep --cached keys：在暂存区中所有文件中搜索keys

