# Redis安装-Linux

## **1.** **Redis官网**

官网 https://redis.io/download

## **2.** **下载**

wget http://download.redis.io/releases/redis-6.0.8.tar.gz

![img](image\wps58B2.tmp.jpg) 

## **3.** **解压**

tar -zxvf redis-6.0.8.tar.gz -C /opt/java/software

![img](image\wps58C2.tmp.jpg) 

## **4.** **编译**

在解压目录 /opt/java/software/redis-6.0.8

![img](image\wps58C3.tmp.jpg) 

## **5.** **安装**

创建目录

mkdir -p /usr/local/redis

![img](image\wps58D4.tmp.jpg) 

安装

make install PREFIX=/usr/local/redis

## **6.** **复制配置文件**

cp /opt/java/software/redis-6.0.8/redis.conf  /usr/local/redis/bin

![img](image\wps58E5.tmp.jpg) 

## **7.** **文件配置**

vim /usr/local/redis/bin/redis.conf

默认绑定的是回环地址，默认不能被其他机器访问

![img](image\wps5905.tmp.jpg) 

启动方式修改为守护进程（后台线程启动模式）

![img](image\wps5915.tmp.jpg) 

密码设置

![img](image\wps5916.tmp.jpg) 

## **8.** **环境配置**

\# redis 环境变量配置

export REDIS_HOME=/usr/local/redis

export PATH=$PATH:$REDIS_HOME/bin

![img](image\wps5927.tmp.jpg) 

设置文件生效

source /etc/profile

## **9.** **启动**

redis-server  /usr/local/redis/bin/redis.conf &

![img](image\wps5928.tmp.jpg) 

## **10.** **验证是否启动成功**

![img](image\wps5939.tmp.jpg) 

## **11.** **客户端链接**

redis-cli -h localhost -p 6379 -a job36@redis

![img](image\wps5949.tmp.jpg) 

 