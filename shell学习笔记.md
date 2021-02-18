# 学习笔记

## 输入内容

命令：read 

例子：

```shell
read -p “Please input something :  ”   num 
```



## 序列

                                        命令：seq
例子：seq 10      一到十
          seq 1 10   开始 到结束
          seq 1 2 10开始 到结束 中间数为步长

```
[root@aliyun scripts]# seq -w 10
01
02
03
04
05
06
07
08
09
10
```

​          

等位补齐



# 忘记密码

## centos6

​                                        e 
在kernel 最后添加single 或 1 
b 重启

passwd
reboot
成功



## centos7

​                                        忘记密码‘

centos7   

linux16 最后添加 init=/bin/sh
ctrl+x  执行
重新挂载根目录
mount -o remount,rw /

passwd

touch /.autorebel

exec /sbin/init

# 基本命令

## 查看ip

ip a

ifconfig     yum -y install net-tools
hostname -I



## journalctl 

查看systemctl的日志

```
journalctl  -xe -u kubelet
```

-x   表示catalog    在日志旁显示简单注释  
-e   从后往前看  默认显示1000行
-u   指定进程
-f    持续输出结尾
-n   显示多少行   -n 200
-k   查看内核日志
--since 从一个时间戳开始 journalctl --since '2020-11-10 00:00:00'  也可以简写 today yesterday
tomorrow now
--until  到一个时间戳为止 journalctl --since '2020-11-10 00:00:00' --until '2020-11-10 00:00:05'
-p  按级别输出： 
\# 0: emerg
\# 1: alert
\# 2: crit
\# 3: err
\# 4: warning
\# 5: notice
\# 6: info
\# 7: debug

## ssh命令

命令：ssh

```
ssh $user@host
ssh bai@192.168.1.1 
```

密钥对远程登陆

生成秘钥命令：

```
ssh-keygen
```

拷贝秘钥命令：

```
ssh-copy-id
```

例子：

```
ssh-copy-id -i /home/alice/.ssh/id_rsa.pub alice@host                
#i可省略，ssh默认公钥在.ssh目录下
ssh-copy-id host
```

远程执行命令

```shell
ssh $ip          "echo '123425354'|passwd --stdin root"
ssh ip “命令”
```



PermitRootLogin yes  允许root用户登陆

\1. 打开 SSH 客户端。(了解操作方法 [使用 PuTTY 连接](https://docs.aws.amazon.com/console/ec2/instances/connect/putty))
\2. 找到您的私有密钥文件(555.pem)。向导会自动检测您用于启动实例的密钥。
\3. 您的密钥必须不公开可见，SSH 才能工作。如果需要，请使用此命令：chmod 400 555.pem
\4. 通过其 公有 DNS 连接到您的实例:ec2-18-191-194-154.us-east-2.compute.amazonaws.com
**示例：**ssh -i "555.pem" ubuntu@ec2-18-191-194-154.us-east-2.compute.amazonaws.com



ssh -t -t root@10.98.1.10 << remotessh
加两个-t -t 是为了强制打开一个窗口

remotessh

## 目录切换命令

### pwd显示当前目录

                                        命令：pwd
用处：显示当前所在文件夹
例子：

```
[root@aliyun baihai]# pwd
/root/baihai/baihai
#当前处于的文件夹
```

### cd切换目录

                                        命令：cd
用处：用于切换目录 change directory
例子：

```
[root@aliyun ~]# cd ~
[root@aliyun ~]# pwd
/root
```

cd~ 切换至当前用户home文件夹
cd-  切换至上一次处于的目录
cd.. 返回上一级目录
cd/  返回根目录



### ls显示当前目录文件

```
命令：ls 
```


用处：显示当前目录的文件 list
例子：

```
[root@aliyun ~]# ls
baihai  dead.letter  pac  scripts
#显示当前目录下的文件
```

```
[root@aliyun ~]# ls -a
.       .bai.swp       .bash_profile  .config      .lesshst  .pip              .python_history  .tcshrc
..      .bash_history  .bashrc        .cshrc       .local    .pki              scripts          .viminfo
baihai  .bash_logout   .cache         dead.letter  pac       .pydistutils.cfg  .ssh
#显示所有文件 包括隐藏的文件
```

```
[root@aliyun ~]# ls -l
total 16
drwxr-xr-x 5 root root 4096 Dec 13 22:45 baihai
-rw------- 1 root root   12 Jan  7 19:44 dead.letter
-rw-r--r-- 1 root root  180 Dec  4 17:16 pac
drwxr-xr-x 2 root root 4096 Jan  7 20:28 scripts
#显示文件全部属性 
#可用ll代替
```

```
[root@aliyun ~]# ls -t
scripts  dead.letter  baihai  pac
#按时间顺序排列
```

```
[root@aliyun ~]# ls -tr
pac  baihai  dead.letter  scripts
#加r，按时间顺序的倒叙排列

#按名称排序
ls -v
```

## 图形化界面

init 0 关机
init 3 命令行
init 5   startx      图形界面
init 6  重启
runlevel 运行等级
halt 关机 但不断电
poweroff  关机 断电
ctrl+alt+F1/F2/F3     切换终端
chvt 1                     切换终端

```
/etc/inittab   centos6

yum groupinstall "X Window System"

yum groupinstall "GNOME Desktop"
```

```
[centos7]
systemctl set-default multi-user.target
systemctl set-default graphical.target 
```

## motd欢迎界面

​                                        vim /etc/motd


                   _ooOoo_
                  o8888888o
                  88" . "88
                  (| -_- |)
                  O\  =  /O
               ____/`---'\____
             .'  \\|     |//  `.
            /  \\|||  :  |||//  \
           /  _||||| -:- |||||-  \
           |   | \\\  -  /// |   |
           | \_|  ''\---/''  |   |
           \  .-\__  `-`  ___/-. /
         ___`. .'  /--.--\  `. . __
      ."" '<  `.___\_<|>_/___.'  >'"".
     | | :  `- \`.;`\ _ /`;.`/ - ` : | |
     \  \ `-.   \_ __\ /__ _/   .-` /  /
======`-.____`-.___\_____/___.-`____.-'======
                   `=---='


^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
           佛祖保佑       永不死机
           心外无法       法外无心
           
           
           
           
           
           
/**
 *　　　　　　　 ┏┓       ┏┓+ +
 *　　　　　　　┏┛┻━━━━━━━┛┻┓ + +
 *　　　　　　　┃　　　　　　 ┃
 *　　　　　　　┃　　　━　　　┃ ++ + + +
 *　　　　　　 █████━█████    ┃+
 *　　　　　　　┃　　　　　　 ┃ +
 *　　　　　　　┃　　　┻　　　┃
 *　　　　　　　┃　　　　　　 ┃ + +
 *　　　　　　　┗━━┓　　　 ┏━┛
 \*                  ┃　　  ┃
 *　　　　　　　　　┃　　  ┃ + + + +
 *　　　　　　　　　┃　　　┃　Code is far away from     bug with the animal protecting
 *　　　　　　　　　┃　　　┃ + 　　　　         神兽保佑,代码无bug
 *　　　　　　　　　┃　　　┃
 *　　　　　　　　　┃　　　┃　　+
 *　　　　　　　　　┃　 　 ┗━━━┓ + +
 *　　　　　　　　　┃ 　　　　 ┣┓
 *　　　　　　　　　┃ 　　　　┏┛
 *　　　　　　　　　┗┓┓┏━━━┳┓┏┛ + + + +
 *　　　　　　　　　 ┃┫┫　 ┃┫┫
 *　　　　　　　　　 ┗┻┛　 ┗┻┛+ + + +
 */
/**
 \*                      江城子 . 程序员之殇
 *
 \*                  十年生死两茫茫，写程序，到天亮。
 \*                      千行代码，Bug何处藏。
 \*                  纵使上线又怎样，朝令改，夕断肠。
 *
 \*                  领导每天新想法，天天改，日日忙。
 \*                      相顾无言，惟有泪千行。
 \*                  每晚灯火阑珊处，夜难寐，加班狂。
*/





## 修改命令提示符

```
PS1='\e[36;40m\][\u@\h \w]\$ \e[0m'
```


修改命令提示符颜色


默认
[\u@\h \W]\$

## 查看内部命令

```
enable                                        
```

```
help
```

enable ls
启用内部命令


enable -n  ls
禁用内部命令

## 查看外部命令

```
which
```

which pwd
whereis 

## type判断命令

```
type help
#判断一个命令的类型
```

## file判断一个文件

```
file 1.txt
#判断一个文件
```

## 开关机

```
shutdown   +5  -h
#比较安全的关机    5分钟后关机

shutdown -c   
#取消关机


shutdown -r
#重启
```

## screen 多窗口命令

```
这个命令可以多个人同时查看同一窗口
创建会话
screen -S   name1

查看会话
screen -ls

进入会话
screen -r   name1

加入会话
screen -x name1

剥离会话
ctrl+a+d

退出会话
exit
```

## alias别名

```
alias bai=ls

alias la="ls -a"

unalias  la


#进入指定容器
alias kdmcse='run() { kubectl -n dmcs exec -it $1 /bin/bash;};run'
alias kdmzje='run() { kubectl -n dmzj exec -it $1 /bin/bash;};run'

这里定义了一个函数，让然后执行了函数      优点：可以在后面加参数
```

## sleep沉睡

```
sleep 10
sleep 100
sleep 1s 和sleep 1 都表示延迟1秒  
sleep 1m 表示延迟一分钟  
sleep 1h 表示延迟一小时  
sleep 1d 表示延迟一天    



usleep 按照微秒计算
usleep 1000000 表示延迟1000000微秒(即为1000ms，即为1s)

之前见过有些人用这个占位
比如if 之后什么也不做usleep
其实可以直接用:
```



