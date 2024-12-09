# VM虚拟机安装-CentOS

### 一、下载CentOS 镜像文件

[vm下载地址](https://www.vmware.com/products/workstation-pro.html)

[CentOS镜像下载地址](https://vault.centos.org/7.6.1810/isos/x86_64/)

**1.1、常见镜像类型**

**DVD ISO**普通光盘完整安装版镜像，可离线安装到计算机硬盘上，包含大量的常用软件，一般选择这种镜像类型即可。

**Everything ISO**：包含了完整安装版的内容，并对其进行补充，集成了所 有软件。

**Minimal ISO**：这个版本为精简版的镜像，可以安装一个基本的CentOS系 统，包含了可启动系统基本所需的最小安装包。

**LiveCD/DVD ISO**: 是一个光盘Centos系统，可通过光盘直接在电脑上启动系统，也可以将系统安装到计算机上使用，部分内容还需要再次下载。根据系统桌面不同live版的又可分为LiveGNOME ISO、LiveKDE ISO种。

**Netinstal**：在线安装版本，启动后需要联网边下载边安装。

示例镜像 CentOS-7-x86_64-Minimal-1810.iso

### 二、创建CentOS系统

**2.1、示例 VMware 版本信息如下：**

![1709561575902.png](image\1709561575902.png)



**2.2、文件->新建虚拟机**

![1709561632751.png](image\1709561632751.png)



**2.3、选择自定义**

![1709561679576.png](image\1709561679576.png)



**2.4、下一步**

![1709561814217.png](image\1709561814217.png)



**2.5、选择镜像文件路径**

![1709561846668.png](image\1709561846668.png)



**2.6、设置虚拟机名称以及位置**

![1709561882584.png](image\1709561882584.png)



**2.7、处理器设置**

![1709561926831.png](image\1709561926831.png)



**2.8、虚拟机内存大小设置**

![1709561958494.png](image\1709561958494.png)



**2.9、网络类型选择**

![1709562000221.png](image\1709562000221.png)



**2.10、选择I/O控制器类型选择**

![1709562068525.png](image\1709562068525.png)



**2.11、磁盘选择**

![1709562116389.png](image\1709562116389.png)



**2.12、磁盘大小设置**

![1709562155132.png](image\1709562155132.png)



**2.13、指定磁盘文件路径**

![1709562179326.png](image\1709562179326.png)



**2.14、点击完成，虚拟机创建完成**

![1709562266232.png](image\1709562266232.png)

### 三、设置固定IP

**3.1、启动虚拟机**

![1709562758044.png](image\1709562758044.png)



**3.2、语言设置**

![1709562864731.png](image\1709562864731.png)



**3.3、系统安装位置，选择自动分区，完成即可**

![1709562894564.png](image\1709562894564.png)

系统安装位置，选择自动分区，完成即可

![1709562955004.png](image\1709562955004.png)



**3.5、网络和主机名设置**

![1709562992774.png](image\1709562992774.png)



![1709563087858.png](image\1709563087858.png)



**3.6、点击安装**

![1709563151560.jpg](image\1709563151560.jpg)



**3.7、ROOT密码设置**

![1709563138884.jpg](image\1709563138884.jpg)



![1709563210986.jpg](image\1709563210986.jpg)



**3.8、等待几分钟，重启即可**

![1709563242630.jpg](image\1709563242630.jpg)



**3.9、完成基本设置后，重启**

![1709564044103.png](image\1709564044103.png)



**3.10、输入用户名和密码**

![1709564053363.png](image\1709564053363.png)

**3.11、国定IP设置**

修改配置文件

```
[root@localhost ~]# vi /etc/sysconfig/network-scripts/ifcfg-ens33
```

内容如下：

```
TYPE="Ethernet"
PROXY_METHOD="none"
BROWSER_ONLY="no"
BOOTPROTO="static"
DEFROUTE="yes"
IPV4_FAILURE_FATAL="no"
IPV6INIT="yes"
IPV6_AUTOCONF="yes"
IPV6_DEFROUTE="yes"
IPV6_FAILURE_FATAL="no"
IPV6_ADDR_GEN_MODE="stable-privacy"
NAME="ens33"
UUID="25957c91-24fa-49d1-979b-01a491db2ac9"
DEVICE="ens33"
ONBOOT="yes"
IPADDR=192.168.131.11
NETMASK=255.255.255.0
GATEWAY=192.168.131.2
DNS1=8.8.8.8
```



![1709564076482.png](image\1709564076482.png)

说明：将BOOTPROTO字段修改为static(静态模式)。GETAWAY需要查看得到。

VM->编辑->虚拟网络编辑器看到。

![1709563939851.png](image\1709563939851.png)



![1709563838826.png](image\1709563838826.png)

**
**

**3.12、重启服务，以及查看ip是否正常解析，检测是否能够上网服务**

重启服务

```
service network restart
```



查看ip是否正常解析

```
ip addr
```



检测是否能够上网服务

```
ping www.baidu.com
```



![1709564111478.png](image\1709564111478.png)