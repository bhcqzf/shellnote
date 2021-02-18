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

 e 
在kernel 最后添加single 或 1 
b 重启

passwd
reboot
成功



## centos7

忘记密码

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
           
           
           
           
           
           

```
/**

 *　　　　　　　 ┏┓       ┏┓+ +
 *　　　　　　　 ┏┛┻━━━━━━━┛┻┓ + +
 *　　　　　　　 ┃　　　　　　 ┃
 *　　　　　　　 ┃　　　━　　　┃ ++ + + +
 *　　　　　　　 █████━█████    ┃+
 *　　　　　　　 ┃　　　　　　 ┃ +
 *　　　　　　　 ┃　　　┻　　　┃
 *　　　　　　　 ┃　　　　　　 ┃ + +
 *　　　　　　　 ┗━━┓　　　 ┏━┛
 *             ┃　　  ┃
 *　　　　　　　 ┃　　  ┃ + + + +
 *　　　　　　　 ┃　　　┃　Code is far away from     bug with the animal protecting
 *　　　　　　　 ┃　　　┃ + 　　　　         神兽保佑,代码无bug
 *　　　　　　　 ┃　　　┃
 *　　　　　　　 ┃　　　┃　　+
 *　　　　　　　 ┃　 　 ┗━━━┓ + +
 *　　　　　　　 ┃ 　　　　 ┣┓
 *　　　　　　　 ┃ 　　　　┏┛
 *　　　　　　　 ┗┓┓┏━━━┳┓┏┛ + + + +
 *　　　　　　　 ┃┫┫　 ┃┫┫
 *　　　　　　　 ┗┻┛　 ┗┻┛+ + + +
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
```





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

## sleep睡眠

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



## 更改语言

```
LANG=zh_CN.utf8

LANG=en_US.utf8


文件位置
/etc/locale.conf
```

## wc统计

这个命令可以做各种统计，比如多少个单词，多少行

```
wc -l  统计多少行
wc -m 统计多少个字符   （注意：echo的话这里会把回车统计进来）建议使用echo -n
wc -c  按照字节统计
wc -w 按照单词统计
```

## 查看主机状态

### ip a查看ip

​                                        命令： ip a    ip addr
ifconfig
显示当前主机的ip地址
例子：

```
[root@aliyun baihai]# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 00:16:3e:06:81:fd brd ff:ff:ff:ff:ff:ff
    inet 172.17.106.226/20 brd 172.17.111.255 scope global dynamic eth0
       valid_lft 312131519sec preferred_lft 312131519sec
```


两个网路
第一个为环路
第二个为网卡
link/ether 后面是mac
inet 后面是ip地址 
brd 后面是广播地址


ip r 查看路由


切换网卡

```
dhclient -r eth0 移除网卡0

dhclient -v eth0 重新获取ip
```

### uname查看系统内核

命令：uname 
用处：查看系统内核，系统版本
例子：

```
[root@aliyun baihai]# uname -a
Linux aliyun 3.10.0-1062.4.1.el7.x86_64 #1 SMP Fri Oct 18 17:15:30 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
查看所有的结果
```

```
[root@aliyun baihai]# uname -r
3.10.0-1062.4.1.el7.x86_64
查看系统内核
```

uname -s        查看系统

uname -m       查看位



### 查看系统

```
[root@aliyun ~]# cat /etc/redhat-release 
CentOS Linux release 7.9.2009 (Core)

[root@aliyun ~]#  cat /etc/centos-release
CentOS Linux release 7.9.2009 (Core)

```

### uptime top命令第一行

                                        命令：uptime
用处：查看系统负载信息，用户，是否重启

我经常配合ansible一起用来查看系统负载

ansible xxx -a "uptime"

例子：

```
[root@aliyun baihai]# uptime
 10:23:01 up 37 days,  8:59,  1 user,  load average: 0.00, 0.01, 0.05
```

相当于top命令的第一行 
load average平均负载
分别是一分钟 五分钟 十五分钟的负载情况



### free查看系统的内存情况

命令：free                 

cat /proc/meminfo        #这个会更详细的显示内存使用情况

用处：用于查看主机当前的内存情况
例子：

```
[root@aliyun baihai]# free 
              total        used        free      shared  buff/cache   available
Mem:        1882088      114572     1046516         428      721000     1593380
Swap:             0           0           0
Mem为内存 swap为交换内存
```

```
[root@aliyun baihai]# free -m
              total        used        free      shared  buff/cache   available
Mem:           1837         111        1021           0         704        1556
Swap:             0           0           0
后面加选项-m意思为用Mb为单位显示
```

```
[root@aliyun baihai]# free -h
              total        used        free      shared  buff/cache   available
Mem:           1.8G        111M        1.0G        428K        704M        1.5G
Swap:            0B          0B          0B
-h表示便于人来查看
```

#### 创建一个swap交换分区

                                        用文件作为Swap分区
1.创建要作为swap分区的文件:增加1GB大小的交换分区，则命令写法如下，其中的count等于想要的块的数量（bs*count=文件大小）。
\# dd if=/dev/zero of=/root/swapfile bs=1M count=1024
2.格式化为交换分区文件:
\# mkswap /root/swapfile #建立swap的文件系统
3.启用交换分区文件:
\# swapon /root/swapfile #启用swap文件
4.使系统开机时自启用，在文件/etc/fstab中添加一行：
/root/swapfile swap swap defaults 0 0



#### 剩余内存过少时

sync;
Linux sync命令用于数据同步,sync命令是在关闭Linux系统时使用的。
Linux 系统中欲写入硬盘的资料有的时候为了效率起见，会写到 filesystem buffer 中，这个 buffer 是一块记忆体空间，如果欲写入硬盘的资料存于此 buffer 中，而系统又突然断电的话，那么资料就会流失了，sync 指令会将存于 buffer 中的资料强制写入硬盘中。

```
echo 3 > /proc/sys/vm/drop_caches
释放掉被系统Cache占用的数据命令
```

### history 历史记录

命令：history
用处：显示历史命令
例子：

```
history

history -c 清除历史命令
history -w 将当前的命令添加到history文件中

!加数字 例如 !1为调用第一条命令
!! 为调用上一条命令
!加字符串 为调用最近以及以字符串开头的命令

ctrl + r 可以有搜索历史命令的功能
```

```
让history显示时间
HISTTIMEFORMAT="`whoami` @ %F %T @"
HISTSIZE=2000

histoty
最多记录一千条

[root@instance-1 ~]# echo $HISTSIZE
1000

在/etc/profile中可以改
```



### 查看内核

​                                        
uname -r

```
[root@localhost ~]# awk -F\' '$1=="menuentry " {print i++ " : " $2}' /etc/grub2.cfg
0 : CentOS Linux (3.10.0-1062.el7.x86_64) 7 (Core)
1 : CentOS Linux (0-rescue-7c4dfa6f2408467ea4d83073358d1cc0) 7 (Core)
```

```
grub2-editenv list  查看当前内核
cat /boot/grub2/grub.cfg |grep "menuentry " 第二种方式

grub2-set-default 1**     设置内核
grub2-set-default 'CentOS Linux (3.10.0-327.el7.x86_64) 7 (Core)' 设置内核两种方式
```

### 查看服务

```
cat /etc/services
```



### lscpu查看cpu

```
[root@localhost ~]# lscpu
Architecture:          x86_64
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian
CPU(s):                1
On-line CPU(s) list:   0
Thread(s) per core:    1
Core(s) per socket:    1
Socket(s):             1
NUMA node(s):          1
Vendor ID:             GenuineIntel
CPU family:            6
Model:                 69
Model name:            Intel(R) Core(TM) i5-4258U CPU @ 2.40GHz
Stepping:              1
CPU MHz:               2394.461
BogoMIPS:              4788.92
Hypervisor vendor:     VMware
Virtualization type:   full
L1d cache:             32K
L1i cache:             32K
L2 cache:              256K
L3 cache:              3072K
NUMA node0 CPU(s):     0
Flags:                 fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss syscall nx pdpe1gb rdtscp lm constant_tsc arch_perfmon nopl xtopology tsc_reliable nonstop_tsc eagerfpu pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand hypervisor lahf_lm abm ssbd ibrs ibpb stibp fsgsbase tsc_adjust bmi1 avx2 smep bmi2 invpcid xsaveopt arat spec_ctrl intel_stibp flush_l1d arch_capabilities

```



### lsblk查看硬盘块

```
[root@aliyun ~]# lsblk
NAME   MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
vda    253:0    0  40G  0 disk 
└─vda1 253:1    0  40G  0 part /

```

### df查看硬盘状态

```
df -h

df -i显示节点编号  就是inode
```



### du查看文件大小

```
du -sh 查看当前整个目录的大小

du   查看某个文件的大小
```

### vmstat查看虚拟机状态

```
[root@wcUItf237757 ~]# vmstat
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 3  0 415736  64556    356 174256    0    0   950     4    3    1  0  1 99  0  0

cpu区域
us       user CPU time
sy       system CPU time
id        idle
wa      iowait
st      steal time
```

## 文本打印

### echo回声

命令：echo
解释：回声，回响
选项：
         -E (默认)不启动\解释功能
         -e  启用反斜杠转义
         -n 段落最后不追加换行符

```
echo加颜色
\e[1;32                              \e[0m
```



```
\#字体颜色：30m-37m 黑、红、绿、黄、蓝、紫、青、白
str="kimbo zhang"
echo -e "\033[30m ${str}\033[0m"      ## 黑色字体
echo -e "\033[31m ${str}\033[0m"      ## 红色
echo -e "\033[32m ${str}\033[0m"      ## 绿色
echo -e "\033[33m ${str}\033[0m"      ## 黄色
echo -e "\033[34m ${str}\033[0m"      ## 蓝色
echo -e "\033[35m ${str}\033[0m"      ## 紫色
echo -e "\033[36m ${str}\033[0m"      ## 青色
echo -e "\033[37m ${str}\033[0m"      ## 白色
```



解决echo之后换行变为空格
echo “$num”



```
\a  发出警报声
echo -e "\a"

\b 退格键
echo -e “abc\bdd”

\c 不换行
echo -e ‘efewf\c’

\n 换行
echo -e ‘abc\n’

\r 回车
echo -e ‘ddd\r’

\t tab键
echo -e ‘a\tb’
```



### printf带格式打印

```
printf   "%-d * %-d = %-2d " $i $j $jieguo
printf “%-s\t%-s”  
```



```
#!/usr/bin/bash
#jiujiuchengfabiao
for j in {1..9}
do
        for i in `seq 1 $j   `
        do
                jieguo=$[$i*$j]
                printf   "%-d * %-d = %-2d " $i $j $jieguo
        done
        echo
done
```

九九乘法表

```
1 * 1 = 1  
1 * 2 = 2  2 * 2 = 4  
1 * 3 = 3  2 * 3 = 6  3 * 3 = 9  
1 * 4 = 4  2 * 4 = 8  3 * 4 = 12 4 * 4 = 16 
1 * 5 = 5  2 * 5 = 10 3 * 5 = 15 4 * 5 = 20 5 * 5 = 25 
1 * 6 = 6  2 * 6 = 12 3 * 6 = 18 4 * 6 = 24 5 * 6 = 30 6 * 6 = 36 
1 * 7 = 7  2 * 7 = 14 3 * 7 = 21 4 * 7 = 28 5 * 7 = 35 6 * 7 = 42 7 * 7 = 49 
1 * 8 = 8  2 * 8 = 16 3 * 8 = 24 4 * 8 = 32 5 * 8 = 40 6 * 8 = 48 7 * 8 = 56 8 * 8 = 64 
1 * 9 = 9  2 * 9 = 18 3 * 9 = 27 4 * 9 = 36 5 * 9 = 45 6 * 9 = 54 7 * 9 = 63 8 * 9 = 72 9 * 9 = 81 

```



## 帮助

### whatis

会显示一句简单的介绍

```
[root@ali ~]# whatis ls
ls (1)               - list directory contents

[root@ali ~]# whatis cd
cd (1)               - bash built-in commands, see bash(1)
cd (n)               - Change working directory

makewhatis   生成缓存 （centos6）
mandb           (centos7）
```

### help

查看帮助

```
help
查看帮助
```

### man手册

```
配合whatis可以查看在man手册的第几章


[root@aliyun ~]# whatis ls
ls (1)               - list directory contents
[root@aliyun ~]# man 1 ls


中文包
man-pages-zh-CN
```





### info命令

```
和man相似

但是不常用
```



## 网络网卡

```
vim /etc/sysconfig/network-scripts/ifcfg-ens33

编辑网卡设置
把onboot打开

获取ip
dhclient -v ens33       获取
 
释放ip
dhclient -r ens33
```



## 快捷键

### vim快捷键

```
:set list 显示空格，换行
:set nolist 取消显示空格
:set number 显示行号
:set nonumber 取消显示行号
:wq 保存并退出
:q 退出
:q! 强制退出
^ 到行开头
$ 到行结尾
G 到段结尾
gg 到段开头
i 在光标前插入
a 在光标后插入
dd 删除某行
d $ 删除光标后所有
daw 删除当前单词
dw 删除当前字符到单词结束


y 复制某行
p 粘贴
① 在编辑模式下输入
ngg 或者 nG
n为指定的行数(如25)
例如：25gg或者25G 跳转到第25行.
②在命令模式下输入行号n
: n
③如果想打开文件即跳转
vim +n FileName

vim /etc/passwd   +50
跳转到第50行

^f 向上翻
^b 向下翻
^n  自动补全


```

### trap

```
命令：trap
解释：防止中止，尤其是用户用快捷键，挂起，中止，退出进程
```





### bash快捷键

```
光标移动：ctrl+a 光标移动到开头
               ctrl+e 光标移动到结尾
文本编辑：ctrl+u 删除光标之前的所有字符
               ctrl+k 删除光标之后的所有字符
               ctrl+y 撤销刚才的操作
重复上个命令：
                    !!
调用历史命令：
                !100
                !-4         调用倒数第四条命令
                !:0         调用上一个命令 不加参数
                !system   调用以     开头
                !?system  调用包含      的命令           
                !system:p   打印以     开头的命令
                !$              上一个命令最后一个参数
                !*              上一个命令的所有参数
搜索历史:
            ctrl+r
            退出 ctrl+g
交换字符：
            ctrl+t 
            [root@ali ~]# ls -a
            [root@ali ~]# ls a-

```



### clear清空屏幕

```
快捷键：ctrl+l
命令：clear
```

## 时间命令

### date时间

```
更改时区

mv /etc/localtime /etc/localtime.bak
ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

同步时间
yum -y install ntp ntpdate
ntpdate cn.pool.ntp.org

ntpdate 192.168.123.222
和另外一台服务器同步时间


手动修改时间
date -s "20170402 19:00:00"

打一个时间戳 
date +"%Y%m%d%H%M%S
```

### cal日历

```
cal

cal 2018

cal 5 2019

cal 9 1752
```



### clock硬件时间

```
[root@ali ~]# clock
Tue 21 Apr 2020 07:55:09 AM CST  -0.343020 seconds

```

## $关键字

```
shell 脚本中$$,$#,$?分别代表什么意思?
给你个全的，你在Linux环境下多试下就明白了：
$0 这个程式的执行名字
$n 这个程式的第n个参数值，n=1..9
$* 这个程式的所有参数,此选项参数可超过9个。
$# 这个程式的参数个数
$$ 这个程式的PID(脚本运行的当前进程ID号)
$! 执行上一个背景指令的PID(后台运行的最后一个进程的进程ID号)
$? 执行上一个指令的返回值 (显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误)
$- 显示shell使用的当前选项，与set命令功能相同
$@ 跟$*类似，但是可以当作数组用
```

## curl功能强大的命令行浏览器

```
功能强大的网页浏览器
-s  安静的输出
-o  下载/输出的位置
-v  版本信息
-I  查看头部信息
-O  按照原文件名下载文件
-o   按照新名字保存文件    curl -o bai.txt  http://bai.com/bai.xx   
-C -  恢复下载   具体语法是    横杠 大写C 横杠
例子：curl -O http://yourdomain.com/yourfile.tar.gz  下载时^c    
恢复中断的下载  curl -C - -O http://yourdomain.com/yourfile.tar.gz

下载多个文件：
curl -O http://yoursite.com/info.html -O http://mysite.com/about.html 

使用代理:
curl -x proxy.yourdomain.com:8080 -U user:password -O http://yourdomain.com/yourfile.tar.gz

post请求
curl --data "firstName=John&lastName=Doe" https://yourdomain.com/info.php

ftp下载
curl -u username:password -O ftp://yourftpserver/yourfile.tar.gz 

自定义user-agent：
curl -I http://localhost --user-agent "I am a new web browser"

保存cookie：
curl --cookie-jar cnncookies.txt https://www.cnn.com/index.html -O

发送cookie
curl --cookie cnncookies.txt https://www.cnn.com

设置解析服务器
curl --resolve www.yourdomain.com:80:localhost http://www.yourdomain.com/

设置下载速度
curl --limit-rate 100K http://yourdomain.com/yourfile.tar.gz -O

获得状态码
curl  -s http://www.gjj12329.cn:32204/dm-app/index.html -o /dev/null -w %{http_code}

 
```

## xargs

```
-n参数  可以使原本一行的文本   变成多行

[root@144 ~]# xargs  echo <test
11111111111111111111 22222222222222222222222222222 333333333333333333333333333333


[root@144 ~]# xargs -n1  echo <test
11111111111111111111
22222222222222222222222222222
333333333333333333333333333333

```

