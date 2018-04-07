---
title: linux中常用的一些命令
date: 2016-01-02 21:26:36
tags: linux
---

tshark抓包
```
sudo tshark -s 512 -i eth0 -n -f 'tcp dst port 80' -R 'http.host and http.request.uri' -T fields -e http.host -e http.request.uri -l | tr -d '\t'
```

查看CPU的型号
```
cat /proc/cpuinfo | grep name | cut -f2 -d: |uniq -c
```
查看CPU 几核几线程
```
grep 'processor' /proc/cpuinfo |sort -u |wc -l
grep 'core id' /proc/cpuinfo ｜sort -u |wc -l
```

<!-- more -->
以人性化的展示文件大小
```shell
du -h file
```

文本按照列进行合并
```shell
 paste -d" " file1 file2 >> newFile
```
查看端口被哪个进程占用 以80端口为例:
```
sudo lsof -i: 80
```
端口扫描：
```
nmap ip
```

删除txt文本中的第一列的命令：
```
 sed -i -r -e "s/^[[:space:]]+//" -e "s/^[^[:space:]]+[[:space:]]+//" *.txt
```
#### 把log.txt中的前600行追加到log1.txt中去 
```
sed -n '1,600 p' log.txt > log1.txt
```
#### 查看文件的编码：
```
enca -L zh filename.java
```
#### 解压/压缩 命令：
##### 后缀为gz:
```
解压：gzip -d FileName.gz
压缩：gzip FileName
```
##### 后缀为.tar.gz
```
解压：tar zxvf FileName.tar.gz
压缩：tar zcvf FileName.tar.gz 
```
#### 压缩为zip 
```
zip -r myfile.zip myfile/*
```
##### 后缀为.bz2
```
解压：bzip2 -d fleName.bz2
压缩： bzip2 -z fileName
```
##### 后缀为.rar
```
解压：rar a FileName.rar
压缩：r ar e FileName.rar
```
##### 后缀为.tgz
```
解压：tar zxvf FileName.tgz
```
linux 查看外网ip
```
curl ifconfig.me
curl http://members.3322.org/dyndns/getip
```
#### 在控制台打开某个文件窗口
```
nautilus /home/***


```

#### 输出某一列 
```
cat ××.txt |awk '{print $1}' >> out.txt 
```
#### 循环读取文件夹中的文件并保存为新的文件
```
for file in *
do
	if test -f $file
	then
		#echo $file is file!
		cat $file |awk '{print $2}' >'N'$file
	else
		echo $file is mulu!
	fi
done
```
windows文件拷贝到linux乱码时 指定编码
```
 iconv -f GBK -t UTF-8 file1 -o file2
```
批量转码shell
```
#!/bin/sh
for i in *
do
iconv -f gb2312 -t utf-8 $i >tmp
cp tmp $i
done
```

文本去空格
```
sed s/[[:space:]]//g
```

文本文件内容洗牌
```
cat in.txt | awk 'BEGIN{srand()}{print rand()"\t"$0}' | sort -k1,1 -n | cut -f2- > out.txt
```
去引号
```
sed 's/"//g'
tr -d '"'
```

```
 awk -F ','  '{print $14,$15}' cup14w15w >> newcup
 tr -d \" < file 
 cut -d\" -f2  file
```

```
cat tag3 | awk '{if($0 ~ /ag/) print " "; else print "C"$0+1 }' >> tag5
~ /ag/ 模糊匹配
```
shell中一行变一列
```
 cat inputFile |tr "\n" " "

```
    1.检查远程端口是否对bash开放：
```
echo >/dev/tcp/8.8.8.8/53 && echo "open"
```
    2.让进程转入后台：
```
Ctrl + z
```
     3、将进程转到前台：
```
fg
```
    4.产生随机的十六进制数，其中n是字符数：
```
openssl rand -hex n
```
    5.在当前shell里执行一个文件里的命令：
```
source /home/user/file.name
```
    6.截取前5个字符：
```
${variable:0:5}
```
    7.SSH debug 模式:
```
ssh -vvv user@ip_address
```
    8.SSH with pem key:
```
ssh user@ip_address -i key.pem
```
    9.用wget抓取完整的网站目录结构，存放到本地目录中：
```
wget -r --no-parent --reject "index.html*" http://hostname/ -P /home/user/dirs
```
    10.一次创建多个目录：
```
mkdir -p /home/user/{test,test1,test2}
```
    11.列出包括子进程的进程树：
```
ps axwef
```
    12.创建 war 文件:
```
jar -cvf name.war file
```
    13.测试硬盘写入速度：
```
dd if=/dev/zero of=/tmp/output.img bs=8k count=256k; rm -rf /tmp/output.img
```
    14.测试硬盘读取速度：
```
hdparm -Tt /dev/sda
```
    15.获取文本的md5 hash：
```
echo -n "text" | md5sum
```
    16.检查xml格式：
```
xmllint --noout file.xml
```
    17.将tar.gz提取到新目录里：
```
 zxvf package.tar.gz -C new_dir
```
    18.使用curl获取HTTP头信息：
```
curl -I http://www.example.com
```
    19.修改文件或目录的时间戳(YYMMDDhhmm):
```
touch -t 0712250000 file
```
    20.用wget命令执行ftp下载：
```
wget -m ftp://username:password@hostname
```
    21.生成随机密码(例子里是16个字符长):
```
LANG=c < /dev/urandom tr -dc _A-Z-a-z-0-9 | head -c${1:-16};echo;
```
    22.快速备份一个文件：
```
cp some_file_name{,.bkp}
```
    23.访问Windows共享目录：
```
smbclient -U "DOMAIN\user" //dc.domain.com/share/test/dir
```
    24.执行历史记录里的命令(这里是第100行):
```
!100
```
    25.解压:
```
unzip package_name.zip -d dir_name
```
    26.输入多行文字(CTRL + d 退出):
```
cat > test.txt
```
    27.创建空文件或清空一个现有文件：
```
\> test.txt
```
    28.与Ubuntu NTP server同步时间：
```
ntpdate ntp.ubuntu.com
```
    29.用netstat显示所有tcp4监听端口：
```
netstat -lnt4 | awk '{print $4}' | cut -f2 -d: | grep -o '[0-9]*'
```
    30.qcow2镜像文件转换：
```
qemu-img convert -f qcow2 -O raw precise-server-cloudimg-amd64-disk1.img \precise-server-cloudimg-amd64-disk1.raw
```
    31.重复运行文件，显示其输出（缺省是2秒一次）：
```
watch ps -ef
```
    32.所有用户列表：
```
getent passwd
```
    33.Mount root in read/write mode:
```
mount -o remount,rw /
```
    34.挂载一个目录（这是不能使用链接的情况）:
```
mount --bind /source /destination
```
    35.动态更新DNS server:
```
nsupdate < <EOF
update add $HOST 86400 A $IP
send
EOF
```
    36.递归grep所有目录：
```
grep -r "some_text" /path/to/dir
```
    37.列出前10个最大的文件：
```
lsof / | awk '{ if($7 > 1048576) print $7/1048576 "MB "$9 }' | sort -n -u | tail
```
    38.显示剩余内存(MB):
```
free -m | grep cache | awk '/[0-9]/{ print $4" MB" }'
```
    39.打开Vim并跳到文件末：
```
vim + some_file_name
```
    40.Git 克隆指定分支(master):
```
git clone git@github.com:name/app.git -b master
```
    41.Git 切换到其它分支(develop):
```
git checkout develop
```
    42.Git 删除分支(myfeature):
```
git branch -d myfeature
```
    43.Git 删除远程分支
```
git push origin :branchName
```
    44.Git 将新分支推送到远程服务器：
```
git push -u origin mynewfeature
```
    45.打印历史记录中最后一次cat命令：
```
!cat:p
```
    46.运行历史记录里最后一次cat命令：
```
!cat
```
    47.找出/home/user下所有空子目录:
```
find /home/user -maxdepth 1 -type d -empty
```
    48.获取test.txt文件中第50-60行内容：
```
< test.txt sed -n '50,60p'
```
    49.运行最后一个命令(如果最后一个命令是mkdir /root/test, 下面将会运行: sudo mkdir /root/test)：
```
sudo !!
```
    50.创建临时RAM文件系统 – ramdisk (先创建/tmpram目录):
```
mount -t tmpfs tmpfs /tmpram -o size=512m
```
    51.Grep whole words:
```
grep -w "name" test.txt
```
    52.在需要提升权限的情况下往一个文件里追加文本：
```
echo "some text" | sudo tee -a /path/file
```
    53.列出所有kill signal参数:
```
kill -l
```
    54.在bash历史记录里禁止记录最后一次会话：
```
kill -9 $$
```
    55.扫描网络寻找开放的端口：
```
nmap -p 8081 172.20.0.0/16

```
     56.设置git email:
```
git config --global user.email "me@example.com"
```
    57.To sync with master if you have unpublished commits:
```
git pull --rebase origin master
```
    58.将所有文件名中含有”txt”的文件移入/home/user目录:
```
find -iname "*txt*" -exec mv -v {} /home/user \;
```
    59.将文件按行并列显示：
```
paste test.txt test1.txt
```
    60.shell里的进度条:
```
pv data.log
```
    61.使用netcat将数据发送到Graphite server:
```
echo "hosts.sampleHost 10 `date +%s`" | nc 192.168.200.2 3000
```
    62.将tabs转换成空格：
```
expand test.txt > test1.txt
```
    63.Skip bash history:
```
< space >cmd
```
    64.去之前的工作目录：
```
cd -
```
    65.拆分大体积的tar.gz文件(每个100MB)，然后合并回去：
```
split –b 100m /path/to/large/archive /path/to/output/files
cat files* > archive
```
    66.使用curl获取HTTP status code:
```
curl -sL -w "%{http_code}\\n" www.example.com -o /dev/null
```
    67.设置root密码，强化MySQL安全安装:
```
/usr/bin/mysql_secure_installation
```
    68.当Ctrl + c不好使时:
```
Ctrl + \
```
    69.获取文件owner:
```
stat -c %U file.txt
```
    70.block设备列表：
```
lsblk -f
```
    71.找出文件名结尾有空格的文件：
```
find . -type f -exec egrep -l " +$" {} \;
```
    72.找出文件名有tab缩进符的文件
```
find . -type f -exec egrep -l $'\t' {} \;
```
    73.用”=”打印出横线:全选复制放进笔记
```
printf '%100s\n' | tr ' ' =

```

   
### 参考文献
[1] http://www.techbar.me/linux-shell-tips/
[2] http://linuxtools-rst.readthedocs.io/zh_CN/latest/base/index.html
[3] http://man.linuxde.net/tee
