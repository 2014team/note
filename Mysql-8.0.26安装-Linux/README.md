# Mysql-8.0.26安装-Linux

##  下载 MySQL 安装文件 

**首先，官网下载**

https://downloads.mysql.com/archives/community/

![1721724118789.jpg](upload\1721724118789.jpg)

**解压安装文件**

解压下载的安装文件：

```
tar -xvf mysql-8.0.26-linux-glibc2.12-x86_64.tar.xz
```

解压后会生成一个 mysql-8.0.26-linux-glibc2.12-x86_64 的目录。

## **创建 MySQL 用户和组** 

创建一个专用的 MySQL 用户和组，用于运行 MySQL 服务：

```
sudo groupadd mysql
sudo useradd -r -g mysql -s /bin/false mysql
```

useradd：这是用于创建新用户的命令。

-r：此选项表示创建一个系统账户。系统账户通常用于运行服务或守护进程，UID（用户标识符）在 0 到 999 之间。

-g mysql：此选项指定新用户所属的初始组，这里指定为 mysql。在此之前必须确保组 mysql 已经存在（通过 groupadd mysql 创建）。

-s /bin/false：此选项指定用户的登录 shell 为 /bin/false，意味着此用户不能登录到系统。这是一个安全措施，防止该用户直接访问系统。

mysql：这是要创建的用户的用户名。

## 安装 MySQL

将解压后的 MySQL 文件移动到适当的安装目录，这里假设安装到 /usr/local/mysql：

```
sudo mv mysql-8.0.26-linux-glibc2.12-x86_64 /usr/local/mysql
```

## 配置 MySQL 数据目录和权限

创建 MySQL 数据目录，并设置合适的权限：

```
sudo mkdir -p /usr/local/mysql/data
sudo chown -R mysql:mysql /usr/local/mysql
```

## 初始化 MySQL 数据库

进入 MySQL 安装目录，并执行初始化数据库的命令：

```
cd /usr/local/mysql
sudo ./bin/mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data
```

初始化过程中会生成一个初始的随机密码，记录下来，稍后需要使用。

## 配置 MySQL

创建 MySQL 配置文件 /etc/my.cnf，并添加以下内容：

```
[mysqld]
character-set-server=utf8mb4
collation-server=utf8mb4_unicode_ci
basedir=/usr/local/mysql
datadir=/usr/local/mysql/data
socket=/tmp/mysql.sock
```

## 设置 MySQL 环境变量

为了方便使用 MySQL 命令，将 MySQL 的 bin 目录添加到系统的 PATH 中。编辑 ~/.bashrc 或 /etc/profile 文件，添加如下行：

```
export PATH=$PATH:/usr/local/mysql/bin
```

使配置生效：

```
source ~/.bashrc   # 或 source /etc/profile
```

## 启动 MySQL 服务 

启动 MySQL 服务：

```
sudo cp support-files/mysql.server /etc/init.d/mysql
sudo chkconfig --add mysql
sudo service mysql start
```

## 设置 MySQL 初始密码 

登录 MySQL，并设置初始密码：

```
mysql -uroot -p 

-- 如果 root 用户已存在，请先更改密码
ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';

-- 授予全部权限
GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION;

-- 刷新权限
FLUSH PRIVILEGES;

-- 验证权限
SHOW GRANTS FOR 'root'@'localhost';
```

## 允许从任何主机连接 

```
-- 登录 MySQL
mysql -u root -p


-- 如果 'root'@'%' 不存在，则创建它
CREATE USER 'root'@'%' IDENTIFIED BY '123456';

-- 授予所有权限
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' WITH GRANT OPTION;

-- 刷新权限
FLUSH PRIVILEGES;

-- 更改密码（如果需要）
ALTER USER 'root'@'%' IDENTIFIED BY '123456';
```



如果遇到 "Client does not support authentication protocol requested by server" 错误，可以尝试以下方法来更改 MySQL 服务器的身份验证插件

更改身份验证插件:

进入 MySQL 控制台，并执行以下命令：

```
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '123456';
FLUSH PRIVILEGES;
```

如果客户端版本较旧，请考虑升级 MySQL 客户端以确保兼容性。