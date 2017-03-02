git : https://github.com/bailihua93/professional-javascript.git



### 安装网站
- 安装好git之后输入一下本地的账户
```
 $ git config --global user.name "Your Name"
 $ git config --global user.email "email@example.com"
```

###  常见命令行
#### 创建并提交
mkdir leargit
cd learngit
pwd   // 显示父目录
git  init   // 初始化
ls  -ah   //  显示所有的文件
git add .  // 添加全部文件
git commit   -m  "discription"
每次必须add 之后才能commit

git status // 显示文件状态
git diff   //显示不同的东西


#### 版本回退
git log  显示每次提交的时的状态
git log --pretty=oneline

git reset --hard  HEAD^   // 版本回退   HEAD   当前   、   HEAD^ 上一次  、HEAD^^   上上次  、前第100次的 所以写成HEAD~100
git reset --hard id   // 直接跳转到id对应的版本

第二天看不到以前的id了的话，可以用
git reflog
git reset --hard id   // 直接跳转到id对应的版本

#### git保存的是修改
现将修改 add 进去，才能commit 
#### 显示区别
git diff HEAD --readme.txt   //这里的HEAD 和前面的一样可以加……
#### 撤回
git checkout  -- filename   撤回所有修改到 add或者commit之前的状态
git checkout --filename  中 --  很重要，没有-- 就会变成"切换到另一个分支"命令

把错误的信息添加到缓存中的话，可以撤销的
git  reset HEAD file 可以吧缓存中文件重新放回工作区中

#### 删除文件
touch delete.txt
git add delete.txt
git commit -m  "我要添加"
rm delete.txt

然后你有两个选择：
+ 在库里面删除然后提交 
 > git rm delete.txt
 > git commit -m ""
+ 还原
 > git checkout --delete.txt
 #### chekout 
 git checkout 其实是用版本库里面的文件替换工作区的版本。无论工作区的修改还是还原
命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，
你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容

####　远程仓库

 怎么修改到别的远程的库呢
1. 创建公私秘钥
ssh-keygen -t rsa -C "youremail@example.com"
由于不用于军事目的所以不用设置密码

SHA256:gigaoDSA4/NrLOkD+DBS+XZQ0QQk49cCoff3xpxahhc bailihua93@163.com

登录github，进入setting ,然后将ssh_pub里的内容添加到key里面
2. 创建仓库


git remote add origin https://github.com/bailihua93/hah.git  //用origin代替远程仓库的名字
git remote add origin git@github.com:bailihua93/responName.git
git push -u origin master　//git push 本来就是将本地库推送到远程库中，　加上-u　会将远程库和现在的库关联起来
git push origin master　　以后就可以用这个命令了


#### 分支管理
##### 创建分支并合并
git checkout -b dev 等价于 git branch dev    git checkout dev
git branch  //显示目前存在的所有分支
// 修改文件， add and commit
git checkout master   修改当前分支位置
git merge dev   //简单的合并，只是把一个主分支的指针移到了dev的指针罢了
git branch -d dev  删除那个分支

##### 解决冲突 
git checkout -b feature1
<!--修改文件并添加提交后-->
git add readme.txt
git commit -m "hello"
<!--切换到主分支-->
git checkout master
<!--在主分支上添加并修改后-->
git add readme.txt
git commit -m "$simple "

解决冲突
git merge feature1　//这里会显示冲突
手动修改文件(不改也行)
然后　add commit 就自动认为合并了的

git log --graph 　显示合并的路径问题

##### 分之策略
通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。

如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

下面我们实战一下--no-ff方式的git merge：

git merge --no-ff -m "merge with no-ff" dev


+ 
首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；

合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。

##### bug分支
newproject工作到一半的时候突然来了个　bug 怎么半
git stash　可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作
然后返回产生　bug 的主分支
git checkout master
git checkout -b bug-fix1
保存并修改 ，返回主分支, 
git merge --no-ff -m "bug fix" bug-fix1
git branch -d bug-fix1

返回
git checkout newproject 
git stash list 显示暂存的东西
git　stash apply     git stash drop    ===   git stash pop
##### feature 分支
添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，
最后，删除该feature分支。
git checkout -b feature-vulcan
开发完毕了
git add vulcan.py
git commit -m "add feature vulcan"
返回并合并
git checkout dev
git merge --no-ff -m "合并新功能" feature 

如果老板不想要新功能了， 就不要合并了　，
git branch -D feature-vulcan     强制删除

##### 多人协作
git remote　　显示远程的库
git remote -v 显示完整的库，如果没有推送权限，就看不到push的地址。

git push origin master
如果要推送其他分支，比如dev，就改成：
git push origin dev


+ 哪些分支需要提交
   - master分支是主分支，因此要时刻与远程同步；

   - dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；

   - bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；

   - feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。
+ 抓取分支
 clone git@github.com:michaelliao/learngit.git
 小伙伴要在dev分支上开发，就必须创建远程origin的dev分支到本地，于是他用这个命令创建本地dev分支：
 git checkout -b dev origin/dev
 他就可以在dev上继续修改，然后，时不时地把dev分支push到远程：
 git commit -m "add /usr/bin/env"
 git push origin dev

 你的小伙伴比你早提交了一些，这时你push会出错的，
 先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送：

 指定本地dev分支与远程origin/dev分支的链接，
 git branch --set-upstream dev origin/<branch>
 git pull
 git pull成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的解决冲突完全一样。解决后，提交，再push：
 git commit -m "merge & fix hello.py"
 git push origin dev

 + 总结
 因此，多人协作的工作模式通常是这样：

首先，可以试图用git push origin branch-name推送自己的修改；

如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

如果合并有冲突，则解决冲突，并在本地提交；

没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！

如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。

