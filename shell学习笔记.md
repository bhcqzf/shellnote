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