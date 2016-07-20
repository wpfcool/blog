---
title: Red5流媒体服务器的安装与配置
date: 2016-05-05 18:10:21
tags: [red5,linux]
---
 

转载自:http://blog.csdn.net/aoshilang2249/article/details/50371870

1、  安装java

```
yum install java-1.7.0-openjdk  

``` 
</br>

2、 下载 red5-server-1.0.6-RELEASE-server.tar.gz 
[下载地址](https://github.com/Red5/red5-server/releases)
选择 选择red5-server-1.0.6-RELEASE-server.tar.gz，
解压到 /usr/local/red5 
</br>

3、 设置为可执行<br>  

```
cd /usr/local/red5  chmod +x *.sh  

```

4、 安装  </br> 

```
/red5.sh

```

5、 添加服务启动项
   
   a、 编辑启动脚本 <br> 
   
   ```
   vi /etc/init.d/red5`
   ```
   
```
#!/bin/bash 
# For RedHat and cousins:  
# chkconfig: 2345 85 85  
# description: Red5 flash streaming server  
# processname: red5  
# Created By: Sohail Riaz (sohaileo@gmail.com)  
  
PROG=red5  
RED5_HOME=/usr/local/red5  
DAEMON=$RED5_HOME/$PROG.sh  
PIDFILE=/var/run/$PROG.pid  
  
# Source function library  
. /etc/rc.d/init.d/functions  
  
[ -r /etc/sysconfig/red5 ] && . /etc/sysconfig/red5  
  
RETVAL=0  
  
case "$1" in  
start)  
echo -n $"Starting $PROG: "  
cd $RED5_HOME  
$DAEMON >/dev/null 2>/dev/null &  
RETVAL=$?  
if [ $RETVAL -eq 0 ]; then  
echo $! > $PIDFILE  
touch /var/lock/subsys/$PROG  
fi  
[ $RETVAL -eq 0 ] && success $"$PROG startup" || failure $"$PROG startup"  
echo  
;;  
stop)  
echo -n $"Shutting down $PROG: "  
killproc -p $PIDFILE  
RETVAL=$?  
echo  
[ $RETVAL -eq 0 ] && rm -f /var/lock/subsys/$PROG  
;;  
restart)  
$0 stop  
$0 start  
;;  
status)  
status $PROG -p $PIDFILE  
RETVAL=$?  
;;  
*)  
echo $"Usage: $0 {start|stop|restart|status}"  
RETVAL=1  
esac  
  
exit $RETVAL 

```
</br>
b、将启动脚本添加到服务

```
chmod +x /etc/rc.d/init.d/red5  
chkconfig --add red5  
chkconfig red5 on 

```  

c、 打开5080、1935等端口

d、 启动red5

```
/etc/init.d/red5 start

```