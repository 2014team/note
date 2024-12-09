# Nginx安装-LinuxMysql-5.6.43安装-Linux

## 一、简介

MySQL是一个[关系型数据库管理系统](https://baike.baidu.com/item/关系型数据库管理系统/696511?fromModule=lemma_inlink)，由瑞典 [MySQL AB](https://baike.baidu.com/item/MySQL AB/2620844?fromModule=lemma_inlink) 公司开发，属于 [Oracle](https://baike.baidu.com/item/Oracle/301207?fromModule=lemma_inlink) 旗下产品。MySQL是最流行的[关系型数据库管理系统](https://baike.baidu.com/item/关系型数据库管理系统/696511?fromModule=lemma_inlink)之一，在 [WEB](https://baike.baidu.com/item/WEB/150564?fromModule=lemma_inlink) 应用方面，MySQL是最好的[RDBMS](https://baike.baidu.com/item/RDBMS/1048260?fromModule=lemma_inlink) (Relational Database Management System，[关系数据库管理系统](https://baike.baidu.com/item/关系数据库管理系统/11032386?fromModule=lemma_inlink))应用软件之一。

MySQL是一种关系型数据库管理系统，[关系数据库](https://baike.baidu.com/item/关系数据库/1237340?fromModule=lemma_inlink)将数据保存在不同的表中，而不是将所有数据放在一个大仓库内，这样就增加了速度并提高了灵活性。

MySQL所使用的 SQL 语言是用于访问数据库的最常用标准化语言。MySQL 软件采用了双授权政策，分为社区版和[商业版](https://baike.baidu.com/item/商业版/1817444?fromModule=lemma_inlink)，由于其体积小、速度快、总体拥有成本低，尤其是[开放源码](https://baike.baidu.com/item/开放源码/7176422?fromModule=lemma_inlink)这一特点，一般中小型和大型网站的开发都选择 MySQL作为[网站数据库](https://baike.baidu.com/item/网站数据库/6399264?fromModule=lemma_inlink)。

## 二、官网下载

安装环境说明

```
[root@centos ~]# cat /etc/os-release 
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"
```

[下载地址](https://downloads.mysql.com/archives/community/)

![1712738035462.png](image\1712738035462.png)

## 三、安装

**3.1 mysql安装包解压到 /usr/local 目录**

先把mysql安装包上传到Linux 服务器。

执行解压命令

```
tar -zxvf mysql-5.6.43-linux-glibc2.12-x86_64.tar.gz -C /usr/local
```

![1712738206794.png](image\1712738206794.png)



**3.2 把 mysql-5.6.43-linux-glibc2.12-x86 64文件夹命名为mysql**

进入到 /usr/local目录下重新命名文件夹

```
mv mysql-5.6.43-linux-glibc2.12-x86 64/ mysql
```

![1712738407008.png](image\1712738407008.png)

执行重命名结果

![1712738513998.png](image\1712738513998.png)

**3.3 创建一个名为mysql的用户**

```
useradd -s /sbin/nologin mysql
```

**![1712738624330.png](image\1712738624330.png)**

**3.4创建数据库文件存放目录**

```
mkdir -p /data/mysql
```

![1712738663389.png](image\1712738663389.png)

**3.5 修改目录（/data/mysql）拥有者为mysql用户**

```
chown -R mysql:mysql /data/mysql
```

![1712738748464.png](image\1712738748464.png)

**3.6进入/usr/local/mysql目录，初始化：**

```
./scripts/mysql_install_db --user=mysql --datadir=/data/mysql
```

![1712738813063.png](image\1712738813063.png)

错误

FATAL ERROR: please install the following Perl modules before executing ./scripts/mysql_install_db:

Data::Dumper

原因： 缺少perl模块中的Data::Dumper

安装 yum-y install autocon

![1712738949465.png](image\1712738949465.png)

再次执行初始化操作

![1712738968217.png](image\1712738968217.png)

**3.7复制配置文件**

```
cp support-files/my-default.cnf /etc/my.cnf
```

![1712739002392.png](image\1712739002392.png)

**3.8 修改配置文件**

```
vim /etc/my.cnf
basedir = /usr/local/mysql
datadir = /data/mysql
port = 3306
```

![1712739056614.png](image\1712739056614.png)

**3.9 复制启动脚本**

```
cp support-files/mysql.server /etc/init.d/mysqld
```

![1712739093756.png](image\1712739093756.png)

**3.10 修改启动脚本权限**

```
chmod 755 /etc/init.d/mysqld
```

![1712739216070.png](image\1712739216070.png)

**3.11 修改启动脚本文件**

```
vim /etc/init.d/mysqld
```

![1712739294557.png](image\1712739294557.png)

**3.12 设置开机启动**

![1712739455808.png](image\1712739455808.png)

## 四、客户端链接

**4.1 环境变量设置**

打开Linux环境变量配置文件

```
vim /etc/profile
```

最后面加上 `export PATH=/usr/local/mysql/bin:$PATH`

 **![1712739693264.png](image\1712739693264.png)**

保存后，使文件马上生效

```
source /etc/profile
```

**4.2 启动服务**

```
service mysqld start
```

**![1712739540251.png](image\1712739540251.png)**

**4.3 修改MySQL的登录密码**

进入skip-grant-tables模式

修改root用户密码并刷新权限

```
use mysql;
update user set password=password("test123") where user="root";
flush privileges;
```

![1712740072180.png](image\1712740072180.png)

修改之后需要密码登录

![1712740205364.png](image\1712740205364.png)

**4.4 远程访问赋权**

mysql 默认是不可以通过远程机器访问的,通过下面的配置可以开启远程访问。

sql>grant all privileges on *.* to 'root'@'%' identified by 'test123' with grant option;

sql>flush privileges;

![1712740240966.png](image\1712740240966.png)

**4.5 关闭防火墙**

![1712740279779.png](image\1712740279779.png)

**4.6 客户端链接**

**![1712740306619.png](image\1712740306619.png)**