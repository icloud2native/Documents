# 1 Web架构介绍

![image-20240930091906348](images/image-20240930091906348.png)

# 2 HAProxy 简介

负载均衡：Load Balance，简称 LB，是一种服务或基于硬件设备等实现的高可用反向代理技术，负载 均衡将特定的业务(web服务、网络流量等)分担给指定的一个或多个后端特定的服务器或设备，从而提高 了公司业务的并发处理能力、保证了业务的高可用性、方便了业务后期的水平动态扩展

阿里云SLB介绍 ：https://yq.aliyun.com/articles/1803

![image-20240930092028997](images/image-20240930092028997.png)

## 2.1 为什么使用负载均衡

- 增加业务并发访问及处理能力-->解决单服务器瓶颈问题
- 节约公网IP地址-->降低IT支出成本
- 隐藏内部服务器IP-->提高内部服务器安全性
- Web服务器的动态水平扩展-->对用户无感知
- 负载均衡配置简单-->固定格式的配置文件
- 负载均衡功能丰富-->支持四层和七层，支持动态下线主机
- 负载均衡性能较强-->并发数万甚至百万

## 2.2 负载均衡类型

四层：

```http
LVS：Linux Virtual Server
Nginx：1.9版之后   stream 
HAProxy：High Availability Proxy mode tcp
```

七层：

```http
HAProxy mode http
nginx http
```

硬件：

````http
F5       https://f5.com/zh
Netscaler https://www.citrix.com.cn/products/citrix-adc/
Array     https://www.arraynetworks.com.cn/
深信服       http://www.sangfor.com.cn/
北京灵州     http://www.lingzhou.com.cn/cpzx/llfzjh/
````

## 2.3 应用场景

```http
四层：Redis、Mysql、RabbitMQ、Memcached等
七层：Nginx、Tomcat、Apache、PHP、图片、动静分离、API等
```

随着公司业务的发展，公司负载均衡服务既有四层的，又有七层的，通过LVS实现四层和Nginx实现七层 的负载均衡对机器资源消耗比较大，并且管理复杂度提升，运维总监要求，目前需要对前端负载均衡服 务进行一定的优化和复用，能否用一种服务同既能实现七层负载均衡，又能实现四层负载均衡，并且性 能高效，配置管理容易，而且还是开源。

在企业生产环境中，每天会有很多的需求变更，比如增加服务器、新业务上线、url路由修改、域名配置 等等，对于前端负载均衡设备来说，容易维护，复杂度低，是首选指标。在企业中，稳定压倒一切，与 其搞得很复杂，经常出问题，不如做的简单和稳定。在企业中，90%以上的故障，来源于需求变更。可 能是程序bug，也可能是人为故障，也可能是架构设计问题等。前端负载均衡设备为重中之重，在软件 选型上一定充分考虑，能满足业务的前提下，尽可能降低复杂度，提高易维护性

## 2.4 HAProxy介绍

```http
HAProxy is a free, very fast and reliable solution offering high availability, 
load balancing, and proxying for TCP and HTTP-based applications.
```

![image-20240930093114527](images/image-20240930093114527.png)

HAProxy是法国开发者 威利塔罗(Willy Tarreau) 在2000年使用C语言开发的一个开源软件，是一款具 备高并发(一万以上)、高性能的TCP和HTTP负载均衡器，支持基于cookie的持久性，自动故障切换，支 持正则表达式及web状态统计

**历史版本**

![image-20240930093330108](images/image-20240930093330108.png)

注意：生产建议下载LTS版本，一般为版本号以偶数尾号，比如：1.8,2.0, 2.4, 2.6 等

从2013年HAProxy 分为社区版和企业版，企业版将提供更多的特性和功能以及全天24小时的技术支持 等服务。

### 2.4.1 企业版

企业版网址：https://www.haproxy.com/

![image-20240930093651994](images/image-20240930093651994.png)

### 2.4.2 社区版

![image-20240930093740601](images/image-20240930093740601.png)



社区版网站：http://www.haproxy.org/

github：https://github.com/haproxy

![image-20240930093836336](images/image-20240930093836336.png)

### 2.4.3 版本对比

| 功能                                      | 社区版 | 企业版 |
| ----------------------------------------- | ------ | ------ |
| 高级HTTP / TCP负载平衡和持久性            | 支持   | 支持   |
| 高级健康检查                              | 支持   | 支持   |
| 应用程序加速                              | 支持   | 支持   |
| 高级安全特性                              | 支持   | 支持   |
| 高级管理                                  | 支持   | 支持   |
| HAProxy Dev Branch新功能                  |        | 支持   |
| 24*7 支持服务                             |        | 支持   |
| 实时仪表盘                                |        | 支持   |
| VRRP和Route Health Injection HA工具       |        | 支持   |
| ACL，映射和TLS票证密钥同步                |        | 支持   |
| 基于应用程序的高级DDoS和Bot保护(自动保护) |        | 支持   |
| Bot(机器人)监测                           |        | 支持   |
| Web应用防火墙                             |        | 支持   |
| HTTP协议验证                              |        | 支持   |
| 实时集群追踪                              |        | 支持   |

### 2.4.4 HAProxy功能

![image-20240930094408003](images/image-20240930094408003.png)

**支持功能**

```http
TCP 和 HTTP反向代理
SSL/TSL服务器
可以针对HTTP请求添加cookie，进行路由后端服务器
可平衡负载至后端服务器，并支持持久连接
支持所有主服务器故障切换至备用服务器
支持专用端口实现监控服务
支持停止接受新连接请求，而不影响现有连接
可以在双向添加，修改或删除HTTP报文首部
响应报文压缩
支持基于pattern实现连接请求的访问控制
通过特定的URI为授权用户提供详细的状态信息
```

![image-20240930094510478](images/image-20240930094510478.png)

```http
支持http反向代理
支持动态程序的反向代理
支持基于数据库的反向代理
```

**不具备的功能：**

```http
正向代理--squid，nginx
缓存代理--varnish
web服务--nginx、tengine、apache、php、tomcat
UDP--目前不支持UDP协议
单机性能--相比LVS性能较差
```

# 3 HAProxy 安装

**介绍HAProxy的基础安装及基础配置**

![image-20240930094713158](images/image-20240930094713158.png)

内网IP地址划分：

```bash
#外部网段：
192.168.10.0/24

#内部网段：
10.0.0.0/24
```

## 3.1 Ubuntu 包安装

![image-20240930104334135](images/image-20240930104334135.png)

打开链接： https://haproxy.debian.net/ ，选择合适的版本，会自动出现下面安装提示

![image-20240930104415477](images/image-20240930104415477.png)

范例：

```bash
root@ubutun2204-1:~# apt-get install --no-install-recommends software-properties-common

root@ubutun2204-1:~# add-apt-repository ppa:vbernat/haproxy-3.0
root@ubutun2204-1:~# apt update

root@ubutun2204-1:~# apt-get install haproxy=3.0.\*
root@ubutun2204-1:~# haproxy -v
HAProxy version 3.0.5-1ppa1~jammy 2024/09/21 - https://haproxy.org/
Status: long-term supported branch - will stop receiving fixes around Q2 2029.
Known bugs: http://www.haproxy.org/bugs/bugs-3.0.5.html
Running on: Linux 5.15.0-112-generic #122-Ubuntu SMP Thu May 23 07:48:21 UTC 2024 x86_64

# 查看历史版本
root@ubutun2204-1:~# apt-cache madison haproxy
   haproxy | 3.0.5-1ppa1~jammy | https://ppa.launchpadcontent.net/vbernat/haproxy-3.0/ubuntu jammy/main amd64 Packages
   haproxy | 2.4.24-0ubuntu0.22.04.1 | http://cn.archive.ubuntu.com/ubuntu jammy-updates/main amd64 Packages
   haproxy | 2.4.22-0ubuntu0.22.04.3 | http://security.ubuntu.com/ubuntu jammy-security/main amd64 Packages
   haproxy | 2.4.14-1ubuntu1 | http://cn.archive.ubuntu.com/ubuntu jammy/main amd64 Packages
```

## 3.2 Ubutun编译安装 HAProxy

编译安装HAProxy 3.0 LTS版本，更多源码包下载地址：http://www.haproxy.org/download/

### 3.2.1 解决lua环境

HAProxy 支持基于lua实现功能扩展，lua是一种小巧的脚本语言，于1993年由巴西里约热内卢天主教大 学（Pontifical Catholic University of Rio de Janeiro）里的一个研究小组开发，其设计目的是为了嵌入 应用程序中，从而为应用程序提供灵活的扩展和定制功能。

Lua 官网：www.lua.org

Lua 应用场景

- 游戏开发
- 独立应用脚本
- Web应用脚本
- 扩展和数据库插件，如MYSQL Proxy
- 安全系统，如入侵检测系统

#### 3.2.1.2 Ubuntu 基础环境

Ubuntu的Lua版本较新，也可以用包安装

```bash
#安装基础命令及编译依赖环境
root@ubutun2204-1:~# apt update && apt -y install gcc make libssl-dev libpcre3 libpcre3-dev zlib1g-dev libreadline-dev libsystemd-dev

#安装Lua方法1：包安装Lua
root@ubutun2204-1:~# apt update && apt -y install liblua5.4-dev


#安装Lua方法2：编译安装Lua
[root@ubuntu1804 ~]# cd /usr/local/src
[root@ubuntu1804 ~]# wget http://www.lua.org/ftp/lua-5.3.5.tar.gz
[root@ubuntu1804 ~]# tar xvf lua-5.3.5.tar.gz
[root@ubuntu1804 ~]# cd lua-5.3.5
[root@ubuntu1804 ~]# make linux test
```

### 3.2.2 编译安装 HAProxy

范例：Ubuntu

```bash
# 安装依赖包
root@ubutun2204-1:~# apt update && apt -y install gcc make libssl-dev libpcre3 libpcre3-dev zlib1g-dev libreadline-dev libsystemd-dev liblua5.4-dev

# 下载
root@ubutun2204-1:~# wget https://www.haproxy.org/download/3.0/src/haproxy-3.0.0.tar.gz
root@ubutun2204-1:~# tar xf haproxy-3.0.0.tar.gz;cd haproxy-3.0.0/

#编译安装
root@ubutun2204-1:~/haproxy-3.0.0# make ARCH=x86_64 TARGET=linux-glibc USE_PCRE=1 USE_OPENSSL=1 USE_ZLIB=1 USE_SYSTEMD=1 USE_PROMEX=1 USE_LUA=1

root@ubutun2204-1:~/haproxy-3.0.0# make install PREFIX=/apps/haproxy

root@ubutun2204-1:~/haproxy-3.0.0# tree /apps/haproxy/
/apps/haproxy/
├── doc
│   └── haproxy
│       ├── 51Degrees-device-detection.txt
│       ├── architecture.txt
│       ├── configuration.txt
│       ├── cookie-options.txt
│       ├── DeviceAtlas-device-detection.txt
│       ├── intro.txt
│       ├── linux-syn-cookies.txt
│       ├── lua.txt
│       ├── management.txt
│       ├── netscaler-client-ip-insertion-protocol.txt
│       ├── network-namespaces.txt
│       ├── peers.txt
│       ├── peers-v2.0.txt
│       ├── proxy-protocol.txt
│       ├── regression-testing.txt
│       ├── seamless_reload.txt
│       ├── SOCKS4.protocol.txt
│       ├── SPOE.txt
│       └── WURFL-device-detection.txt
├── sbin
│   └── haproxy
└── share
    └── man
        └── man1
            └── haproxy.1
```

### 3.2.3 验证HAProxy版本

```bash
#验证HAProxy版本：
root@ubutun2204-1:~# /apps/haproxy/sbin/haproxy -v
HAProxy version 3.0.0-5590ada 2024/05/29 - https://haproxy.org/
Status: long-term supported branch - will stop receiving fixes around Q2 2029.
Known bugs: http://www.haproxy.org/bugs/bugs-3.0.0.html
Running on: Linux 5.15.0-112-generic #122-Ubuntu SMP Thu May 23 07:48:21 UTC 2024 x86_64
```

### 3.2.4 准备用户

```bash
#设置用户和目录权限
root@ubutun2204-1:~# useradd -m -r -s /sbin/nologin -d /var/lib/haproxy haproxy
root@ubutun2204-1:~# id haproxy 
uid=998(haproxy) gid=998(haproxy) groups=998(haproxy)
root@ubutun2204-1:~# chown -R haproxy.haproxy /var/lib/haproxy/
root@ubutun2204-1:~# ll /var/lib/haproxy/
total 20
drwxr-x---  2 haproxy haproxy 4096 Sep 30 03:19 ./
-rw-r--r--  1 haproxy haproxy  220 Jan  6  2022 .bash_logout
-rw-r--r--  1 haproxy haproxy 3771 Jan  6  2022 .bashrc
-rw-r--r--  1 haproxy haproxy  807 Jan  6  2022 .profile

```

### 3.2.5 配置文件

haproxy.cfg文件中定义了chroot、pidfile、user、group等参数，如果系统没有相应的资源会导致 haproxy无法启动，具体参考日志文件 /var/log/messages

```bash
#查看配置文件范例
root@ubutun2204-1:~/haproxy-3.0.0/examples# tree /root/haproxy-3.0.0/examples
/root/haproxy-3.0.0/examples
├── basic-config-edge.cfg
├── content-sw-sample.cfg
├── errorfiles
│   ├── 400.http
│   ├── 403.http
│   ├── 408.http
│   ├── 500.http
│   ├── 502.http
│   ├── 503.http
│   ├── 504.http
│   └── README
├── haproxy.init
├── lua
│   ├── event_handler.lua
│   ├── mailers.lua
│   └── README
├── option-http_proxy.cfg
├── quick-test.cfg
├── socks4.cfg
├── transparent_proxy.cfg
└── wurfl-example.cfg

2 directories, 19 files

#创建自定义的配置文件
root@ubutun2204-1:~#  mkdir /etc/haproxy
root@ubutun2204-1:~# cat /etc/haproxy/haproxy.cfg 
global
   maxconn 100000
   chroot /apps/haproxy
   stats socket /var/lib/haproxy/haproxy.sock mode 600 level admin
   #uid 99
   #gid 99
   user haproxy
   group haproxy
   daemon
   #nbproc 4
   #cpu-map 1 0
   #cpu-map 2 1
   #cpu-map 3 2
   #cpu-map 4 3
   #pidfile /var/lib/haproxy/haproxy.pid
   log 127.0.0.1 local2 info
defaults
   option http-keep-alive
   option forwardfor
   maxconn 100000
   mode http
   timeout connect 300000ms
   timeout client 300000ms
   timeout server 300000ms
listen stats
   mode http
   bind 0.0.0.0:9999
   stats enable
   log global
   stats uri    /haproxy-status
   stats auth   admin:123456

# 检查配置文件语法
root@ubutun2204-1:~# ln -sv /apps/haproxy/sbin/haproxy /usr/local/bin/haproxy
'/usr/local/bin/haproxy' -> '/apps/haproxy/sbin/haproxy'

root@ubutun2204-1:~# haproxy -c -f /etc/haproxy/haproxy.cfg
```

### 3.2.6 准备HAProxy启动文件

```bash
#默认如果缺少配置文件，无法启动
root@ubutun2204-1:~# systemctl daemon-reload
root@ubutun2204-1:~# systemctl start haproxy
Failed to start haproxy.service: Unit haproxy.service not found.


#创建service文件
root@ubutun2204-1:~# cat  /lib/systemd/system/haproxy.service 
[Unit]
Description=HAProxy Load Balancer
After=syslog.target network.target

[Service]
ExecStartPre=/apps/haproxy/sbin/haproxy -f /etc/haproxy/haproxy.cfg  -c -q
ExecStart=/apps/haproxy/sbin/haproxy -Ws -f /etc/haproxy/haproxy.cfg -p /var/lib/haproxy/haproxy.pid
ExecReload=/bin/kill -USR2 $MAINPID

[Install]
WantedBy=multi-user.target
```

### 3.2.7 启动haproxy

```bash
root@ubutun2204-1:~# systemctl daemon-reload
root@ubutun2204-1:~# systemctl restart haproxy
root@ubutun2204-1:~# systemctl status haproxy
● haproxy.service - HAProxy Load Balancer
     Loaded: loaded (/lib/systemd/system/haproxy.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2024-09-30 03:53:35 UTC; 3s ago
    Process: 6490 ExecStartPre=/apps/haproxy/sbin/haproxy -f /etc/haproxy/haproxy.cfg -c -q (code=exited, status=0/SUCCESS)
   Main PID: 6492 (haproxy)
      Tasks: 3 (limit: 2176)
     Memory: 19.6M
        CPU: 88ms
     CGroup: /system.slice/haproxy.service
             ├─6492 /apps/haproxy/sbin/haproxy -Ws -f /etc/haproxy/haproxy.cfg -p /var/lib/haproxy/haproxy.pid
             └─6494 /apps/haproxy/sbin/haproxy -Ws -f /etc/haproxy/haproxy.cfg -p /var/lib/haproxy/haproxy.pid

Sep 30 03:53:35 ubutun2204-1 systemd[1]: Starting HAProxy Load Balancer...
Sep 30 03:53:35 ubutun2204-1 systemd[1]: Started HAProxy Load Balancer.
Sep 30 03:53:35 ubutun2204-1 haproxy[6492]: [NOTICE]   (6492) : haproxy version is 3.0.0-5590ada
Sep 30 03:53:35 ubutun2204-1 haproxy[6492]: [NOTICE]   (6492) : path to executable is /apps/haproxy/sbin/haproxy
Sep 30 03:53:35 ubutun2204-1 haproxy[6492]: [ALERT]    (6492) : config : parsing [/etc/haproxy/haproxy.cfg:15] : 'pidfile' already specified. Continuing.
Sep 30 03:53:35 ubutun2204-1 haproxy[6492]: [NOTICE]   (6492) : New worker (6494) forked
Sep 30 03:53:35 ubutun2204-1 haproxy[6492]: [NOTICE]   (6492) : Loading success.

root@ubutun2204-1:~# pstree -p| grep haproxy
|-haproxy(6492)---haproxy(6504)---{haproxy}(6506)
```

### 3.2.8 查看haproxy的状态页面

浏览器访问： `http://haproxy-server:9999/haproxy-status`

![image-20240930120237463](images/image-20240930120237463.png)

![image-20240930120331511](images/image-20240930120331511.png)

# 4 HAProxy 基础配置

官方帮助文档

![image-20240930120523419](images/image-20240930120523419.png)

![image-20240930120623105](images/image-20240930120623105.png)



HAProxy 的配置文件haproxy.cfg由两大部分组成，分别是global和proxies部分

- global：全局配置段

  ```http
  进程及安全配置相关的参数
  性能调整相关参数
  Debug参数
  ```

- proxies：代理配置段

  ```http
  defaults：为frontend, backend, listen提供默认配置
  listen：同时拥有前端和后端配置,配置简单,生产推荐使用
  frontend：前端，相当于nginx中的server {}
  backend：后端，相当于nginx中的upstream {}
  ```

## 4.1 Global配置

### 4.1.1 Global 配置参数说明

官方文档：

```http
http://docs.haproxy.org/3.0/configuration.html#3
```

常见配置指令

```bash
chroot /apps/haproxy #锁定运行目录
deamon               #以守护进程运行
stats socket /var/lib/haproxy/haproxy.sock mode 600 level admin process 1 #socket文件,并可以通过此文件管理
user, group, uid, gid  #运行haproxy对应worker进程的用户身份
#nbproc   n   #开启的haproxy worker 进程数，默认进程数是一个, nbproc从HAProxy 2.5开始不再支持
nbthread  1 #默认值auto，和多进程 nbproc配置互斥（版本有关,CentOS8的haproxy1.8无此问题）,指定每个haproxy进程开启的线程数，默认为每个进程一个线程
#如果同时启用nbproc和nbthread 会出现以下日志的错误，无法启动服务
Apr  7 14:46:23 haproxy haproxy: [ALERT] 097/144623 (1454) : config : cannot 
enable multiple processes if multiple threads are configured. Please use either 
nbproc or nbthread but not both.

# 注意：下面方式不支持线程绑定
#cpu-map 1 0   #绑定haproxy worker 进程至指定CPU，将第1个worker进程绑定至0号CPU
#cpu-map 2 1     #绑定haproxy worker 进程至指定CPU，将第2个worker进程绑定至1号CPU

cpu-map auto:1/1-8 0-7 #haproxy2.4中启用nbthreads，在global配置中添加此选项，可以进行线程和CPU的绑定，nbproc选项2.5版本中将会删除,每个进程中1-8个线程分别绑定0-7号CPU，注意：新版用此项进行线程绑定(1号线程绑定0号cpu,2号线程绑定1号cpu .....)

maxconn n   #每个haproxy进程的最大并发连接数
maxsslconn n   #每个haproxy进程ssl最大连接数,用于haproxy 配置了证书的场景下
maxconnrate n   #每个进程每秒创建的最大连接数量
spread-checks n #后端server状态check随机提前或延迟百分比时间，建议2-5(20%-50%)之间，默认值0
pidfile #指定pid文件路径
log 127.0.0.1 local2 info #定义全局的syslog服务器；日志服务器需要开启UDP协议，最多可以定义两个
```

### 4.1.2 多进程和线程

从2.5以上新版中用多线程代替多worker进程

范例：多线程和CPU绑定

```bash
# 范例1
root@ubutun2204-1:~# vim /etc/haproxy/haproxy.cfg
cpu-map auto:1/1-4 0-3
root@ubutun2204-1:~# systemctl reload haproxy.service

# 查看CPU和线程之间的绑定关系
root@ubutun2204-1:~# ps axo pid,cmd,psr -L |grep haproxy
   1299 /apps/haproxy/sbin/haproxy    3 #主进程
   1312 /apps/haproxy/sbin/haproxy    0 #线程
   1312 /apps/haproxy/sbin/haproxy    1 #线程
   1312 /apps/haproxy/sbin/haproxy    2 #线程
   1312 /apps/haproxy/sbin/haproxy    3 #线程
   
root@ubutun2204-1:~# ps auxf | grep haproxy
root        1299  0.1  0.6  93056 12260 ?        Ss   06:15   0:00 /apps/haproxy/sbin/haproxy -Ws -f /etc/haproxy/haproxy.cfg -p /var/lib/haproxy/haproxy.pid
haproxy     1312  0.0  0.9 264104 19012 ?        Sl   06:15   0:00  \_ /apps/haproxy/sbin/haproxy -sf 1301 -x sockpair@4 -Ws -f /etc/haproxy/haproxy.cfg -p /var/lib/haproxy/haproxy.pid
 
```

### 4.1.3 HAProxy日志配置

HAProxy本身不记录客户端的访问日志，此外为减少服务器负载，一般生产中HAProxy不记录日志。

也可以配置HAProxy利用rsyslog服务记录日志到指定日志文件中

#### 4.1.3.1 HAProxy配置

```bash
#在global配置项定义：
log 127.0.0.1 local{0-7} info #基于syslog记录日志到指定设备，级别包括:err、warning、info、debug


listen web_port
 bind 127.0.0.1:80
 mode http
 log global #开启当前web_port的日志功能，默认不记录日志
 server web1  127.0.0.1:8080 check inter 3000 fall 2 rise 5

# systemctl restart haproxy
```

#### 4.1.3.2 Rsyslog配置

```bash
root@ubutun2204-1:~# vim /etc/rsyslog.conf
$ModLoad imudp
$UDPServerRun 514
......
local2.*   /var/log/haproxy.log
......

root@ubutun2204-1:/etc/rsyslog.d# systemctl restart rsyslog
```

#### 4.1.3.3 验证HAProxy日志

重启syslog服务并访问 Web 页面，然后验证是否生成日志

```bash
root@ubutun2204-1:~# tail -f /var/log/haproxy.log 
Sep 30 06:49:20 localhost haproxy[2366]: Connect from 127.0.0.1:38920 to 127.0.0.1:80 (web/HTTP)
Sep 30 06:49:21 localhost haproxy[2366]: Connect from 127.0.0.1:38930 to 127.0.0.1:80 (web/HTTP)
Sep 30 06:51:17 localhost haproxy[2366]: Connect from 192.168.159.1:61733 to 192.168.159.103:9999 (stats/HTTP)
```

#### 4.1.3.4 实战案例：启动本地和远程日志

```bash
root@ubutun2204-1:~# vim /etc/haproxy/haproxy.cfg
global
   ......
   log 127.0.0.1 local2 info
   log 192.168.159.104 local2 info
.....
listen stats
   mode http
   bind 0.0.0.0:9999
   stats enable
   log global
   stats uri    /haproxy-status
   stats auth   admin:123456
   
root@ubutun2204-1:~# systemctl restart haproxy.service

#开启本地日志
root@ubutun2204-1:~# vim /etc/rsyslog.conf
$ModLoad imudp
$UDPServerRun 514
......
local2.*   /var/log/haproxy.log
......

root@ubutun2204-1:/etc/rsyslog.d# systemctl restart rsyslog

# 在syslog日志服务器开启远程主机日志（在192.168.159.104操作）
root@ubutun2204-1:~# vim /etc/rsyslog.conf 
module(load="imudp") # needs to be done just once   
input(type="imudp" port="514")
local2.*                   /var/log/haproxy.log 
root@ubutun2204-1:~# systemctl restart rsyslog.service

#浏览器访问：http://haproxy-server:9999/haproxy-status,观察本机和远程主机生成的日志

#本机haproxy查看Log
root@ubutun2204-1:~# tail -f /var/log/haproxy.log 
Sep 30 07:01:38 localhost haproxy[2466]: Connect from 127.0.0.1:39490 to 127.0.0.1:80 (web/HTTP)
Sep 30 07:01:46 localhost haproxy[2466]: Connect from 192.168.159.1:61967 to 192.168.159.103:9999 (stats/HTTP)

#远程syslog机器查看log
root@ubutun2204-1:~# tail -f  /var/log/haproxy.log 
Sep 30 06:59:18 192.168.159.103 haproxy[2466]: Connect from 192.168.159.1:61842 to 192.168.159.103:9999 (stats/HTTP)
Sep 30 06:59:19 192.168.159.103 haproxy[2466]: message repeated 4 times: [ Connect from 192.168.159.1:61842 to 192.168.159.103:9999 (stats/HTTP)]
Sep 30 07:00:06 192.168.159.103 haproxy[2466]: Connect from 127.0.0.1:58002 to 127.0.0.1:80 (web/HTTP)
Sep 30 07:00:43 192.168.159.103 haproxy[2466]: Connect from 127.0.0.1:52664 to 127.0.0.1:80 (web/HTTP)
Sep 30 07:00:54 192.168.159.103 haproxy[2466]: Connect from 192.168.159.1:61915 to 192.168.159.103:9999 (stats/HTTP)
Sep 30 07:01:02 192.168.159.103 haproxy[2466]: message repeated 3 times: [ Connect from 192.168.159.1:61915 to 192.168.159.103:9999 (stats/HTTP)]
Sep 30 07:01:38 192.168.159.103 haproxy[2466]: Connect from 127.0.0.1:39490 to 127.0.0.1:80 (web/HTTP)
Sep 30 07:01:46 192.168.159.103 haproxy[2466]: Connect from 192.168.159.1:61967 to 192.168.159.103:9999 (stats/HTTP)
```

## 4.2 Proxies 配置

官方文档：http://docs.haproxy.org/3.0/configuration.html#4

```bash
defaults [<name>] #默认配置项，针对以下的frontend、backend和listen生效，可以多个name也可以没有name
frontend <name>   #前端servername，类似于Nginx的一个虚拟主机 server和LVS服务集群。
backend <name>   #后端服务器组，等于nginx的upstream和LVS中的RS服务器
listen   <name>   #将frontend和backend合并在一起配置，相对于frontend和backend配置更简洁，生产常用
```

注意：name字段只能使用大小写字母，数字，‘-’(dash)，'_‘(underscore)，'.' (dot)和 ':'(colon)，并且严 格区分大小写

![image-20240930150821631](images/image-20240930150821631.png)

### 4.2.1 Proxies配置 defaults

defaults 配置参数：

```bash
option redispatch #当server Id对应的服务器挂掉后，强制定向到其他健康的服务器，重新派发
option abortonclose # 当服务器负载很高时，自动结束掉当前队列处理比较久的连接，针对业务情况选择开启
option http-keep-alive #开启与客户端的会话保持
option forwardfor     #透传客户端真实IP至后端web服务器
mode http|tcp #设置默认工作类型,使用TCP服务器性能更好，减少压力
timeout http-keep-alive 120s #session 会话保持超时时间，此时间段内会转发到相同的后端服务器
timeout connect 120s #客户端请求从haproxy到后端server最长连接等待时间(TCP连接之前)，默认单位ms
timeout server 600s #客户端请求从haproxy到后端服务端的请求处理超时时长(TCP连接之后)，默认单位ms，如果超时，会出现502错误，此值建议设置较大些，防止出现502错误
timeout client 600s #设置haproxy与客户端的最长非活动时间，默认单位ms，建议和timeout server相同
timeout check   5s   #对后端服务器的默认检测超时时间
default-server inter 1000 weight 3   #指定后端服务器的默认设置
```

### 4.2.2 Proxies配置 listen

使用listen替换frontend和backend的配置方式，可以简化设置，常用于TCP协议的应用

```bash
#官网业务访问入口
listen WEB_PORT_80 
   bind 192.168.159.103:80  # 外网地址
   mode http
   option forwardfor
   server web1   10.0.0.17:8080   check inter 3000 fall 3 rise 5 #内网地址
   server web2   10.0.0.27:8080   check inter 3000 fall 3 rise 5
   
# 检查语法
root@ubutun2204-1:~# haproxy -c -f /etc/haproxy/haproxy.cfg
Configuration file is valid
```

### 4.2.3 Proxies配置 frontend

**frontend配置参数：**

```bash
bind: #指定HAProxy的监听地址，可以是IPV4或IPV6，可以同时监听多个IP或端口，可同时用于listen字段中
      #格式：
       bind [<address>]:<port_range> [, ...] [param*]
      # 注意：如果需要绑定在非本机的IP，需要开启内核参数：net.ipv4.ip_nonlocal_bind=1

backlog <backlog> #针对所有server配置,当前端服务器的连接数达到上限后的后援队列长度，注意：不支持backend
```

范例：

```bash
frontend http_proxy   #监听htp的多个ip的多个端口和sock文件
   bind :80,:443,:8801-8810
   bind 10.0.0.1:10080,10.0.0.1:10443
   bind /var/run/ssl-frontend.sock user root mode 600 accept-proxy


frontend http_https_proxy #https监听
   bind :80
   bind :443 ssl crt /etc/haproxy/site.pem #公钥和私钥公共文件


frontend http_https_proxy_explicit #监听ipv6、ipv4和unix sock文件
   bind ipv6@:80
   bind ipv4@public_ssl:443 ssl crt /etc/haproxy/site.pem
   bind unix@ssl-frontend.sock user root mode 600 accept-proxy

listen external_bind_app1 #监听file descriptor
   bind "fd@${FD_APP1}"
```

**生产示例：**

```bash
frontend wanglei_web_port     #建议采用后面形式命名：业务-服务-端口号
   bind :80,:8080
   bind 10.0.0.7:10080,:8801-8810,10.0.0.17:9001-9010
   mode http|tcp
   use_backend <backend_name>  #调用的后端服务器组名称
```

### 4.2.4 Proxies配置 backend

定义一组后端服务器，backend服务器将被frontend进行调用。

注意: backend 的名称必须唯一,并且必须在listen或frontend中事先定义才可以使用,否则服务无法启动

```bash
mode http|tcp     #指定负载协议类型,和对应的frontend必须一致
option #配置选项
server   #定义后端real server,必须指定IP和端口
```

注意：option后面加 httpchk，smtpchk,mysql-check,pgsql-check，ssl-hello-chk方法，可用于实现更 多应用层检测功能。

**server配置**

```bash
#针对一个server配置
check #对指定real进行健康状态检查，如果不加此设置，默认不开启检查,只有check后面没有其它配置也可以启用检查功能
      # 默认对相应的后端服务器IP和端口,利用TCP连接进行周期性健康性检查,注意必须指定端口才能实现健康性检查
      addr <IP>   #可指定的健康状态监测IP，可以是专门的数据网段，减少业务网络的流量
      port <num> #指定的健康状态监测端口
      inter <num> #健康状态检查间隔时间，默认2000 ms
      fall <num>   #后端服务器从线上转为线下的检查的连续失效次数，默认为3
      rise <num>   #后端服务器从下线恢复上线的检查的连续有效次数，默认为2

weight <weight> #默认为1，最大值为256. 0(状态为蓝色)表示不参与负载均衡，但仍接受持久连接
backup #将后端服务器标记为备份状态,只在所有非备份主机down机时提供服务，类似Sorry Server
disabled #将后端服务器标记为不可用状态，即维护状态，除了持久模式，将不再接受连接,状态为深黄色,支持优雅平滑下线,继续处理旧请求，不接受新请求
maxconn <maxconn> #当前后端server的最大并发连接数,放在,放在server 指令后面
redir http://www.baidu.com       #将请求临时(302)重定向至其它URL，只适用于http模式,放在server 指令后面
```

**redirect配置**

```bash
#注意：此指令和redir功能相似，但不属于server指令后面，是独立存放在listen,frontend,backend语句块
redirect prefix http://www.baidu.com/ #将请求临时(302)重定向至其它URL，只适用于http模式
```

### 4.2.5 frontend和backend 组合配置案例

范例1：

```bash
root@ubutun2204-1:~# cat /etc/haproxy/haproxy.cfg
......
frontend wanglei-test-web
   bind :80,:8008
   mode tcp
   use_backend wanglei-servers
backend wanglei-servers
   mode tcp
   default-server inter 1000 weight 6 
   server web1 192.168.159.104:80 check addr 192.168.159.103 port 8008
   server web2 192.168.159.105:80 check

#访问haproxy-server:80，发现轮询调度到后端服务器
root@ubutun2204-1:~# while true;do curl 192.168.159.103;sleep 0.5;done
wanglei web2 192.168.159.105
wanglei web1 192.168.159.104
wanglei web2 192.168.159.105
wanglei web1 192.168.159.104
wanglei web2 192.168.159.105
wanglei web1 192.168.159.104
wanglei web2 192.168.159.105
wanglei web1 192.168.159.104
wanglei web2 192.168.159.105

# 将web2上的nginx停掉，发现只是调度到web1
root@ubutun2204-1:~# while true;do curl 192.168.159.103;sleep 0.5;done
wanglei web1 192.168.159.104
wanglei web2 192.168.159.105
wanglei web1 192.168.159.104
wanglei web2 192.168.159.105
wanglei web1 192.168.159.104
wanglei web2 192.168.159.105
wanglei web1 192.168.159.104
curl: (52) Empty reply from server # web2停掉后，经过健康检查，后续只是调度到web1
wanglei web1 192.168.159.104
wanglei web1 192.168.159.104
wanglei web1 192.168.159.104
wanglei web1 192.168.159.104
wanglei web1 192.168.159.104
wanglei web1 192.168.159.104
wanglei web1 192.168.159.104
wanglei web1 192.168.159.104
```

范例2：

```bash
root@ubutun2204-1:~# cat /etc/haproxy/haproxy.cfg 
......
frontend web_80
   bind 192.168.159.103:80
   mode http
   use_backend wanglei-servers
backend wanglei-servers
   mode http
   option forwardfor #透传真实ip
   server web1 192.168.159.104:80 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 check inter 1000 fall 3 rise 3
```

## 4.3 使用子配置文件

当业务众多时，将所有配置都放在一个配置文件中，会造成维护困难。

可以考虑按业务分类，将配置信息拆分，放在不同的子配置文件中，从而达到方便维护的目的。

**注意: 子配置文件的文件后缀必须为.cfg**

```bash
# 创建子配置目录
root@ubutun2204-1:~# mkdir /etc/haproxy/conf.d/

#添加子配置目录到unit文件中
root@ubutun2204-1:~# cat  /lib/systemd/system/haproxy.service
[Unit]
Description=HAProxy Load Balancer
After=syslog.target network.target

[Service]
#修改下面两行
ExecStartPre=/apps/haproxy/sbin/haproxy -f /etc/haproxy/haproxy.cfg -f /etc/haproxy/conf.d/  -c -q
ExecStart=/apps/haproxy/sbin/haproxy -Ws -f /etc/haproxy/haproxy.cfg -f /etc/haproxy/conf.d/ -p /var/lib/haproxy/haproxy.pid
ExecReload=/bin/kill -USR2 $MAINPID

[Install]
WantedBy=multi-user.target


# 创建子配置文件，注意：必须为cfg后缀非.开头的配置文件
root@ubutun2204-1:~# vim /etc/haproxy/conf.d/wanglei_web.cfg
frontend web_80
   bind 192.168.159.103:80
   mode http
   use_backend wanglei-servers
backend wanglei-servers
   mode http
   option forwardfor
   server web1 192.168.159.104:80 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 check inter 1000 fall 3 rise 3
   
root@ubutun2204-1:~# systemctl daemon-reload
root@ubutun2204-1:~# systemctl restart haproxy.service   
```

# 5 HAProxy 调度算法

HAProxy通过固定参数 `balance `指明对后端服务器的调度算法，该参数可以配置在listen或backend选 项中。

HAProxy的调度算法分为静态和动态调度算法，但是有些算法可以根据不同的参数实现静态和动态算法 相互转换。

官方文档：http://docs.haproxy.org/3.0/configuration.html#4-balance

## 5.1 Socat 工具

对服务器动态权重和其它状态可以利用 socat 工具进行调整，Socat 是 Linux 下的一个多功能的网络工 具，名字来由是Socket CAT，相当于netCAT的增强版.Socat 的主要特点就是在两个数据流之间建立双向 通道，且支持众多协议和链接方式。如 IP、TCP、 UDP、IPv6、Socket文件等

范例：利用工具socat对服务器动态权重调整

```bash
# 安装socat
root@ubutun2204-1:~# apt update && apt -y install socat

#查看帮助
root@ubutun2204-1:~# echo "help" | socat stdio /var/lib/haproxy/haproxy.sock
The following commands are valid at this level:
  abort ssl ca-file <cafile>              : abort a transaction for a CA file
  abort ssl cert <certfile>               : abort a transaction for a certificate file
  abort ssl crl-file <crlfile>            : abort a transaction for a CRL file
  add acl [@<ver>] <acl> <pattern>        : add an acl entry
  add map [@<ver>] <map> <key> <val>      : add a map entry (payload supported instead of key/val)
  add server <bk>/<srv>                   : create a new server
  add ssl ca-file <cafile> <payload>      : add a certificate into the CA file
  add ssl crt-list <list> <cert> [opts]*  : add to crt-list file <list> a line <cert> or a payload
  clear acl [@<ver>] <acl>                : clear the contents of this acl
  clear counters [all]                    : clear max statistics counters (or all counters)
  clear map [@<ver>] <map>                : clear the contents of this map
  clear table <table> [<filter>]*         : remove an entry from a table (filter: data/key)
  commit acl @<ver> <acl>                 : commit the ACL at this version
  commit map @<ver> <map>                 : commit the map at this version
  commit ssl ca-file <cafile>             : commit a CA file
  commit ssl cert <certfile>              : commit a certificate file
  commit ssl crl-file <crlfile>           : commit a CRL file
  debug dev hash   [msg]                  : return msg hashed if anon is set
  del acl <acl> [<key>|#<ref>]            : delete acl entries matching <key>
  del map <map> [<key>|#<ref>]            : delete map entries matching <key>
  del server <bk>/<srv>                   : remove a dynamically added server
  del ssl ca-file <cafile>                : delete an unused CA file
  del ssl cert <certfile>                 : delete an unused certificate file
  del ssl crl-file <crlfile>              : delete an unused CRL file
  del ssl crt-list <list> <cert[:line]>   : delete a line <cert> from crt-list file <list>
  disable agent                           : disable agent checks
  disable dynamic-cookie backend <bk>     : disable dynamic cookies on a specific backend
  disable frontend <frontend>             : temporarily disable specific frontend
  disable health                          : disable health checks
  disable server (DEPRECATED)             : disable a server for maintenance (use 'set server' instead) #禁用服务器
  dump stats-file                         : dump stats for restore
  enable agent                            : enable agent checks
  enable dynamic-cookie backend <bk>      : enable dynamic cookies on a specific backend
  enable frontend <frontend>              : re-enable specific frontend
  enable health                           : enable health checks
  enable server  (DEPRECATED)             : enable a disabled server (use 'set server' instead) #启用服务器
  get acl <acl> <value>                   : report the patterns matching a sample for an ACL
  get map <acl> <value>                   : report the keys and values matching a sample for a map
  get var <name>                          : retrieve contents of a process-wide variable
  get weight <bk>/<srv>                   : report a server's current weight
  new ssl ca-file <cafile>                : create a new CA file to be used in a crt-list
  new ssl cert <certfile>                 : create a new certificate file to be used in a crt-list or a directory
  new ssl crl-file <crlfile>               : create a new CRL file to be used in a crt-list
  operator                                : lower the level of the current CLI session to operator
  prepare acl <acl>                       : prepare a new version for atomic ACL replacement
  prepare map <acl>                       : prepare a new version for atomic map replacement
  set anon global-key <value>             : change the global anonymizing key
  set anon off                            : deactivate the anonymized mode
  set anon on [value]                     : activate the anonymized mode
  set dynamic-cookie-key backend <bk> <k> : change a backend secret key for dynamic cookies
  set map <map> [<key>|#<ref>] <value>    : modify a map entry
  set maxconn frontend <frontend> <value> : change a frontend's maxconn setting
  set maxconn global <value>              : change the per-process maxconn setting
  set maxconn server <bk>/<srv>           : change a server's maxconn setting
  set profiling <what> {auto|on|off}      : enable/disable resource profiling (tasks,memory)
  set rate-limit <setting> <value>        : change a rate limiting value
  set server <bk>/<srv> [opts]            : change a server's state, weight, address or ssl #设置服务器
  set severity-output [none|number|string]: set presence of severity level in feedback information
  set ssl ca-file <cafile> <payload>      : replace a CA file
  set ssl cert <certfile> <payload>       : replace a certificate file
  set ssl crl-file <crlfile> <payload>    : replace a CRL file
  set ssl ocsp-response <resp|payload>       : update a certificate's OCSP Response from a base64-encode DER
  set ssl tls-key [id|file] <key>         : set the next TLS key for the <id> or <file> listener to <key>
  set table <table> key <k> [data.* <v>]* : update or create a table entry's data
  set timeout [cli] <delay>               : change a timeout setting
  set weight <bk>/<srv>  (DEPRECATED)     : change a server's weight (use 'set server' instead)
  show acl [@<ver>] <acl>]                : report available acls or dump an acl's contents
  show activity [-1|0|thread_num]         : show per-thread activity stats (for support/developers)
  show anon                               : display the current state of anonymized mode
  show backend                            : list backends in the current running config
  show cache                              : show cache status
  show cli level                          : display the level of the current CLI session
  show cli sockets                        : dump list of cli sockets
  show dev                                : show debug info for developers
  show env [var]                          : dump environment variables known to the process
  show errors [<px>] [request|response]   : report last request and/or response errors for each proxy
  show events [<sink>] [-w] [-n]          : show event sink state
  show fd [-!plcfbsd]* [num]              : dump list of file descriptors in use or a specific one
  show info [desc|json|typed|float]*      : report information about the running process
  show libs                               : show loaded object files and libraries
  show map [@ver] [map]                   : report available maps or dump a map's contents
  show peers [dict|-] [section]           : dump some information about all the peers or this peers section
  show pools [by*] [match <pfx>] [nb]     : report information about the memory pools usage
  show profiling [<what>|<#lines>|<opts>]*: show profiling state (all,status,tasks,memory)
  show resolvers [id]                     : dumps counters from all resolvers section and associated name servers
  show schema json                        : report schema used for stats
  show servers conn [<backend>]           : dump server connections status (all or for a single backend)
  show servers state [<backend>]          : dump volatile server information (all or for a single backend)
  show sess [<id>|all|susp|older <age>]   : report the list of current sessions or dump this exact session
  show ssl ca-file [<cafile>[:<index>]]   : display the SSL CA files used in memory, or the details of a <cafile>, or a single certificate of index <index> of a CA file <cafile>
  show ssl cert [<certfile>]              : display the SSL certificates used in memory, or the details of a file
  show ssl crl-file [<crlfile[:<index>>]] : display the SSL CRL files used in memory, or the details of a <crlfile>, or a single CRL of index <index> of CRL file <crlfile>
  show ssl crt-list [-n] [<list>]         : show the list of crt-lists or the content of a crt-list file <list>
  show ssl ocsp-response [[text|base64] id]  : display the IDs of the OCSP responses used in memory, or the details of a single OCSP response (in text or base64 format)
  show ssl ocsp-updates                      : display information about the next 'nb' ocsp responses that will be updated automatically
  show ssl providers                      : show loaded SSL providers
  show startup-logs                       : report logs emitted during HAProxy startup
  show stat [desc|json|no-maint|typed|up]*: report counters for each proxy and server
  show table <table> [<filter>]*          : report table usage stats or dump this table's contents (filter: data/key)
  show tasks                              : show running tasks
  show threads                            : show some threads debugging information
  show tls-keys [id|*]                    : show tls keys references or dump tls ticket keys when id specified
  show trace [<module>]                   : show live tracing state
  show version                            : show version of the current process
  shutdown frontend <frontend>            : stop a specific frontend
  shutdown session [id]                   : kill a specific session
  shutdown sessions server <bk>/<srv>     : kill sessions on a server
  trace [<module>|0] [cmd [args...]]      : manage live tracing (empty to list, 0 to stop all)
  update ssl ocsp-response <certfile>     : send ocsp request and update stored ocsp response
  user                                    : lower the level of the current CLI session to user
  wait {-h|<delay_ms>} cond [args...]     : wait the specified delay or condition (-h to see list)
  help [<command>]                        : list matching or all commands
  prompt [timed]                          : toggle interactive mode with prompt
  quit                                    : disconnect


# 拿到的数据可以用来监控
root@ubutun2204-1:~# echo "show info" | socat stdio /var/lib/haproxy/haproxy.sock
Name: HAProxy
Version: 3.0.0-5590ada
Release_date: 2024/05/29
Nbthread: 4
Nbproc: 1
Process_num: 1
Pid: 3092
Uptime: 0d 0h25m05s
Uptime_sec: 1505
Memmax_MB: 0
PoolAlloc_MB: 1
PoolUsed_MB: 1
PoolFailed: 0
Ulimit-n: 200038
Maxsock: 200038
Maxconn: 100000
Hard_maxconn: 100000
CurrConns: 0
CumConns: 45670
CumReq: 40027
MaxSslConns: 0
CurrSslConns: 0
CumSslConns: 0
Maxpipes: 0
PipesUsed: 0
PipesFree: 0
ConnRate: 0
ConnRateLimit: 0
MaxConnRate: 12636
SessRate: 0
SessRateLimit: 0
MaxSessRate: 12636
SslRate: 0
SslRateLimit: 0
MaxSslRate: 0
SslFrontendKeyRate: 0
SslFrontendMaxKeyRate: 0
SslFrontendSessionReuse_pct: 0
SslBackendKeyRate: 0
SslBackendMaxKeyRate: 0
SslCacheLookups: 0
SslCacheMisses: 0
CompressBpsIn: 0
CompressBpsOut: 0
CompressBpsRateLim: 0
ZlibMemUsage: 0
MaxZlibMemUsage: 0
Tasks: 22
Run_queue: 0
Idle_pct: 100
node: ubutun2204-1
Stopping: 0
Jobs: 6
Unstoppable Jobs: 1
Listeners: 4
ActivePeers: 0
ConnectedPeers: 0
DroppedLogs: 0
BusyPolling: 0
FailedResolutions: 0
TotalBytesOut: 17420708
TotalSplicedBytesOut: 0
BytesOutRate: 0
DebugCommandsIssued: 0
CumRecvLogs: 0
Build info: 3.0.0-5590ada
Memmax_bytes: 0
PoolAlloc_bytes: 2054960
PoolUsed_bytes: 2054960
Start_time_sec: 1727683014
Tainted: 0
TotalWarnings: 0
MaxconnReached: 0
BootTime_ms: 39
Niced_tasks: 0

#获取当前连接数
root@ubutun2204-1:~# echo "show info" | socat stdio /var/lib/haproxy/haproxy.sock | awk '/CurrConns/{print $2}'


root@ubutun2204-1:~# cat /etc/haproxy/conf.d/wanglei_web.cfg 
frontend web_80
   bind 192.168.159.103:80
   mode http
   use_backend wanglei-servers
backend wanglei-servers
   mode http
   option forwardfor
   server web1 192.168.159.104:80 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 check inter 1000 fall 3 rise 3


root@ubutun2204-1:~# echo "get weight wanglei-servers/web2" | socat stdio /var/lib/haproxy/haproxy.sock
1 (initial 1)

# 修改weight，注意只针对单进程有效
root@ubutun2204-1:~# echo "set weight wanglei-servers/web2 2" | socat stdio /var/lib/haproxy/haproxy.sock
root@ubutun2204-1:~# echo "get weight wanglei-servers/web2" | socat stdio /var/lib/haproxy/haproxy.sock
2 (initial 1)


#将后端服务器禁用，注意只针对单进程有效
root@ubutun2204-1:~# echo "disable server wanglei-servers/web2" | socat stdio /var/lib/haproxy/haproxy.sock

#启用后端服务器
root@ubutun2204-1:~# echo "enable server wanglei-servers/web2" | socat stdio /var/lib/haproxy/haproxy.sock

#将后端服务器软下线，即weight设为0
root@ubutun2204-1:~# echo "set weight wanglei-servers/web1 0" | socat stdio /var/lib/haproxy/haproxy.sock
```

## 5.2 静态算法

静态算法：按照事先定义好的规则轮询进行调度，不关心后端服务器的当前负载、连接数和响应速度 等，

且无法实时动态修改权重(只能为0和1,不支持其它值)或者修改后不生效，如果需要修改只能靠重启 HAProxy生效。

### 5.2.2 static-rr 算法

static-rr：基于权重的轮询调度，不支持运行时利用socat进行权重的动态调整(只支持0和1,不支持其它 值)及后端服务器慢启动，其后端主机数量没有限制，相当于LVS中的 wrr

```http
listen wanglei_web
   bind :80
   mode http
   option forwardfor
   log global
   balance static-rr
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 2 check inter 1000 fall 3 rise 3
```

范例：调整权重

```bash
# 只支持0或100%
root@ubutun2204-1:~# echo "set weight wanglei_web/web1 0" | socat stdio /var/lib/haproxy/haproxy.sock
root@ubutun2204-1:~# echo "set weight wanglei_web/web1 100%" | socat stdio /var/lib/haproxy/haproxy.sock

root@ubutun2204-1:~# echo "set weight wanglei_web/web1 2" | socat stdio /var/lib/haproxy/haproxy.sock
Backend is using a static LB algorithm and only accepts weights '0%' and '100%'.
```

### 5.2.3 first 算法

first：根据服务器在列表中的位置，自上而下进行调度，但是其只会当第一台服务器的连接数达到上 限，新请求才会分配给下一台服务，因此会忽略服务器的权重设置，此方式使用较少

不支持用socat进行动态修改权重,可以设置0和1,可以设置其它值但无效

```http
listen wanglei_web
   bind :80
   mode http
   option forwardfor
   log global
   balance first
   server web1 192.168.159.104:80 maxconn 2 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
```

## 5.3 动态算法

动态算法：基于后端服务器状态进行调度适当调整，新请求将优先调度至当前负载较低的服务器，且权 重可以在haproxy运行时动态调整无需重启。

### 5.3.1 roundrobin 算法

roundrobin：基于权重的轮询动态调度算法，支持权重的运行时调整，不同于lvs中的rr轮训模式， HAProxy中的roundrobin支持慢启动(新加的服务器会逐渐增加转发数)，其每个后端backend中最多支 持4095个real server，支持对real server权重动态调整，roundrobin为默认调度算法,此算法使用广泛

```http
listen wanglei_web
   bind :80
   mode http
   option forwardfor
   log global
   balance roundrobin
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
```

支持动态调整权重：

```bash
root@ubutun2204-1:~# echo "set weight wanglei_web/web1 3" | socat stdio /var/lib/haproxy/haproxy.sock 

root@ubutun2204-1:~# echo "get weight wanglei_web/web1 " | socat stdio /var/lib/haproxy/haproxy.sock 
3 (initial 1)
```

### 5.3.2 leastconn 算法

leastconn 加权的最少连接的动态，支持权重的运行时调整和慢启动，即根据当前连接最少的后端服务 器而非权重进行优先调度(新客户端连接)，比较适合长连接的场景使用，比如：MySQL等场景。

相当于LVS中的WLC算法

```http
listen wanglei_web
   bind :80
   mode http
   option forwardfor
   log global
   balance leastconn
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
```

### 5.3.3 random 算法

在1.9版本开始增加 random的负载平衡算法，其基于随机数作为一致性hash的key，随机负载平衡对于 大型服务器场或经常添加或删除服务器非常有用，支持weight的动态调整，weight较大的主机有更大概 率获取新请求

```bash
listen wanglei_web
   bind :80
   mode http
   option forwardfor
   log global
   balance random
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
```

## 5.4 其他算法

其它算法即可作为静态算法，又可以通过选项成为动态算法

### 5.4.1 source 算法

源地址hash，基于用户源地址hash并将请求转发到后端服务器，后续同一个源地址请求将被转发至同一 个后端web服务器。此方式当后端服务器数据量发生变化时，会导致很多用户的请求转发至新的后端服 务器，默认为静态方式，但是可以通过hash-type选项进行更改

这个算法一般是在不插入Cookie的TCP模式下使用，也可给不支持会话cookie的客户提供会话粘性，适 用于需要session会话保持但不支持cookie和缓存的场景

源地址有两种转发客户端请求到后端服务器的服务器选取计算方式，分别是取模法和一致性hash

#### 5.4.1.1 map-base 取模法

map-based：取模法，对source地址进行hash计算，再基于服务器总权重的取模，最终结果决定将此 请求转发至对应的后端服务器。

此方法是静态的，即不支持在线调整权重，不支持慢启动，可实现对后端服务器均衡调度。缺点是当服 务器的总权重发生变化时，即有服务器上线或下线，都会因总权重发生变化而导致调度结果整体改变， hash-type 指定的默认值为此算法

```http
所谓取模运算，就是计算两个数相除之后的余数，10%7=3, 7%4=3
map-based算法：基于权重取模，hash(source_ip)%所有后端服务器相加的总权重
```

取模法配置示例：

```bash
listen wanglei_web
   bind :80
   mode http
   option forwardfor
   log global
   balance source
   hash-type map-based  #默认就是这种类型
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
   
 # 不支持动态调整权重
 root@ubutun2204-1:~# echo "set weight wanglei_web/web1 10" | socat stdio /var/lib/haproxy/haproxy.sock 
Backend is using a static LB algorithm and only accepts weights '0%' and '100%'.
```

#### 5.4.1.2 一致性 hash

一致性哈希，当服务器的总权重发生变化时，对调度结果的影响是局部的，不会引起大的变动，hash（o）mod n ，该hash算法是动态的，支持使用 socat等工具进行在线权重调整，支持慢启动

**算法：**

```http
1、key1=hash(source_ip)%(2^32) [0---4294967295]
2、keyA=hash(后端服务器虚拟ip)%(2^32)
3、将key1和keyA都放在hash环上，将用户请求调度到离key1最近的keyA对应的后端服务器
```

**hash环偏斜问题**

```http
增加虚拟服务器IP数量，比如：一个后端服务器根据权重为1生成1000个虚拟IP，再hash。而后端服务器权
重为2则生成2000的虚拟IP，再进行hash运算,最终在hash环上生成3000个节点，从而解决hash环偏斜问题
```

##### 5.4.1.2.1 hash对象

Hash对象到后端服务器的映射关系：

![image-20240930170913747](images/image-20240930170913747.png)

#### 5.4.1.2.2 一致性hash示意图

后端服务器在线与离线的调度方式

![image-20240930170949114](images/image-20240930170949114.png)

![image-20240930171003059](images/image-20240930171003059.png)

##### 5.4.1.2.3 一致性hash配置示例

```bash
listen wanglei_web
   bind :80
   mode http
   option forwardfor
   log global
   balance source
   hash-type consistent
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
```

### 5.4.2 uri 算法

基于对用户请求的URI的左半部分或整个uri做hash，再将hash结果对总权重进行取模后，根据最终结果 将请求转发到后端指定服务器，适用于后端是缓存服务器场景，默认是静态算法，也可以通过hash-type 指定map-based和consistent，来定义使用取模法还是一致性hash。

**注意：此算法基于应用层，所以只支持 mode http ，不支持 mode tcp**

```http
scheme>://<user>:<password>@<host>:<port>/<path>;<params>?<query>#<frag>
左半部分：/<path>;<params>
整个uri：/<path>;<params>?<query>#<frag>
```

#### 5.4.2.1 uri 取模法配置示例

```bash
listen wanglei_web
   bind :80
   mode http
   option forwardfor
   log global
   balance uri
   hash-type map-based #默认
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
```

#### 5.4.2.2 uri 一致性hash配置示例

```http
listen wanglei_web
   bind :80
   mode http
   option forwardfor
   log global
   balance uri
   hash-type consistent
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
```

#### 5.4.2.3 访问测试

访问不同的uri，确认可以将用户同样的请求转发至不同的服务器；

不同的客户端访问相同的uri，转发到同一服务器

```bash
root@ubutun2204-1:~# curl 192.168.159.103/test1.html
test1 192.168.159.105
root@ubutun2204-1:~# curl 192.168.159.103/test2.html
test2 192.168.159.104
```

### 5.4.3 url_param 算法

url_param对用户请求的url中的 params 部分中的一个参数key对应的value值作hash计算，并由服务器 总权重相除以后派发至某挑出的服务器；通常用于追踪用户，以确保来自同一个用户的请求始终发往同 一个real server，如果无key，将按roundrobin算法

```bash
# 假设
url= http://www.wanglei.com/foo/bar/index.php?key=value

#则：
host = "www.wanglei.com"
url_param = "key=value"
```

#### 5.4.3.1 url_param取模法配置示例

```http
listen wanglei_web
   bind :80
   mode http
   option forwardfor
   log global
   balance url_param userid  #对url里面的key为userid的value取模
   hash-type map-based
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
```

#### 5.4.3.2 url_param一致性hash配置示例

```bash
listen wanglei_web
   bind :80
   mode http
   option forwardfor
   log global
   balance url_param userid  #对url里面的key为userid的value取模
   hash-type consistent
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
```

#### 5.4.3.3 测试访问

只要不同的url里面包括`userid=wanglei`就会调度到同一台机器

```bash
root@ubutun2204-1:~# curl 192.168.159.103/test1.html?userid=alblue
root@ubutun2204-1:~# curl 192.168.159.103/test2.html?userid=alblue&typeid=man
```

### 5.4.4 hdr 算法

针对用户每个http头部(header)请求中的指定信息做hash，此处由 name 指定的http首部将会被取出并 做hash计算，然后由服务器总权重取模以后派发至某挑出的服务器，如果无有效值，则会使用默认的轮 询调度。

#### 5.4.4.1 hdr取模法配置示例

```bash
listen wanglei_web
   bind :80
   mode http
   option forwardfor
   log global
   balance hdr(User-Agent)
   hash-type map-based
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
```

#### 5.4.4.2 一致性hash配置示例

```bash
listen wanglei_web
   bind :80
   mode http
   option forwardfor
   log global
   balance hdr(User-Agent)
   hash-type consistent
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
```

#### 5.4.4.3 测试访问

只要`User-Agent` 所对应的值一样，就会调度到同一台机器上

```bash
# 模拟curl客户端
root@ubutun2204-1:~# curl -v 192.168.159.103
*   Trying 192.168.159.103:80...
* Connected to 192.168.159.103 (192.168.159.103) port 80 (#0)
> GET / HTTP/1.1
> Host: 192.168.159.103
> User-Agent: curl/7.81.0  # User-Agent 为curl/7.81.0 
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< server: nginx/1.18.0 (Ubuntu)
< date: Wed, 02 Oct 2024 08:41:23 GMT
< content-type: text/html
< content-length: 29
< last-modified: Mon, 30 Sep 2024 07:40:53 GMT
< etag: "66fa5605-1d"
< accept-ranges: bytes
< 
wanglei web2 192.168.159.105 #调度到105

#模拟chrome客户端
root@ubutun2204-1:~# curl -vA 'chrome' 192.168.159.103
*   Trying 192.168.159.103:80...
* Connected to 192.168.159.103 (192.168.159.103) port 80 (#0)
> GET / HTTP/1.1
> Host: 192.168.159.103
> User-Agent: chrome
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< server: nginx/1.18.0 (Ubuntu)
< date: Wed, 02 Oct 2024 08:42:49 GMT
< content-type: text/html
< content-length: 29
< last-modified: Mon, 30 Sep 2024 07:40:28 GMT
< etag: "66fa55ec-1d"
< accept-ranges: bytes
< 
wanglei web1 192.168.159.104 #调度到104

#模拟火狐浏览器
root@ubutun2204-1:~# curl -vA 'firefox' 192.168.159.103
*   Trying 192.168.159.103:80...
* Connected to 192.168.159.103 (192.168.159.103) port 80 (#0)
> GET / HTTP/1.1
> Host: 192.168.159.103
> User-Agent: firefox
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< server: nginx/1.18.0 (Ubuntu)
< date: Wed, 02 Oct 2024 08:43:53 GMT
< content-type: text/html
< content-length: 29
< last-modified: Mon, 30 Sep 2024 07:40:53 GMT
< etag: "66fa5605-1d"
< accept-ranges: bytes
< 
wanglei web2 192.168.159.105 #调度到105
```

### 5.4.5 rdp-cookie 算法

rdp(windows远程桌面协议)-cookie对windows远程桌面的反向代理，使用cookie保持会话；此调度算法专门适用于windows远程桌面连接场景。当连接到后端服务器后，会生成一个cookie，下次相同的cookie连接时，还会被调度到同一台后端服务器，适用于后端多服务器场景。

默认是静态，也可以通过hash-type 指定map-based和consistent，来定义使用取模法还是一致性hash。

#### 5.4.5.1 rdp-cookie 取模法配置示例

```bash
root@ubutun2204-1:~# cat /etc/haproxy/conf.d/windows_rdp.cfg 
listen RDP
 bind 192.168.159.103:3389
 balance rdp-cookie
 mode tcp
 server rdp0 192.168.3.6:3389 check fall 3 rise 5 inter 2000 weight 1
```

#### 5.4.5.2 rdp-cookie 一致性hash配置示例

```bash
root@ubutun2204-1:~# cat /etc/haproxy/conf.d/windows_rdp.cfg 
listen RDP
 bind 192.168.159.103:3389
 balance rdp-cookie
 hash-type consistent
 mode tcp
 server rdp0 192.168.3.6:3389 check fall 3 rise 5 inter 2000 weight 1
```

### 5.4.6 算法总结

```bash
#静态
static-rr--------->tcp/http  
first------------->tcp/http 

#动态
roundrobin-------->tcp/http 
leastconn--------->tcp/http 
random------------>tcp/http

#以下静态和动态取决于hash_type是否consistent
source------------>tcp/http
Uri--------------->http
url_param--------->http     
hdr--------------->http
rdp-cookie-------->tcp

#各种算法使用场景
first #使用较少
static-rr #做了session共享的 web 集群
roundrobin
random


leastconn #数据库
source #基于客户端公网 IP 的会话保持


Uri--------------->http  #缓存服务器，CDN服务商，蓝汛、百度、阿里云、腾讯
url_param--------->http  #可以实现session保持

hdr #基于客户端请求报文头部做下一步处理

rdp-cookie #基于Windows主机,很少使用
```

# 6 HAProxy 高级功能

介绍HAProxy高级配置及实用案例

## 6.1 基于 Cookie 的会话保持

cookie value：为当前server指定cookie值，实现基于cookie的会话黏性，相对于基于 source 地址  hash 调度算法对客户端的粒度更精准，但同时也加重了haproxy负载，目前此模式使用较少， 已经被 session共享服务器代替

注意：不支持tcp mode，使用http mode

### 6.1.1 配置选项

```bash
cookie name [ rewrite | insert | prefix ][ indirect ] [ nocache ][ postonly ] [ 
preserve ][ httponly ] [ secure ][ domain ]* [ maxidle <idle> ][ maxlife ]

name: #cookie 的 key名称，用于实现持久连接
insert： #插入新的cookie,默认不插入cookie
indirect： #如果客户端已经有cookie,则不会再发送cookie信息
nocache： #当client和hapoxy之间有缓存服务器（如：CDN）时，不允许中间缓存器缓存cookie，因为这会导致很多经过同一个CDN的请求都发送到同一台后端服务器
```

### 6.1.2 配置示例

```bash
root@ubutun2204-1:~# vim /etc/haproxy/conf.d/wanglei_web.cfg
listen wanglei_web
   bind :80
   mode http  #只支持http
   log global
   balance roundrobin
   cookie WEBSERV insert nocache indirect #cookie 的key WEBSERV
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3 cookie web11 #当cookie的WEBSERV的value值为web11,永远调度到web1
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3 cookie web22
```

### 6.1.3 验证 Cookie 信息

![image-20241002171058670](images/image-20241002171058670.png)

![image-20241002171138215](images/image-20241002171138215.png)



范例: 通过命令行验证

```bash
root@ubutun2204-1:~# curl -b WEBSERV=web11 192.168.159.103
wanglei web1 192.168.159.104

root@ubutun2204-1:~# curl -b WEBSERV=web22 192.168.159.103
wanglei web2 192.168.159.105
```

## 6.2 HAProxy 状态页

通过web界面，显示当前HAProxy的运行状态 

官方帮助：

```http
http://docs.haproxy.org/3.0/configuration.html#4-stats%20admin
```

### 6.2.1 状态页配置项

```bash
stats enable   #基于默认的参数启用stats page
stats hide-version   #将状态页中haproxy版本隐藏
stats refresh <delay> #设定自动刷新时间间隔，默认不自动刷新,以秒为单位
stats uri <prefix> #自定义stats page uri，默认值：/haproxy?stats 
stats realm <realm> #账户认证时的提示信息，示例：stats realm   HAProxy\ Statistics
stats auth <user>:<passwd> #认证时的账号和密码，可定义多个用户,每行指定一个用户.默认：no authentication
stats admin { if | unless } <cond> #启用stats page中的管理功能
```

### 6.2.2 启用状态页示例

```bash
listen stats
   mode http
   bind 0.0.0.0:9999
   stats enable
   stats hide-version
   stats realm HAProxy\ Stats\ Page #账户认证时的提示信息
   stats uri    /haproxy-status #自定义stats page uri
   stats auth   admin:123456
   stats auth haadmin:123456 #支持多个用户
   stats refresh 30
   stats admin if TRUE #开启管理功能，基于安全原因，不建议开启
```

### 6.2.3 登录状态页说明

```bash
pid = 31992 (process #1, nbproc = 1, nbthread = 4) #pid为当前pid号，process为当前进程号，nbproc和nbthread为一共多少进程和每个进程多少个线程
uptime = 0d 0h04m34s; warnings = 0 #启动了多长时间
system limits: memmax = unlimited; ulimit-n = 200039 #系统资源限制：内存/最大打开文件数/
maxsock = 200039; maxconn = 100000; reached = 0; maxpipes = 0 #最大socket连接数/单进程最大连接数/最大管道数maxpipes
current conns = 1; current pipes = 0/0; conn rate = 0/sec; bit rate = 0.000 kbps #当前连接数/当前管道数/当前连接速率
Running tasks: 0/22 (0 niced); idle = 100 % #运行的任务/当前空闲率

active UP： #在线服务器
backup UP： #标记为backup的服务器
active UP, going down： #监测未通过正在进入down过程
backup UP, going down： #备份服务器正在进入down过程
active DOWN, going up： #down的服务器正在进入up过程
backup DOWN, going up： #备份服务器正在进入up过程
active or backup DOWN： #在线的服务器或者是backup的服务器已经转换成了down状态
not checked： #标记为不监测的服务器
active or backup DOWN for maintenance (MAINT) #active或者backup服务器人为下线的
active or backup SOFT STOPPED for maintenance #active或者backup被人为软下线(人为将weight改成0)
```

![image-20241002173507191](images/image-20241002173507191.png)

### 6.2.4 Backend Server 信息说明

| session rate(每秒的连接会话信息)： | Errors(错误统计信息)：            |
| ---------------------------------- | --------------------------------- |
| cur:每秒的当前会话数量             | Req:错误请求量                    |
| max:每秒新的最大会话数量           | conn:错误链接量                   |
| limit:每秒新的会话限制量           | Resp:错误响应量                   |
| **sessions(会话信息)：**           | **Warnings(警告统计信息)：**      |
| cur:当前会话量                     | Retr:重新尝试次数                 |
| max:最大会话量                     | Redis:再次发送次数                |
| limit: 限制会话量                  |                                   |
| Total:总共会话量                   | **Server(real server信息)：**     |
| LBTot:选中一台服务器所用的总时间   | Status:后端机的状态，包括UP和DOWN |
| Last：和服务器的持续连接时间       | LastChk:持续检查后端服务器的时间  |
| **Weight:权重**                    |                                   |
| **Bytes(流量统计)：**              | Act:活动链接数量                  |
| In:网络的字节输入总量              | Bck:备份的服务器数量              |
| Out:网络的字节输出总量             | Chk:心跳检测时间                  |
| Dwn:后端服务器连接后都是DOWN的数量 |                                   |
| **Denied(拒绝统计信息)：**         | Dwntme:总的downtime时间           |
| Req:拒绝请求量                     | Thrtle:server 状态                |
| Resp:拒绝回复量                    |                                   |

### 6.2.5 利用状态页实现haproxy服务器的健康性检查

```bash
root@ubutun2204-1:~# curl -I -m 1 http://haadmin:123456@192.168.159.103:9999/haproxy-status
HTTP/1.1 200 OK
cache-control: no-cache
content-type: text/html
refresh: 30
connection: close

root@ubutun2204-1:~# echo $?
0
```

## 6.3 IP透传

web服务器中需要记录客户端的真实IP地址，用于做访问统计、安全防护、行为分析、区域排行等场 景。

### 6.3.1 Layer 4 与 Layer 7

- 四层：IP+PORT转发
- 七层：协议+内容交换

![image-20241002174610053](images/image-20241002174610053.png)

#### 6.3.1.1 四层负载

在LVS 传统的四层负载设备中，把client发送的报文目标地址(原来是负载均衡设备的IP地址)，根据均衡 设备设置的选择web服务器的规则选择对应的web服务器IP地址，这样client就可以直接跟此服务器建立 TCP连接并发送数据，而四层负载自身不参与建立连接.

而和LVS不同，haproxy是伪四层负载均衡，因为haproxy 需要分别和前端客户端及后端服务器建立连接

#### 6.3.1.2 七层代理

七层负载均衡服务器起了一个反向代理服务器的作用，服务器建立一次TCP连接要三次握手，而client要 访问Web Server要先与七层负载设备进行三次握手后建立TCP连接，把要访问的报文信息发送给七层负 载均衡；然后七层负载均衡再根据设置的均衡规则选择特定的 Web Server，然后通过三次握手与此台  Web Server建立TCP连接，然后Web Server把需要的数据发送给七层负载均衡设备，负载均衡设备再把 数据发送给client；所以，七层负载均衡设备起到了代理服务器的作用，七层代理需要和Client和后端服 务器分别建立连接

### 6.3.2 四层IP透传

```bash
# haproxy 配置：
listen wanglei_web
   bind :80
   mode tcp  #改成tcp协议
   log global
   balance roundrobin
   server web1 192.168.159.104:80 weight 1 send-proxy check inter 1000 fall 3 rise 3 #添加send-proxy
   
   
# 192.168.159.104 nginx配置：在访问日志中通过变量$proxy_protocol_addr 记录透传过来的客户端IP
 http {
 ...
 	# Logging Settings
	log_format main '$remote_addr - $remote_user [$time_local] "$request" "$proxy_protocol_addr"';
	##

	access_log /var/log/nginx/access.log main;
	server {
       listen       80 proxy_protocol; #启用此项，将无法直接访问此网站，只能通过四层代理访问	
 } 
```

抓包可以看到 `continuation` 信息中带有客户端的源IP

![image-20241002181442597](images/image-20241002181442597.png)

范例: nginx 开启四层日志功能

```bash
#nginx在开启proxy_protocol后，可以看客户端真实源IP
root@ubutun2204-1:~# tail -f /var/log/nginx/access.log 
192.168.159.103 - - [02/Oct/2024:10:18:38 +0000] "GET / HTTP/1.1" "192.168.159.1"
192.168.159.103 - - [02/Oct/2024:10:18:38 +0000] "GET / HTTP/1.1" "192.168.159.1"
192.168.159.103 - - [02/Oct/2024:10:18:39 +0000] "GET / HTTP/1.1" "192.168.159.1"
192.168.159.103 - - [02/Oct/2024:10:18:39 +0000] "GET / HTTP/1.1" "192.168.159.1"
192.168.159.103 - - [02/Oct/2024:10:18:39 +0000] "GET / HTTP/1.1" "192.168.159.1"

```

### 6.3.3 七层IP透传

当haproxy工作在七层的时候，也可以透传客户端真实IP至后端服务器

#### 6.3.3.1 HAProxy配置

在由haproxy发往后端主机的请求报文中添加“X-Forwarded-For"首部，其值为前端客户端的地址；用于 向后端主发送真实的客户端IP

```bash
option forwardfor [ except <network> ] [ header <name> ] [ if-none ]

[ except <network> ]：请求报请来自此处指定的网络时不予添加此首部，如haproxy自身所在网络
[ header <name> ]：使用自定义的首部名称，而非“X-Forwarded-For"，示例：X-client
[ if-none ] 如果没有首部才添加首部，如果有使用默认值
```

范例：

```bash
#haproxy 配置
defaults

#此为默认值,首部字段默认为：X-Forwarded-For
option forwardfor

#或者自定义首部,如:X-client
option forwardfor except 127.0.0.0/8 header X-client 

# listen配置
listen wanglei_web
   bind :80
   mode http
   log global
   balance roundrobin
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
```

#### 6.3.3.2 后端 Web 服务器日志格式配置

配置web服务器，记录负载均衡透传的客户端IP地址

```bash
#nginx 日志格式：默认就支持
$proxy_add_x_forwarded_for：包括客户端IP和中间经过的所有代理的IP
$http_x_forwarded_For：只有客户端IP

http {
  # Logging Settings
	log_format main '"$proxy_add_x_forwarded_for" - $remote_user [$time_local] "$request" "$proxy_protocol_addr" "$http_x_forwarded_for"';
        ##
	access_log /var/log/nginx/access.log main;
	
}


```

#### 6.3.3.3 验证客户端IP地址

```bash
root@ubutun2204-1:~# tail -f /var/log/nginx/access.log 
"192.168.159.1, 192.168.159.103" - - [02/Oct/2024:10:44:58 +0000] "GET / HTTP/1.1" "-" "192.168.159.1"
"192.168.159.1, 192.168.159.103" - - [02/Oct/2024:10:44:58 +0000] "GET / HTTP/1.1" "-" "192.168.159.1"
"192.168.159.1, 192.168.159.103" - - [02/Oct/2024:10:44:59 +0000] "GET / HTTP/1.1" "-" "192.168.159.1"
"192.168.159.1, 192.168.159.103" - - [02/Oct/2024:10:44:59 +0000] "GET / HTTP/1.1" "-" "192.168.159.1"
```

## 6.4 报文修改

### 6.4.1 新版

**2.1版本以上用下面指令http-request和http-response代替**

官方文档：

```http
https://docs.haproxy.org/3.0/configuration.html#4-http-request
https://docs.haproxy.org/3.0/configuration.html#4-http-response
```

配置说明：

```bash
#修改请求host首部,默认host首部会保留客户端原首部haproxy不会修改
http-request set-header host www.wanglei.com

#添加向后端服务器发送的请求报文首部
http-request add-header <name> <fmt> [ { if | unless } <condition> ]
#示例：http-request add-header X-Haproxy-Current-Date %T
#删除向后端服务器发送的请求报文首部
http-request del-header <name> [ { if | unless } <condition> ]


#修改响应首部
http-response set-header server wangleiserver

#添加向客户端发送的响应报文首部
http-response add-header <name> <fmt> [ { if | unless } <condition> ]
#删除向客户端发送的响应报文首部
http-response del-header <name>
#示例：http-response del-header Server 
```

范例: 添加向后端服务器发送的请求报文首部

```bash
# haproxy配置
root@ubutun2204-1:~# cat  /etc/haproxy/conf.d/wanglei_web.cfg 
listen wanglei_web
   bind :80
   mode http
   log global
   http-request add-header X-Haproxy-Current-Date %T
   balance roundrobin
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3


# 修改nginx的log
http {
   ....
   log_format main '"$proxy_add_x_forwarded_for" - $remote_user [$time_local] "$request" "$proxy_protocol_addr" "$http_x_forwarded_for" --- "$http_x_haproxy_current_date"';
}

# 查看log
root@ubutun2204-1:~# tail -f /var/log/nginx/access.log
"192.168.159.1, 192.168.159.103" - - [02/Oct/2024:11:27:33 +0000] "GET / HTTP/1.1" "-" "192.168.159.1" --- "02/Oct/2024:11:27:33 +0000"
```

范例: 修改向后端服务器的请求首部user-agent

```bash
root@ubutun2204-1:~# cat    /etc/haproxy/conf.d/wanglei_web.cfg 
listen wanglei_web
   bind :80
   mode http
   log global
   http-request set-header user-agent test-browser
   balance roundrobin
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
```

范例: 添加向客户端发送的响应报文首部

```bash
listen wanglei_web
   bind :80
   mode http
   log global
   http-response add-header X-BOT haproxy-wanglei
   balance roundrobin
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
   
root@ubutun2204-1:~# systemctl restart haproxy.service 
root@ubutun2204-1:~# curl -I 192.168.159.103
HTTP/1.1 200 OK
server: nginx/1.18.0 (Ubuntu)
date: Wed, 02 Oct 2024 11:33:35 GMT
content-type: text/html
content-length: 29
last-modified: Mon, 30 Sep 2024 07:40:53 GMT
etag: "66fa5605-1d"
accept-ranges: bytes
x-bot: haproxy-wanglei
```

范例: 修改向客户端发送的响应报文首部,实现自定义Server首部

```bash
root@ubutun2204-1:~# cat    /etc/haproxy/conf.d/wanglei_web.cfg 
listen wanglei_web
   bind :80
   mode http
   log global
   http-response set-header server wanglei-server
   balance roundrobin
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3


root@ubutun2204-1:~# systemctl reload haproxy.service 
root@ubutun2204-1:~# curl -I 192.168.159.103
HTTP/1.1 200 OK
date: Wed, 02 Oct 2024 11:35:30 GMT
content-type: text/html
content-length: 29
last-modified: Mon, 30 Sep 2024 07:40:28 GMT
etag: "66fa55ec-1d"
accept-ranges: bytes
server: wanglei-server
```

## 6.5 自定义日志格式

log global 开启日志功能，默认只会在记录下面格式的日志

```http
root@ubutun2204-1:~# tail -f /var/log/haproxy.log 
Oct  2 11:35:30 localhost haproxy[110128]: Connect from 192.168.159.103:35970 to 192.168.159.103:80 (wanglei_web/HTTP)
```

`option httplog` 可以采用 http 格式记录下来，并且可以使用相关指令将特定信息记录在haproxy的日志 中 但一般不建议开启，这会加重 HAProxy 负载

### 6.5.1 配置选项

```bash
log global 								#开启记录日志,默认不开启
option httplog                          #开启记录httplog日志格式选项
capture cookie <name> len <length>      #捕获请求和响应报文中的 cookie及值的长度,将之记录到日志 
capture request header <name> len <length> #捕获请求报文中指定的首部内容和长度并记录日志
capture response header <name> len <length> #捕获响应报文中指定的内容和长度首部并记录日志


#示例
log global 
option httplog
capture request header Host len  256
capture request header User-Agent len 512 
capture request header Referer len 15
capture request header X-Forwarded-For len 15
```

同时开启日志功能log global和option httplog，记录日志格式如

```bash
root@ubutun2204-1:~# tail -f /var/log/haproxy.log 
Oct  2 11:41:04 localhost haproxy[110255]: 192.168.159.1:55683 [02/Oct/2024:11:41:04.997] wanglei_web wanglei_web/web1 0/0/0/1/1 200 270 - - ---- 1/1/0/0/0 0/0 {|Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36||} "GET / HTTP/1.1"
Oct  2 11:41:05 localhost haproxy[110255]: 192.168.159.1:55683 [02/Oct/2024:11:41:05.133] wanglei_web wanglei_web/web2 0/0/1/1/2 200 270 - - ---- 1/1/0/0/0 0/0 {|Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36||} "GET / HTTP/1.1"
Oct  2 11:41:05 localhost haproxy[110255]: 192.168.159.1:55683 [02/Oct/2024:11:41:05.299] wanglei_web wanglei_web/web1 0/0/0/1/1 200 270 - - ---- 1/1/0/0/0 0/0 {|Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/129.0.0.0 Safari/537.36||} "GET / HTTP/1.1"
```

## 6.6 压缩功能

对响应给客户端的报文进行压缩，以节省网络带宽，但是会占用部分CPU性能

建议在后端服务器开启压缩功能，而非在HAProxy上开启压缩

注意：默认Ubuntu的包安装nginx开启压缩功能

### 6.6.1 配置选项

```bash
compression algo <algorithm> ... #启用http协议中的压缩机制，常用算法有gzip，deflate

#压缩算法<algorithm>支持下面类型：
     identity #debug调试使用的压缩方式
     gzip #常用的压缩方式，与各浏览器兼容较好
     deflate #有些浏览器不支持
     raw-deflate #新式的压缩方式

compression type <mime type> ... #要压缩的文件类型MIME


#示例：
compression algo gzip deflate
compression type text/html text/css text/plain 
```

### 6.6.2 配置示例

```bash
root@ubutun2204-1:~# cat /etc/haproxy/conf.d/wanglei_web.cfg
listen wanglei_web
   bind :80
   mode http
   log global 
   option httplog
   compression algo gzip deflate  #启用压缩和指定算法
   compression type compression type text/plain text/html text/css text/xml text/javascript application/javascript  #指定压缩文件类型
   balance roundrobin
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3

# 后端服务器nginx关闭gzip
root@ubutun2204-1:~# vim /etc/nginx/nginx.conf
http {
 ...
 gzip off
}

#后端服务器准备一个文本文件
root@ubutun2204-1:~# dd if=/dev/zero of=/var/www/html/m.txt bs=1M count=100
root@ubutun2204-1:~# ll /var/www/html/m.txt -h
-rw-r--r-- 1 root root 100M Oct  2 11:52 /var/www/html/m.txt
```

### 6.6.3 验证压缩功能

```bash
root@ubutun2204-1:~# curl -is --compressed   192.168.159.103/m.txt|less
HTTP/1.1 200 OK
server: nginx/1.18.0 (Ubuntu)
date: Wed, 02 Oct 2024 11:57:37 GMT
content-type: text/plain
last-modified: Wed, 02 Oct 2024 11:52:25 GMT
etag: W/"66fd33f9-6400000"
accept-ranges: bytes
transfer-encoding: chunked
vary: Accept-Encoding
content-encoding: deflate
......
```

## 6.7 后端服务器健康性监测

### 6.7.1 三种状态监测方式

```http
基于四层的传输端口做状态监测，此为默认方式
基于指定 URI 做状态监测,需要访问整个页面资源,占用更多带宽
基于指定 URI 的 request 请求头部内容做状态监测，占用较少带宽,建议使用此方式
```

### 6.7.2 基于应用层http协议进行健康性检测

基于应用层http协议，采有不同的监测方式，对后端real server进行状态监测

注意: 此方式会导致在后端服务器生成很多的HAProxy发起的访问日志

```bash
option httpchk   #支持Listen和backendf块，启用七层健康性检测，对tcp 和 http 模式都支持，
默认为：OPTIONS / HTTP/1.0，nginx默认不支持OPTIONS
option httpchk <uri>
option httpchk <method> <uri>
option httpchk <method> <uri> <version>

# 期望以上检查得到的响应码
http-check expect [!] <match> <pattern>
#示例：
http-check expect status 200
http-check expect ! rstatus ^5 #支持正则表达式

#关于HTTP/1.1的说明
<version> is the optional HTTP version string. It defaults to "HTTP/1.0" but 
some servers might behave incorrectly in HTTP 1.0, so turning it to HTTP/1.1 may 
sometimes help. Note that the Host field is         mandatory in HTTP/1.1, and 
as a trick, it is possible to pass it after "\r\n" following the version string.
```

### 6.7.3 配置示例

```bash
root@ubutun2204-1:~# cat  /etc/haproxy/conf.d/wanglei_web.cfg 
listen wanglei_web
   bind :80
   mode http
   log global 
   option httplog
   #option httpchk GET /monitor/check.html #默认HTTP/1.0
  #option httpchk GET /monitor/check.html HTTP/1.0
   option httpchk GET /monitor/check.html HTTP/1.1
   http-check send hdr Host www.lei.com #注意：新版要求：HTTP/1.1强制要求必须有Host字段
   balance roundrobin
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
   
#在所有后端服务建立检测页面
root@ubutun2204-1:~# mkdir /var/www/html/monitor/
root@ubutun2204-1:~# echo monitor > /var/www/html/monitor/check.html

#关闭一台Backend服务器
root@ubutun2204-1:~# systemctl stop nginx.service
```

### 6.7.4 验证http监测

查看到状态页，可以看到启用了七层检测功能：**LastChk字段：L7**

![image-20241002210311128](images/image-20241002210311128.png)

```bash
# 后端服务器查看访问日志
root@ubutun2204-1:~# tail -f /var/log/nginx/access.log 
"192.168.159.103" - - [02/Oct/2024:13:03:38 +0000] "GET /monitor/check.html HTTP/1.1" "-" "-"
"192.168.159.103" - - [02/Oct/2024:13:03:39 +0000] "GET /monitor/check.html HTTP/1.1" "-" "-"
"192.168.159.103" - - [02/Oct/2024:13:03:40 +0000] "GET /monitor/check.html HTTP/1.1" "-" "-"
"192.168.159.103" - - [02/Oct/2024:13:03:41 +0000] "GET /monitor/check.html HTTP/1.1" "-" "-"
```

## 6.8 ACL

访问控制列表（ACL，Access Control Lists）是一种基于包过滤的访问控制技术，它可以根据设定的条 件对经过服务器传输的数据包进行过滤(条件匹配)，即对接收到的报文进行匹配和过滤，基于请求报文头 部中的源地址、源端口、目标地址、目标端口、请求方法、URL、文件后缀等信息内容进行匹配并执行 进一步操作，比如允许其通过或丢弃。

官方文档：

```http
http://docs.haproxy.org/3.0/configuration.html#7
```

### 6.8.1 定义ACL配置选项

```http
acl   <aclname> <criterion>   [flags]     [operator]   [<value>]
acl     名称     匹配规范     匹配模式     具体操作符     操作对象类型
```

#### 6.8.1.1 ACL-Name

```bash
acl   image_service hdr_dom(host)   -i   img.wang.com

#ACL名称，可以使用大字母A-Z、小写字母a-z、数字0-9、冒号：、点.、中横线和下划线，并且严格区分大小写，比如:my_acl和My_Acl就是两个完全不同的acl
```

#### 6.8.1.2 ACL-criterion

**定义ACL匹配规范，即：判断条件**

```bash
hdr string，提取在一个HTTP请求报文的首部
hdr（[<name> [，<occ>]]）：完全匹配字符串,header的指定信息，<occ> 表示在多值中使用的值的出
现次数
hdr_beg（[<name> [，<occ>]]）：前缀匹配，header中指定匹配内容的begin
hdr_end（[<name> [，<occ>]]）：后缀匹配，header中指定匹配内容end
hdr_dom（[<name> [，<occ>]]）：域匹配，header中的domain name
hdr_dir（[<name> [，<occ>]]）：路径匹配，header的uri路径
hdr_len（[<name> [，<occ>]]）：长度匹配，header的长度匹配
hdr_reg（[<name> [，<occ>]]）：正则表达式匹配，自定义表达式(regex)模糊匹配
hdr_sub（[<name> [，<occ>]]）：子串匹配，header中的uri模糊匹配

#示例
hdr(<string>) 用于测试请求头部首部指定内容
hdr_dom(host) 请求的host名称，如 www.wanglei.com,m.wanglei.com
hdr_beg(host) 请求的host开头，如 www.   img.   video.   download.   ftp.
hdr_end(host) 请求的host结尾，如 .com   .net   .cn 

#示例
acl bad_agent hdr_sub(User-Agent) -i curl wget
http-request deny  if bad_agent

hdr(host) ==>www.wang.org:8080
hdr_domain(host) ==> www.wang.org


# 有些功能是类似的，比如以下几个都是匹配用户请求报文中host的开头是不是www
acl short_form hdr_beg(host)       www.
acl alternate1 hdr_beg(host) -m beg www.
acl alternate2 hdr_dom(host) -m beg www.
acl alternate3 hdr(host)     -m beg www.


base: string
#返回第一个主机头和请求的路径部分的连接，该请求从主机名开始，并在问号之前结束,对虚拟主机有用,下面的例子中是两个#中间的内容,实际#是没有的
<scheme>://<user>:<password>@#<host>:<port>/<path>;<params>#?<query>#<frag>
 base     : exact string match
 base_beg : prefix match
 base_dir : subdir match
 base_dom : domain match
 base_end : suffix match
 base_len : length match
 base_reg : regex match
 base_sub : substring match

path : string
<scheme>://<user>:<password>@<host>:<port>#/<path>;<params>#?<query>#<frag>
 path     : exact string match
 path_beg : prefix match  #请求的URL开头，如/static、/images、/img、/css
 path_end : suffix match  #请求的URL中资源的结尾，如 .gif .png .css .js .jpg .jpeg
 path_dom : domain match
 path_dir : subdir match
 path_len : length match
 path_reg : regex match
 path_sub : substring match


#示例
  path_beg -i /haproxy-status/
  path_end .jpg .jpeg .png .gif 
  path_reg ^/images.*\.jpeg$ 
  path_sub image 
  path_dir jpegs
  path_dom www.wanglei.org


url : string
#提取请求中的整个URL。一个典型的应用是具有预取能力的缓存，以及需要从数据库聚合多个信息并将它们保存在缓存中的网页门户入口，推荐使用path
 url ：exact string match
 url_beg : prefix match
 url_dir : subdir match
 url_dom : domain match
 url_end : suffix match
 url_len : length match
 url_reg : regex match
 url_sub : substring match
 
 
src   #源IP
src_port #源PORT

dst #目标IP
dst_port #目标PORT

#示例
acl invalid_src src 10.0.0.7 192.168.1.0/24
acl invalid_src src 172.16.0.0/24
http-request deny if ! invalid_src

acl invalid_port src_port 0:1023

status : integer  #返回在响应报文中的状态码 

#七层协议
acl valid_method method GET HEAD
http-request deny if ! valid_method
```

#### 6.8.1.3 ACL-flags

**ACL匹配模式**

```bash
-i 不区分大小写
-m 使用指定的pattern匹配方法，beg 开头，end 结尾
-n 不做DNS解析
-u 禁止acl重名，否则多个同名ACL匹配或关系
```

#### 6.8.1.4 ACL-operator

ACL 操作符

```http
整数比较：eq、ge、gt、le、lt
字符比较：
- exact match     (-m str) :字符串必须完全匹配模式
- substring match (-m sub) :在提取的字符串中查找模式，如果其中任何一个被发现，ACL将匹配
- prefix match   (-m beg) :在提取的字符串首部中查找模式，如果其中任何一个被发现，ACL将匹配
- suffix match   (-m end) :将模式与提取字符串的尾部进行比较，如果其中任何一个匹配，则ACL进行匹配
- subdir match   (-m dir) :查看提取出来的用斜线分隔（“/"）的字符串，如其中任一个匹配，则ACL进行匹配
- domain match   (-m dom) :查找提取的用点（“."）分隔字符串，如果其中任何一个匹配，则ACL进行匹配
```

#### 6.8.1.5 ACL-value

value的类型

```bash
The ACL engine can match these types against patterns of the following types :
- Boolean #布尔值
- integer or integer range #整数或整数范围，比如用于匹配端口范围
- IP address / network #IP地址或IP范围, 192.168.0.1 ,192.168.0.1/24
- string--> www.wang.com
 exact #精确比较
 substring #子串
 suffix #后缀比较
 prefix #前缀比较
 subdir #路径， /wp-includes/js/jquery/jquery.js
 domain #域名，www.wang.com
- regular expression #正则表达式
- hex block #16进制
```

### 6.8.2 多个ACL的组合调用方式

**多个ACL的逻辑处理**

```http
与：隐式（默认）使用
或：使用“or" 或 “||"表示
否定：使用 "!" 表示 
```

**多个ACL调用方式：**

```bash
#示例：
if valid_src valid_port #与关系，ACL中A和B都要满足为true，默认为与
if invalid_src || invalid_port  #或，ACL中A或者B满足一个为true
if ! invalid_src #非，取反，不满足ACL才为true
```

### 6.8.3 ACL示例：域名匹配

```bash
# haproxy配置
root@ubutun2204-1:~# cat /etc/haproxy/conf.d/wanglei_web.cfg 
frontend wanglei_web
   bind :80
   mode http
   log global 
   option httplog
   balance roundrobin
###################### acl setting ###############################
   acl pc_domain hdr_dom(host) -i www.wanglei.com
   acl mobile_domain hdr_dom(host) -i mobile.wanglei.com
###################### acl hosts #################################
   use_backend pc_hosts if pc_domain
   use_backend mobile_hosts if mobile_domain
   default_backend pc_hosts  #所有ACL都不匹配,则使用的默认backend

###################### backend hosts #############################
backend pc_hosts
   mode http
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
backend mobile_hosts
   mode http
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
```

测试结果：

```bash
root@ubutun2204-1:~# curl -H "host: www.wanglei.com" 192.168.159.103
wanglei web1 192.168.159.104 ---pc
root@ubutun2204-1:~# curl -H "host: mobile.wanglei.com" 192.168.159.103
wanglei web2 192.168.159.105 ---mobile
```

### 6.8.4 ACL示例：基于源IP或子网调度访问

将指定的源地址调度至指定的web服务器组。

```bash
root@ubutun2204-1:~# cat  /etc/haproxy/conf.d/wanglei_web.cfg 
frontend wanglei_web
   bind :80
   mode http
   log global 
   option httplog
   balance roundrobin
###################### acl setting ###############################
   acl pc_domain hdr_dom(host) -i www.wanglei.com
   acl mobile_domain hdr_dom(host) -i mobile.wanglei.com
   acl ip_range_test src 192.168.159.0/24 #基于源地址的ACL,定义多个ACL的顺序无关
   acl ip_range_test2 src 192.168.159.1
###################### acl hosts #################################
   use_backend pc_hosts if ip_range_test #放在前面的ACL规则优先生效,引用ACL时,严格的ACL应放在前面
   use_backend pc_hosts if pc_domain
   use_backend mobile_hosts if mobile_domain
   default_backend pc_hosts

###################### backend hosts #############################
backend pc_hosts
   mode http
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
backend mobile_hosts
   mode http
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3

```

测试结果:

```bash
#可以发现第一个acl匹配成功后，后面的acl将不匹配
root@ubutun2204-1:~# hostname -I
192.168.159.103 
root@ubutun2204-1:~# curl -H "host: www.wanglei.com" 192.168.159.103
wanglei web1 192.168.159.104 ---pc
root@ubutun2204-1:~# curl -H "host: mobile.wanglei.com" 192.168.159.103
wanglei web1 192.168.159.104 ---pc
```

### 6.8.5 ACL示例：基于源地址的访问控制

拒绝指定IP或者IP范围访问

```bash
root@ubutun2204-1:~# cat  /etc/haproxy/conf.d/wanglei_web.cfg 
frontend wanglei_web
   bind :80
   mode http
   log global 
   option httplog
   balance roundrobin
###################### acl setting ###############################
   acl deny_ip src 192.168.159.0/24
###################### acl hosts #################################
   http-request deny if deny_ip
   default_backend mobile_hosts

###################### backend hosts #############################
backend pc_hosts
   mode http
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
backend mobile_hosts
   mode http
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
```

测试：

```bash
root@ubutun2204-1:~# curl 192.168.159.103
<html><body><h1>403 Forbidden</h1>
Request forbidden by administrative rules.
</body></html>
```

### 6.8.6 ACL示例：匹配浏览器类型

匹配客户端浏览器，将不同类型的浏览器调动至不同的服务器组

范例: 

```bash
root@ubutun2204-1:~# cat  /etc/haproxy/conf.d/wanglei_web.cfg 
frontend wanglei_web
   bind :80
   mode http
   log global 
   option httplog
   balance roundrobin
###################### acl setting ###############################
   acl acl_user_agent hdr_sub(User-Agent)  -i curl wget #基于浏览器的ACL
   acl acl_user_agent_ab hdr_sub(User-Agent)  -i ApacheBench 
###################### acl hosts #################################
   redirect prefix http://www.baidu.com  if acl_user_agent #302 临时重定向至新URL
   http-request deny if acl_user_agent_ab #拒绝ab
   default_backend mobile_hosts

###################### backend hosts #############################
backend pc_hosts
   mode http
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
backend mobile_hosts
   mode http
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3

```

测试

```bash
root@ubutun2204-1:~# curl -I 192.168.159.103
HTTP/1.1 302 Found
content-length: 0
location: http://www.baidu.com/
cache-control: no-cache

#模拟ab
root@ubutun2204-1:~# curl -A ApacheBench 192.168.159.103
<html><body><h1>403 Forbidden</h1>
Request forbidden by administrative rules.
</body></html>
```

### 6.8.7 ACL示例：基于文件后缀名实现动静分离

```bash
root@ubutun2204-1:~# cat  /etc/haproxy/conf.d/wanglei_web.cfg 
frontend wanglei_web
   bind :80
   mode http
   log global 
   option httplog
   balance roundrobin
###################### acl setting ###############################
   acl acl_static path_end -i .jpg .jpeg .png .gif .css .js .html #基于文件后缀名的ACL
   acl acl_php path_end -i .php 
###################### acl hosts #################################
   use_backend static_hosts if acl_static
   use_backend php_hosts if acl_php
   default_backend static_hosts

###################### backend hosts #############################
backend static_hosts
   mode http
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
backend php_hosts
   mode http
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
   
# 分别在后端两台主机准备相关文件
root@ubutun2204-1:/var/www/html# hostname -I
192.168.159.104
root@ubutun2204-1:/var/www/html# ls | grep jpg
cncf.jpg


root@ubutun2204-1:~# hostname -I
192.168.159.105 
root@ubutun2204-1:~# cat  /var/www/html/test.php
<?php
echo "<h1>http://192.168.159.105/test.php</h1>\n";
?>
```

测试：

```bash
root@ubutun2204-1:~# curl 192.168.159.103/test.php
<?php
 echo "<h1>http://192.168.159.105/test.php</h1>\n";
?>
```

### 6.8.8 ACL示例：匹配访问路径实现动静分离

```bash
root@ubutun2204-1:~# cat  /etc/haproxy/conf.d/wanglei_web.cfg 
frontend wanglei_web
   bind :80
   mode http
   log global 
   option httplog
   balance roundrobin
###################### acl setting ###############################
   acl acl_static path_beg -i /static /images /javascript  #基于路径的ACL
   acl acl_static path_end -i .jpg .jpeg .png .gif .css .js .html .htm #ACL同名为或关系
   acl acl_php path_beg -i /api
###################### acl hosts #################################
   use_backend static_hosts if acl_static
   use_backend php_hosts if acl_php
   default_backend static_hosts

###################### backend hosts #############################
backend static_hosts
   mode http
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
backend php_hosts
   mode http
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3
   
#创建相关文件
root@ubutun2204-1:~# mkdir /var/www/html/static
root@ubutun2204-1:~# echo 192.168.159.104  > /var/www/html/static/test.html

#测试访问
root@ubutun2204-1:~# curl 192.168.159.103/static/test.html
192.168.159.104
```

### 6.8.9 ACL示例：预定义ACL使用

官方帮助文档：

```http
http://docs.haproxy.org/3.0/configuration.html#7.4
```

#### 6.8.9.1 预定义ACL

![image-20241003133845909](images/image-20241003133845909.png)

#### 6.8.9.2 预定义ACL使用

范例： 禁止TRACE方法和HTTP/1.1协议

```bash
root@ubutun2204-1:~# cat  /etc/haproxy/conf.d/wanglei_web.cfg 
frontend wanglei_web
   bind :80
   mode http
   log global 
   option httplog
   balance roundrobin
###################### acl setting ###############################
   acl acl_static path_beg -i /static /images /javascript
   acl acl_static path_end -i .jpg .jpeg .png .gif .css .js .html .htm
   acl acl_php path_beg -i /api
###################### acl hosts #################################
   use_backend static_hosts if acl_static
   use_backend php_hosts if acl_php
   http-request deny if METH_TRACE HTTP_1.1 #引用预定义的ACL，多个ACL默认为与关系
   default_backend static_hosts

###################### backend hosts #############################
backend static_hosts
   mode http
   server web1 192.168.159.104:80 weight 1 check inter 1000 fall 3 rise 3
backend php_hosts
   mode http
   server web2 192.168.159.105:80 weight 1 check inter 1000 fall 3 rise 3

```
## 6.9 自定义 HAProxy 错误界面

对指定的报错进行重定向，进行优雅的显示错误页面

使用errorfile和errorloc指令的两种方法，可以实现自定义各种错误页面

默认情况下，所有后端服务器都down机后，会显示下面页面

![image-20241002210557369](images/image-20241002210557369.png)

### 6.9.1 基于自定义的错误页面文件

**注意：页面文件格式错误可能会导致Haproxy服务无法启动**

```bash
#自定义错误页 
errorfile <code> <file>

<code> #HTTP status code.支持200, 400, 403, 405, 408, 425, 429, 500, 502，503,504
<file> #包含完整HTTP响应头的错误页文件的绝对路径。 建议后缀为".http"，以和一般的html文件相区分


#示例
errorfile 400 /etc/haproxy/errorfiles/400badreq.http
errorfile 403 /etc/haproxy/errorfiles/403forbid.http
errorfile 503 /etc/haproxy/errorfiles/503sorry.http 
```

范例：

```bash
defaults
#option forwardfor
#no option http-use-htx 支持html文件,此设置和版本有关，2.1不支持
#...... 
#加下面行
errorfile 500 /usr/local/haproxy/html/500.http
errorfile 502 /usr/local/haproxy/html/502.http
errorfile 503 /usr/local/haproxy/html/503.http
```

范例：

```bash
root@ubutun2204-1:~# cat  /etc/haproxy/haproxy.cfg
defaults
   option http-keep-alive
   option forwardfor
   maxconn 100000
   mode http
   timeout connect 300000ms
   timeout client 300000ms
   timeout server 300000ms
   #no option http-use-htx 支持html文件,此设置和版本有关，2.1不支持
   errorfile 503 /apps/haproxy/html/503.http
listen ...


root@ubutun2204-1:~# cat  /apps/haproxy/html/503.http
HTTP/1.1 503 Service Unavailable
Content-Type:text/html;charset=utf-8

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>报错页面</title>
</head>
<body>
<center><h1>网站维护中......请稍候再试</h1></center>
<center><h2>联系电话：400-123-4567</h2></center>
<center><h3>503 Service Unavailable</h3></center>
</body>

```

将后端服务器down，可以观察到以下页面

![image-20241002211726113](images/image-20241002211726113.png)

范例：启用 no option http-use-htx

```bash

defaults
   ...
   no option http-use-htx #在defaults 块中添加
   errorfile 503 /apps/haproxy/html/503.html
   
root@ubutun2204-1:~# cat  /apps/haproxy/html/503.html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>报错页面</title>
</head>
<body>
<center><h1>网站维护中......请稍候再试</h1></center>
<center><h2>联系电话：400-123-4567</h2></center>
<center><h3>503 Service Unavailable</h3></center>
</body>

#可以看到下面
```

![image-20241002212413569](images/image-20241002212413569.png)



### 6.9.2 基于http重定向错误页面

```bash
#错误页面重定向
errorloc <code> <url>
#相当于errorloc302 <code> <url>，利用302重定向至指URL

#示例：
errorloc 503 http://www.baidu.com
```

范例: 

```bash
root@ubutun2204-1:~# cat  /etc/haproxy/haproxy.cfg
defaults
   option http-keep-alive
   option forwardfor
   maxconn 100000
   mode http
   timeout connect 300000ms
   timeout client 300000ms
   timeout server 300000ms
   #no option http-use-htx
   #errorfile 503 /apps/haproxy/html/503.html
   errorloc 503 http://www.baidu.com/

#浏览器访问http://haproxy/ 302自动跳转至百度页面
```

![image-20241002212932604](images/image-20241002212932604.png)

## 6.10 HAProxy 四层负载

针对除HTTP以外的TCP协议应用服务访问的应用场景

```http
MySQL
Redis
Memcached
RabbitMQ
```

问题: 后端服务器到底是与haproxy还是和客户端建立三次握手呢?

### 6.10.1 四层负载示例

注意：如果使用frontend和backend，一定在 frontend 和 backend 段中都指定mode tcp 

```http
listen redis-port
   bind 192.168.159.103:6379
   mode tcp
   balance leastconn
   server server1 192.168.159.104:6379 check
   server server2 192.168.159.105:6379 check backup
```

范例：对 MySQL 服务实现四层负载

```bash
root@ubutun2204-1:~# cat   /etc/haproxy/conf.d/wanglei_mysql.cfg 
listen wanglei_mysql
   bind 192.168.159.103:3306
   mode tcp
   balance leastconn
   server server1 192.168.159.104:3306 check
   server server2 192.168.159.105:3306 check

root@ubutun2204-1:~# systemctl reload haproxy.service

#在后端服务器安装和配置mysql8.0服务
root@ubutun2204-1:~# apt install mysql-server
root@ubutun2204-1:~# mysql -e "CREATE USER 'test'@'%' IDENTIFIED BY '123456'"
root@ubutun2204-1:~# mysql -e "grant all privileges on *.* to 'test'@'%'"
root@ubutun2204-1:~# vim   /etc/mysql/mysql.conf.d/mysqld.cnf
server-id=104 #在另一台主机为105
root@ubutun2204-1:~# systemctl restart mysql.service



# 测试
root@ubutun2204-1:~# mysql -utest -p123456 -h192.168.159.103 -e 'select @@server_id'
+-------------+
| @@server_id |
+-------------+
|         104 |
+-------------+
root@ubutun2204-1:~# mysql -utest -p123456 -h192.168.159.103 -e 'select @@server_id'
+-------------+
| @@server_id |
+-------------+
|         105 |
+-------------+
```

![image-20241003141124391](images/image-20241003141124391.png)

### 6.10.2 ACL示例-四层访问控制

```bash
frontend web_host
  bind 10.0.0.7:80
  mode http
  balance roundrobin
  log global
  option httplog
###################### acl setting ###############################  
  acl invalid_src src 192.168.1.0/24 10.0.0.8
###################### acl hosts #################################
  tcp-request connection reject if invalid_src     #四层ACL控制  
  default_backend default_web 
################### backend hosts ################################
backend php_server_host
  mode http
  server web1 10.0.0.17 check inter 2000 fall 3 rise 5
  
backend static_path_host
  mode http
  server web1 10.0.0.27 check inter 2000 fall 3 rise 5
  
backend default_web
  mode http
  server web1 10.0.0.37:80 check inter 2000 fall 3 rise 5

```

## 6.11 HAProxy Https 实现

haproxy支持https,基于性能考虑,证书是在后端服务器比如nginx上实现,即用户到haproxy利用tcp模式 再到后端服务器

范例: 基于tcp 模式实现

```bash
listen web_http                                                                 
                            
     bind 192.168.159.103:80
     redirect scheme https if !{ ssl_fc }
     mode http
     log global
     server web1  192.168.159.104:80 check
     server web2  192.168.159.105:80 check
listen web_https
     bind 192.168.159.103:443
     mode tcp
     log global
     server web1  192.168.159.104:443 check
     server web2  192.168.159.105:443 check
```

Haproxy 可以实现 Https 的证书安全,即从用户到haproxy为https,从haproxy到后端服务器用http通信

```bash
#配置HAProxy支持https协议，支持ssl会话；
     bind *:443 ssl crt /PATH/TO/SOME_PEM_FILE 
     
 #指令 crt 后证书文件为PEM格式，需要同时包含证书和所有私钥 
     cat demo.key demo.crt > demo.pem
     
#把80端口的请求利用302重向定443
      bind *:80
      redirect scheme https if !{ ssl_fc } 
#向后端传递用户请求的协议和端口（frontend或backend）
      http_request set-header X-Forwarded-Port %[dst_port]
      http_request add-header X-Forwared-Proto https if { ssl_fc }
```

### 6.11.1 证书制作

```bash
root@ubutun2204-1:~# mkdir /etc/haproxy/certs/
root@ubutun2204-1:~# cd /etc/haproxy/certs/
root@ubutun2204-1:/etc/haproxy/certs# openssl genrsa -out haproxy.key 2048
root@ubutun2204-1:/etc/haproxy/certs# openssl req -new -x509 -key haproxy.key -out haproxy.crt -subj "/CN=www.wanglei.com" -days 365
root@ubutun2204-1:/etc/haproxy/certs# cat haproxy.key haproxy.crt > haproxy.pem
root@ubutun2204-1:/etc/haproxy/certs# ll
total 20
drwxr-xr-x 2 root root 4096 Oct  3 06:22 ./
drwxr-xr-x 4 root root 4096 Oct  3 06:20 ../
-rw-r--r-- 1 root root 1131 Oct  3 06:21 haproxy.crt
-rw------- 1 root root 1704 Oct  3 06:21 haproxy.key
-rw-r--r-- 1 root root 2835 Oct  3 06:22 haproxy.pem
root@ubutun2204-1:/etc/haproxy/certs# openssl x509 -in haproxy.pem -noout -text 
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            07:e8:92:89:6e:c9:97:22:9b:32:ed:ad:b0:8b:14:94:5d:59:8b:3c
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: CN = www.wanglei.com
        Validity
            Not Before: Oct  3 06:21:58 2024 GMT
            Not After : Oct  3 06:21:58 2025 GMT
        Subject: CN = www.wanglei.com
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                Public-Key: (2048 bit)
                Modulus:
                    00:88:25:3a:9a:ff:fc:37:9d:f6:98:c2:cb:e7:99:
                    0e:46:19:2d:af:1b:ba:c8:eb:3b:83:a1:a4:87:16:
                    29:f9:71:e8:6e:3a:b5:4b:58:ab:b7:96:ac:51:a8:
                    8c:64:17:e6:7e:22:fb:4e:75:45:b6:da:0e:c3:40:
                    79:7c:06:39:b2:97:4a:19:4b:7e:0e:fb:66:1e:5d:
                    ce:3a:01:4a:5c:94:8a:fb:e5:42:b6:ee:02:64:73:
                    4f:12:6c:6d:07:74:8a:21:19:1c:61:d3:1c:f5:2d:
                    8d:c2:0f:37:a2:b5:8a:f6:c9:c9:c1:4c:8d:d5:06:
                    b5:c9:19:75:f2:54:3b:e6:55:d9:df:7c:46:c0:0a:
                    bc:f1:88:7e:57:3c:8a:1c:c1:ad:12:bd:57:3f:8f:
                    27:99:25:02:18:6d:bb:44:22:a8:6f:09:63:c6:7d:
                    63:10:4c:83:03:09:bc:75:09:83:d0:18:02:c6:b0:
                    d5:5b:81:71:f3:dd:c1:84:e4:73:99:a7:44:ef:27:
                    38:aa:3a:87:5c:a5:ce:05:20:06:46:4e:29:01:c9:
                    d5:5a:33:b6:a8:51:83:9e:67:05:3c:d1:1c:12:27:
                    e3:59:7a:55:3f:44:63:97:62:ce:fe:a4:62:f9:92:
                    2e:87:24:95:3a:79:ea:20:74:df:52:56:87:4d:2b:
                    98:9d
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            X509v3 Subject Key Identifier: 
                70:ED:4A:0E:8F:CB:EC:1C:D3:09:8E:3F:FF:01:73:B9:0A:84:00:CF
            X509v3 Authority Key Identifier: 
                70:ED:4A:0E:8F:CB:EC:1C:D3:09:8E:3F:FF:01:73:B9:0A:84:00:CF
            X509v3 Basic Constraints: critical
                CA:TRUE
    Signature Algorithm: sha256WithRSAEncryption
    Signature Value:
        3d:b6:22:ed:72:76:67:0d:b2:31:47:d0:ad:54:b1:4c:08:e8:
        66:14:fb:3b:f7:a7:91:77:39:8e:d5:00:e8:55:5b:54:83:a8:
        7a:94:7e:2a:82:47:4c:ca:72:43:6a:80:32:80:e0:e0:94:65:
        36:5d:84:12:63:c8:0c:a5:9b:11:a1:33:54:17:93:ad:4a:a2:
        21:af:20:d6:40:c9:30:d2:69:96:e1:f7:55:5a:95:1b:2f:66:
        a5:db:bb:e0:bb:9f:07:04:b2:4b:29:37:f3:3e:3f:cf:93:a8:
        87:af:16:9e:94:e7:ad:98:2a:11:18:e2:ca:1c:97:de:84:1a:
        ae:a9:36:6e:6e:2e:7a:43:0c:fc:e4:34:6b:7c:8e:2a:14:14:
        a9:b0:fa:42:c8:79:a4:15:6e:71:22:f2:f8:f7:1b:9e:f4:db:
        da:21:a5:d7:31:64:c5:10:4b:80:f3:95:9f:47:ba:90:1e:12:
        84:51:02:e6:6e:49:bd:93:aa:36:25:df:cf:24:03:84:08:f2:
        76:aa:7e:67:d1:92:cb:45:9e:ac:6c:55:33:a6:4b:be:ce:e4:
        d1:65:57:e5:27:a5:b2:95:56:3f:14:2a:11:d9:70:98:e1:89:
        da:c1:cb:25:b4:e3:9c:d8:ad:80:08:48:97:31:ef:5d:c4:d2:
        c0:4e:21:15
```

### 6.11.2 Https 配置示例

```bash
root@ubutun2204-1:~# cat /etc/haproxy/conf.d/wanglei_web.cfg
listen wanglei_web
   bind 192.168.159.103:80
   # https设置
   bind 192.168.159.103:443 ssl crt /etc/haproxy/certs/haproxy.pem
   redirect scheme https if !{ ssl_fc }
   http-request set-header X-forwarded-Port %[dst_port]
   http-request add-header X-forwarded-Proto https if { ssl_fc } 
   
   mode http
   balance leastconn
   server server1 192.168.159.104:80 check
   server server2 192.168.159.105:80 check

root@ubutun2204-1:~# systemctl reload haproxy.service
```

### 6.11.3 修改后端服务器的日志格式

```bash
root@ubutun2204-1:~# vim /etc/nginx/nginx.conf 
log_format main '"$proxy_add_x_forwarded_for" - $remote_user [$time_local] "$request" "$proxy_protocol_addr" "$http_x_forwarded_for" --- "$http_x_haproxy_current_date" --- "$http_x_forwarded_port" "$http_x_forwarded_proto"'
```

### 6.11.4 验证 Https

```bash
#请求http自动跳转到https
root@ubutun2204-1:~# curl -IkL http://www.wanglei.com
HTTP/1.1 302 Found
content-length: 0
location: https://www.wanglei.com/
cache-control: no-cache

HTTP/2 200 
server: nginx/1.18.0 (Ubuntu)
date: Thu, 03 Oct 2024 06:33:17 GMT
content-type: text/html
content-length: 35
last-modified: Thu, 03 Oct 2024 04:16:03 GMT
etag: "66fe1a83-23"
accept-ranges: bytes


root@ubutun2204-1:~# curl -Ik https://www.wanglei.com
HTTP/2 200 
server: nginx/1.18.0 (Ubuntu)
date: Thu, 03 Oct 2024 06:34:18 GMT
content-type: text/html
content-length: 39
last-modified: Thu, 03 Oct 2024 04:16:24 GMT
etag: "66fe1a98-27"
accept-ranges: bytes

# 查看后端服务器的访问日志
192.168.159.103 - - [04/OCT/2024:10:40:17 +0800] "HEAD / HTTP/1.1" 200 - "-" 
"curl/7.19.7 (x86_64-redhat-linux-gnu) libcurl/7.19.7 NSS/3.27.1 zlib/1.2.3 
libidn/1.18 libssh2/1.4.2" "443" "https"
```

![image-20241003144103269](images/image-20241003144103269.png)

![image-20241003144145890](images/image-20241003144145890.png)

# 7 本章重点总结

- HAProxy调度算法
-  ACL使用与报文修改
-  动静分离(根据文件后缀或URL) 
- 客户端源IP透传 
- 服务器动态下线 编写shell脚本，实现能够基于参数传递 Real Server 服务器IP，并实现将其从多个HAProxy进程下 线与上线 
- 比较LVS,haproxy,nginx三者的特性和调度算法区别(面试题)
