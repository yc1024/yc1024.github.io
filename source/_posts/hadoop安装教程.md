---
title: hadoop安装教程
date: 2018-04-05 13:32:04
tags: hadoop
---


### 预备工作
- 硬件准备

 假设已经有3台机器组成的局域网，并且是可以相互ping通的

- 软件准备

需要准备jdk-1.8的安装包和hadoop的安装包
在每台机器上安装 vim、ssh
```
以ubuntu为例
sudo apt-get install vim
sudo apt-get install openssh-server
```


### 设置ssh免秘钥登陆
在三台机器分别执行如下命令
```
ssh-keygen -t rsa  // 连续敲三次回车就好
cd ~/.ssh/ && touch authorized_keys && chmod 600  authorized_keys // 创建出 authorized_keys文件，并且讲权限置为600
cat id_rsa.pub >> authorized_keys //将公钥追加到authorized_keys文件中
```
到目前为止，应该是每台机器可以免密码登录自己的机器了
<!-- more -->
登录机器2，把机器2上的公钥传给机器1
```
其中 hdusr为用户名 1307-01为ip（可在/etc/hosts中配置）
scp ~/.ssh/id_rsa.pub hdusr@1307-01:/home/hdusr/.ssh/02
```
同理登录机器3，把机器3上的公钥传给机器1
```
 scp ~/.ssh/id_rsa.pub hdusr@1307-01:/home/hdusr/.ssh/03
```
把02机器和03机器的公钥加入01机器中，然后把01中的`authorized_keys` 复制到02机器和03机器覆盖掉原有的`authorized_keys`
```
cat 02 03 >>  authorized_keys
scp /home/hdusr/.ssh/authorized_keys hdusr@1307-02:/home/hdusr/.ssh/authorized_keys
scp /home/hdusr/.ssh/authorized_keys hdusr@1307-03:/home/hdusr/.ssh/authorized_keys
```
到现在为止就可以开心的互相链接不用密码了
顺手记录一下1307实验室集群中的一个坑，不知道哪个坑把用户的权限改成了777，然后ssh怎么都需要密码，差点把电脑拆了，在打算重装的前一刻发现了这个问题。

### 安装java hadoop
```
安装Java
tar -zxvf jdk1.8.0_05-linux-x64.tar.gz(你的jdk的安装包)
sudo vim /etc/profile
编辑环境变量，加入如下的配置其中 `/opt/software/jdk1.8.0_05` 应该替换为你解压jdk的路径
export JAVA_HOME=/opt/software/jdk1.8.0_05
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$JAVA_HOME/bin:$PATH
完事之后 java -version 瞅一眼，看看是不是装上java了
```


```
hadoop也一样也是一阵解压
export HADOOP_HOME=/opt/software/hadoop-2.7.2
export PATH=$PATH:$HADOOP_HOME/bin
```

### 遇到的坑
1. 一定要注意文件的用户，文件的用户必须是自己的hadoop的用户，否则会出问题
2. /etc/hosts 一定要配好最好只留下三台机器和对应的名字，别的都可以删除
3. 在配置好ssh无秘钥登录以后记要互相登一下校验一下
4. 参考文项中的某些路径有问题

比如我配置第一个节点是　master,但是他叫namenode,然后配置的时候遇到坑，不能自拔 

### 参考文献

http://blog.csdn.net/zl007700/article/details/50533675
http://blog.csdn.net/zcf1002797280/article/details/49500027



### 为了不留坑，做了更详细的压缩
 建议hadoop和java都解压到/opt目录下：
```
sudo tar -zxvf hadoop-2.5.1.tar.gz -C /opt
cd /opt && sudo chown -R hdusr:hdusr hadoop-2.5.1/
//这里的hdusr表示你的用户名
cd /opt/hadoop-2.5.1/ && mkdir tmp && mkdir -p dfs/data dfs/name 
```
```
cd /opt/software/hadoop-2.5.1/etc/hadoop/
配置文件都在这个路径下，照着改
```
core-site.xml
```
<configuration>
<property>
        <name>fs.defaultFS</name>
        <value>hdfs://master:9000</value>
    </property>
    <property>
        <name>hadoop.tmp.dir</name>
        <value>/opt/hadoop-2.5.1/tmp</value>
    </property>
    <property>
        <name>io.file.buffer.size</name>
        <value>131702</value>
    </property>
</configuration>

```
```
hdfs-site.xml
```
```
<configuration>
<property>
        <name>dfs.namenode.name.dir</name>
        <value>/opt/hadoop-2.5.1/dfs/name</value>
    </property>
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>/opt/hadoop-2.5.1/dfs/data</value>
    </property>
    <property>
        <name>dfs.replication</name>
        <value>2</value>
    </property>
    <property>
        <name>dfs.namenode.secondary.http-address</name>
        <value>master:9001</value>
    </property>
    <property>
        <name>dfs.webhdfs.enabled</name>
        <value>true</value>
    </property>
</configuration>

```

```
cp /opt/hadoop-2.5.1/etc/hadoop/mapred-site.xml.template /opt/hadoop-2.5.1/etc/hadoop/mapred-site.xml
vim /opt/hadoop-2.5.1/etc/hadoop/mapred-site.xml
```
```
<configuration>
<property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
    <property>
        <name>mapreduce.jobhistory.address</name>
        <value>master:10020</value>
    </property>
    <property>
        <name>mapreduce.jobhistory.webapp.address</name>
        <value>master:19888</value>
    </property>
</configuration>
                  
```

```
yarn-site.xml
```
```
<configuration>
<property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
    <property>
        <name>yarn.nodemanager.auxservices.mapreduce.shuffle.class</name>
        <value>org.apache.hadoop.mapred.ShuffleHandler</value>
    </property>
    <property>
        <name>yarn.resourcemanager.address</name>
        <value>master:8032</value>
    </property>
    <property>
        <name>yarn.resourcemanager.scheduler.address</name>
        <value>master:8030</value>
    </property>
    <property>
        <name>yarn.resourcemanager.resource-tracker.address</name>
        <value>master:8031</value>
    </property>
    <property>
        <name>yarn.resourcemanager.admin.address</name>
        <value>master:8033</value>
    </property>
    <property>
        <name>yarn.resourcemanager.webapp.address</name>
        <value>master:8088</value>
    </property>
    <property>
        <name>yarn.nodemanager.resource.memory-mb</name>
        <value>768</value>
    </property>
</configuration>

```
```
slaves
```

```
slave1 //host里配置
slave2
```
贴一份我的host，ip替换为你自己的（/etc/hosts）
```
192.168.0.101 master
192.168.0.103 slave1
192.168.0.104 slave2
```

我的环境变量（在/etc/profile中加入下面的）
```
export JAVA_HOME=/opt/jdk1.8.0_05
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
export PATH=$JAVA_HOME/bin:$PATH

export HADOOP_HOME=/opt/hadoop-2.5.1
export PATH=$PATH:$HADOOP_HOME/bin
```
