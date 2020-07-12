# git

## 常用命令

### pwd                   

- 查看当前终端所在目录的路径

### cd                       

- 用于切换目录的命令

	- 还可以在在终端中输入cd后拖动文件夹回车，然后终端就会切换到所拖动的文件或者文件夹的位置；eg：cd Desktop

### cd ..                    

- 当前到上一级目录去

### cd ~                    

- 回到用户的目录

### cd /                     

- 回到根目录下

### ls                        

- 查看当前目录下所有文件或者文件夹，但不包括隐藏的文件或者文件夹

### ls -la                   

- 查看当前目录下所有的文件或者文件夹，包括隐藏的文件或文件夹

### ls <文件夹名>   

- eg：ls /src   查看src下的所有文件夹和文件

### clear                  

- 清除当前终端内当前行以上的所有操作记录

### mkdir <文件夹名>

- 用于创建文件夹；eg：mkdir test

### rm -rf <文件夹> 

- 删除一个文件夹；注意，不能再当前文件夹内删除当前文件夹；-rf是强制删除，所以要特别注意文件和文件夹的删除操作

### touch <文件名>

- 用于创建文件；eg：touch home.vue

### rm <文件名>     

- 用于删除文件；eg：rm home.vue

## 配置

### 配置用户名和邮箱

- 用户名

	- git config --global user.name 'mr lin'

- 邮箱    

	- git config --global user.email '123@qq.com'

### 查看配置的邮箱或者昵称

- git --list

### 单独获取邮箱或者昵称

- git config user.name
- git config user.email

### 查看所有git命令

- git help

### 查看某一命令的详细用法或者描述

- git hlep <命令>

	- eg：git help commit

## 分支

### 创建分支

- git branch <分支名>

### 查看分支

- git branch

### 切换分支

- git checkout <分支名>

	- eg：git checkout develop    切换develop分支

### 创建并切换分支

- git checkout -b <分支名>

	- eg：git checkout -b v3   创建v3分支并且还要切换v3分支

### 删除分支

- git branch -d <分支名>

	- 注意：在当前分支下不能删除当前分支；

- git branch -D <分支名>

	- 强制删除分支

- git branch --merge | egrep -v "(^\*|master|develop)" | xargs git branch -d

	- 删除除master和deve分支以外的所有已合并的分支

- git branch --no-merge | egrep -v "(^\*|master)" | xargs git branch -D

	- 删除master以外的所有未合并的分支

- git push origin --delete <分支名>

	- 删除远端分支和远端追踪分支

### 在主线下查看已合并分支和未合并分支

- git branch --merged

	- 如果出已合并的分支外和主分支一样的话，则其他分支是新建分支

- git branch --no-merged

	- 查看未合并的分支

### 合并分支

- git merage <分支名>

	- eg：git merge develop     意为：合并develop分支

- 解决合并时的冲突

	- git status

		- 查看冲突原因

	- git merge --abort

		- 撤销合并

- git reset --hard ORIG_HEAD

	- 回到合并之前

- git merge <分支名> --no-ff

	- --no-ff 就是不执行快转机制

- git merge <分支名> --no-ff --no-commit

	- 自动合并，但是并没有提到工作区，通常用于测试合并，在合并之后没问题，就再次使用commit提交

- git branch -a

	- 查看远端追踪分支

## 管理项目

### git init

- 在当前终端所打开的目录里初始化一个本地仓库；创建后是一个隐藏文件，可以使用ls -la命令查看
- git init <文件夹>

	- eg：git init demo  意为创建一个demo文件夹且生成git本地仓库

### git add

- git add <文件或者文件夹>

	- eg：git add main.ts  意为将main.ts添加到本地仓库

- git add .

	- 将所有的文件和文件夹添加到本地仓库中

### git rm --cached <文件或者文件夹>

- git rm --cached home.vue  意为将home.vue从本地仓库中删除

### git status

- 查看当前创库所管理的文件或文件夹

### git commit

- git commit -am '文字描述'

	- 注意：只有在文件被添加到本地仓库中的时候，才可以commit

- git commit -m '此次提交的文字描述'

### git rm

- git rm <文件夹或者文件名>

	- eg：git rm 'home.js'  意为删除home.jswenjian

### git mv <被修改文件夹或者文件的名称> <被修改文件夹或者文件后的名称>

- eg：git mv home.js newHome.js  意为将home.js修改为newHome.js

### git mv <被移动的文件夹或者文件的名称> <移动到的文件或者文件夹下的文件或者文件夹，可以重新命名也可以不重新命名>

- eg：git mv home.js src/newhome.js   意为：将home.js移动到src下并重新命名为newhome.js    注意：只有在add后才能移动

### .gitignore

- 配置要忽略的文件或者文件夹；与.git目录同级；但是对已经被add到git的文件或者文件夹无效

### git rm -r --cached .

- 将已经被添加到git的所有文件或者文件夹进行’删除操作'

### git rm -r --cached <文件或者文件夹>

- eg：git rm -r --cached src/  意为：将src文件夹在git仓库中剔除，删除它的记录

### git reset HEAD <文件夹或者文件的名称>

- eg：git reset HEAD src   意为：将src从git仓库中撤销

### git checkout -- <文件或者文件夹名称>

- 在没有add之前可以对指定的文件或者文件夹进行操作；eg：git checkout -- home.js   意为：将home.js进行撤销操作

### 查看修改文件前后的区别

- git diff
- git diff <文件或者文件夹>
- git diff --staged

	- 查看最近一次提交的与上一次提交的区别

### 版本回退

- git reset --hard HEAD^

	- 回到上一个版本

- git reset --hard HEAD^^

	- 回到上上一个版本

- git reset --hard <hash值或者版本标识>

	- eg：git reset --hard b1dc588   意为：版本回退到hash值为b1dc588的那次记录

- git checkout <hash值> -- <文件或者文件夹>

	- eg：git checkout b52e27d -- index.js      回退到hash所指向版本的index.js文件的代码

- git checkout <hash值> -- .

	- eg：git checkout b52ee27d -- .    回退到hash值b52eex7d指向的版本的所有代码

### 查看版本线图

- git log --oneline --graph --all

	- 查看所有的版本提交信息

### 快转机制

- git merge <分支名> --no-ff
- git reset --head <hash值>

## 日志管理

### git log        

- 查看git本地仓库里所有的记录(包括：作者、邮箱、提交时间、所提交的文件)

### git log -p -2

- 查看最近两次提交内容的差别

### git log --oneline

- 信息都在一行显示

### git log --graph

- 查看所有分支下的信息

### git log --graph --oneline

- 查看所有分支下的信息且在一行显示

### git log --pretty=oneline

- 一行显示所有的信息，包括完整的hash值

### git log --pretty=format : <格式>

- 定制显示内容的格式

### git log --author="<作者名>"

- eg：git log --author="lin"  意为：查看作者为lin提交的所有内容

## 远程操作

### 推送的前提就是必须现在github上注册账号，登录后创建仓库

###  git remote add origin <仓库地址>

- git remote add origin https://github.com/changlin93/changlin93.github.io.git

### git push -u origin <分支名>

- git push -u origin master

### *master

- 本地分支

### remotes/origin/master

- 远端追踪分支

### github master

- 远端分支

### git push --all

- 将所有的信息进行push到远程仓库中

### 远端追踪

- git pull
- git fetch
- git merge

### 删除远端分支

- 可在远端网页中进行删除也可以命令删除
- 子主题 2

### 仓库迁移

- git remote -v

	- 获取push到远端和远端pull的地址

- git remote set-url origin <目标网址>

## 克隆项目

### 进入项目所要放的文件夹中打开终端

### git clone <目标网址>

- eg：git clone https://github.com/ant-design/ant-design.git

### git clone --no-checkout <目标网址>

- 克隆项目不切换分支

### git clone <目标网址> <自定义名称>

- 不切换分支

	- eg：git clone --no-checkout https://github.com/ant-design/ant-design.git

- 切换分支

	- eg：git clone --no-checkout https://github.com/ant-design/ant-design.git antd源码

### git clone --bare <目标网址>

- 克隆一个项目的裸的仓库信息

## ssh配置

### 概念：ssh是一种安全协议

### 进入根目录生成公钥和私钥(cd ~)

- ssh-keygen

### 进入GitHub---->点击头像---->settings---->左侧边栏SSH and GPG keys---->选择右上角的new ssh key---->将刚生成的.pub文件的内容复制到里面---->点击Add SSH keys

## 自动化部署

### 本地连接服务器

- ssh root@<公网ip>

	- eg：ssh root@127.0.0.1
