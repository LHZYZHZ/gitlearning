Git is a distributed version control system.
Git is free software distributed under the GPL.
Creating a new branch is quick.
Creating a new branch is quick AND simple
Creating a new branch is quick and simple
add merge

git
git是分布式版本控制系统，集中式和分布式版本控制系统有什么区别呢？
集中式版本库是在中央服务器的，而干活的时候，用的都是自己的电脑，所以要先从中央
服务器取得最新的版本，然后开始干活，干完活了，再把自己的活推送给中央服务器。
中央服务器就好比是一个图书馆，你要改一本书，必须先从图书馆借出来，然后回到家
自己改，改完了，再放回图书馆。
缺点:要联网，受网速控制

分布式
每台电脑都有版本库，不用联网

创建版本库
首先，选择一个合适的地方。创建一个空目录
mkdir learngit
git init 目录会多出个.git目录

git add readme.txt
git commit -m"xxx"

git status查看结果
git diff 查看修改的内容
git log显示从最近到最远的提交日志
git reflog记录每次命令
git diff HEAD --xx查看工作区和版本区的区别

git branch 查看分支
git branch <name>创建分支
git reset --hard HEAD^版本回退
往上100个版本 git reset --hard~100
git 内部是用一个HEAD指针指向当前版本的

git reflog记录每一次命令

版本库
文件夹可以认为是一个工作区
工作区有一个隐藏目录.git
.git是版本库。
里面有一个stage的暂存区，还有
Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。
git add实际上是先把文件加到暂存区
git commit是提交到分支

撤销修改
git checkout--file 可以丢弃工作区的修改
git reset HEAD xx可以把暂存区的修改撤销，退回到工作区

git rm xx用于删除个文件
git checkout用版本库里的替代暂存区的

本地git和github传输时通过SSH加密的
要先创建SSH key
ssh-keygen -t rsa -C"邮箱地址"

github需要通过ssh key识别是你推送的
关联一个远程库
git remote add origin git@github。com：zhangrui1/learngit.git
把本地库的内容推送到远程，用git push -u origin master
git push origin master

要克隆一个仓库，首先必须知道仓库的地址，用git clone
git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。

一开始HEAD指向master，master指向提交
新创建个dev分支，HEAD指向dev，每提交一次，dev往前指一步，最后改变matser指针
的指向
查看分支：git branch
当前分支前会有一个*号
创建分支：git branch <name>

切换分支：git checkout <name>

创建+切换分支：git checkout -b <name>

合并某分支到当前分支：git merge <name>

删除分支：git branch -d <name>
git log --graph命令可以看到分支合并图

git merge --no-ff可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并

修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

开发一个新feature，最好新建一个分支；

如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。

多人协作
查看远程库信息，使用git remote -v
本地新建的分支如果不推送到远程，对其他人就是不可见的；
从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；

从远程抓取分支，使用git pull，如果有冲突，要先处理冲突，并在本地提交。


当手头工作没有完成时，先把工作现场git stash一下，
然后去修复bug，修复后，再git stash pop，回到工作现场。

git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；

另一种方式是用git stash pop，恢复的同时把stash内容也删了：
master分支是主分支，因此要时刻与远程同步；

dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；

bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；

feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

总之，就是在Git中，分支完全可以在本地自己藏着玩，是否推送，视你的心情而定！

git rebase把分支的提交历史整理成一条直线，看上去更直观，但
本地的分叉提交已经被修改过。
目的是查看历史提交的时候看提交的变化更加容易


