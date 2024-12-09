# Java开发工具Eclipse

工欲善其事，必先利其器。要使用Java语言进行程序开发,就必须选择一种功能强大、使用方便且能够辅助程序开发的IDE集成开发工具。而Eclipse就是目前最流行的Java语言辅助开发工具。它具有强大的代码辅助功能，能够帮助程序开发人员自动完成输入语法、补全文字、修正代码等操作，能够减少程序开发人员的时间和精力。



### 一、Eclipse 概述

​    Eclipse 是 IBM 花巨资开发的IDE集成开发环境（Integrated Development Environment）。其前身是 IBM 的 Visual Age for Java(VA4J)。Eclipse 是一个发开放源代码的、基于Java的可扩展开发平台。就其本身而言，它只是一个框架和一组服务，用于通过插件组件构建开发环境是可扩展的体系结构。可以集成不同软件开发供应商开发的产品，将他们开发的工具和组件加入到 Eclipse平台中。另外 Eclipse 还附带了一个标准的插件集，包括 Java 开发工具 (Java Development Tools JDT )。

​     其他流行开发工具：

**IntelliJ Idea**

​    [IntelliJ Idea](https://www.jetbrains.com/idea/)是由JetBrains公司开发的一个功能强大的IDE，分为免费版和商用付费版。JetBrains公司的IDE平台也是基于IDE平台+语言插件的模式，支持Python开发环境、Ruby开发环境、PHP开发环境等，这些开发环境也分为免费版和付费版。



**NetBeans**



​    [NetBeans](https://netbeans.apache.org/front/main/index.html)是最早由SUN开发的开源IDE，由于使用人数较少，目前已不再流行。



### 二、Eclipse 安装与汉化

  1、[Eclipse 下载](https://www.eclipse.org/)

到Eclipse官网点击 Download

  ![1709107050207.png](image\1709107050207.png)

   

  2、选择 Download Packages

![1709107061332.png](image\1709107061332.png)



  3、选择符合安装平台软件

![1709107066988.png](image\1709107066988.png)



   4、下载汉化包

 在[Eclipse汉化包](https://eclipse.dev/babel/downloads.php)下载

 点击[Latest Release ](https://download.eclipse.org/technology/babel/babel_language_packs/latest/index.php)

![1709107072595.png](image\1709107072595.png)



  5、选择Language: Chinese (Simplified)

![1709107079534.png](image\1709107079534.png)



  6、将下载 Eclipse汉化包下载解压，将 features 和 plugins 文件夹复制到安装的 Eclipse 目录，替换相对应文件，这样就可以实现 Eclpse 汉化。

  7 、启动 Eclipse

运行 D:\Program Files\eclipse\eclipse.exe

![1709107097470.png](image\1709107097470.png)



### 三、创建 Java 项目    

  1、创建Hello World 项目

选择【文件】> 【新建】> 【项目】命令，打开新建项目对话框。

![1709107106062.png](image\1709107106062.png)



  2、在向导列表中选择【 Java 项目】选项，单击 【下一步】按钮

![1709107112543.png](image\1709107112543.png)



  3、在新建 Java 项目对话框，输入项目名称，单击 【完成】按钮

![1709107121334.png](image\1709107121334.png)



  4、单击 【完成】按钮，之后的效果

![1709107126340.png](image\1709107126340.png)

### 四、创建 Java 类     

  1、鼠标点击 HelloWorld 项目的源目录（src），右键创建 Java 类

![1709107132624.png](image\1709107132624.png)



  2、输入包、名称，勾选【public static void main(String args)】

![1709107136936.png](image\1709107136936.png)





  3、点击【完成】按钮

![1709107142987.png](image\1709107142987.png)



  4、编写 Java 代码，在代码编辑框输入sys后，按住【 Alt + / 】选择 【sysout】项，便可以自动输入该项

![1709107147469.png](image\1709107147469.png)





   5、键盘按住【Enter】

![1709107151642.png](image\1709107151642.png)



  6、编写代码，键盘按住【Crtl + S】保存

![1709107155961.png](image\1709107155961.png)



### 五、运行 Java 程序

  1、在编码对话框【右键】> 【运行方式】>【Java应用程序】

![1709107163294.png](image\1709107163294.png)



  2、控制台显示

![1709107167635.png](image\1709107167635.png)



### 六、Eclipse 调试程序 （方法一）

   1、打断点，鼠标左双击两下 

![1709107173076.png](image\1709107173076.png)



  2、编写代码对话框，【鼠标右击】>【调试方式】>【Java应用程序】

![1709107178596.png](image\1709107178596.png)



  3、切换调试视图

![1709107184687.png](image\1709107184687.png)



  4、调试视图界面

![1709107188882.png](image\1709107188882.png)

  

   5、选择 ![1709106765068.png](image\1709106765068.png)【继续】

![1709107194213.png](image\1709107194213.png)

  

  6、执行完毕，控制台输出信息

![1709107209947.png](image\1709107209947.png)

### 七、Eclipse 调试程序 （方法二）

  1、打断点，鼠标左双击两下 

![1709107213974.png](image\1709107213974.png)



  

  2、编写代码对话框，【鼠标右击】>【调试方式】>【运行 配置】

![1709107218809.png](image\1709107218809.png)

 

  3、调试 配置框

![1709107223040.png](image\1709107223040.png)



  4、选择【调试】按钮

![1709107226735.png](image\1709107226735.png)



  5、选择【切换】按钮，变成调试模式

![1709107233194.png](image\1709107233194.png)



  6、选择 ![1709106833233.png](image\1709106833233.png)【继续】

![1709107238426.png](image\1709107238426.png)



​    7、执行完毕，控制台输出信息

![1709107251987.png](image\1709107251987.png)