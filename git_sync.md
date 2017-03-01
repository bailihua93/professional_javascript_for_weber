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
+ 创建一个新的分支并选择
git checkout -b dev 等价于 git branch dev    git checkout dev
git branch  //显示目前存在的所有分支
git checkout branchname   修改当前分支位置