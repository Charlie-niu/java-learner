## **二、使用**

**1. 安装**

Redis官方网址是：http://redis.io/ 源码地址：https://github.com/antirez/redis

由于采用ANSI C编写，Redis官方支持POSIX类型系统如linux等，Windows环境下有第三方的移植程序，在本次教学中主要在windows环境下使用。Windows版本下载地址https://github.com/MSOpenTech/redis/releases

linux系统下 : 

```shell
wget http://download.redis.io/redis-stable.tar.gz
tar xzf redis-stable.tar.gz
cd redis-stable
make      
```

编译后在redis源代码目录的src文件夹中可以找到若干个可执行程序，可直接执行make install命令来将这些可执行程序复制到/usr/local/bin 目录中。

windows系统下 : 

从上文中的地址下载zip压缩包，解压之后（最好在某个盘符中直接解压，如果有父级目录不要出现中文字符），文件夹中有若干个可执行程序，如下所示

 ![img](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image004.jpg)

- redis-server    redis 服务器
- redis-cli        redis 命令行客户端
- redis-benchmar     redis 性能测试工具
- redis-check-aof     AOF 文件修复工具
- redis-check-dump   RDB 文件检查工具



**2. 启动**

在commander中运行redis-server.exe

![img](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image006.jpg)

由于没有添加配置文件所以会有一个使用默认配置的警告，默认端口号为6379，第一次启动时不会有DB loaded from disk的提示。此窗口不要关闭，如果关闭redis-server就会停止运行。



重新打开一个commander运行redis-cli.exe

![img](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image008.jpg)

默认连接的端口号为6379，下面就可以体验简单的命令操作

![img](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image010.jpg)

 

在redis-cli中使用shutdown命令关闭服务端，不要直接关闭服务端窗口（因为需要将内存中的数据保存到硬盘中）。

![img](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image012.jpg)



**3. 配置**

前面我们启动时没有指定配置文件，一般情况下，我们需要指定配置文件启动。在主目录下，有个redis.windows.conf配置文件模板。

模板文件里的配置参数有详细的解释说明，下面是几个常用参数：

daemonize 缺省是no, 一般使用改为yes,这样启动redis-server时自动是后台运行方式。

port 6379 指定端口号，可以调整自己需要的端口值。

tcp-backlog 511 这个值就是前面需要调整somaxconn值的原因，它涉及到TCP连接时accept queue队列的大小，是取它们的最小值。这个参数和redis高并发处理请求密切相关，根据实际运行情况调整。

bind 只接受来自某IP的请求，安全考虑，缺省不限制。

tcp-keepalive 60 主动检测客户端连接是否正常，官方建议是60s

loglevel notice 定义日志级别
 logfile "" 定义日志文件位置

save 900 1 存储数据到硬盘策略，这条定义的是900s内如有1个key值发生变化，就执行save存数据快照到硬盘操作。

dbfilename dump.rdb 指定数据快照文件名
 dir ./ 指定数据快照文件目录

调整好参数后，我们用redis-server.exe redis.windows.conf命令启动即可。
