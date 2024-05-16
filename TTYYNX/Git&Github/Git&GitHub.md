# Github基本概念
## 1. Repository
仓库用来放项目代码，每个项目对应一个仓库，有多个开源项目即有多个仓库
### 1.1. 创建文件
创建后需输入文件名以及文件内容，提交时需要输入该文件的详细信息
### 1.2. 编辑文件
点击文件名找寻修改功能 点击描述信息即可看见提交时作者输入的的详细信息
### 1.3. 搜索仓库文件
在仓库界面中按T即可跳转到搜索界面，或直接在仓库界面中选择Go to file按钮
### 1.4. 上传文件
上传文件的按钮和创建文件的按钮挨在一起，上传文件时可以拖拽也可以选择，并且可以同时上传多个文件
## 2. Star
收藏项目，方便查看
## 3. Fork
复制他人项目（仓库），一模一样，然后可以随意对这个项目进行改进创造，但丝毫不影响原有项目
## 4. Pull Request
假设自己开源的一个项目，有人在你原有的基础上做出改进，发出PR请求，自己可以收到通知，并且自己会仔细查看ta的代码，如果觉得不错，并且通过测试，就会接受ta的PR，那么ta做的改进原项目就会有了
## 5. Watch
类似于订阅，如果watch了一个项目，只要这个项目有更新，会第一时间通知你
## 6. Issue
假设自己做了一个项目，别人发现你项目有Bug或者说你的项目有地方需要改进，那么ta就会给你提出issue，提多了就变成issues了，你解决这些后就可以一个个的去close掉了。简单来说就是自己给别人项目提出问题，或别人给自己的项目提出问题会用到这个功能。

## 7. 开源项目贡献流程
### 7.1. 1、issue
给作者提出问题，讨论并解决问题
### 7.2. 2、Pull Request
1、fork
2、在fork的项目中改进或添加自己的想法
3、新建 Pull Request
4、等待原作者审核

# Git基本概念
## 1. 下载与教程
[下载地址](https://git-scm.com/downloads)
[视频教程](https://www.bilibili.com/video/BV1HM411377j?p=1&vd_source=7664b55184fd63da03a03ef6c9be4310)
## 2. 设置用户名称和email
下载安装好后的第一件事 设置好的信息其实就是一个文件
## 3. git 的工作区域与文件状态
### 3.1. 工作区域
1、工作区 2、暂存区 3、本地仓库
git add将文件添加到暂存区  git commit 将文件提交到本地仓库 （顺序不可乱）

### 3.2. 文件状态
1、未跟踪 2、未修改 3、已修改 4、已暂存
untrack 指的是还没有被git管理的文件
unmodified 指的是被git管理的文件 但还未做修改
modified 指的是在git的管理下被修改的文件
staged 指的是被add到暂存区的文件

## 4. git 相关命令
git init 初始化仓库（本地仓库）
git status 查看文件夹下文件状态
git add 文件名 将该文件提交至暂存区
git rm --cached 文件名 将该文件从暂存区提出
git add`*.txt ` 指将当前目录所有以txt结尾的文件全部提交
git add `.` 指的是将当前目录所有文件全部提交
git commit -m 'xxx' 将暂存区内容提交到本地仓库
git log 查看提交记录 若后面加上 --oneline 则会返回简洁的提交记录
git ls-files 查看暂存区的内容
git diff 查看工作区与暂存区内容的区别
git diff HEAD 查看工作区与本地仓库的区别
git diff 版本号1 版本号2 查看两个版本的区别
git diff head~x head 查看当前版本与上个版本的区别（x不写）x指的是head前x版本
git diff head~x head 文件名 这种情况下只会查看两版本该文件的差异内容
还有比较分支的差异的
git rm 文件名 指把文件从工作区和暂存区同时删除(记得提交，不然文件还在本地仓库中)
git rm --cached 文件名 将该文件只从暂存区删除
ls -la 显示所有文件的详细信息 包括隐藏文件
rm -rf .git [删除本地库](https://blog.csdn.net/legend818/article/details/125556428)

### 4.1. 版本控制功能（特别重要）
三个模式如下：
![](Pasted%20image%2020231028105144.png)
soft 保留工作区与暂存区的内容
hard 不保留工作区与暂存区的内容
mixed 保留工作区内容，不保留暂存区的内容
在进行版本控制时，需要使用的相关语句有(需要在初始化好的仓库进行)
git add xxx
git commit -m"xxx"
git log --oneline
git reset --hard 版本号
**多练习使用**


### 4.2. 忽略文件（常用）
[视频教程](https://www.bilibili.com/video/BV1EG4y1Z7WW/?spm_id_from=333.337.search-card.all.click&vd_source=7664b55184fd63da03a03ef6c9be4310)
在.gitignore中写入信息，以此来忽略一些文件
模式匹配通配符写法要熟悉
模式匹配通配符如下:
![](Pasted%20image%2020231029100532.png)
### 4.3. 远程仓库
[视频教程](https://www.bilibili.com/video/BV15F411z7V7?p=1&vd_source=7664b55184fd63da03a03ef6c9be4310)
1、使用本地git客户端生成ssh公钥和私钥 执行命令如下:
```
ssh-keygen -t rsa -C "github账户邮箱" 
若是第一次生成，一直回车即可
```
![](Pasted%20image%2020231029154651.png)
执行完成后，C:/user/.ssh/id_rsa.pub即为公钥，将内容添加到github即可。
复制完成后，粘贴到github时，在最后按一次delete键，删去空格。

2、检查测试链接 执行命令如下：
```
ssh -T git@github.com
```
![](Pasted%20image%2020231029154731.png)
出现以上界面即为绑定成功。
#### 4.3.1. 本地推送至远程仓库
1、创建远程仓库和本地仓库
2、本地仓库绑定远程仓库 执行命令如下:
```
git remote add origin 远程仓库ssh链接
```
3、将**已提交至本地仓库的文件**推送至远程仓库 执行命令如下:
```
git push origin master
```
4、拉取远程仓库文件以更新本地文件 执行命令如下:(在提交前最好拉取下，拉取导致文件变化，可以回溯回去)
```
git pull origin master
```
`注` :3、4两点的执行命令中 master只是分支名 可以选择其他分支
### 4.4. 分支功能
本地分支常用命令如下:
```
git branch  //查看所有分支，并且在当前分支上标注*号

git checkout -b 分支名 //新建一个分支，且以"分支名"命名

git checkout 分支名 //将分支切换到"分支名"这个分支

git branch -m|-M oldname newname //修改分支名，oldname改为newname.大写M表示即使要改的分支名存在，也强制改为该分支名。

git branch -d|D 分支名 //删除（D强制）分支，记得在主分支操作

git merge 分支名 //特别注意在主分支上进行该操作！要主干合并其他分支！ 合并"分支名"分支，分支合并后可以将分支删除
```
远程分支常用命令如下:
```
git branch -a //查看本地分支与远程分支
git push origin :分支名 //删除远程分支 相对于推送语句加上了':'
git fetch //获取远程仓库最新的状态
git checkout -b 本地分支名x origin/远程分支名x //拉取远程分支x，并在本地创建x
```
[git pull & git fetch区别](https://blog.csdn.net/riddle1981/article/details/74938111)

### 4.5. 冲突解决
1、本地冲突
冲突条件: 分支与主干的同一个文件的同一个地方发生都修改了，且修改后的内容不一致，那么在合并的时候就会发生冲突。前提条件是主干与分支的内容都已经提交。
`解决方法`:切换到任务进行的分支 修改发生冲突的文件 添加提交即可
`注`：在测试冲突时，切换到其他分支时，若只是在（与主干）同一个文件的后面加上新内容，并不会发生冲突。
2、远程冲突（即多人协同冲突）
当多人协同开发一个文件，第一个人推送该文件不会发生冲突，随后只需要满足冲突条件，便会发生冲突。
`解决方法`:当文件推送至远程仓库时发生冲突后，先拉取远程仓库的信息，然后修改发生冲突的文件，再次添加、提交、推送即可。

### 4.6. 标签管理
标签的作用就是能更好地管理版本。
相关命令如下：
```
git tag 查看本地标签
git ls-remote --tags origin 查看远程标签
git tag tagname 给最近一次提交到的版本打上tagname标签
git tag tagname 版本号 给任意版本打上tagname标签 版本号查看日志记录
git tag -a tagname -m 'xxx' 版本号 给任意版本打上tagname标签，并指定标签信息xxx
git push origin tagname 将tagname标签推送到远程仓库
git push origin --tags 将未推送的标签全部推送至远程
git tag origin :refs/tags/tagname 删除远程仓库标签内容
git tag -d tagname 删除本地标签
```

