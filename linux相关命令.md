### linux 相关命令

#### 1.查看端口

###### （1）lsof

(list open files)是一个列出当前系统打开文件的工具。

lsof 查看端口占用语法格式：

```
lsof -i:端口号
```

实例：

查看服务器 8000 端口的占用情况：

```
# lsof -i:8000
COMMAND   PID USER   FD   TYPE   DEVICE SIZE/OFF NODE NAME
nodejs  26993 root   10u  IPv4 37999514      0t0  TCP *:8000 (LISTEN)
```

可以看到 8000 端口已经被轻 nodejs 服务占用。

lsof -i 需要 root 用户的权限来执行，如下图：

![image-20201220002630410](.\linux相关命令.assets\image-20201220002630410.png)

更多 lsof 的命令如下：

```
lsof -i:8080：查看8080端口占用
lsof abc.txt：显示开启文件abc.txt的进程
lsof -c abc：显示abc进程现在打开的文件
lsof -c -p 1234：列出进程号为1234的进程所打开的文件
lsof -g gid：显示归属gid的进程情况
lsof +d /usr/local/：显示目录下被进程开启的文件
lsof +D /usr/local/：同上，但是会搜索目录下的目录，时间较长
lsof -d 4：显示使用fd为4的进程
lsof -i -U：显示所有打开的端口和UNIX domain文件
```

###### （2）netstat

netstat -tunlp 用于显示 tcp，udp 的端口和进程等相关情况。

netstat 查看端口占用语法格式：

```
netstat -tunlp | grep 端口号
```

- -t (tcp) 仅显示tcp相关选项
- -u (udp)仅显示udp相关选项
- -n 拒绝显示别名，能显示数字的全部转化为数字
- -l 仅列出在Listen(监听)的服务状态
- -p 显示建立相关链接的程序名

例如查看 8000 端口的情况，使用以下命令：

```
# netstat -tunlp | grep 8000
tcp        0      0 0.0.0.0:8000            0.0.0.0:*               LISTEN      26993/nodejs   
```

更多命令：

```
netstat -ntlp   //查看当前所有tcp端口
netstat -ntulp | grep 80   //查看所有80端口使用情况
netstat -ntulp | grep 3306   //查看所有3306端口使用情况
```

netstat -nat  | grep '端口'

#### 2.文件上传下载

secureCRT alt+p start sftp

ls linux find files

lls local find files

cd linux cd dir

lcd local cd dir

put put local file to linux dir

get linux file from linux dir to local dir

#### 3.统计文件行数

wc -l fileName

#### 4.查看某个进程的线程情况

ps -ef | grep '进程名称等关键字'

top -H -p {pid}

#### 5.杀死某个进程

kill -9 pid

#### 6.修改jar包内配置文件

①查看文件所在路径

jar tvf jar包名称|grep {文件名称}

eg.  jar tvf test.jar |grep application.yml

②将文件解压

jar xvf jar包名称 目标文件名(上面查出来的全路径)

eg. jar xvf test.jar BOOT-INF/classes/application.yml

然后编辑文件

③将编辑好的文件替换原来的文件

jar uvf jar包名称 目标文件名（将新目标文件替换到jar包中）

eg. jar uvf test.jar BOOT-INF/classes/application.yml

#### 7.从远程服务器拷贝文件

scp remoteName@remoteIP:remotePath/文件名称 .

①拷贝一个文件到当前路径

scp dsadm@128.192.156.73:/home/ap/dsadm/file/20201201/test.dat .

②拷贝所有文件到当前路径

scp dsadm@128.192.156.73:/home/ap/dsadm/file/20201201/* .

③拷贝多个文件到当前路径

scp dsadm@128.192.156.73:/home/ap/dsadm/file/20201201/{test.dat,test1.dat...} .

#### 8.解压缩

tar

-c: 建立压缩档案
-x：解压
-t：查看内容
-r：向压缩归档文件末尾追加文件
-u：更新原压缩包中的文件

这五个是独立的命令，压缩解压都要用到其中一个，可以和别的命令连用但只能用其中一个。下面的参数是根据需要在压缩或解压档案时可选的。

-z：有gzip属性的
-j：有bz2属性的
-Z：有compress属性的
-v：显示所有过程
-O：将文件解开到标准输出

下面的参数-f是必须的
-f: 使用档案名字，切记，这个参数是最后一个参数，后面只能接档案名。

```
# tar -cf all.tar *.jpg 
这条命令是将所有.jpg的文件打成一个名为all.tar的包。-c是表示产生新的包，-f指定包的文件名。
# tar -rf all.tar *.gif 
这条命令是将所有.gif的文件增加到all.tar的包里面去。-r是表示增加文件的意思。
# tar -uf all.tar logo.gif 
这条命令是更新原来tar包all.tar中logo.gif文件，-u是表示更新文件的意思。
# tar -tf all.tar 
这条命令是列出all.tar包中所有文件，-t是列出文件的意思
# tar -xf all.tar 
这条命令是解出all.tar包中所有文件，-x是解开的意思
```

###### （1）压缩

```
tar –cvf jpg.tar *.jpg //将目录里所有jpg文件打包成tar.jpg

tar –czf jpg.tar.gz *.jpg   //将目录里所有jpg文件打包成jpg.tar后，并且将其用gzip压缩，生成一个gzip压缩过的包，命名为jpg.tar.gz

tar –cjf jpg.tar.bz2 *.jpg //将目录里所有jpg文件打包成jpg.tar后，并且将其用bzip2压缩，生成一个bzip2压缩过的包，命名为jpg.tar.bz2

tar –cZf jpg.tar.Z *.jpg   //将目录里所有jpg文件打包成jpg.tar后，并且将其用compress压缩，生成一个umcompress压缩过的包，命名为jpg.tar.Z

rar a jpg.rar *.jpg //rar格式的压缩，需要先下载rar for linux

zip jpg.zip *.jpg //zip格式的压缩，需要先下载zip for linux
```

###### （2）解压

```
tar –xvf file.tar //解压 tar包

tar -xzvf file.tar.gz //解压tar.gz

tar -xjvf file.tar.bz2   //解压 tar.bz2

tar –xZvf file.tar.Z   //解压tar.Z
unrar e file.rar //解压rar
unzip file.zip //解压zip
```

###### （3）总结

1、*.tar 用 tar –xvf 解压
2、*.gz 用 gzip -d或者gunzip 解压
3、*.tar.gz和*.tgz 用 tar –xzf 解压
4、*.bz2 用 bzip2 -d或者用bunzip2 解压
5、*.tar.bz2用tar –xjf 解压
6、*.Z 用 uncompress 解压
7、*.tar.Z 用tar –xZf 解压
8、*.rar 用 unrar e解压
9、*.zip 用 unzip 解压