---
title: maven常用命令
date: 2016-02-05 11:08:28
tags: maven
---
maven 打jar包：
```
mvn package
```
maven 清除项目:
```
mvn clean
```
maven 转eclipse项目:
```
mvn eclipse:eclipse
```
maven 转idea项目
```
mvn idea:idea
```
maven  拷贝依赖
```
mvn dependency:copy-dependencies
```
<!-- more -->
在maven项目下创建lib文件夹：
```
mvn dependency:copy-dependencies -DoutputDirectory=lib
```
mvn安装jar包到本地仓库
```
mvn install -Dfile=./target/yourjar.jar
-DgroupId=  
-DartifactId=
-Dversion=0.0.1-SNAPSHOT 
-Dpackaging=jar
```
mvn 下载jar包对应的源码
```
mvn dependency:sources
mvn dependency:resolve -Dclassifier=javadoc
#第一个命令是尝试下载在pom.xml中依赖的文件的源代码。
#第二个命令：是尝试下载对应的javadocs
```



mvn项目所需的pom文件查询地址：

> http://mvnrepository.com/
> http://search.maven.org


maven 打包时指定主类
```
  <build>
    <pluginManagement>
      <plugins>
        <!--这个plugin不要删除，为了屏蔽上层需要检查代码是否JAVA1.6，因为我们用了JAVA1.8-->
        <plugin>
          <groupId>org.codehaus.mojo</groupId>
          <artifactId>animal-sniffer-maven-plugin</artifactId>
          <version>${mvn.animal.sniffer.version}</version>
          <executions>
          </executions>
        </plugin>
      </plugins>
    </pluginManagement>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-jar-plugin</artifactId>
        <configuration>
          <archive>
            <manifest>
              <mainClass>主类</mainClass>
            </manifest>
          </archive>
        </configuration>
      </plugin>
    </plugins>
  </build>
```

使用maven编译scala https://github.com/nileader/note/wiki/using-maven-build-scala
sbt 参考 ： http://www.scala-sbt.org/release/tutorial/zh-cn/index.html
