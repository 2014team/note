# JDK-Linux

### 一、下载

在Windows电脑下载安装包以后，上传至Linux中进行安装。

[JDK下载](https://www.oracle.com/java/technologies/downloads/#java8)



**1.1、安装环境说明**

*![1709651665580.png](image\1709651665580.png)**

**1.2、官网下载**

![1709649532656.png](image\1709649532656.png)



登陆账号之后，直接下载

![1709649554455.png](image\1709649554455.png)

**1.3、下载完成如下**

**![1709649645975.png](image\1709649645975.png)**

### 二、安装

**2.1、上传Linux服务器**

先在Linux创建路径

```
mkdir -p /usr/java/
```

![1709651676345.png](image\1709651676345.png)

把下载jdk上传/usr/java目录



![1709649729122.png](image\1709649729122.png)



**2.2、解压**

![1709650807310.png](image\1709650807310.png)

### 三、环境变量配置

**3.1、修改配置文件**

```
vi /etc/profile
```



![1709650873732.png](image\1709650873732.png)

在文件最后新增如下内容:

```
export JAVA_HOME=/usr/java/jdk1.8.0_401
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```

![1709652435432.png](image\1709652435432.png)

**3.1、使配置文件生效**

```
source /etc/profile
```

![1709651029148.png](image\1709651029148.png)

### 四、验证

```
 java -version
```

![1709651092860.png](image\1709651092860.png)