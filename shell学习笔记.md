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

