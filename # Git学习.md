# Git学习

## 简介

Git是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。方便产生分支、合并、回滚等操作

## 安装

Windows下直接下载安装程序，正常安装； 在某个文件夹右键，选择Git Bash Here，进入命令行界面【可以使用一些基本的Linux命令,ll、vi等】

## Git中的概念和流程

### 仓库

代码仓库了，仓库（Repository）是用于保存版本管理所需信息的地方
本地使用git init 初始化一个仓库【会新增一个.git隐藏文件夹】，或git clone 从网上克隆一个仓库；git 网页上可以fork别人的仓库，或通过点击新建

为了上传到自己的仓库，或上传给别人显示出谁在修改，需要添加用户名和邮箱：
git config --global user.name "xxx"
git config --global user.email "xxx@xxx.com"

#进入到项目中，在有.git文件的目录下 连接到远端仓库地址
git remote add upstream https://github.com/其他人的库.git（主仓库的URL）
 
#禁止向远端主仓库进行的代码提交
git remote set-url --push upstream no_push
 
#查看本地关联的代码库
git remote -v


git branch [your branch]   # 新建分支；不加参数是查看现有分支，并显示目前激活的分支
git checkout [your branch] # 切换到自己的分支 
#也可以修改本地分支的名称
git branch -m [old_name] [new_name]
git branch -d [your branch]  # 删除分支
git push origin --delete [your branch]  # 删除远端分支
git rebase [your branch]  # 合并分支，一般会提示冲突，查看冲突文件、修改、add、commit
git diff [your branch]  # 查看分支差异

#修改一些代码

#查看那些文件修改了
git status
 
#提交好修改的【部分】文件到本地仓库
git add filename1 filename2
git add -u #-u表示只增加文件修改，不添加新创建的文件
git add -A #-A表示增加所有文件修改  或 git add .
 
#提交comit 信息（这个是作为代码提交的检查的 符合你们公司的开发规范）
git commit --amend (git commit -m "公司的规范"  #网上会看备注信息，但文件并没有更新)

#推送到本地同时提交PR
git push -f origin topic/jiale_xiong/data/vxp568(本地分支):vxrail-cr（个人远端分支）  #其中的orgin已设置为一个网址
#git push 的命令格式一般是
git push <远程主机名> <本地分支名>：<远程分支名>
一般情况下之间写 git push即可。

Pull 将远程仓库的更新（比如其他人提交的代码）合并到本地仓库
Pull request 提交PR，将本地仓库的更新（比如自己提交的代码）合并到远程仓库，网上的pull request可以把自己的修改，提交给之前fork的其他人的仓库，等待审核，审核通过会合并到主仓库，并显示贡献人

#拉取远端主仓库 拉取最新的代码到本地
git fetch upstream

### 工作区

工作区/工作目录是文件被检查更新、变动（增、删）的地方。
git init 新建一个仓库，里面的所有文件更新、变动（增、删）都能被检测到

### 暂存区

暂存区（Stage）是工作区与仓库之间的缓冲区，如果某些文件有变化，需要先提交到暂存区，然后再提交到仓库
git add .   #把工作区中的所有文件添加到暂存区——commit的时候只提交暂存区中的文件
git add [filename] #只添加一个文件

### 版本库

Git仓库/版本库（Repository）是Git用来保存项目的元数据和对象数据库的地方，版本库里包含了所有文件的历史，以及所有分支

### 工作流程

  1. 克隆仓库
   fork：把其他人的某个仓库repository复制一份到自己的账号下（以便修改）
   clone：将Git仓库中的代码复制到本地，以便修改。【当clone其他人的仓库时，注意其中的.git配置，可能指向了其他人的服务器，此时需要修改为指向自己的服务器】
   也可以新建仓库，使用git init命令，然后使用git add .和git commit -m 命令，将代码提交到本地仓库
  2. 创建分支
  3. 提交修改
   Commit：将修改提交到暂存区，并保存修改的快照。
  4. 合并冲突
  5. 回滚版本
  6. 标签
  7. 提交到远程仓库
   push: 把本地仓库的修改推送到远程仓库