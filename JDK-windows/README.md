# windows JDK安装

Java Development Kit（JDK）是Java开发环境的一部分，提供了Java编程所需的工具和资源。JDK包括Java运行时环境（Java Runtime Environment，JRE）以及用于编写、编译和调试Java程序的开发工具。

Java Development Kit（JDK）是Java开发环境的一部分，提供了Java编程所需的工具和资源。JDK包括Java运行时环境（Java Runtime Environment，JRE）以及用于编写、编译和调试Java程序的开发工具。

Java Development Kit（JDK）是Java开发环境的一部分，提供了Java编程所需的工具和资源。JDK包括Java运行时环境（Java Runtime Environment，JRE）以及用于编写、编译和调试Java程序的开发工具。

### 一、下载JDK

访问 [Oracle JDK](https://www.oracle.com/java/technologies/downloads/#java8-windows)下载页面 或[ OpenJDK](https://jdk.java.net/java-se-ri/8-MR5)下载页面

如果你是开发者，请选择Oracle JDK。否则，你可以选择OpenJDK，它是开源的JDK版本。

点击适用于 Windows 的下载链接。

**1.1、示例选择**[**Oracle JDK**](https://www.oracle.com/java/technologies/downloads/#java8-windows)**下载。**

![1709394626476.png](image\1709394626476.png)

**1.2、登陆账号，下载jdk执行程序。**

![1709394681424.png](image\1709394681424.png)

### 二、运行与安装程序

**2.1、打开下载的安装程序（通常是一个 .exe 文件）。**

![1709394806878.png](image\1709394806878.png)

**2.2、根据安装向导的提示进行安装，点击 "Next"（下一步）。**

![1709394812013.png](image\1709394812013.png)

**2.3、在安装类型中，选择 "JDK"，然后点击 "Next"（下一步）。**

![1709394818695.png](image\1709394818695.png)

**2.4、选择安装路径，通常保持默认即可，然后点击 "Next"（下一步）。**

![1709394850426.png](image\1709394850426.png)

![1709394857732.png](image\1709394857732.png)

**2.5、完成安装。**

![1709394948222.png](image\1709394948222.png)

### 三、配置环境变量

**3.1、设置JAVA_HOME变量**

右键点击“此电脑”或“计算机”，选择“属性”。

![1709395295700.png](image\1709395295700.png)

点击“高级系统设置”。

![1709395301216.png](image\1709395301216.png)

点击“环境变量”按钮。

![1709395310693.png](image\1709395310693.png)

在“用户变量”或“系统变量”中，点击“新建”。

![1709395318928.png](image\1709395318928.png)

变量名：JAVA_HOME

![1709395330042.png](image\1709395330042.png)

变量值：JDK的安装路径，例如 C:\Program Files\Java\jdk1.8.0_45



**3.2、更新Path变量**

在“系统变量”中找到 Path，双击编辑。

![1709395637939.png](image\1709395637939.png)

在变量值的末尾添加 ;%JAVA_HOME%\bin;

![1709395387197.png](image\1709395387197.png)

**3.3、验证设置**

打开命令提示符（Command Prompt）并运行以下命令：

```
java -version
```

如果显示 Java 和编译器的版本信息，则安装和配置成功。

![1709395276889.png](image\1709395276889.png)

### 四、完成

现在，你已经成功安装并配置了Java JDK。你可以开始使用Java编写和运行程序了。