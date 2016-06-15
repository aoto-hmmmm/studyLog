# [maven](http://maven.apache.org/)
##- 构建WEB项目命令
> mvn archetype:generate -DgroupId=**项目结构** -DartifactId=**项目名** -DarchetypeArtifactId=maven-archetype-webapp

##- 当maven无法获取catalog时,加入此参数使maven不在远程服务器获取该文件
> -DarchetypeCatalog=internal

##- 某些jar包无法通过xml搜索maven库自动添加解决(比如ojdbc14),此时需手动下载相关jar包并添加至本地maven库解决依赖
> mvn install:install-file -DgroupId=**jar包结构** -DartifactId=**jar包名** -Dversion=**版本号** -Dpackaging=jar -Dfile=**本地jar包路径**