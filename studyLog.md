# 小记
##1. [pandoc](http://www.pandoc.org/)
###- 将.md文件转换成.docx文件命令
> pandoc -f markdown -t html ./input.md | pandoc -f html -t docx -o output.docx

##2. [maven](http://maven.apache.org/)
###- 构建WEB项目命令
> mvn archetype:generate -DgroupId=**项目结构** -DartifactId=**项目名** -DarchetypeArtifactId=maven-archetype-webapp

###- 当maven无法获取catalog时,加入此参数使maven不在远程服务器获取该文件
> -DarchetypeCatalog=internal

##3. [git](https://git-scm.com/download/)
###- 查看当前目录文件相关状态
> git status

###- 将test.txt文件加入到暂存区
> git add test.txt

###- 将暂存区文件提交到仓库更新并注释
> git commit -m "注释"

###- 链接本地仓库与远程仓库
> git remote add origin URL

###- 更改本地仓库与远程仓库的链接
> git remote set-url origin URL

###- 创建分支,无分支名则为查看当前所有分支
> git branch **分支名**

###- 克隆远程仓库文件至本地仓库
> git clone URL

###- 切换分支
> git checkout **分支名**

###- 查看日志
> git log