##### linux 相关命令

###### 1.查看端口

netstat -nat  | grep '端口'

###### 2.文件上传下载

secureCRT alt+p start sftp

ls linux find files

lls local find files

cd linux cd dir

lcd local cd dir

put put local file to linux dir

get linux file from linux dir to local dir

###### 3.统计文件行数

wc -l fileName

###### 4.查看某个进程的线程情况

ps -ef | grep '进程名称等关键字'

top -H -p {pid}

###### 5.杀死某个进程

kill -9 {pid}

###### 6.修改jar包内配置文件

①查看文件所在路径

jar tvf {jar包名称}|grep {文件名称}

eg.  jar tvf test.jar |grep application.yml

②将文件解压

jar xvf {jar包名称} 目标文件名(上面查出来的全路径)

eg. jar xvf test.jar BOOT-INF/classes/application.yml

然后编辑文件

③将编辑好的文件替换原来的文件

jar uvf {jar包名称} 目标文件名（将新目标文件替换到jar包中）

eg. jar uvf test.jar BOOT-INF/classes/application.yml