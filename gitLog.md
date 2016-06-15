# [git](https://git-scm.com/download/)
##- 查看当前目录文件相关状态
> git status

##- 将test.txt文件加入到暂存区
> git add test.txt

##- 将暂存区文件提交到仓库更新并注释
> git commit -m "注释"

##- 链接本地仓库与远程仓库
> git remote add origin URL

##- 更改本地仓库与远程仓库的链接
> git remote set-url origin URL

##- 创建分支,无分支名则为查看当前所有分支
> git branch **分支名**

##- 克隆远程仓库文件至本地仓库
> git clone URL

##- 将本地分支文件上传至github
> git push -u origin master

##- 切换分支
> git checkout **分支名**

##- 查看日志
> git log