# [maven](http://maven.apache.org/)
##- 构建WEB项目命令
> mvn archetype:generate -DgroupId=**项目结构** -DartifactId=**项目名** -DarchetypeArtifactId=maven-archetype-webapp

##- 当maven无法获取catalog时,加入此参数使maven不在远程服务器获取该文件
> -DarchetypeCatalog=internal