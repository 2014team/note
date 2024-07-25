# 反向代理服务器Nginx

## 第1章Nginx概述

### 1.1Nginx简介

Nginx (engine x) 是一个轻量级的、高性能的、基于Http的、反向代理服务器，静态web服务器。
Nginx最初是由俄罗斯人Igor Sysoev（伊戈尔·赛索耶夫）使用C语言为俄罗斯访问量第二的Rambler.ru站点开发的一款服务器。2004年10月发布第一个版本。
Nginx的官网： http://nginx.org
国内大型的站点，例如百度、京东、新浪、网易、腾讯、淘宝等，都使用了Nginx。
https://www.netcraft.com/

### 1.2代理服务器

#### 1.2.1 正向代理

（1） 隐藏

![image-20240724172310954](upload\image-20240724172310954.png)

（2） 翻墙

![image-20240724172625391](upload\image-20240724172625391.png)

（3） 提速

![image-20240724172709745](upload\image-20240724172709745.png)

（4） 缓存

![image-20240724172738803](upload\image-20240724172738803.png)

（5） 授权

![image-20240724172751360](upload\image-20240724172751360.png)

#### 1.2.2 反向代理

（1） 保护隐藏

![image-20240724172832063](upload\image-20240724172832063.png)

（2） 分布式路由

![image-20240724172847596](upload\image-20240724172847596.png)

（3） 负载均衡

![image-20240724172906451](upload\image-20240724172906451.png)

（4） 动静分离

![image-20240724172919482](upload\image-20240724172919482.png)

（5） 数据缓存

![image-20240724172931105](upload\image-20240724172931105.png)

#### 1.2.3 正向代理与反向代理的区别

客户端是否清楚自己所要访问的服务器是谁？
架设的位置不同

### 1.3Nginx的特点

#### 1.3.1 高并发

一个Nginx服务器在不做任何配置的情况下并发量可达1000左右。在硬件条件允许的前提下，Nginx可以支持高达5-10万的并发量（除了Nginx的设置外，Linux主机需要做大量的设置来配合Nginx）。
对比一下Tomcat。Tomcat服务器默认的并发量为150（不做任何配置）。即，当有超过150个用户同时访问某Servlet时，Tomcat的响应就会变得非常慢。

#### 1.3.2 低消耗

官方给出的测试结果，10000个非活跃连接，在Nginx中仅消耗2.5M内存。对于一般性的DoS攻击来说就不是事儿，但对于DDoS也会是问题。

#### 1.3.3 热部署

可以在7*24小时不间断服务的前提下，进行Nginx版本的平滑升级，Nginx配置文件的平滑修改。即在不停机的情况下升级Nginx，修改替换Nginx配置文件。

#### 1.3.4 高可用

Nginx只所以可以实现高并发，是因为其具有很多工作进程worker。当这些工作进程中的某些出现问题停止工作时，并不会影响整个系统的整体运行。因为其它worker会接替那些出问题的线程。

#### 1.3.5 高扩展

Nginx只所以现在的用户很多，是因为很多功能都已经开发好并模块化。若需要哪些功能，只需要安装相应功能的扩展模块即可。根据编写扩展模块所使用的语言的不同，可以划分为两类：C语言扩展模块与LUA脚本扩展模块。 http://openresty.org/cn/

### 1.4Nginx的下载与安装

#### 1.4.1 Nginx的下载

nginx的官网为： http://nginx.org。

#### 1.4.2 Nginx的源码安装

**（1） 安装Nginx**
**A、上传Nginx**
将下载好的Nginx上传到新复制的主机的/usr/tools目录。
**B、安装gcc**
由于Nginx是由C/C++语言编写的，所以对其进行编译就必须要使用相关编译器。对于C/C++语言的编译器，使用最多的是gcc与gcc-c++，而这两款编译器在CentOS7中是没有安装的，所以首先要安装这两款编译器。

![image-20240724173305176](upload\image-20240724173305176.png)

**C、安装依赖库**
基本的Nginx功能依赖于一些基本的库，在安装Nginx之前需要提前安装这些库。

![image-20240724173319513](upload\image-20240724173319513.png)

**D、创建解压目录**
在/usr下创建apps目录，用于存放解压后的安装包程序。

![image-20240724173329925](upload\image-20240724173329925.png)

**E、解压Nginx**
将Nginx解压到/usr/apps目录中。

![image-20240724173339481](upload\image-20240724173339481.png)

进入到/usr/apps目录中的Nginx解压包目录，查看Nginx的目录。

![image-20240724173400472](upload\image-20240724173400472.png)

**F、生成makefile**
在Nginx解压目录下运行make命令，用于完成编译。但此时会给出提示：没有指定目标，并且没有发现编译文件makefile。

![image-20240724173411318](upload\image-20240724173411318.png)

编译命令make需要根据编译文件makefile进行编译，所以在编译之前需要先生成编译文件makefile。使用configure命令可以生成该文件。

**G、编译安装**

![image-20240724173424534](upload\image-20240724173424534.png)

**（2） 使nginx命令随处可用**

在Nginx的安装目录/usr/local/nginx中有一个sbin目录，其中存放着nginx的命令程序nginx。

![image-20240724173452347](upload\image-20240724173452347.png)

![image-20240724173456109](upload\image-20240724173456109.png)

#### 1.4.3 Nginx命令

（1） 查看命令选项nginx -h
使用nginx –h 可以查看Nginx命令的选项。

![image-20240724173518811](upload\image-20240724173518811.png)

**（2） 相看Nginx版本信息nginx –v 或-V**
nginx –v：显示Nginx版本信息。

![image-20240724173537951](upload\image-20240724173537951.png)

nginx –V：显示更多的版本相关信息，例如gcc的版本，OpenSSL的版本等。

![image-20240724173548217](upload\image-20240724173548217.png)

**（3） 测试配置文件命令nginx -tq**
nginx –t：测试配置文件是否正确，默认只测试默认的配置文件conf/nginx.conf。
nginx –T：测试配置文件是否正确，并显示配置文件内容。
nginx –tq：在配置文件测试过程中，禁止显示非错误信息，即只显示错误信息。

![image-20240724173601513](upload\image-20240724173601513.png)

可以结合-c选项指定要测试的配置文件。注意，其不会启动nginx。

![image-20240724173617101](upload\image-20240724173617101.png)

**（4） 停止命令nginx –s stop/quit**
在nginx命令后通过-s选项，可以指定不同的信号完成不同的功能。
nginx –s stop：强制停止Nginx，无论当前工作进程是否正在处理工作。
nginx –s quit：优雅停止Nginx，使当前的工作进程完成当前工作后停止。

![image-20240724173636012](upload\image-20240724173636012.png)

![image-20240724173640477](upload\image-20240724173640477.png)

**（5） 平滑重启命令nginx –s reload**
在不重启Nginx的前提下重新加载Nginx配置文件，称为平滑重启。

![image-20240724173703018](upload\image-20240724173703018.png)

**（6） nginx –s reopen**
重新打开日志文件。
**（7） nginx –p**
指定Nginx配置文件的存放路径。

**（8） 启动命令nginx –c file**
nginx –c（小写字母）可启动Nginx，启动成功后无任何提示。

![image-20240724173723871](upload\image-20240724173723871.png)

若不指定配置文件，则默认加载的是Nginx安装目录下的conf/nginx.cnf。

![image-20240724173732491](upload\image-20240724173732491.png)

**（9） nginx –g**
设置配置文件以外的全局指令。

#### 1.4.4 页面访问测试

**（1） 关闭防火墙**

![image-20240724173759902](upload\image-20240724173759902.png)

**（2） 浏览器访问**
由于Nginx服务器默认的端口号为80，所以在浏览器中直接输入Nginx的主机名或IP，就可以看到Nginx欢迎页面。只要可以看到以下页面信息，则说明Nginx安装运行成功。

![image-20240724173818635](upload\image-20240724173818635.png)

![image-20240724173826709](upload\image-20240724173826709.png)

## 第2章Nginx核心配置

### 2.1Nginx性能调优

在Nginx性能调优中，有两个非常重要的理论点（面试点）需要掌握。所以，下面首先讲解这两个知识点，再进行性能调优的配置。

#### 2.1.1 零拷贝（Zero Copy）

**（1） 零拷贝基础**
零拷贝指的是，从一个存储区域到另一个存储区域的copy任务没有CPU参与。零拷贝通常用于网络文件传输，以减少CPU消耗和内存带宽占用，减少用户空间与CPU内核空间的拷贝过程，减少用户上下文与CPU内核上下文间的切换，提高系统效率。
用户空间指的是用户可操作的内存缓存区域，CPU内核空间是指仅CPU可以操作的寄存器缓存及内存缓存区域。
用户上下文指的是用户状态环境，CPU内核上下文指的是CPU内核状态环境。
零拷贝需要DMA控制器的协助。DMA，Direct Memory Access，直接内存存取，是CPU的组成部分，其可以在CPU内核（算术逻辑运算器ALU等）不参与运算的情况下将数据从

一个地址空间拷贝到另一个地址空间。
**（2） 传统拷贝方式**
下面均以“将一个硬盘中的文件通过网络发送出去”的过程为例，来详细详细分析不同拷贝方式的实现细节。

**A、实现细节**
首先通过应用程序的read()方法将文件从硬盘读取出来，然后再调用send()方法将文件发送出去。

![image-20240724174019888](upload\image-20240724174019888.png)

**B、总结**
该拷贝方式共进行了4次用户空间与内核空间的上下文切换，以及4次数据拷贝，其中两次拷贝存在CPU参与。
我们发现一个很明显的问题：应用程序的作用仅仅就是一个数据传输的中介，最后将kernel buffer中的数据传递到了socket buffer。显然这是没有必要的。所以就引入了零拷贝。

**（3） 零拷贝方式**
**A、实现细节**
Linux系统（CentOS6及其以上版本）对于零拷贝是通过sendfile系统调用实现

![image-20240724174046628](upload\image-20240724174046628.png)

**B、总结**
该拷贝方式共进行了2次用户空间与内核空间的上下文切换，以及3次数据拷贝，但整个拷贝过程均没有CPU的参与，这就是零拷贝。
我们发现这里还存在一个问题：kernel buffer到socket buffer的拷贝需要吗？kernel buffer与socket buffer有什么区别呢？DMA控制器所控制的拷贝过程有一个要求，数据在源头的存放地址空间必须是连续的。kernel buffer中的数据无法保证其连续性，所以需要将数据再拷贝到socket buffer，socket buffer可以保证了数据的连续性。
这个拷贝过程能否避免呢？可以，只要主机的DMA支持Gather Copy功能，就可以避免由kernel buffer到socket buffer的拷贝。

**（4） Gather Copy DMA零拷贝方式**
由于该拷贝方式是由DMA完成，与系统无关，所以只要保证系统支持sendfile系统调用功能即可。

**A、实现细节**
该方式中没有数据拷贝到socket buffer。取而代之的是只是将kernel buffer中的数据描述信息写到了socket buffer中。数据描述信息包含了两方面的信息：kernel buffer中数据的地址及偏移量。

![image-20240724174123889](upload\image-20240724174123889.png)

**B、总结**
该拷贝方式共进行了2次用户空间与内核空间的上下文切换，以及2次数据拷贝，并且整个拷贝过程均没有CPU的参与。
该拷贝方式的系统效率是高了，但与传统相比，也存在有不足。传统拷贝中user buffer中存有数据，因此应用程序能够对数据进行修改等操作；零拷贝中的user buffer中没有了数据，所以应用程序无法对数据进行操作了。Linux的mmap零拷贝解决了这个问题。

**（5） mmap零拷贝**
mmap零拷贝是对零拷贝的改进。当然，若当前主机的DMA支持Gather Copy，mmap同样可以实现Gather Copy DMA的零拷贝。
**A、实现细节**
该方式与零拷贝的唯一区别是，应用程序与内核共享了Kernel buffer。由于是共享，所以应用程序也就可以操作该buffer了。当然，应用程序对于Kernel buffer的操作，就会引发

用户空间与内核空间的相互切换。

![image-20240724174201143](upload\image-20240724174201143.png)

**B、总结**
该拷贝方式共进行了4次用户空间与内核空间的上下文切换，以及2次数据拷贝，并且整个拷贝过程均没有CPU的参与。虽然较之前面的零拷贝增加了两次上下文切换，但应用程序可以对数据进行修改了。

#### 2.1.2 多路复用器select|poll|epoll

**（1） 基本知识**
若要理解select、poll与epoll多路复用器的工作原理，就需要首先了解什么是多路复用器。而要了解什么是多路复用器，就需要先了解什么是“多进程/多线程连接处理模型”。

A、多进程/多线程连接处理模型

![image-20240724174241425](upload\image-20240724174241425.png)

在该模型下，一个用户连接请求会由一个内核进程处理，而一个内核进程会创建一个应用程序进程，即app进程来处理该连接请求。应用程序进程在调用IO时，采用的是BIO通讯方式，即应用程序进程在未获取到IO响应之前是处于阻塞态的。
该模型的优点是，内核进程不存在对app进程的竞争，一个内核进程对应一个app进程。但，也正因为如此，所以其弊端也就显而易见了。需要创建过多的app进程，而该创建过程十分的消耗系统资源。且一个系统的进程数量是有上限的，所以该模型不能处理高并发的情况。

B、多路复用连接处理模型

![image-20240724174258083](upload\image-20240724174258083.png)

在该模型下，只有一个app进程来处理内核进程事务，且app进程一次只能处理一个内核进程事务。故这种模型对于内核进程来说，存在对app进程的竞争。
在前面的“多进程/多线程连接处理模型”中我们说过，app进程只要被创建了就会执行内核进程事务。那么在该模型下，应用程序进程应该执行哪个内核进程事务呢？谁的准备就绪了，app进程就执行哪个。但app进程怎么知道哪个内核进程就绪了呢？需要通过“多路复用器”来获取各个内核进程的状态信息。那么多路复用器又是怎么获取到内核进程的状态信息的呢？不同的多路复用器，其算法不同。常见的有三种：select、poll与epoll。
app进程在进行IO时，其采用的是NIO通讯方式，即该app进程不会阻塞。当一个IO结果返回时，app进程会暂停当前事务，将IO结果返回给对应的内核进程。然后再继续执行暂停的线程。
该模型的优点很明显，无需再创建很多的应用程序进程去处理内核进程事务了，仅需一个即可。

**（2） 多路复用器工作原理**
**A、select**
select多路复用器是采用轮询的方式，一直在轮询所有的相关内核进程，查看它们的进程状态。若已经就绪，则马上将该内核进程放入到就绪队列。否则，继续查看下一个内核进程状态。在处理内核进程事务之前，app进程首先会从内核空间中将用户连接请求相关数据复制到用户空间。
该多路复用器的缺陷有以下几点：

对所有内核进程采用轮询方式效率会很低。因为对于大多数情况下，内核进程都不属于就绪状态，只有少部分才会是就绪态。所以这种轮询结果大多数都是无意义的。

由于就绪队列底层由数组实现，所以其所能处理的内核进程数量是有限制的，即其能够处理的最大并发连接数量是有限制的。

 从内核空间到用户空间的复制，系统开销大。

**B、poll**
poll多路复用器的工作原理与select几乎相同，不同的是，由于其就绪队列由链表实现，所以，其对于要处理的内核进程数量理论上是没有限制的，即其能够处理的最大并发连接数量是没有限制的（当然，要受限于当前系统中进程可以打开的最大文件描述符数ulimit，后面会讲到）。
**C、epoll**
epoll多路复用是对select与poll的增强与改进。其不再采用轮询方式了，而是采用回调方式实现对内核进程状态的获取：一旦内核进程就绪，其就会回调epoll多路复用器，进入到多路复用器的就绪队列（由链表实现）。所以epoll多路复用模型也称为epoll事件驱动模型。
另外，应用程序所使用的数据，也不再从内核空间复制到用户空间了，而是使用mmap零拷贝机制，大大降低了系统开销。
当内核进程就绪信息通知了epoll多路复用器后，多路复用器就会马上对其进行处理，将其马上存放到就绪队列吗？不是的。根据处理方式的不同，可以分为两种处理模式：LT模式与ET模式。

**a、LT模式**
LT，Level Triggered，水平触发模式。即只要内核进程的就绪通知由于某种原因暂时没有被epoll处理，则该内核进程就会定时将其就绪信息通知epoll。直到epoll将其写入到就绪队列，或由于某种原因该内核进程又不再就绪而不再通知。其支持两种通讯方式：BIO与NIO。
**b、ET模式**
ET，Edge Triggered，边缘触发模式。其仅支持NIO的通讯方式。
当内核进程的就绪信息仅会通知一次epoll，无论epoll是否处理该通知。明显该方式的效率要高于LT模式，但其有可能会出现就绪通知被忽视的情况，即连接请求丢失的情况。

#### 2.1.3 Nginx的并发处理机制

一般情况下并发处理机制有三种：多进程、多线程，与异步机制。Nginx对于并发的处理同时采用了三种机制。当然，其异步机制使用的是异步非阻塞方式。
我们知道Nginx的进程分为两类：master进程与worker进程。每个master进程可以生成多个worker进程，所以其是多进程的。每个worker进程可以同时处理多个用户请求，每个用户请求会由一个线程来处理，所以其是多线程的。
那么，如何解释其“异步非阻塞”并发处理机制呢？
worker进程采用的就是epoll多路复用机制来对后端服务器进行处理的。当后端服务器返回结果后，后端服务器就会回调epoll多路复用器，由多路复用器对相应的worker进程进行通知。此时，worker进程就会挂起当前正在处理的事务，拿IO返回结果去响应客户端请求。响应完毕后，会再继续执行挂起的事务。这个过程就是“异步非阻塞”的。

#### 2.1.4 全局模块下的调优

（1） worker_processes 2
打开nginx.conf配置文件，可以看到worker_processes的默认值为1。

![image-20240724174549056](upload\image-20240724174549056.png)

worker_processes，工作进程，用于指定Nginx的工作进程数量。其数值一般设置为CPU内核数量，或内核数量的整数倍。
不过需要注意，该值不仅仅取决于CPU内核数量，还与硬盘数量及负载均衡模式相关。在不确定时可以指定其值为auto。![image-20240724174604149](upload\image-20240724174604149.png)

**（2） worker_cpu_affinity 01 10**
将worker进程与具体的内核进行绑定。不过，若指定worker_processes的值为auto，则无法设置worker_cpu_affinity。

![image-20240724174617654](upload\image-20240724174617654.png)

该设置是通过二进制进行的。每个内核使用一个二进制位表示，0代表内核关闭，1代表内核开启。也就是说，有几个内核，就需要使用几个二进制位。

![image-20240724174734584](upload\image-20240724174734584.png)

**（3） worker_rlimit_nofile 65535**
用于设置一个worker进程所能打开的最多文件数量。其默认值与当前Linux系统可以打开的最大文件描述符数量相同。

![image-20240724174755015](upload\image-20240724174755015.png)

#### 2.1.5 events模块下的调优

**（1） worker_connections 1024**
设置每一个worker进程可以并发处理的最大连接数。该值不能超过worker_rlimit_nofile的值。
**（2） accept_mutex on**
 on：默认值，表示当一个新连接到达时，那些没有处于工作状态的worker将以串行方式来处理；
 off：表示当一个新连接到达时，所有的worker都会被唤醒，不过只有一个worker能获取新连接，其它的worker会重新进入阻塞状态，这就是“惊群”现象。
**（3） accept_mutex_delay 500ms**
设置队首worker会尝试获取互斥锁的时间间隔。默认值为500毫秒。
**（4） multi_accept on**
 off：系统会逐个拿出新连接按照负载均衡策略，将其分配给当前处理连接个数最少的worker。
on：系统会实时的统计出各个worker当前正在处理的连接个数，然后会按照“缺编”最多的worker的“缺编”数量，一次性将这么多的新连接分配给该worker。

**（5） use epoll**
设置worker与客户端连接的处理方式。Nginx会自动选择适合当前系统的最高效的方式。当然，也可以使用use指令明确指定所要使用的连接处理方式。user的取值有以下几种： select | poll | epoll | rtsig | kqueue | /dev/poll 。
**A、select | poll | epoll**
这是三种多路复用机制。select与poll工作原理几乎相同，而epoll的效率最高，是现在使用最多的一种多路复用机制。
**B、rtsig**
realtime signal，实时信号，Linux 2.2.19+的高效连接处理方式。但在 在Linux 2.6版本后，不再支持该方式。
**C、kqueue**
应用在BSD系统上的epoll。

**D、/dev/poll**
UNIX系统上使用的poll。

#### 2.1.6 http模块下的调优

**（1） 非调优属性简介**

![image-20240724180418174](upload\image-20240724180418174.png)

include mime.types;
将当前目录(conf目录)中的mime.types文件包含进来。
default_type application/octet-stream;
对于无扩展名的文件，默认其为application/octet-stream类型，即Nginx会将其作为一个八进制流文件来处理。

charset utf-8;
设置请求与响应的字符编码。
**（2） sendfile on**
设置为on则开启Linux系统的零拷贝机制，否则不启用零拷贝。当然，开启后是否起作用，要看所使用的系统版本。CentOS6及其以上版本支持sendfile零拷贝。

**（3） tcp_nopush on**
 on：以单独的数据包形式发送Nginx的响应头信息，而真正的响应体数据会再以数据包的形式发送，这个数据包中就不再包含响应头信息了。
off：默认值，响应头信息包含在每一个响应体数据包中。
**（4） tcp_nodelay on**
 on：不设置数据发送缓存，即不推迟发送，适合于传输小数据，无需缓存。
off：开启发送缓存。若传输的数据是图片等大数据量文件，则建议设置为off。

**（5） keepalive_timeout 60**
设置客户端与Nginx间所建立的长连接的生命超时时间，时间到达，则连接将自动关闭。单位秒。
**（6） keepalive_requests 10000**
设置一个长连接最多可以发送的请求数。该值需要在真实环境下测试。
**（7） client_body_timeout 10**
设置客户端获取Nginx响应的超时时限，即一个请求从客户端发出到接收到Nginx的响应的最长时间间隔。若超时，则认为本次请求失败。

### 2.2请求定位

#### 2.2.1 资源访问

**（1） 修改配置文件**

![image-20240724180812977](upload\image-20240724180812977.png)

**（2） 创建目录**

在真实目录中，必须要在root属性指定的目录下存在location指定的URI路径目录。所以需要在/opt/aaa下创建xxx/ooo目录。

![image-20240725090348129](upload\image-20240725090348129.png)

**（3） 创建文件**
在/opt/aaa/xxx/ooo目录下新建一个myfile.txt文件，文件内容为：this default page。

![image-20240725090404568](upload\image-20240725090404568.png)

再新建一个hello.txt文件，文件内容为：hello nginx world

![image-20240725090416716](upload\image-20240725090416716.png)

#### 2.2.2 路径匹配优先级

**（1） 优先级规则**
优先级由低到高依次是：
普通匹配 < 长路径匹配 < 正则匹配 < 短路匹配 < 精确匹配
**（2） 普通匹配**
浏览器地址栏中的访问路径均为如下形式，不变。

![image-20240725090439245](upload\image-20240725090439245.png)

下面的匹配规则是：只要请求是以/xxx开头的路径就可命中。

![image-20240725090503275](upload\image-20240725090503275.png)

![image-20240725090512263](upload\image-20240725090512263.png)

**（3） 长路径匹配**
当一个请求径既可以与一个长路径相匹配，又可以与一个短路径相匹配时，长路径优先级高。

![image-20240725090531055](upload\image-20240725090531055.png)

![image-20240725090536120](upload\image-20240725090536120.png)

**（4） 正则匹配**
在正则匹配与普通匹配（长路径匹配也属于普通匹配）均可匹配上时，正则匹配的优先级高。
**A、区分大小写的正则匹配**
~表示这里是正则表达式，默认匹配是区分大小写的。
在长路径匹配与正则匹配间，仍然是正则匹配的优先级要高于长路径匹配的，即使正则匹配的要短于长路径匹配的。

![image-20240725090558847](upload\image-20240725090558847.png)

![image-20240725090604064](upload\image-20240725090604064.png)

当请求中的XXX写为大写字母，会报404找到资源。

![image-20240725090614908](upload\image-20240725090614908.png)

**B、不区分大小写的正则匹配**
~后跟上*号，表示这是不区分大小写的正则表达式。

![image-20240725090644559](upload\image-20240725090644559.png)

当请求中的XXX写为大写字母时，依然可以访问。

![image-20240725090700834](upload\image-20240725090700834.png)

**（5） 短路匹配**
以^~开头的匹配路径称为短路匹配，表示只要匹配上，就不再匹配其它的了，即使是正则匹配也不再匹配了。即其优先级要高于正则匹配的。

![image-20240725090728667](upload\image-20240725090728667.png)

![image-20240725090734977](upload\image-20240725090734977.png)

**（6） 精确匹配**
以等号（=）开头的匹配称为精确匹配，其是优先级最高的匹配。

![image-20240725090753588](upload\image-20240725090753588.png)

![image-20240725090758709](upload\image-20240725090758709.png)

#### 2.2.3 缓存配置

Nginx具有很强大的缓存功能，可以对请求的response进行缓存，起到类似CDN的作用，甚至有比CDN更强大的功能。同时，Nginx缓存还可以用来“数据托底”，即当后台web服务器挂掉的时候，Nginx可以直接将缓存中的托底数据返回给用户。此功能就是Nginx实现“服务降级”的体现。
Nginx缓存功能的配置由两部分构成：全局定义与局部定义。在http{}模块的全局部分中进行缓存全局定义，在server{}模块的各个location{}模块中根据业务需求进行缓存局部定义。

**（1） http{}模块的缓存全局定义**

![image-20240725090856876](upload\image-20240725090856876.png)

**A、proxy_cache_path**
用于指定Nginx缓存的存放路径及相关配置。
B、proxy_temp_path
指定Nginx缓存的临时存放目录。若proxy_cache_path中的use_temp_path设置为了off，则该属性可以不指定。
**（2） location{}模块的缓存局部定义**
**A、proxy_cache mycache**
指定用于存放缓存key内存区域名称。其值为http{}模块中proxy_cache_path中的keys_zone的值。
**B、proxy_cache_key $host$request_uri$arg_age**
指定Nginx生成的缓存的key的组成。

**C、proxy_cache_bypass $arg_age**
指定是否越过缓存。
**D、proxy_cache_methods GET HEAD**
指定客户端请求的哪些提交方法将被缓存，默认为GET与HEAD，但不缓存POST。
**E、proxy_no_cache $aaa $bbb $ccc**
指定对本次请求是否不做缓存。只要有一个不为0，就不对该请求结果缓存。
**F、proxy_cache_purge $ddd $eee $fff**
指定是否清除缓存key。
**G、proxy_cache_lock on**

指定是否采用互斥方式回源。

**H、proxy_cache_lock_timeout 5s**
指定再次生成回源互斥锁的时限。
**I、proxy_cache_valid 5s**
对指定的 HTTP 状态码的响应数据进行缓存，并指定缓存时间。默认指定的状态码为200，301，302。

![image-20240725091005395](upload\image-20240725091005395.png)

**J、proxy_cache_use_stale http_404 http_500**
设置启用托底缓存的条件。而一旦这里指定了相应的状态码，则前面proxy_cache_calid中指定的相应状态码所生成的缓存就变为了“托底缓存”。

**K、expires 3m**
为请求的静态资源开启浏览器端的缓存。

**（3） Nginx变量**
**A、自定义变量**
由于Nginx配置文件是perl脚本，所以其是可以使用如下方式自定义变量的。

![image-20240725091040575](upload\image-20240725091040575.png)

B、内置变量
Nginx中已经内置定义了很多变量，这些变量的意义如下：

|                                                              |
| ------------------------------------------------------------ |
| $args 请求中的参数;<br/>$binary_remote_addr 远程地址的二进制表示<br/>$body_bytes_sent 已发送的消息体字节数<br/>$content_length HTTP请求信息里的"Content-Length"<br/>$content_type 请求信息里的"Content-Type"<br/>$document_root 针对当前请求的根路径设置值<br/>$document_uri 与$uri相同<br/>$host 请求信息中的"Host"，如果请求中没有Host行，则等于设置的服务器名;<br/>$http_cookie cookie 信息<br/>$http_referer 来源地址<br/>$http_user_agent 客户端代理信息<br/>$http_via 最后一个访问服务器的Ip地址<br/>$http_x_forwarded_for 相当于网络访问路径。<br/>$limit_rate 对连接速率的限制<br/>$remote_addr 客户端地址<br/>$remote_port 客户端端口号<br/>$remote_user 客户端用户名，认证用<br/>$request 用户请求信息 <br/> $request_body 用户请求主体<br/>$request_body_file 发往后端的本地文件名称<br/>$request_filename 当前请求的文件路径名<br/>$request_method 请求的方法，比如"GET"、"POST"等<br/>$request_uri 请求的URI，带参数<br/>$server_addr 服务器地址，如果没有用listen指明服务器地址，使用这个变量将发起一次系统调用以取得地址(造成资源浪费)<br/>$server_name 请求到达的服务器名<br/>$server_port 请求到达的服务器端口号<br/>$server_protocol 请求的协议版本，"HTTP/1.0"或"HTTP/1.1"<br/>$uri 请求的URI，可能和最初的值有不同，比如经过重定向之类的 |

### 2.3Nginx日志管理及自动切割

对于程序员、运维来说，日志非常得重要。通过日志可以查看到很多请求访问信息，及异常信息。Nginx也提供了对日志的强大支持。

#### 2.3.1 日志管理范围

首先，下面要讲的这些日志相关属性可以配置在任意模块。在不同的模块，记录的是不同请求的日志信息。即，日志记录的请求范围是不同的。Nginx日志一般可以指定三个范围：http{}模块范围、server{}模块范围，与location{}模块范围。

**（1） http{}模块范围**
只要有请求通过http协议访问该Nginx，就会有日志信息写入到这里的日志文件。

![image-20240725091335074](upload\image-20240725091335074.png)

**（2） server{}模块范围**
只要有请求访问当前Server，就会有日志信息写入到这里的日志文件。

![image-20240725091348413](upload\image-20240725091348413.png)

**（3） location{}模拟范围**
只要有请求访问当前location，就会有日志信息写入到这里的日志文件。

![image-20240725091401529](upload\image-20240725091401529.png)

#### 2.3.2 日志管理指令

下面以http{}模块下的日志为例来学习Nginx日志管理指令。

![image-20240725091420301](upload\image-20240725091420301.png)

Nginx的日志分为两类：访问日志与错误日志。Nginx整个系统的默认日志在生成预编译文件makefile时就已经默认给配置好了。当然，无论是访问日志还是错误日志，其默认路径与名称在nginx.conf中均是可以修改的。在配置文件中不仅定义了日志文件的路径及名称，还定义了日志格式。

![image-20240725091432713](upload\image-20240725091432713.png)

**（1） log_format**

![image-20240725091445691](upload\image-20240725091445691.png)

用于设置访问日志的格式，其后的main是为该格式所起的名称，可以任意，而其后面的内容则为具体格式，通过Nginx内置变量定义。

- $remote_addr：获取访问者的IP地址。若当前Nginx是反代服务器，则此变量获取到的就是客户端的IP地址；若当前Nginx是静态代理服务器，则此变量获取到的是反代服务器的IP地址。
-  $http_x_forwarded_for：获取客户端浏览器的IP。若当前Nginx是反代服务器，则此变量获取到的值为杠(-)。若当前Nginx是静态代理服务器，则此变量获取到的是客户端的IP地址。
-  $remote_user：获取访问者的用户名。
- $time_local：获取请求访问的时间与时区。
- $request：获取请求的相关信息，包含请求方式、请求的URI，及访问协议。
- $status：后端服务器向其返回的状态码，例如200。
- $body_bytes_sent：后端服务器向客户端发送的响应体内容字节数。
- $http_referer：获取当前请求是从哪个页面过来的。其值在这里显示为杠(-)。
- $http_user_agent：用户所使用的代理，一般为浏览器。

**（2） access_log**

![image-20240725091543835](upload\image-20240725091543835.png)

- 该指令用于设置访问日志。上面的格式包含三个参数：
-  第一个参数是日志的存放路径与日志文件名；
-  第二个参数是日志格式名；
-  第三个参数是日志文件所使用的缓存。不过，即使不指定buffer，其也会存在默认日志缓存的。
  access_log还可以跟一个参数off，用于关闭访问日志，即直接写access_log off即可关闭访问日志。

**（3） error_log**

![image-20240725092207124](upload\image-20240725092207124.png)

该指令用于指定错误日志的路径与文件名。需要注意以下几点：

- 其不能指定格式，因为其有默认格式。
- 可以使用自己指定的错误日志文件，不过，将来的访问异常日志就不会再写入到默认的logs/error.log文件中了。所以关于错误日志，一般使用默认的即可。
- 错误日志级别由低到高有：[debug | info | notice | warn | error | crit | alert | emerg]，默认为error，级别越高记录的信息越少。
- 错误日志默认是开启的。关闭错误日志的写法为 error_log /dev/null;

**（4） open_log_file_cache**

![image-20240725092317476](upload\image-20240725092317476.png)

该指令用于打开日志文件读缓存，将日志信息读取到缓存中，以加快对日志的访问。该功能默认为off，即open_log_file_cache off;

#### 2.3.3 默认的/favicon.ico请求

客户端对于服务端页面会自动提交一个/favicon.ico请求，若没有favicon.ico文件则会在日志文件中报出404。
从网上任意下载一个ico图标，将其重命名为favicon.ico，然后放到Linux中的任意目录。然后再修改nginx.conf文件，在其中添加如下的location{}模块。注意，若将其添加到的位置与页面在同一个目录，下面的location{}模块不用设置。

![image-20240725092335973](upload\image-20240725092335973.png)

#### 2.3.4 日志自动切割

这里仅仅简单介绍一下日志切割的实现步骤，具体实现，网上非常多，用时再查即可。

**（1） 创建切割shell脚本文件**
在Linux下创建一个实现日志切割的shell脚本文件，脚本文件的具体内容可以从网上查找，资源很多。例如，将该shell文件创建在Nginx安装目录下的logs目录中，并命名为cut_nginx_log.sh。

**（2） 为该文件添加可执行权限**
该文件是要作为定时任务被执行的，所以该文件需要具有可执行权限。
**（3） 向crontab中添加一个定时任务**
crontab是Linux中的一个定义任务文件，每一行都代表一项定义任务。每行由6个字段组成，前5段是时间设定段，第6段是任务段。具体格式如下：
minute(0-59) hour(0-23) day(1-31) month(1-12) week(0-6) command
本例执行如下命令后会打开文本编辑器，然后再输入如下文本内容即可。

![image-20240725092412739](upload\image-20240725092412739.png)

![image-20240725092416342](upload\image-20240725092416342.png)

### 2.4静态代理

Nginx静态代理是指，将所有的静态资源，例如，css、js、html、jpg等资源存放到Nginx服务器，而不存放在应用服务器Tomcat中。当客户端发出的请求是对这些静态资源的请求时，Nginx直接将这些静态资源响应给客户端，而无需提交给应用服务器处理。这样就减轻了应用服务器的压力。

#### 2.4.1 扩展名拦截

**（1） 修改配置文件**

![image-20240725092448407](upload\image-20240725092448407.png)

**（2） 创建目录**
在/opt目录中创建statics目录。

![image-20240725092500021](upload\image-20240725092500021.png)

在/opt/statics目录中创建css、js、images目录。

![image-20240725092515143](upload\image-20240725092515143.png)

**（3） 上传图片**
向/opt/statics/images目录中上传一个图片car.jpg。
**（4） 重启Nginx**

![image-20240725092527527](upload\image-20240725092527527.png)

**（5） 浏览器访问**

![image-20240725092538649](upload\image-20240725092538649.png)

#### 2.4.2 目录名拦截

**（1） 修改配置文件**

![image-20240725092559531](upload\image-20240725092559531.png)

**（2） 重启Nginx**

![image-20240725092609144](upload\image-20240725092609144.png)

**（3） 浏览器访问**

![image-20240725092620297](upload\image-20240725092620297.png)

#### 2.4.3 页面压缩

**（1） 浏览器常见的压缩协议**

浏览器中最常见的压缩算法有：

- deflate：是一种过时的压缩算法，是huffman编码的一种加强。
-  gzip：是目前大多数浏览器都支持的一种压缩算法，是对deflate的改进。
-  sdch：谷歌开发的一种压缩算法，一种全新的压缩思路。deflate与gzip的的压缩思想是，修改传输数据的编码格式以达到减少体量的目的，其最终传输的数据并没有减少。而sdch压缩算法的思想是，让冗余的数据仅出现一次，其最终传输的数据减少了。
- Zopfli：谷歌开发的一种压缩算法，Deflate 压缩算法的改进。比标准的gzip -9要小 3%-8%，但压缩用时是gzip -9的80多倍。
-  br：即Brotli，谷歌开发的一种压缩算法，是一种全新的数据格式。与Zopfli相比，压缩率能够降低20%-26%。Brotli -1有着与Gzip -9相近的压缩比和更快的压缩解压速度。

**（2） 常用设置**

![image-20240725092707482](upload\image-20240725092707482.png)

**A、gzip on;**
开启gzip压缩，默认为off。
**B、gzip_min_length 5k;**
指定最小启用压缩的文件大小。

**C、gzip_comp_level 4;**
指定压缩级别，取值为1-9，数字越大，压缩比越高，但压缩所用时间会越长。默认为1，建议使用4。
**D、gzip_buffers 4 16k;**
“4”表示的是缓存颗粒数量，而“16k”表示的是缓存颗粒大小。
**E、gzip_vary on;**
开启动态压缩。默认值off。
**F、gzip_types mimeType;**

![image-20240725092736010](upload\image-20240725092736010.png)

通过MIME类型来指定要压缩的文件类型。默认值text/html。

### 2.5反向代理

通过在location{}中添加通行代理proxy_pass可以指定当前Nginx所要代理的真正服务器。

#### 2.5.1 反向代理tomcat服务器

**（1） 定义一个web工程**
定义一个Maven Web工程，并命名为webdemo。其包含一个JSP页面，及一个Servlet。

**A、修改pom.xml**

```java

<properties> 
<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding> <maven.compiler.source>1.8</maven.compiler.source> <maven.compiler.target>1.8</maven.compiler.target> 
</properties> 
<dependencies>
<!-- Servlet依赖 -->
	<dependency> 
        <groupId>javax.servlet</groupId> 
        <artifactId>javax.servlet-api</artifactId> 
        <version>3.1.0</version> 
        <scope>provided</scope> 
    </dependency> 
    <!-- JSP依赖 -->
    <dependency> 
        <groupId>javax.servlet.jsp</groupId>
        <artifactId>javax.servlet.jsp-api</artifactId> 
        <version>2.2.1</version>
        <scope>provided</scope> 
    </dependency> 
 </dependencies>
```

**B、定义index.jsp**

```
<%@ page contentType="text/html;charset=UTF-8"%>
<html>
<head>
<title>webdemo</title>
</head>
<body>
	Nginx World Welcome You!
	<br> Nginx Addr = ${pageContext.request.remoteAddr}
	<br> Tomcat Addr = ${pageContext.request.localAddr}
	<br>
</body>
</html>
```

**C、定义SomServlet**

```
@WebServlet("/some")
public class SomeServlet extends HttpServlet {
	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		PrintWriter writer = response.getWriter();
		writer.println("NginxIp = " + request.getRemoteAddr());
		writer.println("TomcatIp = " + request.getLocalAddr());
	}
}
```

**（2） 克隆一台Tomcat并部署工程**
克隆一台Tomcat主机，将webdemo工程打包后部署到Tomcat的webapps/ROOT目录中。当然，需要首先将ROOT目录中的文件全部删除。
**（3） 修改Nginx配置文件**

![image-20240725093334536](upload\image-20240725093334536.png)

**（4） 访问**
通过Nginx反向代理访问Tomcat主机的index.jsp页面。

![image-20240725093348482](upload\image-20240725093348482.png)

通过Nginx反向代理访问Tomcat主机的SomeServlet。

![image-20240725093403359](upload\image-20240725093403359.png)

#### 2.5.2 反向代理的属性设置

**（1） client_max_body_size 100k;**
Nginx允许客户端请求的单文件最大大小，单位字节。
**（2） client_body_buffer_size 80k;**
Nginx为客户端请求设置的缓存大小。
**（3） proxy_buffering on**

开启从后端被代理服务器的响应内容缓冲区。默认值on。
**（4） proxy_buffers 4 8k;**
该指令用于设置缓冲区的数量与大小。从被代理的后端服务器取得的响应内容，会缓存到这里。
**（5） proxy_busy_buffers_size 16k;**
高负荷下缓存大小，其默认值为一般为单个proxy_buffers的2倍。

**（6） proxy_connect_timeout 60s;**
Nginx跟后端服务器连接超时时间。默认60秒。
**（7） proxy_read_timeout 60s;**
Nginx发出请求后等待后端服务器响应的最长时限。默认60秒。

### 2.6负载均衡

#### 2.6.1 负载均衡简介

负载均衡，Load Balancing，就是将对请求的处理分摊到多个操作单元上进行。

#### 2.6.2 负载均衡分类

**（1） 软硬件分类**
**A、硬件负载均衡**
硬件负载均衡器的性能稳定，且有生产厂商作为专业的服务团队。但其成本很高，一台硬件负载均衡器的价格一般都在十几万到几十万，甚至上百万。知名的负载均衡器有F5、Array、深信服、梭子鱼等。

![image-20240725094050099](upload\image-20240725094050099.png)

**B、软件负载均衡**
软件负载均衡成本几乎为零，基本都是开源软件。例如，LVS、HAProxy、Nginx等。

**（2） 负载均衡工作层分类**
负载均衡就其所工作的OSI层次，在生产应用层面分为两类：七层负载均衡与四层负载均衡。当然，为四层负载均衡提供更为底层实现的，还有三层负载均衡与二层负载均衡。

- 七层负载均衡：应用层，基于HTTP协议，通过虚拟URL将请求分配到真实服务器。一般应用于B/S架构系统。Nginx就是七层负载均衡。
-  四层负载均衡：传输层，基于TCP协议，通过“虚拟IP + 端口号” 将请求分配到真实服务器。一般应用于C /S架构系统。例如，LVS、F5、Nginx Plus都属于四层负载均衡。
-  三层负载均衡：网络层，基于IP协议，通过虚拟IP将请求分配到真实服务器。
- 二层负载均衡：链路层，基于虚拟MAC地址将请求分配到真实服务器。

#### 2.6.3 负载均衡的实现

**（1） 总体规划**
该机群包含一台Nginx服务器，两台Tomcat服务器。将前面打过包的web工程直接部署到两台Tomcat主机上。然后，在Nginx服务器上设置对这两台Tomcat主机的负载均衡。
**（2） 配置Nginx主机**
**A、修改Nginx主机的hosts文件**

![image-20240725094402528](upload\image-20240725094402528.png)

**B、修改Nginx配置文件**

![image-20240725094414446](upload\image-20240725094414446.png)

#### 2.6.4 Nginx负载均衡策略

Nginx内置了三种负载均衡策略，另外，其还支持第三方的负载均衡。而每种负载均衡主机根据负载均衡策略的不同，又可设置很多性能相关的属性。

**（1） 轮询**
默认的负载均衡策略，其是按照各个主机的权重比例依次进行请求分配的。

![image-20240725094436619](upload\image-20240725094436619.png)

- backup：表示当前服务器为备用服务器。
- down：表示当前服务器永久停机。
- fail_ timeout：表示当前主机被Nginx认定为停机的最长失联时间，默认为10秒。常与max_fails联合使用。
  max_fails：表示在fail_timeout时间内最多允许的失败次数。

**（2） ip_hash**
指定负载均衡器按照基于客户端IP的分配方式。

![image-20240725094523080](upload\image-20240725094523080.png)

对于该策略需要注意以下几点：

-  在nginx1.3.1版本之前，该策略中不能指定weight属性。
-  该策略不能与backup同时使用。
-  此策略适合有状态服务，比如session。
-  当有服务器宕机，必须手动指定down属性，否则请求仍是会落到该服务器。

**（3） least_conn**
把请求转发给连接数最少的服务器。

![image-20240725094616208](upload\image-20240725094616208.png)

#### 2.6.5 Nginx Plux的四层负载均衡实现

同样是修改nginx.conf文件，添加一个stream模块，其与events、http等模块同级。在其中配置upstream{}与server{}模块。此时需要注意，通行代理配置在server{}中（前面的是配置在server模块的location模块中），且不能再是http://开头的了，因为其负载均衡协议不再是HTTP协议了。

![image-20240725094703058](upload\image-20240725094703058.png)

### 2.7动静分离

#### 2.7.1 Nginx动静分离的实现

下面要搭建的Nginx环境中有三台Nginx主机：一台用于完成负载均衡，两台用于存放项目中的静态资源。另外，还包含前面的两台Tomcat主机。
**（1） 修改前面的web工程**
在前面的web工程的jsp页面中添加一个背景图片，无需在工程中添加images目录及bj.jpg图片。因为这些都是要存放在Nginx静态代理服务器的。

![image-20240725094727417](upload\image-20240725094727417.png)

**（2） 复制并配置一台Nginx服务器**

**A、修改nginx.conf**

![image-20240725094751122](upload\image-20240725094751122.png)

**B、添加静态资源**
在/opt/statics下创建images目录，并将bj.jpg存放到该目录。

![image-20240725094803666](upload\image-20240725094803666.png)

**（3） 再复制一台Nginx服务器**

以nginxOS1为母机，再复制一台Nginx主机，并命名为nginxOS2。完成以下配置：

- 修改主机名：/etc/hostname
- 修改网络配置：/etc/sysconfig/network-scripts/ifcfg-ens33

**（4） 修改负载均衡Nginx主机**
在nginxOS主机的nginx.conf文件中添加静态代理的负载均衡配置。

![image-20240725094841354](upload\image-20240725094841354.png)

#### 2.7.2 项目的启动

**（1） 启动两台Tomcat服务器**

![image-20240725094902917](upload\image-20240725094902917.png)	



![image-20240725094907764](upload\image-20240725094907764.png)

**（2） 启动两台Nginx静态代理服务器**

![image-20240725094939990](upload\image-20240725094939990.png)

![image-20240725094943236](upload\image-20240725094943236.png)

**![image-20240725094955145](upload\image-20240725094955145.png)**

### 2.8虚拟主机

#### 2.8.1 总体规划

现在很多生活服务类网络平台都具有这样的功能：不同城市的用户可以打开不同城市专属的站点。用户首先打开的是平台总的站点，然后允许用户切换到不同的城市。其实，不同的城市都是一个不同的站点。
这里我们要实现的功能是为平台总站点，北京、上海两个城市站点分别创建一个虚拟主机。每一个虚拟主机都具有两台Tomcat的负载均衡主机。由于有三个站点，所以共需六台Tomcat主机，克隆Tomcat主机太过麻烦，所以这六台Tomcat我们使用一台主机实现。在一台主机中安装六个Tomcat，它们分别使用六个不同的端口号。
首先要创建一个web工程，其中就一个index.jsp页面，页面除了显示当前城市外，还要显示城市切换的超链接。为了能够再明显的区分出当前访问的Tomcat，再在页面中显示出当前工程所在的主机名与端口号。

#### 2.8.2 创建三个web工程

直接复制前面的web工程，每个工程都仅需一个JSP即可。最终打为三个war包。三个工程的JSP页面内容各不相同。

![image-20240725095138440](upload\image-20240725095138440.png)

**（1） 总站**
注意，JSP文件的EL中通过request获取的是localAddr与localPort。

```
<%@ page contentType="text/html;charset=UTF-8"%>
<html>
<head>
<title>entry68</title>
</head>
<body>
	这是68平台总站
	<br> 站点切换：
	<a href="http://bj.68.com">北京</a>
	<a href="http://sh.68.com">上海</a>
	<br>
	<hr>
	Tomcat Addr = ${pageContext.request.localAddr}
	<br> Tomcat Port = ${pageContext.request.localPort}
	<br>
</body>
</html>
```

**（2） 北京站**

```
<%@ page contentType="text/html;charset=UTF-8"%>
<html>
<head>
<title>bj68</title>
</head>
<body>
	这是68平台【北京】站
	<br> 站点切换：
	<a href="http://www.68.com">总站</a>
	<a href="http://sh.68.com">上海</a>
	<br>
	<hr>
	Tomcat Addr = ${pageContext.request.localAddr}
	<br> Tomcat Port = ${pageContext.request.localPort}
	<br>
</body>
</html>
```

**（3） 上海站**

```
<%@ page contentType="text/html;charset=UTF-8"%>
<html>
<head>
<title>sh68</title>
</head>
<body>
	这是68平台【上海】站
	<br> 站点切换：
	<a href="http://www.68.com">总站</a>
	<a href="http://bj.68.com">北京</a>
	<br>
	<hr>
	Tomcat Addr = ${pageContext.request.localAddr}
	<br> Tomcat Port = ${pageContext.request.localPort}
	<br>
</body>
</html>
```

#### 2.8.3 修改hosts文件

![image-20240725095321480](upload\image-20240725095321480.png)

#### 2.8.4 配置Tomcat主机

**（1） 项目部署规划**

![image-20240725095340637](upload\image-20240725095340637.png)

第一、二台Tomcat中部署着entry68.war包；
第三、四台Tomcat中部署着bj68.war包；
第五、六台Tomcat中部署着sh68.war包。

**（2） 配置Tomcat主机**
打开Tomcat安装目录下的conf/server.xml文件，修改三处端口号。

![image-20240725095403529](upload\image-20240725095403529.png)

![image-20240725095407961](upload\image-20240725095407961.png)

![image-20240725095415194](upload\image-20240725095415194.png)

#### 2.8.5 配置虚拟主机

**（1） 直接配置到nginx.conf中**
修改nginx的核心配置文件，在其中添加如下内容：

![image-20240725095437723](upload\image-20240725095437723.png)



![image-20240725095443356](upload\image-20240725095443356.png)

**（2） 单独配置到一个文件**
**A、定义vhosts.conf文件**

![image-20240725095507567](upload\image-20240725095507567.png)

**B、修改nginx.conf文件**

![image-20240725095541995](upload\image-20240725095541995.png)