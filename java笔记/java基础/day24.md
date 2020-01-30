一、要想实现网络通信，需要解决两个问题：

​       1.如何准确的定位互联网上的一台或多台主机

​       2.如何实现可靠而高效的数据传输

 二、网络通信的两个要素：

​      1.使用IP地址，定位网络中的主机

​      2.遵循相关的网络通信协议

 三、针对要素一：

​      1.IP：一个ip地址，对应着网络中的一台主机。 "192.168.20.16"   "127.0.0.1"--本地回路地址

​                使用InetAddress类来代表IP，一个InetAddress类的对象，就代表着一个具体的ip地址。

​      2.如何实例化InetAddress:

​           ①getByName(String hostName)

​           ②getLocalHost()

​      3.域名： www.baidu.com   www.jd.com   www.mi.com  www.vip.com

​                      www.facebook.com

​         localhost对应着127.0.0.1

​      4.InetAddress类的常用方法：getHostName() / getHostAddress()

​      5.端口号标识正在计算机上运行的进程（程序）

​           注意：不同的进程有不同的端口号

​           常见的端口号： http:80   tomcat : 8080   mysql：3306  oracle:1521等