# 1: Redis部署

## 1.1：Redis基础

### 1.1.1： NoSQL数据库

#### 1.1.1.1： 什么是NoSQL

数据库主要分为两大类：关系型数据库与NoSQL数据库。

关系型数据库，是建立在关系模型基础上的数据库，其借助于集合代数等数学概念和方法处理数据库中的数据。主流的MYSQL、Oracle、MS SQL Server 和 DB2 都属于这类传统数据库。

NoSQL数据库，全称为Not Only SQL，意思是适用关系型数据库的时候就使用关系型数据库，不适用的时候可以使用更加合适的数据存储。NoSQL 是对不同于传统的关系型数据库的数据库管理系统 的统称。

NoSQL用于超大规模数据的存储。这些类型的数据存储不需要固定的模式，无需多余操作就可以横向扩展。

#### 1.1.1.2：NoSQL起源

NoSQL一词最早出现于1998年，是Carlo Strozzi开发的一个轻量、开源、不提供SQL功能的关系数据 库。

2009年，Last.fm的Johan Oskarsson发起了一次关于分布式开源数据库的讨论，来自Rackspace的Eric  Evans再次提出了NoSQL的概念，这时的NoSQL主要指非关系型、分布式、不提供ACID的数据库设计模 式。

2009年在亚特兰大举行的"no:sql(east)"讨论会是一个里程碑，其口号是"select fun, profit from  real_world where relational=false;"。因此，对NoSQL最普遍的解释是"非关联型的"，强调Key-Value  Stores和文档数据库的优点，而不是单纯的反对RDBMS。

#### 1.1.1.3：为社么使用NoSQL

Oracle，MySQL 等传统的关系数据库非常成熟并且已大规模商用，为什么还要用 NoSQL 数据库呢？

主要是由于随着互联网发展，数据量越来越大，对性能要求越来越高，传统数据据库存在着先天性的缺陷，即单机（单裤）性能瓶颈，并且扩展困难。这样既有单机单库瓶颈，却又扩展困难，自然无法满足日益增长的海量数据存储及其性能要求，所以才会出现了各种不同的 NoSQL 产品，NoSQL 根本性的优 势在于在云计算时代，简单、易于大规模分布式扩展，并且读写性能非常高。

通过第三方平台（如：Google,Facebook等）可以很容易的访问和抓取数据。用户的个人信息，社交网 络，地理位置，用户生成的数据和用户操作日志已经成倍的增加。如果要对这些用户数据进行挖掘，那 SQL数据库已经不适合这些应用了, NoSQL 数据库的发展却能很好的处理这些大的数据。

![image-20240428143648003](D:\云原生\redis\images\image-20240428143648003.png)

![image-20240428143707505](D:\云原生\redis\images\image-20240428143707505.png)

#### 1.1.1.4：RDBMS和NOSQL对比

**RDBMS**

- 高度组织化结构化数据
- 结构化查询语言(SQL)
- 数据和关系都存储在单独的表中
- 数据操纵语言，数据定义语言
- 严格的一致性
- 基础事务

**NoSQL**

- 代表着不仅仅是SQL,没有声明性查询语言
- 没有预定义的模式
- 最终一致性，而非ACID属性
- 非结构化和不可预知的数据
- CAP定理
- 高性能，高可用性和可伸缩性

#### 1.1.1.5：NoSQL的优缺点

|      | 关系型数据库                                                 | NoSQL数据库                                                  |
| ---- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 特点 | - 数据关系模型基于关系模型，结构化存储，完整性约束<br />-基于二维表及其之间的关系，需要连接，并，交，差，除等操作<br />-采用结构化查询语言（SQL）做数据读写<br />-操作需要数据的一致性，需要事务甚至是强一致性 | -  非结构化存储<br />- 基于多维关系模型<br />- 具有特有的使用场景 |
| 优点 | - 保持数据的一致性（事务处理）<br />- 可以进行join等复杂查询<br />- 通用化，技术成熟 | - 高并发，大数据下读写能力较强<br />- 基本支持分布式，易于扩展，可伸缩<br />- 简单，弱结构化存储 |
| 缺点 | - 数据读写必须经过sql解析，大量数据，高并发下读写性能不足<br />- 对数据做读写，或者修改数据结构需要加锁，影响并发操作<br />- 无法适用非结构化存储<br />- 扩展困难<br />- 昂贵，复杂 | - join等复杂操作能力较弱<br />- 事务支持较弱<br />- 通用性较差 |

#### 1.1.1.6：CAP定理

![image-20240428145400510](images\image-20240428145400510.png)

在计算机科学中，CAP定理（CAP theorem）, 它指出对于一个分布式计算系统，不可能同时满足以下三点：

- C：Consistency

  即一致性，访问所有的节点得到的数据应该是一样的。注意，这里的一致性指的是强一致性，也就是数据更新完，访问任何节点看到的数据完全一致，要和弱一致性，最终一致性区分开。

  每次读取的数据都应该是最近写入的数据或者返回一个错误, 而不是过期数据，也就是说，数据是 一致的。

- A：Availability

  即可用性，所有的节点都保持高可用性

  注意，这里的高可用还包括不能出现延迟，比如节点B由于等待数据同步而阻塞请求，那么节点B就不满足高可用性。

  也就是说，任何没有发生故障的服务必须在有限的时间内返回合理的结果集。

  每次请求都应该得到一个响应，而不是返回一个错误或者失去响应，不过这个响应不需要保证数据 是最近写入的,也就是说系统需要一直都是可用正常使用的，不会引起调用者的异常，但是并不保证 响应的数据是最新的。

- P：Partiton tolerance

  即分区容忍性，这里的分区是指网络意义上的分区。由于网络是不可靠的，所有节点之间很可能出 现无法通讯的情况，在节点不能通信时，要保证系统可以继续正常服务。

  在分布式系统中，机器分布在各个不同的地方，由网络进行连接。由于各地的网络情况不同，网络 的延迟甚至是中断是不可避免的。分区容错性指的就是服务器之间通信异常的情况。

  比如: 有两台MySQL数据库服务器，做了读写分离。一台主服务器在北京，负责所有的写操作；一 台从服务器在上海，负责所有的读操作，两台服务器之间进行主从复制。两台服务器之间很有可能 出现网络抖动，异常的情况，从而导致主从复制失败。这就是所谓的“分区容错”。

遵循CAP原理，一个分布式系统不可能同时满足C,A,P这3个条件。所以系统架构师在设计系统时，不要将精力浪费在如何设计能满足三者的完美分布式系统，而是应该进行取舍。由于网络的不可靠的性质，大多数开源的分布式系统都会实现P，也就是分区容忍性，之后在C和A做抉择。

比如: MySQL的主从服务器之间网络没有问题，主从复制正常，那么数据一致性，可用性是有保障的。

但是如果网络出现了问题，主从复制异常，那么就会有数据不同步的情况。这种情况下有两个选择，第 一个方法是保证可用性，允许出现数据不一致的情况，依然在主数据库写，从数据库读。第二个方法是 保证一致性，关闭主数据库，禁止写操作，确保主从数据一致，等服务器之间网络恢复了，再开放写操 作。

也就是说，在服务器之间的网络出现异常的情况下，一致性和可用性是不可能同时满足的，必须要放弃 一个，来保证另一个。这也正是CAP定理所说的，在分布式系统中，P总是存在的。在P发生的前提下， C(一致性)和A（可用性）不能同时满足。这种情况在做架构设计的时候就要考虑到，要评估对业务的影 响，进行权衡决定放弃哪一个。在通常的业务场景下，系统不可用是不能接受的，所以要优先保证可用 性，暂时放弃一致性。

因此，根据CAP原理将NoSQL数据库分成了满足CA原则，满足CP原则和满足AP原则三大类：

- CA-单点集群，满足一致性，可用性的系统，通常在可扩展性上不太强大。

  放弃分区容忍性，即不进行分区，不考虑由于网络不通或结点挂掉的问题，则可以实现一致性和可 用性。那么系统将不是一个标准的分布式系统。

  最常用的关系型数据就满足了CA，例如: 主数据库和从数据库中间不再进行数据同步，数据库可以 响应每次的查询请求，通过事务隔离级别实现每个查询请求都可以返回最新的数据。

- CP - 满足一致性，分区容忍性的系统，通常性能不是特别高。 放弃可用性，追求一致性和分区容 错性。

  例如: Zookeeper,PXC集群就是追求的强一致，再比如跨行转账，一次转账请求要等待双方银行系 统都完成整个事务才算完成。

- AP - 满足可用性，分区容忍性的系统，通常可能对一致性要求低一些。

  放弃一致性，追求分区容忍性和可用性。这是很多分布式系统设计时的选择。

  例如：MySQL主从复制，默认是异步机制就可以实现AP，但是用户接受所查询的到数据在一定时 间内不是最新的.

  通常实现AP都会保证最终一致性，而BASE理论就是根据AP来扩展的，一些业务场景 比如：订单退 款，今日退款成功，明日账户到账，只要用户可以接受在一定时间内到账即可。

#### 1.1.1.7：Base理论

Base理论是三要素的缩写：基本可用（Basically Available）、软状态（Soft-state）、最终一致性 （Eventually Consistency）。

![image-20240428151457727](images\image-20240428151457727.png)

- 基本可用

  相对于CAP理论中可用性的要求：【任何时候，读写都是成功的】，‘基本可用’要求系统能够基本运行，一直提供服务，强调的是分布式系统在出现不可预知故障的时候，允许损失部分可用性。

  相比正常的系统，可能响应时间延长，或者服务被降级。

  比如在秒杀活动，如果抢购的人数太多，超过了系统的QPS,可能会出现排队或者提示限流。

- 软状态

  相对于ACID事务中原子性要求的要么全做，要么全不做，强调的是强制一致性，要求多个节点的数 据副本是一致的，强调数据的一致性。这种原子性可以理解为”硬状态“。

  而软状态则允许系统中的数据存在中间状态，并认为该状态不影响系统的整体可用性，即允许系统 在不同节点的数据副本上存在数据延时。

  比如粉丝数，关注后需要过一段时间才会显示正确的数据。

- 最终一致性

  数据不可能一直处于软状态，必须在一个时间期限后达到各个节点的一致性。在期限过后，应当保 证所有副本中的数据保持一致性，也就是达到了数据的最终一致性。

  在系统设计中，最终一致性实现的时间取决于网络延时，系统负载，不同的存储选型表，不同的数据复制方案设计等因素。也就是说，谁都不保证用户什么时候能看到更新好的数据，但是总会看到的。

#### 1.1.1.8 NoSQL 数据库分类

| 类型           | 部分代表                                       | 特点                                                         |
| -------------- | ---------------------------------------------- | ------------------------------------------------------------ |
| 列存储         | HbaseCassandraHypertable                       | 顾名思义，是按列存储数据的。最大的特点是方便存 储结构化和半结构化数据，方便做数据压缩，对针对 某一列或者某几列的查询有非常大的IO优势。 |
| 文档 存储      | MongoDB CouchDB                                | 文档存储一般用类似json的格式存储，存储的内容是 文档型的。这样也就有机会对某些字段建立索引，实 现关系数据库的某些功能。 |
| key-value 存储 | Tokyo Cabinet / TyrantBerkeley Memcached Redis | 可以通过key快速查询到其value。一般来说，存储不 管value的格式，照单全收。（Redis包含了其他功 能） |
| 图存 储        | Neo4JFlockDB                                   | 图形关系的最佳存储。使用传统关系数据库来解决的 话性能低下，而且设计使用不方便。 |
| 对象 存储      | db4oVersant                                    | 通过类似面向对象语言的语法操作数据库，通过对象 的方式存取数据。 |
| xml 数据 库    | Berkeley DB XMLBaseX                           | 高效的存储XML数据，并支持XML的内部查询语法， 比如XQuery,Xpath。 |

### 1.1.2：Redis简介

![image-20240428152706572](images\image-20240428152706572.png)

Redis (Remote Dictionary Server远程字典服务)是一个遵循BSD MIT开源协议的高性能的NoSQL.Redis  基于ANSI C语言语言)编写的key-value数据库,是意大利的Salvatore Sanfilippo在2009年发布，从2010 年3月15日起，Redis的开发工作由VMware主持。从2013年5月开始，Redis的开发由Pivotal公司赞助。 目前国内外使用的公司众多,比如:阿里,腾讯,百度,京东,新浪微博,GitHub,Twitter 等。

Redis的出现，很大程度补偿了memcached这类key/value存储的不足，在部分场合可以对关系数据库 起到很好的补充作用。它提供了Java，C/C++，Go, C#，PHP，JavaScript，Perl，Object-C，Python， Ruby，Erlang等客户端。

DB-Engine月度排行榜Redis在键值型存储类的数据库长期居于首位,远远高于第二位的memcached。

```http
https://db-engines.com/en/ranking
```

![image-20240428152936130](images\image-20240428152936130.png)

Redis官网地址：https://redis.io/

### 1.1.3：Redis特性

- 速度块：10W QPS，基于内存，C语言实现
- 单线程
- 持久化
- 支持多种数据结构
- 支持多种编程语言
- 功能丰富: 支持Lua脚本,发布订阅,事务,pipeline等功能
- 简单: 代码短小精悍(单机核心代码只有23000行左右),单线程开发容易,不依赖外部库,使用简单
- 主从复制
- 支持高可用和分布式

### 1.1.4：单线程

Redis 6.0版本前一直是单线程方式处理用户的请求。

![image-20240428153432023](images\image-20240428153432023.png)

单线程为何如此块？

- 纯内存
- 非阻塞
- 避免线程切换和竞态消耗
- 基于Epoll实现IO多路复用

![image-20240428153556655](images\image-20240428153556655.png)

注意事项：

- 一次只能运行一条命令
- 避免执行长(慢)命令:keys *, flushall, flushdb, slow lua script, mutil/exec, operate big  value(collection)
- 其实不是单线程；早期版本是单进程单线程,3.0 版本后实际还有其它的线程, 实现特定功能,如: fysnc  file descriptor,close file descriptor。

### 1.1.5：Redis对比Memcached

| 比较 类别         | Redis                                                        | memcached                                                    |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 支持的数据结构    | 哈希、列表、集合、有序集合                                   | 纯kev-value                                                  |
| 持久 化支 持      | 有                                                           | 无                                                           |
| 高可 用支 持      | redis支持集群功能，可以实现主动复制，读写分离。 官方也提供了sentinel集群管理工具，能够实现主从 服务监控，故障自动转移，这一切，对于客户端都是 透明的，无需程序改动，也无需人工介入 | 需要二次开发                                                 |
| 存储 value 容量   | 最大512M                                                     | 最大1M                                                       |
| 内存 分配         | 临时申请空间，可能导致碎片                                   | 预分配内存池的方式管理内 存，能够省去内存分配时间            |
| 虚拟 内存 使用    | 有自己的VM机制，理论上能够存储比物理内存更多 的数据，当数据超量时，会引发swap，把冷数据刷 到磁盘上 | 所有的数据存储在物理内存里                                   |
| 网络 模型         | 非阻塞IO复用模型,提供一些非KV存储之外的排序， 聚合功能，在执行这些功能时，复杂的CPU计算，会 阻塞整个IO调度 | 非阻塞IO复用模型                                             |
| 水平 扩展 的支 持 | redis cluster 可以横向扩展                                   | 暂无                                                         |
| 多线 程           | Redis6.0之前是只支持单线程                                   | Memcached支持多线程,CPU 利用方面Memcache优于 Redis           |
| 过期 策略         | 有专门线程，清除缓存数据                                     | 懒淘汰机制：每次往缓存放入 数据的时候，都会存一个时 间，在读取的时候要和设置的 时间做TTL比较来判断是否过 期 |
| 单机 QPS          | 约10W                                                        | 约60W                                                        |
| 源代 码可 读性    | 代码清爽简洁                                                 | 可能是考虑了太多的扩展性， 多系统的兼容性，代码不清爽        |
| 适用 场景         | 复杂数据结构、有持久化、高可用需求、value存储 内容较大       | 纯KV，数据量非常大，并发量 非常大的业务                      |

### 1.1.6: Redis常见的应用场景

- 缓存：缓存RDBMS中的数据，比如网站的查询结果，商品信息，微博，新闻，消息
- session共享：实现web集群中多服务器间的session共享
- 计数器：商品访问排行榜、浏览数、粉丝数、关注、点赞、评论等和次数相关的数值统计场景
- 社交：朋友圈，共同好友，可能认识他们等
- 地理位置： 基于地理信息系统GIS（Geographic Information System)实现摇一摇、附近的人、外卖 等功能
- 消息队列：ELK等日志系统缓存、业务的订阅/发布系统

![image-20240428154926437](images\image-20240428154926437.png)

![image-20240428154939247](images\image-20240428154939247.png)

![image-20240428154950425](images\image-20240428154950425.png)



![image-20240428155007065](images\image-20240428155007065.png)

![image-20240428155021987](images\image-20240428155021987.png)

### 1.1.7：缓存的实现流程

**数据更新操作流程：**

![image-20240428155204023](images\image-20240428155204023.png)

**数据读操作流程**

![image-20240428155259412](images\image-20240428155259412.png)

### 1.1.8：缓存穿透，缓存击穿和缓存雪崩

#### 1.1.8.1：缓存穿透

缓存穿透是指缓存和数据库中都没有数据，而用户不断发起请求，比如：发起为id为"-1"的数据或id为特别大不存在的数据。这时的用户很可能是攻击者，攻击会导致数据库压力过大。

解决方法：

- 接口层增加校验，如用户鉴权校验，id做基础校验，id<=0的直接拦截
- 从缓存取不到的数据，在数据库中也没有取到，这时也可以将key-value对写为key-null，缓存有效 时间可以设置短点，如30秒（设置太长会导致正常情况也没法使用）。这样可以防止攻击用户反复 用同一个id暴力攻击

#### 1.1.8.2: 缓存击穿

缓存击穿是指缓存中没有但数据库中有的数据，比如：热点数据的缓存时间到期后，这时由于并发用户多，同时读缓存没读到数据，又同时去数据库去取数据，引起数据库压力瞬间增大，造成过大压力。

解决方法：

- 设置热点数据永远不过期。

#### 1.1.8.3：缓存雪崩

缓存雪崩是指缓存中数据大批量到过期时间，而查询数据量巨大，引起数据库压力过大甚至down机。和 缓存击穿不同的是，缓存击穿指并发查同一条数据，缓存雪崩是不同数据都过期了，很多数据都查不到 从而查数据库。

解决方法：

- 缓存数据的过期时间设置随机，防止同一时间大量数据过期现象发生
- 如果缓存数据库是分布式部署，将热点数据均匀分布在不同搞得缓存数据库中
- 设置热点数据永远不过期

### 1.1.9：Pipeline流水线

Redis客户端执行一条命令分4个过程：

发送命令--》命令排队--》命令执行--》返回结果

这个过程称为Round trip time(简称RTT, 往返时间)，mget,mset指令可以一次性的批量对多个数据的执 行操作,所以有效节约了RTT

但大部分命令（如hgetall）不支持批量操作，需要消耗N次RTT ，利用 Pipeline 技术可以解决这一问题 未使用pipeline执行N条命令如下图

![image-20240428160349902](images\image-20240428160349902.png)

使用了pipeline执行N条命令如下图

![image-20240428160415870](images\image-20240428160415870.png)

两者性能对比

![image-20240428160454369](images\image-20240428160454369.png)

以上对比结果说明在使用Pipeline执行时速度比逐条执行要快，特别是客户端与服务端的网络延迟越 大，性能体能越明显。

## 1.2：Redis安装及连接

官方安装方法说明：

```http
https://redis.io/docs/getting-started/installation/
```

### 1.2.1: 编译安装Redis

Redis源码包官方下载链接：

```http
http://download.redis.io/releases/
```

![image-20240428161353601](images\image-20240428161353601.png)

#### 1.2.1.1：编译安装

官方的安装方法：

```http
https://redis.io/docs/latest/operate/oss_and_stack/install/install-redis/install-redis-from-source/
```

**范例：编译安装**

```bash
环境说明：

操作系统：Ubuntu 20.04.5
Redis: Redis-7.0.15
```

```bash
# 如果支持systemd需要安装下面包
root@redis01:~# apt update & apt -y install make gcc libjemalloc-dev libsystemd-dev

# 下载源码
root@redis01:~# wget http://download.redis.io/releases/redis-7.0.15.tar.gz
root@redis01:~# tar xf redis-7.0.15.tar.gz -C /usr/local/src/

# 编译安装
root@redis01:~# mkdir -p /apps/redis
root@redis01:~# cd /usr/local/src/redis-7.0.15/
#如果支持systemd,需要执行下面
root@redis01:/usr/local/src/redis-7.0.15# make -j 1 USE_SYSTEMD=yes PREFIX=/apps/redis install # 指定安装目录，其中2是cpu数量


# 配置软连接
root@redis01:/usr/local/src/redis-7.0.15# ln -s /apps/redis/bin/redis-* /usr/local/bin/

#目录结构
root@redis01:/usr/local/src/redis-7.0.15# tree /apps/redis/
/apps/redis/
└── bin
    ├── redis-benchmark
    ├── redis-check-aof -> redis-server
    ├── redis-check-rdb -> redis-server
    ├── redis-cli
    ├── redis-sentinel -> redis-server
    └── redis-server

1 directory, 6 files


# 准备相关目录和配置文件
root@redis01:~# mkdir /apps/redis/{etc,log,data,run} #创建配置文件、日志、数据等目录
root@redis01:/usr/local/src/redis-7.0.15# cp redis.conf /apps/redis/etc/
```

#### 1.2.1.2: 前台启动Redis

```bash
root@redis01:~# redis-server /apps/redis/etc/redis.conf
22294:C 28 Apr 2024 08:49:40.896 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
22294:C 28 Apr 2024 08:49:40.896 # Redis version=7.0.15, bits=64, commit=00000000, modified=0, pid=22294, just started
22294:C 28 Apr 2024 08:49:40.896 # Configuration loaded
22294:M 28 Apr 2024 08:49:40.897 * Increased maximum number of open files to 10032 (it was originally set to 1024).
22294:M 28 Apr 2024 08:49:40.897 * monotonic clock: POSIX clock_gettime
                _._                                                  
           _.-``__ ''-._                                             
      _.-``    `.  `_.  ''-._           Redis 7.0.15 (00000000/0) 64 bit
  .-`` .-```.  ```\/    _.,_ ''-._                                  
 (    '      ,       .-`  | `,    )     Running in standalone mode
 |`-._`-...-` __...-.``-._|'` _.-'|     Port: 6379
 |    `-._   `._    /     _.-'    |     PID: 22294
  `-._    `-._  `-./  _.-'    _.-'                                   
 |`-._`-._    `-.__.-'    _.-'_.-'|                                  
 |    `-._`-._        _.-'_.-'    |           https://redis.io       
  `-._    `-._`-.__.-'_.-'    _.-'                                   
 |`-._`-._    `-.__.-'    _.-'_.-'|                                  
 |    `-._`-._        _.-'_.-'    |                                  
  `-._    `-._`-.__.-'_.-'    _.-'                                   
      `-._    `-.__.-'    _.-'                                       
          `-._        _.-'                                           
              `-.__.-'                                               

22294:M 28 Apr 2024 08:49:40.899 # Server initialized
22294:M 28 Apr 2024 08:49:40.899 # WARNING Memory overcommit must be enabled! Without it, a background save or replication may fail under low memory condition. Being disabled, it can can also cause failures without low memory condition, see https://github.com/jemalloc/jemalloc/issues/1328. To fix this issue add 'vm.overcommit_memory = 1' to /etc/sysctl.conf and then reboot or run the command 'sysctl vm.overcommit_memory=1' for this to take effect.
22294:M 28 Apr 2024 08:49:40.900 * Ready to accept connections

root@redis01:~# ss -ntl
State                       Recv-Q                      Send-Q                                           Local Address:Port                                             Peer Address:Port                      Process                      
LISTEN                      0                           511                                                  127.0.0.1:6379                                                  0.0.0.0:*                                                      
LISTEN                      0                           4096                                             127.0.0.53%lo:53                                                    0.0.0.0:*                                                      
LISTEN                      0                           128                                                    0.0.0.0:22                                                    0.0.0.0:*                                                      
LISTEN                      0                           128                                                  127.0.0.1:6010                                                  0.0.0.0:*                                                      
LISTEN                      0                           128                                                  127.0.0.1:6011                                                  0.0.0.0:*                                                      
LISTEN                      0                           511                                                      [::1]:6379                                                     [::]:*                                                      
LISTEN                      0                           128                                                       [::]:22                                                       [::]:*                                                      
LISTEN                      0                           128                                                      [::1]:6010                                                     [::]:*                                                      
LISTEN                      0                           128                                                      [::1]:6011                                                     [::]:*   
```

#### 1.2.1.3 消除启动时的三个Warning提示信息(可选)

前面直接启动Redis时有三个Waring信息,可以用下面方法消除告警,但非强制消除

##### 1.2.1.3.1: Tcp backlog

```bash
WARNING: The TCP backlog setting of 511 cannot be enforced because 
/proc/sys/net/core/somaxconn is set to the lower value of 128.
```

Tcp backlog 是指TCP的第三次握手服务器端收到客户端 ack确认号之后到服务器用Accept函数处理请求 前的队列长度，即全连接队列.

注意：Ubuntu20.04默认值满足要求，不再有此告警

```bash
root@redis01:~# cat /proc/sys/net/core/somaxconn
4096
```

##### 1.2.1.3.2:  overcommit_memory

```bash
WARNING Memory overcommit must be enabled! Without it, a background save or replication may fail under low memory condition. Being disabled, it can can also cause failures without low memory condition, see https://github.com/jemalloc/jemalloc/issues/1328. To fix this issue add 'vm.overcommit_memory = 1' to /etc/sysctl.conf and then reboot or run the command 'sysctl vm.overcommit_memory=1' for this to take effect.
```

内核参数说明：

```http
内核参数overcommit_memory 实现内存分配策略,可选值有三个：0、1、2
0 表示内核将检查是否有足够的可用内存供应用进程使用；如果有足够的可用内存，内存申请允许；否则内存
申请失败，并把错误返回给应用进程
1 表示内核允许分配所有的物理内存，而不管当前的内存状态如何
2 表示内核允许分配超过所有物理内存和交换空间总和的内存
```

范例：

```bash
#默认值为0
root@redis01:~# sysctl vm.overcommit_memory
vm.overcommit_memory = 0

#修改
root@redis01:~# vim /etc/sysctl.conf
vm.overcommit_memory = 1  #新版只允许1，不支持2

# 生效
root@redis01:~# sysctl -p
vm.overcommit_memory = 1
```

##### 1.2.1.3.3 transparent hugepage

```bash
WARNING you have Transparent Huge Pages (THP) support enabled in your kernel. 
This will create latency and memory usage issues with Redis. To fix this issue 
run the command 'echo never > /sys/kernel/mm/transparent_hugepage/enabled' as 
root, and add it to your /etc/rc.local in order to retain the setting after a 
reboot. Redis must be restarted after THP is disabled.
警告：您在内核中启用了透明大页面（THP,不同于一般4k内存页,而为2M）支持。 这将在Redis中造成延迟
和内存使用问题。 要解决此问题，请以root 用户身份运行命令“echo never> 
/sys/kernel/mm/transparent_hugepage/enabled”，并将其添加到您的/etc/rc.local中，以便在
重启后保留设置。禁用THP后，必须重新启动Redis。
```

注意：Ubuntu20.04默认值满足要求，不再有此告警

```bash
root@redis01:~# cat /sys/kernel/mm/transparent_hugepage/enabled
always [madvise] never
```

##### 1.2.1.3.4 验证是否消除 Warning

重新启动redis 服务不再有前面的三个Waring信息

```bash
root@redis01:~# redis-server /apps/redis/etc/redis.conf
22681:C 28 Apr 2024 08:59:40.575 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
22681:C 28 Apr 2024 08:59:40.576 # Redis version=7.0.15, bits=64, commit=00000000, modified=0, pid=22681, just started
22681:C 28 Apr 2024 08:59:40.576 # Configuration loaded
22681:M 28 Apr 2024 08:59:40.576 * Increased maximum number of open files to 10032 (it was originally set to 1024).
22681:M 28 Apr 2024 08:59:40.576 * monotonic clock: POSIX clock_gettime
                _._                                                  
           _.-``__ ''-._                                             
      _.-``    `.  `_.  ''-._           Redis 7.0.15 (00000000/0) 64 bit
  .-`` .-```.  ```\/    _.,_ ''-._                                  
 (    '      ,       .-`  | `,    )     Running in standalone mode
 |`-._`-...-` __...-.``-._|'` _.-'|     Port: 6379
 |    `-._   `._    /     _.-'    |     PID: 22681
  `-._    `-._  `-./  _.-'    _.-'                                   
 |`-._`-._    `-.__.-'    _.-'_.-'|                                  
 |    `-._`-._        _.-'_.-'    |           https://redis.io       
  `-._    `-._`-.__.-'_.-'    _.-'                                   
 |`-._`-._    `-.__.-'    _.-'_.-'|                                  
 |    `-._`-._        _.-'_.-'    |                                  
  `-._    `-._`-.__.-'_.-'    _.-'                                   
      `-._    `-.__.-'    _.-'                                       
          `-._        _.-'                                           
              `-.__.-'                                               

22681:M 28 Apr 2024 08:59:40.579 # Server initialized
22681:M 28 Apr 2024 08:59:40.579 * Loading RDB produced by version 7.0.15
22681:M 28 Apr 2024 08:59:40.579 * RDB age 2 seconds
22681:M 28 Apr 2024 08:59:40.579 * RDB memory usage when created 0.82 Mb
22681:M 28 Apr 2024 08:59:40.579 * Done loading RDB, keys loaded: 0, keys expired: 0.
22681:M 28 Apr 2024 08:59:40.580 * DB loaded from disk: 0.000 seconds
22681:M 28 Apr 2024 08:59:40.580 * Ready to accept connections
```

#### 1.2.1.4: 创建Redis用户和设置数据目录权限

```bash
root@redis01:~# useradd -r -s /sbin/nologin redis
# 设置目录权限
root@redis01:~# chown -R redis.redis /apps/redis/

# 查看权限
root@redis01:~# ll /apps/redis/
total 28
drwxr-xr-x 7 redis redis 4096 Apr 28 08:47 ./
drwxr-xr-x 3 root  root  4096 Apr 28 08:42 ../
drwxr-xr-x 2 redis redis 4096 Apr 28 08:44 bin/
drwxr-xr-x 2 redis redis 4096 Apr 28 08:47 data/
drwxr-xr-x 2 redis redis 4096 Apr 28 08:48 etc/
drwxr-xr-x 2 redis redis 4096 Apr 28 08:47 log/
drwxr-xr-x 2 redis redis 4096 Apr 28 08:47 run/
```

#### 1.2.1.5: 创建Redis服务Service文件

```bash
root@redis01:~# vim /lib/systemd/system/redis.service
[Unit]
Description=Redis persistent key-value database
After=network.target
[Service]
ExecStart=/apps/redis/bin/redis-server /apps/redis/etc/redis.conf --supervised systemd
ExecStop=/bin/kill -s QUIT $MAINPID
Type=notify #如果支持systemd可以启用此行
User=redis
Group=redis
RuntimeDirectory=redis
RuntimeDirectoryMode=0755
LimitNOFILE=1000000   #指定此值才支持更大的maxclients值
[Install]
WantedBy=multi-user.target


# 启动服务
root@redis01:~# systemctl daemon-reload
root@redis01:~# systemctl start redis
root@redis01:~# systemctl status redis
● redis.service - Redis persistent key-value database
     Loaded: loaded (/lib/systemd/system/redis.service; disabled; vendor preset: enabled)
     Active: active (running) since Sun 2024-04-28 09:05:56 UTC; 2s ago
   Main PID: 23260 (redis-server)
      Tasks: 5 (limit: 1011)
     Memory: 2.3M
     CGroup: /system.slice/redis.service
             └─23260 /apps/redis/bin/redis-server 127.0.0.1:6379

Apr 28 09:05:56 redis01 redis-server[23260]: 23260:C 28 Apr 2024 09:05:56.226 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
Apr 28 09:05:56 redis01 redis-server[23260]: 23260:C 28 Apr 2024 09:05:56.226 # Redis version=7.0.15, bits=64, commit=00000000, modified=0, pid=23260, just started
Apr 28 09:05:56 redis01 redis-server[23260]: 23260:C 28 Apr 2024 09:05:56.227 # Configuration loaded
Apr 28 09:05:56 redis01 redis-server[23260]: 23260:M 28 Apr 2024 09:05:56.227 * Increased maximum number of open files to 10032 (it was originally set to 1024).
Apr 28 09:05:56 redis01 redis-server[23260]: 23260:M 28 Apr 2024 09:05:56.229 * monotonic clock: POSIX clock_gettime
Apr 28 09:05:56 redis01 redis-server[23260]: 23260:M 28 Apr 2024 09:05:56.231 * Running mode=standalone, port=6379.
Apr 28 09:05:56 redis01 redis-server[23260]: 23260:M 28 Apr 2024 09:05:56.231 # Server initialized
Apr 28 09:05:56 redis01 redis-server[23260]: 23260:M 28 Apr 2024 09:05:56.232 * Ready to accept connections
Apr 28 09:05:56 redis01 redis-server[23260]: 23260:M 28 Apr 2024 09:05:56.232 # systemd supervision error: NOTIFY_SOCKET not found!
Apr 28 09:05:56 redis01 redis-server[23260]: 23260:M 28 Apr 2024 09:05:56.232 # systemd supervision error: NOTIFY_SOCKET not found!
```

#### 1.2.1.6 验证客户端连接 Redis

```bash
root@redis01:~# redis-cli 
127.0.0.1:6379> info
# Server
redis_version:7.0.15
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:7ed1a2d8893f5a3b
redis_mode:standalone
os:Linux 5.4.0-177-generic x86_64
arch_bits:64
monotonic_clock:POSIX clock_gettime
multiplexing_api:epoll
atomicvar_api:c11-builtin
gcc_version:9.4.0
process_id:23410
process_supervised:no
run_id:154a5484ae2987f04df11d9e29b79a76bad9c53a
tcp_port:6379
server_time_usec:1714295542466618
uptime_in_seconds:117
uptime_in_days:0
hz:10
configured_hz:10
lru_clock:3019510
executable:/apps/redis/bin/redis-server
config_file:/apps/redis/etc/redis.conf
io_threads_active:0

# Clients
connected_clients:2
cluster_connections:0
maxclients:10000
...
```

#### 1.2.1.7 实战案例：一键编译安装Redis脚本

```bash
root@redis01:~# cat install_redis.sh 
#!/bin/bash
#
#********************************************************************
#Author:          wanglei
#QQ:              353938339
#Date:            2024-04-28
#FileName：       install_redis.sh
#URL:             http://github.com/icloud2native
#Description:     The test script
#Copyright (C):   2024 All rights reserved
#********************************************************************

#本脚本支持在线和离线安装

REDIS_VERSION=redis-7.0.15
#REDIS_VERSION=redis-7.0.11
#REDIS_VERSION=redis-7.0.7
#REDIS_VERSION=redis-7.0.3
#REDIS_VERSION=redis-6.2.6
#REDIS_VERSION=redis-4.0.14
PASSWORD=123456
INSTALL_DIR=/apps/redis

CPUS=`lscpu |awk '/^CPU\(s\)/{print $2}'`

. /etc/os-release

color () {
    RES_COL=60
    MOVE_TO_COL="echo -en \\033[${RES_COL}G"
    SETCOLOR_SUCCESS="echo -en \\033[1;32m"
    SETCOLOR_FAILURE="echo -en \\033[1;31m"
    SETCOLOR_WARNING="echo -en \\033[1;33m"
    SETCOLOR_NORMAL="echo -en \E[0m"
    echo -n "$1" && $MOVE_TO_COL
    echo -n "["
    if [ $2 = "success" -o $2 = "0" ] ;then
        ${SETCOLOR_SUCCESS}
        echo -n $"  OK  "    
    elif [ $2 = "failure" -o $2 = "1"  ] ;then 
        ${SETCOLOR_FAILURE}
        echo -n $"FAILED"
    else
        ${SETCOLOR_WARNING}
        echo -n $"WARNING"
    fi
    ${SETCOLOR_NORMAL}
    echo -n "]"
    echo 
}


prepare(){
    if [ $ID = "centos" -o $ID = "rocky" ];then
        yum  -y install gcc make jemalloc-devel systemd-devel
    else
        apt update 
        apt -y install  gcc make libjemalloc-dev libsystemd-dev
    fi
    if [ $? -eq 0 ];then
        color "安装软件包成功"  0
    else
        color "安装软件包失败，请检查网络配置" 1
        exit
    fi
}

install() {   
    if [ ! -f ${REDIS_VERSION}.tar.gz ];then
        wget http://download.redis.io/releases/${REDIS_VERSION}.tar.gz || { color "Redis 源码下载失败" 1 ; exit; }
    fi
    tar xf ${REDIS_VERSION}.tar.gz -C /usr/local/src
    cd /usr/local/src/${REDIS_VERSION}
    make -j $CUPS USE_SYSTEMD=yes PREFIX=${INSTALL_DIR} install && color "Redis 编译安装完成" 0 || { color "Redis 编译安装失败" 1 ;exit ; }

    ln -s ${INSTALL_DIR}/bin/redis-*  /usr/local/bin/
    
    mkdir -p ${INSTALL_DIR}/{etc,log,data,run}
  
    cp redis.conf  ${INSTALL_DIR}/etc/

    sed -i -e 's/bind 127.0.0.1/bind 0.0.0.0/'  -e "/# requirepass/a requirepass $PASSWORD"  -e "/^dir .*/c dir ${INSTALL_DIR}/data/"  -e "/logfile .*/c logfile ${INSTALL_DIR}/log/redis-6379.log"  -e  "/^pidfile .*/c  pidfile ${INSTALL_DIR}/run/redis_6379.pid" ${INSTALL_DIR}/etc/redis.conf


    if id redis &> /dev/null ;then 
         color "Redis 用户已存在" 1 
    else
         useradd -r -s /sbin/nologin redis
         color "Redis 用户创建成功" 0
    fi

    chown -R redis.redis ${INSTALL_DIR}

    cat >> /etc/sysctl.conf <<EOF
net.core.somaxconn = 1024
vm.overcommit_memory = 1
EOF
    sysctl -p 
    if [ $ID = "centos" -o $ID = "rocky" ];then
        echo 'echo never > /sys/kernel/mm/transparent_hugepage/enabled' >> /etc/rc.d/rc.local
        chmod +x /etc/rc.d/rc.local
        /etc/rc.d/rc.local 
    else 
        echo -e '#!/bin/bash\necho never > /sys/kernel/mm/transparent_hugepage/enabled' >> /etc/rc.local
        chmod +x /etc/rc.local
        /etc/rc.local
    fi


cat > /lib/systemd/system/redis.service <<EOF
[Unit]
Description=Redis persistent key-value database
After=network.target

[Service]
ExecStart=${INSTALL_DIR}/bin/redis-server ${INSTALL_DIR}/etc/redis.conf --supervised systemd
ExecStop=/bin/kill -s QUIT \$MAINPID
Type=notify
User=redis
Group=redis
RuntimeDirectory=redis
RuntimeDirectoryMode=0755
LimitNOFILE=1000000

[Install]
WantedBy=multi-user.target

EOF
     systemctl daemon-reload 
     systemctl enable --now  redis &> /dev/null 
     if [ $? -eq 0 ];then
         color "Redis 服务启动成功,Redis信息如下:"  0 
     else
        color "Redis 启动失败" 1 
        exit
     fi
     sleep 2
     redis-cli -a $PASSWORD INFO Server 2> /dev/null
}

prepare 

install
```

### 1.2.2: Redis的多实例

测试环境中经常使用多实例，需要指定不同实例的相应的端口，配置文件，日志文件等相关配置

实例：以编译安装为例实现redis多实例

```sh
# 生成的文件列表
root@redis01:~# ll /apps/redis/
total 28
drwxr-xr-x 7 redis redis 4096 Apr 28 08:47 ./
drwxr-xr-x 3 root  root  4096 Apr 28 08:42 ../
drwxr-xr-x 2 redis redis 4096 Apr 28 08:44 bin/
drwxr-xr-x 2 redis redis 4096 Apr 28 08:47 data/
drwxr-xr-x 2 redis redis 4096 Apr 28 08:48 etc/
drwxr-xr-x 2 redis redis 4096 Apr 28 08:47 log/
drwxr-xr-x 2 redis redis 4096 Apr 28 08:47 run/


#编辑配置文件
root@redis01:/apps/redis/etc# cp redis.conf redis6379.conf
oot@redis01:/apps/redis/etc# grep 6379 /apps/redis/etc/redis6379.conf
# Accept connections on the specified port, default is 6379 (IANA #815344).
port 6379
# tls-port 6379
pidfile /apps/redis/run/redis_6379.pid
logfile /apps/redis/log/redis6379.log
dbfilename dump6379.rdb
# cluster-config-file nodes-6379.conf
# cluster-announce-tls-port 6379

## 6380
root@redis01:/apps/redis/etc# sed 's/6379/6380/' /apps/redis/etc/redis6379.conf > /apps/redis/etc/redis6380.conf
root@redis01:/apps/redis/etc# grep 6380 /apps/redis/etc/redis6380.conf
# Accept connections on the specified port, default is 6380 (IANA #815344).
port 6380
# tls-port 6380
pidfile /apps/redis/run/redis_6380.pid
logfile /apps/redis/log/redis6380.log
dbfilename dump6380.rdb
# cluster-config-file nodes-6380.conf
# cluster-announce-tls-port 6380
# cluster-announce-bus-port 6380

##6381
root@redis01:/apps/redis/etc# sed 's/6379/6381/' /apps/redis/etc/redis6379.conf > /apps/redis/etc/redis6381.conf
root@redis01:/apps/redis/etc# grep 6381 /apps/redis/etc/redis6381.conf
# Accept connections on the specified port, default is 6381 (IANA #815344).
port 6381
# tls-port 6381
pidfile /apps/redis/run/redis_6381.pid
logfile /apps/redis/log/redis6381.log
dbfilename dump6381.rdb
# cluster-config-file nodes-6381.conf
# cluster-announce-tls-port 6381


# 生成service文件
root@redis01:~# cat /lib/systemd/system/redis6379.service 
[Unit]
Description=Redis persistent key-value database
After=network.target
[Service]
ExecStart=/apps/redis/bin/redis-server /apps/redis/etc/redis6379.conf --supervised systemd
ExecStop=/bin/kill -s QUIT $MAINPID
Type=notify #如果支持systemd可以启用此行
User=redis
Group=redis
RuntimeDirectory=redis
RuntimeDirectoryMode=0755
LimitNOFILE=1000000   #指定此值才支持更大的maxclients值
[Install]
WantedBy=multi-user.target

root@redis01:~# cat /lib/systemd/system/redis6380.service
[Unit]
Description=Redis persistent key-value database
After=network.target
[Service]
ExecStart=/apps/redis/bin/redis-server /apps/redis/etc/redis6380.conf --supervised systemd
ExecStop=/bin/kill -s QUIT $MAINPID
Type=notify #如果支持systemd可以启用此行
User=redis
Group=redis
RuntimeDirectory=redis
RuntimeDirectoryMode=0755
LimitNOFILE=1000000   #指定此值才支持更大的maxclients值
[Install]
WantedBy=multi-user.target


root@redis01:~# cat /lib/systemd/system/redis6381.service
[Unit]
Description=Redis persistent key-value database
After=network.target
[Service]
ExecStart=/apps/redis/bin/redis-server /apps/redis/etc/redis6381.conf --supervised systemd
ExecStop=/bin/kill -s QUIT $MAINPID
Type=notify #如果支持systemd可以启用此行
User=redis
Group=redis
RuntimeDirectory=redis
RuntimeDirectoryMode=0755
LimitNOFILE=1000000   #指定此值才支持更大的maxclients值
[Install]
WantedBy=multi-user.target


# 重启服务
root@redis01:~# systemctl daemon-reload
root@redis01:~# systemctl enable --now redis6379 redis6380 redis6381
root@redis01:~# ss -ntl
State                       Recv-Q                      Send-Q                                           Local Address:Port                                             Peer Address:Port                      Process                      
LISTEN                      0                           511                                                    0.0.0.0:6379                                                  0.0.0.0:*                                                      
LISTEN                      0                           511                                                    0.0.0.0:6380                                                  0.0.0.0:*                                                      
LISTEN                      0                           511                                                    0.0.0.0:6381                                                  0.0.0.0:*                                                      
LISTEN                      0                           4096                                             127.0.0.53%lo:53                                                    0.0.0.0:*                                                      
LISTEN                      0                           128                                                    0.0.0.0:22                                                    0.0.0.0:*                                                      
LISTEN                      0                           128                                                  127.0.0.1:6010                                                  0.0.0.0:*                                                      
LISTEN                      0                           128                                                  127.0.0.1:6011                                                  0.0.0.0:*                                                      
LISTEN                      0                           128                                                       [::]:22                                                       [::]:*                                                      
LISTEN                      0                           128                                                      [::1]:6010                                                     [::]:*                                                      
LISTEN                      0                           128                                                      [::1]:6011                                                     [::]:*                                                      

```

### 1.2.3：Redis相关工具和客户端连接

#### 1.2.3.1：安装的相应程序介绍

```bash
# Redis7.0以上
root@redis01:~# ll /apps/redis/bin/
-rwxr-xr-x 1 redis redis  8127464 Apr 28 08:44 redis-benchmark*  #性能测试程序
lrwxrwxrwx 1 redis redis       12 Apr 28 08:44 redis-check-aof -> redis-server* #AOF
文件检查程序
lrwxrwxrwx 1 redis redis       12 Apr 28 08:44 redis-check-rdb -> redis-server* #RDB
文件检查程序
-rwxr-xr-x 1 redis redis  8097784 Apr 28 08:44 redis-cli*  #客户端程序
lrwxrwxrwx 1 redis redis       12 Apr 28 08:44 redis-sentinel -> redis-server* #哨兵程
序，软连接到服务器端主程序
-rwxr-xr-x 1 redis redis 15630592 Apr 28 08:44 redis-server* #服务端主程序
```

#### 1.2.3.2：客户端程序redis-cli

```sh
# 默认为本机无密码链接
redis-cli
# 远程客户端连接,注意:Redis没有用户的概念
redis-cli -h <Redis服务器ip> -p <PORT> -a <PASSWORD> --no-auth-warning
```

#### 1.2.3.3： 程序连接Redis

Redis 支持多种开发语言访问.

```http
https://redis.io/clients
```

![image-20240428180502583](images\image-20240428180502583.png)



##### 1.2.3.3.1: shell脚本访问Redis

```bash
root@redis01:~# cat redis_test.sh 
#!/bin/bash
NUM=100
PASS=123456
for i in `seq $NUM`;do
    redis-cli -h 127.0.0.1 -a "$PASS" --no-auth-warning set key${i} value${i}
    echo "key${i} value${i} 写入完成"
done
echo "$NUM个key写入到Redis完成"
```

##### 1.2.3.3.2: Python 程序连接 Redis

python 提供了多种开发库,都可以支持连接访问 Redis.

下面选择使用redis-py 库连接 Redis .

github redis-py库 : 

```http
https://github.com/andymccurdy/redis-py
```

```bash
# Ubuntu 2004安装
root@redis01:~# apt update && apt -y install python3-redis

#注意文件名不要为redis,会和redis模块名称冲突
root@redis01:~# cat redis_test.py 
#!/usr/bin/python3
import redis

pool = redis.ConnectionPool(host="127.0.0.1",port=6379,password="123456",decode_responses=True)

c = redis.Redis(connection_pool=pool)

for i in range(100):
 c.set("k%d" % i,"v%d" % i)
 data=c.get("k%d" % i)
 print(data)
```

#### 1.2.3.4：图形工具

有一些第三方开发的图形工具也可以连接redis, 比如: RedisDesktopManager。

![image-20240429091526281](images\image-20240429091526281.png)

# 2：Redis配置管理

## 2.1：Redis配置文件说明

![image-20240429091711659](images\image-20240429091711659.png)

```bash
root@redis01:~# grep -Ev "^#|^$" /apps/redis/etc/redis.conf 
bind 0.0.0.0              #指定监听地址，支持用空格隔开的多个监听IP

protected-mode yes        #redis3.2之后加入的新特性，在没有设置bind IP和密码的时候,redis只允许访问127.0.0.1:6379，可以远程连接，但当访问将提示警告信息并拒绝远程访问,redis-7版本后，只要没有密码就不能远程访问

port 6379                 #监听端口,默认6379/tcp

tcp-backlog 511           #三次握手的时候server端收到client ack确认号之后的队列值，即全连接队列长度
timeout 0                 #客户端和Redis服务端的连接超时时间，默认是0，表示永不超时

tcp-keepalive 300         #tcp 会话保持时间300s

daemonize no              #默认no,即直接运行redis-server程序时,不作为守护进程运行，而是以前台方式运行，如果想在后台运行需改成yes,当redis作为守护进程运行的时候，它会写一个 pid 到 /var/run/redis.pid 文件

pidfile /apps/redis/run/redis_6379.pid  #pid文件路径,可以修改

loglevel notice                         #日志级别

logfile /apps/redis/log/redis.log        #日志路径

databases 16                #设置数据库数量，默认：0-15，共16个库

always-show-logo no         #在启动redis 时是否显示或在日志中记录记录redis的logo

save 900 1 #在900秒内有1个key内容发生更改,就执行快照机制
save 300 10 #在300秒内有10个key内容发生更改,就执行快照机制
save 60 10000  #60秒内如果有10000个key以上的变化，就自动快照备份

stop-writes-on-bgsave-error yes #默认为yes时,可能会因空间满等原因快照无法保存出错时，会禁止redis写入操作，生产建议为no，#此项只针对配置文件中的自动save有效

rdbcompression yes #持久化到RDB文件时，是否压缩，"yes"为压缩，"no"则反之

rdbchecksum yes #是否对备份文件开启RC64校验，默认是开启

dbfilename dump.rdb #快照文件名

dir ./ #快照文件保存路径，示例：dir "/apps/redis/data"


#主从复制相关
# replicaof <masterip> <masterport> #指定复制的master主机地址和端口，5.0版之前的指令为slaveof 
# masterauth <master-password> #指定复制的master主机的密码

replica-serve-stale-data yes #当从库同主库失去连接或者复制正在进行，从机库有两种运行方式
1、设置为yes(默认设置)，从库会继续响应客户端的读请求，此为建议值
2、设置为no，除去特定命令外的任何请求都会返回一个错误"SYNC with master in progress"。

replica-read-only yes #是否设置从库只读，建议值为yes,否则主库同步从库时可能会覆盖数据，造成数据丢失

repl-diskless-sync no #是否使用socket方式复制数据(无盘同步)，新slave第一次连接master时需要做数据的全量同步，redis server就要从内存dump出新的RDB文件，然后从master传到slave，有两种方式把RDB文件传输给客户端：
1、基于硬盘（disk-backed）：为no时，master创建一个新进程dump生成RDB磁盘文件，RDB完成之后由父进程（即主进程）将RDB文件发送给slaves，此为默认值
2、基于socket（diskless）：master创建一个新进程直接dump RDB至slave的网络socket，不经过主
进程和硬盘
#推荐使用基于硬盘（为no），是因为RDB文件创建后，可以同时传输给更多的slave，但是基于socket(为yes)， 新slave连接到master之后得逐个同步数据。只有当磁盘I/O较慢且网络较快时，可用diskless(yes),否则一般建议使用磁盘(no)


repl-diskless-sync-delay 5 #diskless时复制的服务器等待的延迟时间，设置0为关闭，在延迟时间内到达的客户端，会一起通过diskless方式同步数据，但是一旦复制开始，master节点不会再接收新slave的复制请求，直到下一次同步开始才再接收新请求。即无法为延迟时间后到达的新副本提供服务，新副本将排队等待下一次RDB传输，因此服务器会等待一段时间才能让更多副本到达。推荐值：30-60


repl-ping-replica-period 10 #slave根据master指定的时间进行周期性的PING master,用于监测master状态,默认10s

repl-timeout 60 #复制连接的超时时间，需要大于repl-ping-slave-period，否则会经常报超时

repl-disable-tcp-nodelay no #是否在slave套接字发送SYNC之后禁用 TCP_NODELAY，如果选择"yes"，Redis将合并多个报文为一个大的报文，从而使用更少数量的包向slaves发送数据，但是将使数据传输到slave上有延迟，Linux内核的默认配置会达到40毫秒，如果 "no" ，数据传输到slave的延迟将会减少，但要使用更多的带宽


repl-backlog-size 512mb #复制缓冲区内存大小，当slave断开连接一段时间后，该缓冲区会累积复制副本数据，因此当slave 重新连接时，通常不需要完全重新同步，只需传递在副本中的断开连接后没有同步的部分数据即可。只有在至少有一个slave连接之后才分配此内存空间,建议建立主从时此值要调大一些或在低峰期配置,否则会导致同步到slave失败。

repl-backlog-ttl 3600 #多长时间内master没有slave连接，就清空backlog缓冲区

replica-priority 100 #当master不可用，哨兵Sentinel会根据slave的优先级选举一个master，此值最低的slave会优先当选master，而配置成0，永远不会被选举，一般多个slave都设为一样的值，让其自动选择


#min-replicas-to-write 3 #至少有3个可连接的slave，mater才接受写操作
#min-replicas-max-lag 10 #和上面至少3个slave的ping延迟不能超过10秒，否则master也将停止写操作


requirepass foobared #设置redis连接密码，之后需要AUTH pass,如果有特殊符号，用" "引起来,生
产建议设置

rename-command #重命名一些高危命令，示例：rename-command FLUSHALL "" 禁用命令
               #示例: rename-command del wang

maxclients 10000 #Redis最大连接客户端

maxmemory <bytes> #redis使用的最大内存，单位为bytes字节，0为不限制，建议设为物理内存一半，8G内存的计算方式8(G)*1024(MB)1024(KB)*1024(Kbyte)，需要注意的是缓冲区是不计算在maxmemory内,生产中如果不设置此项,可能会导致OOM

maxmemory-policy 
# MAXMEMORY POLICY：当达到最大内存时，Redis 将如何选择要删除的内容。您可以从以下行为中选择一
种：
#
# volatile-lru -> Evict 使用近似 LRU，只有设置了过期时间的键。
# allkeys-lru -> 使用近似 LRU 驱逐任何键。
# volatile-lfu -> 使用近似 LFU 驱逐，只有设置了过期时间的键。
# allkeys-lfu -> 使用近似 LFU 驱逐任何键。
# volatile-random -> 删除设置了过期时间的随机密钥。
# allkeys-random -> 删除一个随机密钥，任何密钥。
# volatile-ttl -> 删除过期时间最近的key（次TTL）
# noeviction -> 不要驱逐任何东西，只是在写操作时返回一个错误。此为默认值
#
# LRU 表示最近最少使用
# LFU 表示最不常用
#
# LRU、LFU 和 volatile-ttl 都是使用近似随机算法实现的。
#
# 注意：使用上述任何一种策略，当没有合适的键用于驱逐时，Redis 将在需要更多内存的写操作时返回错误。这些通常是创建新密钥、添加数据或修改现有密钥的命令。一些示例是：SET、INCR、HSET、LPUSH、SUNIONSTORE、SORT（由于 STORE 参数）和 EXEC（如果事务包括任何需要内存的命令）。


appendonly no #是否开启AOF日志记录，默认redis使用的是rdb方式持久化，这种方式在许多应用中已经足够用了，但是redis如果中途宕机，会导致可能有几分钟的数据丢失(取决于dump数据的间隔时间)，根据save来策略进行持久化，Append Only File是另一种持久化方式，可以提供更好的持久化特性，Redis会把每次写入的数据在接收后都写入 appendonly.aof 文件，每次启动时Redis都会先把这个文件的数据读入内存里，先忽略RDB文件。默认不启用此功能

appendfilename "appendonly.aof" #文本文件AOF的文件名，存放在dir指令指定的目录中

appendfsync everysec #aof持久化策略的配置
#no表示由操作系统保证数据同步到磁盘,Linux的默认fsync策略是30秒，最多会丢失30s的数据
#always表示每次写入都执行fsync，以保证数据同步到磁盘,安全性高,性能较差
#everysec表示每秒执行一次fsync，可能会导致丢失这1s数据,此为默认值,也生产建议值

#同时在执行bgrewriteaof操作和主进程写aof文件的操作，两者都会操作磁盘，而bgrewriteaof往往会涉及大量磁盘操作，这样就会造成主进程在写aof文件的时候出现阻塞的情形,以下参数实现控制

no-appendfsync-on-rewrite no #在aof rewrite期间,是否对aof新记录的append暂缓使用文件同步策略,主要考虑磁盘IO开支和请求阻塞时间
#默认为no,表示"不暂缓",新的aof记录仍然会被立即同步到磁盘，是最安全的方式，不会丢失数据，但是要忍受阻塞的问题
#为yes,相当于将appendfsync设置为no，这说明并没有执行磁盘操作，只是写入了缓冲区，因此这样并不会造成阻塞（因为没有竞争磁盘），但是如果这个时候redis挂掉，就会丢失数据。丢失多少数据呢？Linux的默认fsync策略是30秒，最多会丢失30s的数据,但由于yes性能较好而且会避免出现阻塞因此比较推荐


# rewrite 即对aof文件进行整理,将空闲空间回收,从而可以减少恢复数据时间

auto-aof-rewrite-percentage 100 #当Aof log增长超过指定百分比例时，重写AOF文件，设置为0表示不自动重写Aof日志，重写是为了使aof体积保持最小，但是还可以确保保存最完整的数据

auto-aof-rewrite-min-size 64mb #触发aof rewrite的最小文件大小

aof-load-truncated yes #是否加载由于某些原因导致的末尾异常的AOF文件(主进程被kill/断电等)，建议yes

aof-use-rdb-preamble no #redis4.0新增RDB-AOF混合持久化格式，在开启了这个功能之后，AOF重写产生的文件将同时包含RDB格式的内容和AOF格式的内容，其中RDB格式的内容用于记录已有的数据，而AOF格式的内容则用于记录最近发生了变化的数据，这样Redis就可以同时兼有RDB持久化和AOF持久化的优点（既能够快速地生成重写文件，也能够在出现问题时，快速地载入数据）,默认为no,即不启用此功能

lua-time-limit 5000 #lua脚本的最大执行时间，单位为毫秒

cluster-enabled yes #是否开启集群模式，默认不开启,即单机模式

cluster-config-file nodes-6379.conf #由node节点自动生成的集群配置文件名称

cluster-node-timeout 15000 #集群中node节点连接超时时间，单位ms,超过此时间，会踢出集群

cluster-replica-validity-factor 10 #单位为次,在执行故障转移的时候可能有些节点和master断开一段时间导致数据比较旧，这些节点就不适用于选举为master，超过这个时间的就不会被进行故障转移,不能当选master，计算公式：(node-timeout * replica-validity-factor) + repl-pingreplica-period

cluster-migration-barrier 1 #集群迁移屏障，一个主节点至少拥有1个正常工作的从节点，即如果主节点的slave节点故障后会将多余的从节点分配到当前主节点成为其新的从节点

cluster-require-full-coverage yes #集群请求槽位全部覆盖，如果一个主库宕机且没有备库就会出现集群槽位不全，那么yes时redis集群槽位验证不全,就不再对外提供服务(对key赋值时,会出现CLUSTERDOWN The cluster is down的提示,cluster_state:fail,但ping 仍PONG)，而no则可以继续使用,但是会出现查询数据查不到的情况(因为有数据丢失)。生产建议为no


cluster-replica-no-failover no #如果为yes,此选项阻止在主服务器发生故障时尝试对其主服务器进行故障转移。 但是，主服务器仍然可以执行手动强制故障转移，一般为no


#Slow log 是 Redis 用来记录超过指定执行时间的日志系统，执行时间不包括与客户端交谈，发送回复等I/O操作，而是实际执行命令所需的时间（在该阶段线程被阻塞并且不能同时为其它请求提供服务）,由于 slow log 保存在内存里面，读写速度非常快，因此可放心地使用，不必担心因为开启 slow log 而影响 Redis 的速度


slowlog-log-slower-than 10000 #以微秒为单位的慢日志记录，为负数会禁用慢日志，为0会记录每个命令操作。默认值为10ms,一般一条命令执行都在微秒级,生产建议设为1ms-10ms之间


slowlog-max-len 128 #最多记录多少条慢日志的保存队列长度，达到此长度后，记录新命令会将最旧的命令从命令队列中删除，以此滚动删除,即,先进先出,队列固定长度,默认128,值偏小,生产建议设为1000以上
```

## 2.2：config命令实现动态修改配置

config命令用于查看当前redis配置，以及不重启redis服务实现动态更改redis配置等

**注意：不是所有配置都可以动态修改,且此方式无法持久保存**

```http
CONFIG SET parameter value
时间复杂度：O(1)
CONFIG SET 命令可以动态地调整 Redis 服务器的配置(configuration)而无须重启。

可以使用它修改配置参数，或者改变Redis的持久化方式。
CONFIG SET 可以修改的配置参数可以使用命令 CONFIG GET * 来列出，所有被 CONFIG SET 修改的配置参数都会立即生效。

CONFIG GET parameter
 时间复杂度： O(N)，其中 N 为命令返回的配置选项数量。
CONFIG GET 命令用于取得运行中的 Redis 服务器的配置参数(configuration parameters)，在 Redis 2.4 版本中， 有部分参数没有办法用 CONFIG GET 访问，但是在最新的 Redis 2.6 版本中，所有配置参数都已经可以用 CONFIG GET 访问了。

CONFIG GET 接受单个参数 parameter 作为搜索关键字，查找所有匹配的配置参数，其中参数和值以“键值对”(key-value pairs)的方式排列。
比如执行 CONFIG GET s* 命令，服务器就会返回所有以 s 开头的配置参数及参数的值：
```

范例：版本差异

```bash
#redis-7支持动态修改端口
127.0.0.1:6379> config set port 8888
OK

#redis-5不支持动态修改端口
127.0.0.1:6379> config set port 8888
(error) ERR Unsupported CONFIG parameter: port

```

### 2.2.1: 设置客户端连接密码

```bash
#设置连接密码
127.0.0.1:6379> CONFIG SET requirepass 123456
OK

#查看连接密码
127.0.0.1:6379> CONFIG GET requirepass  
1) "requirepass"
2) "123456"
```

### 2.2.2: 获取当前配置

```bash
#奇数行为键，偶数行为值
127.0.0.1:6379> config get *
  1) "slowlog-max-len"
  2) "128"
  3) "replica-priority"
  4) "100"
  5) "io-threads"
  6) "1"
  7) "lazyfree-lazy-user-flush"
  8) "no"
  9) "client-query-buffer-limit"
 10) "1073741824"
 11) "list-max-ziplist-size"
 12) "-2"
 13) "lfu-log-factor"
 14) "10"
 15) "shutdown-on-sigterm"
 16) "default"
 17) "masterauth"
 18) ""
 19) "stream-node-max-bytes"
 20) "4096"
 21) "stop-writes-on-bgsave-error"
 22) "yes"
 23) "syslog-enabled"
 24) "no"
 25) "slave-read-only"
 26) "yes"
 27) "io-threads-do-reads"
 28) "no"
 29) "tcp-keepalive"
 30) "300"
 31) "lfu-decay-time"
 32) "1"
 33) "min-replicas-max-lag"
 34) "10"
 35) "slave-serve-stale-data"
 36) "yes"
 37) "propagation-error-behavior"
 38) "ignore"
 39) "slave-ignore-maxmemory"
 40) "yes"
 41) "replica-ignore-maxmemory"
 42) "yes"
 43) "rdb-del-sync-files"
 44) "no"
 45) "min-replicas-to-write"
 46) "0"
 47) "repl-ping-replica-period"
 48) "10"
 49) "hash-max-ziplist-entries"
 50) "512"
 51) "auto-aof-rewrite-min-size"
 52) "67108864"
 53) "enable-debug-command"
 54) "no"
 55) "disable-thp"
 56) "yes"
 57) "lazyfree-lazy-expire"
 58) "no"
 59) "maxmemory-clients"
 60) "0"
 61) "lazyfree-lazy-eviction"
 62) "no"
 63) "active-defrag-ignore-bytes"
 64) "104857600"
 65) "active-defrag-cycle-max"
 66) "25"
 67) "appendfilename"
 68) "appendonly.aof"
 69) "rdbchecksum"
 70) "yes"
 71) "syslog-ident"
 72) "redis"
 73) "notify-keyspace-events"
 74) ""
 75) "ignore-warnings"
 76) ""
 77) "activerehashing"
 78) "yes"
 79) "socket-mark-id"
 80) "0"
 81) "cluster-allow-pubsubshard-when-down"
 82) "yes"
 83) "bind-source-addr"
 84) ""
 85) "cluster-announce-bus-port"
 86) "0"
 87) "zset-max-ziplist-entries"
 88) "128"
 89) "crash-log-enabled"
 90) "yes"
 91) "repl-diskless-sync-max-replicas"
 92) "0"
 93) "min-slaves-to-write"
 94) "0"
 95) "maxmemory-eviction-tenacity"
 96) "10"
 97) "dir"
 98) "/apps/redis/data"
 99) "replica-lazy-flush"
100) "no"
101) "hll-sparse-max-bytes"
102) "3000"
103) "cluster-preferred-endpoint-type"
104) "ip"
105) "zset-max-listpack-value"
...

# 查看bind
127.0.0.1:6379> CONFIG GET bind
1) "bind"
2) "0.0.0.0"

#Redis5.0有些设置无法修改,Redis6.2.6版本支持修改bind
127.0.0.1:6379> CONFIG SET bind 127.0.0.1
(error) ERR Unsupported CONFIG parameter: bind
```

### 2.2.3: 设置Redis使用的最大内存量

```bash
127.0.0.1:6379> CONFIG SET maxmemory 8589934592 或 1g|G # 默认以字节为单位
127.0.0.1:6379> CONFIG GET maxmemory
1) "maxmemory"
2) "8589934592"
```

## 2.3：慢查询

![image-20240429104035113](images\image-20240429104035113.png)

范例：SLOW LOG

```bash
root@redis01:~# cat /apps/redis/etc/redis.conf | grep "slowlog"
slowlog-log-slower-than 1  #单位为us，指定超过1us即为慢的指令，默认值为10000us
slowlog-max-len 1000       #指定只保存最近的1024条慢记录，默认值为128

127.0.0.1:6379> slowlog len   #查看慢日志的记录条数
(integer) 10
127.0.0.1:6379> SLOWLOG GET [n] #查看慢日志的最近n条记录，默认为10
1) 1) (integer) 14
2) (integer) 1544690617       #第2）行表示命令执行的时间戳，距离1970-1-1的秒数，date -d +@1544690617 可以转换
3) (integer) 4                #第3)行表示每条指令的执行时长,单位us
4) 1) "slowlog"

127.0.0.1:6379>  SLOWLOG GET 3
1) 1) (integer) 10
   2) (integer) 1714358884
   3) (integer) 2
   4) 1) "slowlog"
      2) "len"
   5) "127.0.0.1:56054"
   6) ""
2) 1) (integer) 9
   2) (integer) 1714358821
   3) (integer) 43
   4) 1) "SLOWLOG"
      2) "GET"
      3) "3"
   5) "127.0.0.1:56054"
   6) ""
3) 1) (integer) 8
   2) (integer) 1714358783
   3) (integer) 10
   4) 1) "SLOWLOG"
      2) "GET"
      3) "[-1]"
   5) "127.0.0.1:56054"
   6) ""
127.0.0.1:6379> SLOWLOG RESET #清空慢日志
OK
```

## 2.4：Redis持久化

Redis是基于内存型的NoSQL，和MySQL是不同的，使用内存进行数据保存。

如果想实现数据持久化，Redis也可支持将内存数据保存到硬盘文件中。

Redis支持两种数据持久化保存方法：

- RDB:Redis DataBase
- AOF:AppendOnlyFile

![image-20240429110631321](images\image-20240429110631321.png)

### 2.4.1： RDB

#### 2.4.1.1：RDB工作原理

![image-20240429110813091](images\image-20240429110813091.png)

RDB(Redis DataBase)：是基于某个时间点的快照，注意RDB只保留当前最新版本的一个快照

相当于MySQL中的完全备份。

RDB持久化功能所生成的RDB文件是一个经过压缩的二进制文件，通过该文件可以还原生成该RDB文件时数据库状态。因为RDB文件是保存到磁盘中，所以即便Redis服务进程甚至服务器宕机，只要磁盘中RDB文件存在，就能将数据恢复。

RDB支持save和bgsave两种命令实现数据文件持久化

**RDB bgsave实现快照的具体过程：**

注意：save指令使用主进程进行备份，而不生成新的子进程

![image-20240429145741606](images\image-20240429145741606.png)

首先从redis主进程先fork生成一个新的子进程，此子进程负责将Redis内存数据保存为一个临时文件tmp-<子进程pid>.rdb，当数据保存完成后，在将此临时文件改名为RDB文件，如果有前一次保存的RDB文件则将会被替换掉，最后关闭子进程。

由于Redis只保留最后一个版本的RDB文件,如果想实现保存多个版本的数据,需要人为实现。

![image-20240429152434208](images\image-20240429152434208.png)

**范例： save 执行过程会使用主进程进行快照**

```bash
[root@centos7 data]#redis-cli -a 123456 save&
[1] 28684
[root@centos7 data]#pstree -p |grep redis ;ll /apps/redis/data
           |-redis-server(28650)-+-{redis-server}(28651)
           |                     |-{redis-server}(28652)
           |                     |-{redis-server}(28653)
           |                     `-{redis-server}(28654)
           |           |                         `-redis-cli(28684)
           |           `-sshd(23494)---bash(23496)---redis-cli(28601)
total 251016
-rw-r--r-- 1 redis redis 189855682 Nov 17 15:02 dump.rdb
-rw-r--r-- 1 redis redis  45674498 Nov 17 15:02 temp-28650.rdb
```

#### 2.4.1.2: RDB相关配置

```bash
# 在配置文件中的save选项设置多个保存条件，只要任意一个条件满足，服务器都会执行BGSAVE命令
#Redis7.0以后支持写在一行，如：save 3600 1 300 100 60 10000，此也为默认值
save 900 1         #900s内修改了1个key即触发保存RDB
save 300 10        #300s内修改了10个key即触发保存RDB
save 60 10000      #60s内修改了10000个key即触发保存RDB

dbfilename dump.rdb
dir /apps/redis/data/ #编泽编译安装时默认RDB文件存放在Redis的工作目录,此配置可指定保存的数据目录
stop-writes-on-bgsave-error yes #当快照失败是否仍允许写入,yes为出错后禁止写入,建议为no
rdbcompression yes
rdbchecksum yes
```

**范例：RDB相关配置**

```bash
root@redis01:~# grep save /apps/redis/etc/redis.conf
# save <seconds> <changes>
# Redis will save the DB if both the given number of seconds and the given
# save ""
# Unless specified otherwise, by default Redis will save the DB:
# save 3600 1
# save 300 100
# save 60 10000
#以上是默认值


root@redis01:~# redis-cli -a 123456 config get save
Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
1) "save"
2) "3600 1 300 100 60 10000"

#禁用系统的自动快照
root@redis01:~# vim /apps/redis/etc/redis.conf
save ""
# save 3600 1
# save 300 100
# save 60 10000
```

#### 2.4.1.3: 实现RDB方法

- save: 同步，不推荐使用，使用主进程完成快照，因此会阻塞其他命令执行
- bgsave：异步后台执行，不影响其他命令执行，会开启独立的子进程，因此不会阻塞其他命令执行
- 配置文件实现自动保存：在配置文件中制定规则，自动执行bgsave

#### 2.4.1.4：RDB模式的优缺点

##### 2.4.1.4.1：RDB模式优点

- RDB只保存某个时间点的数据，恢复的时候直接加载到内存即可，不用做其他处理，这种文件适用于做灾备处理，可以通过自定义时间点执行redis指令bgsave或save保存快照，实现多个版本的备份

  比如: 可以在最近的24小时内，每小时备份一次RDB文件，并且在每个月的每一天，也备份一个 RDB文件。这样的话，即使遇上问题，也可以随时将数据集还原到指定的不同的版本。

- RDB在大数据集时恢复的速度比AOF方式要快

##### 2.4.1.4.2：RDB模式的缺点

- 不能实时保存数据，可能会丢失自上一次执行RDB备份到当前的内存数据

  如果需要尽量避免在服务器故障时丢失数据，那么RDB并不适合。虽然Redis允许设置不同的保存 点（save point）来控制保存RDB文件的频率，但是，因为RDB文件需要保存整个数据集的状态， 所以它可能并不是一个非常快速的操作。因此一般会超过5分钟以上才保存一次RDB文件。在这种 情况下，一旦发生故障停机，就可能会丢失较长时间的数据。

- 在数据集比较大时，fork子进程可能会非常耗时，造成服务器在一定时间内停止处理客户端请求，如果数据量非常巨大，并且CPU时间非常紧张，那么这种停止时间甚至可能会长达整整一秒 或更久。另外子进程完成生成RDB文件的时间也会花更长时间.

#### 2.4.1.5：备份脚本

**范例：手动执行备份RDB**

```bash
127.0.0.1:6379> set xxx yyy
OK
127.0.0.1:6379> bgsave
Background saving started

root@redis01:~# ll /apps/redis/data/
total 12
drwxr-xr-x 2 redis redis 4096 Apr 29 07:50 ./
drwxr-xr-x 7 redis redis 4096 Apr 28 08:47 ../
-rw-r--r-- 1 redis redis 2493 Apr 29 07:50 dump.rdb
```

**范例: 手动备份RDB文件的脚本**

```bash
# 配置文件
root@redis01:~# cat /apps/redis/etc/redis.conf
save ""   #关闭自动备份
dbfilename dump.rdb
dir "/apps/redis/data/redis"
appendonly no 


#脚本

```

```bash
#!/bin/bash
#
#********************************************************************
#Author:           wanglei
#QQ:               353538339
#Date:             2024-04-29
#FileName:         redis_rdb.sh
#URL:              https://github.com/icloud2native
#Description:      The test script
#Copyright (C):    2024 All rights reserved
#********************************************************************
BACKUP=/backup/redis-rdb
DIR=/apps/redis/data/
FILE=dump.rdb
PASS=123456
color () {
    RES_COL=60
    MOVE_TO_COL="echo -en \\033[${RES_COL}G"
    SETCOLOR_SUCCESS="echo -en \\033[1;32m"
    SETCOLOR_FAILURE="echo -en \\033[1;31m"
    SETCOLOR_WARNING="echo -en \\033[1;33m"
    SETCOLOR_NORMAL="echo -en \E[0m"
    echo -n "$1" && $MOVE_TO_COL
    echo -n "["
    if [ $2 = "success" -o $2 = "0" ] ;then
        ${SETCOLOR_SUCCESS}
        echo -n $"  OK  "    
    elif [ $2 = "failure" -o $2 = "1"  ] ;then 
        ${SETCOLOR_FAILURE}
        echo -n $"FAILED"
    else
        ${SETCOLOR_WARNING}
        echo -n $"WARNING"
    fi
    ${SETCOLOR_NORMAL}
    echo -n "]"
    echo 
}

redis-cli -h 127.0.0.1 -a $PASS --no-auth-warning bgsave 
result=`redis-cli -a $PASS --no-auth-warning info Persistence |awk -F: '/rdb_bgsave_in_progress/{print $2}'`

while [ $result == "1" ]
do
  sleep 1
  result=`redis-cli -a $PASS --no-auth-warning info Persistence |awk -F: '/rdb_bgsave_in_progress/{print $2}'`
done


DATE=`date +%F_%H-%M-%S`
[ -e $BACKUP ] || { mkdir -p $BACKUP ; chown -R redis.redis $BACKUP; }
cp $DIR/$FILE $BACKUP/dump_6379-${DATE}.rdb
color "Backup redis RDB" 0


#执行
root@redis01:~# bash redis_backup_rdb.sh 
Background saving started
Backup redis RDB                                           [  OK  ]

root@redis01:~# ll /backup/redis-rdb/ -h
total 32K
drwxr-xr-x 2 redis redis 4.0K Apr 29 08:28 ./
drwxr-xr-x 3 root  root  4.0K Apr 29 08:18 ../
-rw-r--r-- 1 root  root  2.5K Apr 29 08:18 dump_6379-2024-04-29_08-18-39.rdb
-rw-r--r-- 1 root  root  2.5K Apr 29 08:23 dump_6379-2024-04-29_08-23-59.rdb
-rw-r--r-- 1 root  root  2.5K Apr 29 08:24 dump_6379-2024-04-29_08-24-42.rdb
-rw-r--r-- 1 root  root  2.5K Apr 29 08:26 dump_6379-2024-04-29_08-26-36.rdb
-rw-r--r-- 1 root  root  2.5K Apr 29 08:27 dump_6379-2024-04-29_08-27-18.rdb
-rw-r--r-- 1 root  root  2.5K Apr 29 08:28 dump_6379-2024-04-29_08-28-15.rdb
```

### 2.4.2： AOF

#### 2.4.2.1： AOF工作原理

![image-20240429163356710](images\image-20240429163356710.png)



AOF即AppendOnlyFile，AOF和RDB都采用COW机制，AOF可以指定不同的保存策略，默认为每秒执行一次fsync，按照操作的顺序将变更命令追加到指定的AOF日志文件尾部

在第一次启用AOF功能时，会做一次完全备份，后续执行增量备份，相当于完全备份+增量备份

如果同时启用RDB和AOF功能时，默认AOF文件优先级高于RDB文件，即会使用AOF文件进行恢复

在第一次开启AOF功能时,会自动备份所有数据到AOF文件中,后续只会记录数据的更新指令

#### 2.4.2.2： 正确和错误开启AOF功能

**注意：AOF模式默认是关闭的，第一次开启AOF后，并重启服务生效后，会因为AOF的优先级高于RDB，而AOF默认没有数据文件存在，从而导致所有数据丢失**

范例：错误开启AOF功能,会导致数据丢失

```bash
root@redis01:~# redis-cli -a 123456
127.0.0.1:6379> dbsize
(integer) 204

root@redis01:~# vim /apps/redis/etc/redis.conf
appendonly yes #修改此行

root@redis01:~# systemctl restart redis

root@redis01:~# redis-cli -a 123456
127.0.0.1:6379> dbsize
(integer) 0
```

范例：正确启用AOF功能，防止数据丢失

```bash
root@redis01:~# ll /apps/redis/data/
-rw-r--r-- 1 redis redis 2493 Apr 29 08:32 dump.rdb

127.0.0.1:6379> config get appendonly
1) "appendonly"
2) "no"
127.0.0.1:6379> config set appendonly  yes
OK

root@redis01:~# ll /apps/redis/data/appendonlydir
-rw-r--r-- 1 redis redis 2493 Apr 29 08:54 appendonly.aof.2.base.rdb
-rw-r--r-- 1 redis redis    0 Apr 29 08:54 appendonly.aof.2.incr.aof
-rw-r--r-- 1 redis redis   88 Apr 29 08:54 appendonly.aof.manifest

#修改配置文件
root@redis01:~# vim /apps/redis/etc/redis.conf
appendonly yes #改为yes
root@redis01:~# systemctl restart redis  #重启服务

#查看数据是否存在
root@redis01:~# redis-cli -a 123456
127.0.0.1:6379> dbsize
(integer) 204
```

范例： Redis 7.0以上版本的AOF是多个文件，Redis6.0以前版本只有一个文件

```bash
# Redis 7.0以上版本
root@redis01:~# ll /apps/redis/data/appendonlydir
-rw-r--r-- 1 redis redis 2493 Apr 29 08:54 appendonly.aof.2.base.rdb
-rw-r--r-- 1 redis redis    0 Apr 29 08:54 appendonly.aof.2.incr.aof
-rw-r--r-- 1 redis redis   88 Apr 29 08:54 appendonly.aof.manifest

#Redis6.0以前版本只有一个文件
[root@ubuntu2204 ~]#file /var/lib/redis/appendonly.aof
/var/lib/redis/appendonly.aof: Redis RDB file, version 0009
```

#### 2.4.2.3: AOF相关配置

```bash
appendonly no #是否开启AOF日志记录，默认redis使用的是rdb方式持久化，这种方式在许多应用中已经足够用了，但是redis如果中途宕机，会导致可能有几分钟的数据丢失(取决于dump数据的间隔时间)，根据save来策略进行持久化，Append Only File是另一种持久化方式，可以提供更好的持久化特性，Redis会把每次写入的数据在接收后都写入 appendonly.aof 文件，每次启动时Redis都会先把这个文件的数据读入内存里，先忽略RDB文件。默认不启用此功能

appendfilename "appendonly.aof" #文本文件AOF的文件名，存放在dir指令指定的目录中
appenddirname "appendonlydir"    #7.X 版指定目录名称

appendfsync everysec #aof持久化策略的配置
#no表示由操作系统保证数据同步到磁盘,Linux的默认fsync策略是30秒，最多会丢失30s的数据
#always表示每次写入都执行fsync，以保证数据同步到磁盘,安全性高,性能较差
#everysec表示每秒执行一次fsync，可能会导致丢失这1s数据,此为默认值,也生产建议值

dir /path

#rewrite相关
no-appendfsync-on-rewrite yes
auto-aof-rewrite-percentage 100
auto-aof-rewrite-min-size 64mb
aof-load-truncated yes 
```

#### 2.4.2.4: AOF Rewrite重写过程和配置

将一些重复的，可以合并的，过期的数据重新写入一个新的AOF文件，从而节约AOF备份占用的硬盘空间，也能加速恢复过程。

可以手动执行bgrewriteaof 触发AOF,第一次开启AOF功能,或定义自动rewrite 策略

**AOF rewrite 过程**

父进程生成一个新的子进程负责生成新的AOF文件，同时父进程将新的数据更新同时写入两个缓冲区 aof_buf和aof_rewrite_buf

![image-20240429171251026](images\image-20240429171251026.png)

**AOF rewrite 重写相关配置**

```bash
#同时在执行bgrewriteaof操作和主进程写aof文件的操作，两者都会操作磁盘，而bgrewriteaof往往会涉及大量磁盘操作， 这样就会造成主进程在写aof文件的时候出现阻塞的情形,以下参数实现控制

no-appendfsync-on-rewrite no #在aof rewrite期间,是否对aof新记录的append暂缓使用文件同步策略,主要考虑磁盘IO开支和请求阻塞时间。
#默认为no,表示"不暂缓",新的aof记录仍然会被立即同步到磁盘，是最安全的方式，不会丢失数据，但是要忍受阻塞的问题
#为yes,相当于将appendfsync设置为no，这说明并没有执行磁盘操作，只是写入了缓冲区，因此这样并不会造成阻塞（因为没有竞争磁盘），但是如果这个时候redis挂掉，就会丢失数据。丢失多少数据呢？Linux的默认fsync策略是30秒，最多会丢失30s的数据,但由于yes性能较好而且会避免出现阻塞因此比较推荐


#rewrite 即对aof文件进行整理,将空闲空间回收,从而可以减少恢复数据时间
auto-aof-rewrite-percentage 100 #当Aof log增长超过指定百分比例时，重写AOF文件，设置为0表示不自动重写Aof日志，重写是为了使aof体积保持最小，但是还可以确保保存最完整的数据

auto-aof-rewrite-min-size 64mb #触发aof rewrite的最小文件大小

aof-load-truncated yes #是否加载由于某些原因导致的末尾异常的AOF文件(主进程被kill/断电等)，建议yes
```

#### 2.4.2.5：手动执行AOF重写 BGREWRITEAOF命令

```http
BGREWRITEAOF
时间复杂度： O(N)， N 为要追加到 AOF 文件中的数据数量。
执行一个 AOF文件 重写操作。重写会创建一个当前 AOF 文件的体积优化版本。


即使BGREWRITEAOF 执行失败，也不会有任何数据丢失，因为旧的 AOF 文件在 BGREWRITEAOF 成功之前不会被修改。

重写操作只会在没有其他持久化工作在后台执行时被触发，也就是说：
如果 Redis 的子进程正在执行快照的保存工作，那么 AOF 重写的操作会被预定(scheduled)，等到保存
工作完成之后再执行 AOF 重写。在这种情况下， BGREWRITEAOF 的返回值仍然是 OK ，但还会加上一条
额外的信息，说明 BGREWRITEAOF 要等到保存操作完成之后才能执行。在 Redis 2.6 或以上的版本，可
以使用 INFO [section] 命令查看 BGREWRITEAOF 是否被预定。

如果已经有别的 AOF 文件重写在执行，那么 BGREWRITEAOF 返回一个错误，并且这个新的 
BGREWRITEAOF 请求也不会被预定到下次执行。

从 Redis 2.4 开始， AOF 重写由 Redis 自行触发， BGREWRITEAOF 仅仅用于手动触发重写操作。
```

范例: 手动 bgrewriteaof

```BASH
#  7.X版本
root@redis01:~# redis-cli -a 123456 BGREWRITEAOF;pstree -p| grep redis-server; ll /apps/redis/data/appendonlydir/
Background append only file rewriting started
           |-redis-server(48991)-+-redis-server(49921) #会fork一个子进程用来生成新的aof文件
           |                     |-{redis-server}(49002)
           |                     |-{redis-server}(49003)
           |                     |-{redis-server}(49004)
           |                     `-{redis-server}(49005)
total 16
drwxr-xr-x 2 redis redis 4096 Apr 29 09:25 ./
drwxr-xr-x 3 redis redis 4096 Apr 29 09:25 ../
-rw-r--r-- 1 redis redis 2493 Apr 29 09:23 appendonly.aof.3.base.rdb
-rw-r--r-- 1 redis redis    0 Apr 29 09:23 appendonly.aof.3.incr.aof
-rw-r--r-- 1 redis redis    0 Apr 29 09:25 appendonly.aof.4.incr.aof
-rw-r--r-- 1 redis redis  132 Apr 29 09:25 appendonly.aof.manifest


# 执行完成后incr文件清空，合并到RDB文件中
root@redis01:~# ll /apps/redis/data/appendonlydir/
-rw-r--r-- 1 redis redis 2493 Apr 29 09:25 appendonly.aof.4.base.rdb
-rw-r--r-- 1 redis redis    0 Apr 29 09:25 appendonly.aof.4.incr.aof
-rw-r--r-- 1 redis redis   88 Apr 29 09:25 appendonly.aof.manifest


#6.X前同时可以观察到下面显示
```

![image-20240429172756120](images\image-20240429172756120.png)

#### 2.4.2.6：AOF模式优缺点

##### 2.4.2.6.1：AOF 模式优点

- 数据安全性相对较高，根据所使用的fsync策略(fsync是同步内存中redis所有已经修改的文件到存 储设备)，默认是appendfsync everysec，即每秒执行一次 fsync,在这种配置下，Redis 仍然可以保 持良好的性能，并且就算发生故障停机，也最多只会丢失一秒钟的数据( fsync会在后台线程执行， 所以主线程可以继续努力地处理命令请求)

- 由于该机制对日志文件的写入操作采用的是append模式，因此在写入过程中不需要seek, 即使出现 宕机现象，也不会破坏日志文件中已经存在的内容。然而如果本次操作只是写入了一半数据就出现 了系统崩溃问题，不用担心，在Redis下一次启动之前，可以通过 redis-check-aof 工具来解决数据 一致性的问题

- Redis可以在 AOF文件体积变得过大时，自动地在后台对AOF进行重写,重写后的新AOF文件包含了 恢复当前数据集所需的最小命令集合。整个重写操作是绝对安全的，因为Redis在创建新 AOF文件 的过程中，append模式不断的将修改数据追加到现有的 AOF文件里面，即使重写过程中发生停 机，现有的 AOF文件也不会丢失。而一旦新AOF文件创建完毕，Redis就会从旧AOF文件切换到新 AOF文件，并开始对新AOF文件进行追加操作。

- AOF包含一个格式清晰、易于理解的日志文件用于记录所有的修改操作。事实上，也可以通过该文 件完成数据的重建

  AOF文件有序地保存了对数据库执行的所有写入操作，这些写入操作以Redis协议的格式保存，因 此 AOF文件的内容非常容易被人读懂，对文件进行分析(parse)也很轻松。导出（export)AOF文件 也非常简单:举个例子，如果不小心执行了FLUSHALL.命令，但只要AOF文件未被重写，那么只要停 止服务器，移除 AOF文件末尾的FLUSHAL命令，并重启Redis ,就可以将数据集恢复到FLUSHALL执 行之前的状态。

##### 2.4.2.6.2：AOF 模式缺点

- 即使有些操作是重复的也会全部记录，AOF 的文件大小一般要大于 RDB 格式的文件
- AOF 在恢复大数据集时的速度比 RDB 的恢复速度要慢
- 如果 fsync 策略是appendfsync no, AOF保存到磁盘的速度甚至会可能会慢于RDB
- bug 出现的可能性更多

### 2.4.3： RDB和AOF的选择

如果主要充当缓存功能，或者可以承受较长时间，比如数分钟数据的丢失，通常生产环境一般只需要启用RDB即可，这也是默认值

如果一点数据都不能丢失，可以选择同时开启RDB和AOF

一般不建议只开AOF

## 2.5 Redis 常用命令

官方文档：

```http
https://redis.io/commands
```

### 2.5.1 INFO

显示当前节点redis运行状态信息

```bash
127.0.0.1:6379> info
# Server
redis_version:7.0.15
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:7ed1a2d8893f5a3b
redis_mode:standalone
os:Linux 5.4.0-177-generic x86_64
arch_bits:64
monotonic_clock:POSIX clock_gettime
multiplexing_api:epoll
atomicvar_api:c11-builtin
........

#只显示指定的部分内容
root@redis01:~# redis-cli -a 123456 info server
# Server
redis_version:7.0.15
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:7ed1a2d8893f5a3b

root@redis01:~# redis-cli -a 123456 info Cluster
# Cluster
cluster_enabled:0
```

### 2.5.2: SELECT

切换数据库，相当于mysql中的use dbname 命令。

```bash
127.0.0.1:6379> select 0
OK
127.0.0.1:6379> select 10
OK
127.0.0.1:6379[10]> select 16
(error) ERR DB index is out of range
```

注意: 在Redis cluster 模式下不支持多个数据库,会出现下面错误

```bash
root@centos8 ~]#redis-cli 
127.0.0.1:6379> info cluster
# Cluster
cluster_enabled:1
127.0.0.1:6379> select 0
OK
127.0.0.1:6379> select 1
(error) ERR SELECT is not allowed in cluster mode
```

### 2.5.3: KEYS

 查看当前库下的所有key，此命令慎用！

![image-20240429174113401](images\image-20240429174113401.png)

```bash
27.0.0.1:6379> keys *
```

### 2.5.4: BGSAVE

手动在后台执行RDB持久化操作。

```bash
root@redis01:~# redis-cli -a 123456 bgsave
Background saving started
```

### 2.5.5: DBSIZE

返回当前库下所有key的数量

```http
127.0.0.1:6379> dbsize
(integer) 204
```

### 2.5.6: FLUSHDB

强制清空当前库中所有的key，此命令慎用

```http
127.0.0.1:6379[1]> SELECT 0
OK
127.0.0.1:6379> DBSIZE
(integer) 4
127.0.0.1:6379> FLUSHDB
OK
127.0.0.1:6379> DBSIZE
(integer) 0
127.0.0.1:6379>
```

### 2.5.7 FLUSHALL

强制清空当前Redis服务器所有数据库中的key，即删除所有数据，此命令慎用！

```bash
127.0.0.1:6379> FLUSHALL
OK
#生产建议修改配置使用rename-command禁用此命令
vim /etc/redis.conf
rename-command FLUSHALL "" #flushdb和flushall 配置和AOF功能冲突，需要设置 appendonly 
no,不区分命令大小写
```

### 2.5.8 SHUTDOWN

```bash
可用版本： >= 1.0.0

时间复杂度： O(N)，其中 N 为关机时需要保存的数据库键数量。
SHUTDOWN 命令执行以下操作：

关闭Redis服务,停止所有客户端连接
如果有至少一个保存点在等待，执行 SAVE 命令
如果 AOF 选项被打开，更新 AOF 文件
关闭 redis 服务器(server)
如果持久化被打开的话， SHUTDOWN 命令会保证服务器正常关闭而不丢失任何数据。

另一方面，假如只是单纯地执行 SAVE 命令，然后再执行 QUIT 命令，则没有这一保证 —— 因为在执行 
SAVE 之后、执行 QUIT 之前的这段时间中间，其他客户端可能正在和服务器进行通讯，这时如果执行 QUIT 
就会造成数据丢失。
#建议禁用此指令
vim /etc/redis.conf
rename-command shutdown ""
```

## 2.6: Redis数据类型

参考资料：http://www.redis.cn/topics/data-types.html 

相关命令参考: http://redisdoc.com/

![image-20240429180445024](images\image-20240429180445024.png)

![image-20240429180518387](images\image-20240429180518387.png)

### 2.6.1 字符串 string

字符串是一种最基本的Redis值类型。Redis字符串是二进制安全的，这意味着一个Redis字符串能包含任 意类型的数据，例如： 一张JPEG格式的图片或者一个序列化的Ruby对象。一个字符串类型的值最多能 存储512M字节的内容。Redis 中所有 key 都是字符串类型的。此数据类型最为常用

![image-20240429180711634](images\image-20240429180711634.png)

#### 2.6.1.1 创建一个key

set指令可以创建一个key并赋值，使用格式

```http
SET key value [EX seconds] [PX milliseconds] [NX|XX]

从 Redis 2.6.12 版本开始， SET 命令的行为可以通过一系列参数来修改：
EX seconds: 设置key的过期时间，单位为秒。执行 SET key value EX seconds 的效果等同于执行 SETEX key seconds value 。
PX milliseconds ： 将键的过期时间设置为 milliseconds 毫秒。 执行 SET key value PX 
milliseconds 的效果等同于执行 PSETEX key milliseconds value 。
NX ： 只在键不存在时， 才对键进行设置操作。 执行 SET key value NX 的效果等同于执行 SETNX 
key value 。
XX ： 只在键已经存在时， 才对键进行设置操作。
```

范例：

```bash
# 不论key是否存在，都设置
127.0.0.1:6379> set key01 value01
OK
127.0.0.1:6379> get key01
"value01" 
127.0.0.1:6379> TYPE key1   #判断值类型
string
127.0.0.1:6379> SET title ceo ex 3 #设置自动过期时间3s
OK
127.0.0.1:6379> set NAME wang
OK
127.0.0.1:6379> get NAME
"wang"


#key大小写敏感
127.0.0.1:6379> get name
(nil)
127.0.0.1:6379> set name "wanglei"
OK
127.0.0.1:6379> get name
"wanglei"
127.0.0.1:6379> get NAME
"wang"


#key不存在,才设置,相当于add
127.0.0.1:6379> get name
"wanglei"
127.0.0.1:6379> setnx  name "littleboy"  #set key value nx
(integer) 0
127.0.0.1:6379> get name
"wanglei"


#key存在才设置，相当于update
127.0.0.1:6379> get name
"wanglei"
127.0.0.1:6379> set name "littleboy" xx
OK
127.0.0.1:6379> get name
"littleboy"
```

#### 2.6.1.2 查看一个key的值

```bash
127.0.0.1:6379> get key1
"value1"

#get只能查看一个key的值
127.0.0.1:6379> get key1 key2
(error) ERR wrong number of arguments for 'get' command
```

#### 2.6.1.3 删除key

```bash
127.0.0.1:6379> del key1
(integer) 1

127.0.0.1:6379> del key2 key3
(integer) 2
```

#### 2.6.1.4 批量设置多个key

```bash
127.0.0.1:6379> mset key001 value001 key002 value002
OK
```

#### 2.6.1.5 批量获取多个key

```bash
127.0.0.1:6379> MGET key001 key002
1) "value001"
2) "value002"
```

#### 2.6.1.6 追加key的数据

```bash
127.0.0.1:6379> get name
"wanglei"

127.0.0.1:6379> append name " is a good boy"
(integer) 21

127.0.0.1:6379> get name
"wanglei is a good boy"
```

#### 2.6.1.7 设置新值并返回旧值

```bash
127.0.0.1:6379> get name
"wanglei is a good boy"

127.0.0.1:6379> getset name "little"
"wanglei is a good boy"

127.0.0.1:6379> get name
"little
```

#### 2.6.1.8 返回字符串 key 对应值的字节数

```bash
127.0.0.1:6379> get name
"little"

127.0.0.1:6379> strlen name
(integer) 6
```

#### 2.6.1.9 判断 key 是否存在

```bash
127.0.0.1:6379> EXISTS NAME
(integer) 1

# 返回值为1,表示存在,0表示不存在
```

#### 2.6.1.10 获取 key 的过期时长

```bash
ttl key #查看key的剩余生存时间,如果key过期后,会自动删除
-1 #返回值表示永不过期，默认创建的key是永不过期，重新对key赋值，也会从有剩余生命周期变成永不过
期
-2 #返回值表示没有此key
num #key的剩余有效期

127.0.0.1:6379> set job cloudnative ex 10
OK

127.0.0.1:6379> ttl job
(integer) 7
```

#### 2.6.1.11 重置key的过期时长

```bash
127.0.0.1:6379> EXPIRE name 1000
(integer) 1
127.0.0.1:6379> ttl name
(integer) 993
```

#### 2.6.1.12 取消key的期限

即永不过期

```bash
127.0.0.1:6379> ttl name
(integer) 950
127.0.0.1:6379> PERSIST name
(integer) 1
127.0.0.1:6379> ttl name
(integer) -1
```

#### 2.6.1.13 数字递增

利用INCR命令集（INCR,DECR,INCRBY,DECRBY）来把字符串当作原子计数器使用。

```shell
127.0.0.1:6379> set num 10 #设置初始值
OK
127.0.0.1:6379> incr num
(integer) 11
127.0.0.1:6379> get num
"11"
```

#### 2.6.1.14 数字递减

```shell
127.0.0.1:6379> set num 10
OK
127.0.0.1:6379> DECR num
(integer) 9
127.0.0.1:6379> get num
"9"
```

#### 2.6.1.15: 数字增加

将key对应的数字加decrement(可以是负数)。如果key不存在，操作之前，key就会被置为0。如果key的 value类型错误或者是个不能表示成数字的字符串，就返回错误。这个操作最多支持64位有符号的正型 数字。

```bash
redis> SET mykey 10
OK
redis> INCRBY mykey 5
(integer) 15
127.0.0.1:6379> get mykey
"15"
127.0.0.1:6379> INCRBY mykey -10
(integer) 5
127.0.0.1:6379> get mykey
"5"
127.0.0.1:6379> INCRBY nokey  5
(integer) 5
127.0.0.1:6379> get nokey
"5"
```

#### 2.6.1.16 数字减少

decrby 可以减小数值(也可以增加).

```bash
127.0.0.1:6379> SET mykey 10
OK
127.0.0.1:6379> DECRBY mykey 8
(integer) 2
127.0.0.1:6379> get mykey
"2"
127.0.0.1:6379> DECRBY mykey -20
(integer) 22
127.0.0.1:6379> get mykey
"22"
127.0.0.1:6379> DECRBY nokey 3
(integer) -3
127.0.0.1:6379> get nokey
"-3"
```

### 2.6.2: 列表list

![image-20240506142112208](images\image-20240506142112208.png)

Redis列表实际就是简单的字符串数组，按照插入顺序进行排序。

支持双向读写，可以添加一个元素到列表的头部（左边）或者尾部（右边），一个列表最多包含2^32-1=4294967295个元素.

每个列表元素用下标来标识,下标 0 表示列表的第一个元素，以 1 表示列表的第二个元素，以此类推。

也可以使用负数下标，以 -1 表示列表的最后一个元素， -2 表示列表的倒数第二个元素，元素值可以重 复，常用于存入日志等场景，此数据类型比较常用.

列表的特点：

- 有序
- 可重复
- 左右都可以操作

#### 2.6.2.1： 创建列表和数据

![image-20240506142539815](images\image-20240506142539815.png)

![image-20240506142552787](images\image-20240506142552787.png)

LPUSH和RPUSH都可以插入列表

```http
LPUSH key value [value …]
时间复杂度： O(1)
将一个或多个值 value 插入到列表 key 的表头

如果有多个 value 值，那么各个 value 值按从左到右的顺序依次插入到表头： 比如说，对空列表 
mylist 执行命令 LPUSH mylist a b c ，列表的值将是 c b a ，这等同于原子性地执行 LPUSH 
mylist a 、 LPUSH mylist b 和 LPUSH mylist c 三个命令。

如果 key 不存在，一个空列表会被创建并执行 LPUSH 操作。
当 key 存在但不是列表类型时，返回一个错误。


RPUSH key value [value …]
时间复杂度： O(1)
将一个或多个值 value 插入到列表 key 的表尾(最右边)。

如果有多个 value 值，那么各个 value 值按从左到右的顺序依次插入到表尾：比如对一个空列表 mylist 
执行 RPUSH mylist a b c ，得出的结果列表为 a b c ，等同于执行命令 RPUSH mylist a 、 
RPUSH mylist b 、 RPUSH mylist c 。

如果 key 不存在，一个空列表会被创建并执行 RPUSH 操作。
当 key 存在但不是列表类型时，返回一个错误。
```

范例：

```shell
#从左边添加数据，已添加的需向右移
127.0.0.1:6379> LPUSH car benchi baoma su7
(integer) 3
127.0.0.1:6379> type car
list


#从右边添加数据
127.0.0.1:6379> RPUSH peope man woman kids
(integer) 3
127.0.0.1:6379> type peope
list
```

#### 2.6.2.2 列表追加新数据

```bash
127.0.0.1:6379> LPUSH list1 tom
(integer) 2
#从右边添加数据，已添加的向左移
127.0.0.1:6379> RPUSH list1 jack
(integer) 3
```

#### 2.6.2.3 获取列表长度(元素个数)

```bash
127.0.0.1:6379> LLEN car
(integer) 3
```

#### 2.6.2.4 获取列表指定位置元素数据

![image-20240506143207534](images\image-20240506143207534.png)

![image-20240506143223023](images\image-20240506143223023.png)



![image-20240506143241789](images\image-20240506143241789.png)

```bash
127.0.0.1:6379> LPUSH list a b c d
(integer) 4
127.0.0.1:6379> LINDEX list 0 #获取0编号的元素
"d"
127.0.0.1:6379> LINDEX list 1 #获取1编号的元素
"c"


#获取指定范围的元素
127.0.0.1:6379> LRANGE list 0 3 #所有元素
1) "d"
2) "c"
3) "b"
4) "a"
```

#### 2.6.2.5 修改列表指定索引值

![image-20240506143608913](images\image-20240506143608913.png)



```bash
127.0.0.1:6379> LPUSH number 5 4 3 2 1
(integer) 5
127.0.0.1:6379> LSET number 2 golang
OK
127.0.0.1:6379> LRANGE number 0 -1
1) "1"
2) "2"
3) "golang"
4) "4"
5) "5"
```

#### 2.6.2.6 删除列表数据

![image-20240506143826220](images\image-20240506143826220.png)

![image-20240506143838616](images\image-20240506143838616.png)

```bash
127.0.0.1:6379> LPUSH list1 a b c d
(integer) 4
127.0.0.1:6379> LRANGE list1 0 3
1) "d"
2) "c"
3) "b"
4) "a"
127.0.0.1:6379> LPOP list1 #弹出左边第一个元素，即删除第一个
"d"
127.0.0.1:6379> LLEN list1
(integer) 3
127.0.0.1:6379> LRANGE list1 0 2
1) "c"
2) "b"
3) "a"
127.0.0.1:6379> RPOP list1  #弹出右边第一个元素，即删除最后一个
"a"
127.0.0.1:6379> LLEN list1
(integer) 2
127.0.0.1:6379> LRANGE list1 0 1
1) "c"
2) "b"
#LTRIM 对一个列表进行修剪(trim)，让列表只保留指定区间内的元素，不在指定区间之内的元素都将被删
除
127.0.0.1:6379> LLEN list1
(integer) 4
127.0.0.1:6379> LRANGE list1 0 3
1) "d"
2) "c"
3) "b"
4) "a"

127.0.0.1:6379> LTRIM list1 1 2 #只保留1，2号元素
OK
127.0.0.1:6379> LLEN list1
(integer) 2
127.0.0.1:6379> LRANGE list1 0 1
1) "c"
2) "b"
#删除list
127.0.0.1:6379> DEL list1
(integer) 1
127.0.0.1:6379> EXISTS list1
(integer) 0
```

### 2.6.3: 集合set

![image-20240506144109633](images\image-20240506144109633.png)

SET是一个无序的字符串合集

同一个集合中的每个元素都是唯一无重复的

支持在两个不同的集合中对数据进行逻辑处理，常用于取交集,并集,统计等场景,例如: 实现共同的朋友

集合特点：

- 无序
- 无重复
- 集合间操作

#### 2.6.3.1 创建集合

```bash
127.0.0.1:6379> SADD set v1
(integer) 1
127.0.0.1:6379> SADD set2 v3 v5 v6
(integer) 3
127.0.0.1:6379> type set
set
127.0.0.1:6379> type set2
set
```

#### 2.6.3.2 集合中追加数据

```bash
#追加时，只能追加不存在的数据，不能追加已经存在的数值
127.0.0.1:6379> SADD set1 v2 v3 v4
(integer) 3
127.0.0.1:6379> SADD set1 v2 #已存在的value,无法再次添加
(integer) 0
127.0.0.1:6379> TYPE set1
set
127.0.0.1:6379> TYPE set2
set
```

#### 2.6.3.3 获取集合的所有数据

```bash
127.0.0.1:6379> SMEMBERS set
1) "v1"
127.0.0.1:6379> SMEMBERS set2
1) "v5"
2) "v6"
3) "v3"
```

#### 2.6.3.4 删除集合中的元素

```bash
127.0.0.1:6379> srem set2 v6
(integer) 1
127.0.0.1:6379> SMEMBERS set2
1) "v5"
2) "v3"
```

**集合间的操作**

![image-20240506144932663](images\image-20240506144932663.png)



#### 2.6.3.5 取集合的交集

交集：同时属于集合A且属于集合B的元素

可以实现共同的朋友

```bash
127.0.0.1:6379> SADD set_1 music football basketball run jump
(integer) 5
127.0.0.1:6379> SADD set_2 run sing dance
(integer) 3

127.0.0.1:6379> SINTER set_1 set_2
1) "run"
```

#### 2.6.3.6 取集合的并集

并集：属于集合A或者属于集合B的元素

```bash
127.0.0.1:6379> SUNION set_1 set_2
1) "dance"
2) "jump"
3) "football"
4) "music"
5) "basketball"
6) "run"
7) "sing"
```

#### 2.6.2.7 取集合的差集

差集：属于集合A但不属于集合B的元素

可以实现我的朋友的朋友

```bash
#属于set_1不属于set_2的元素
127.0.0.1:6379> SDIFF set_1 set_2
1) "basketball"
2) "music"
3) "jump"
4) "football"

#属于set_2不属于set_2的元素
127.0.0.1:6379> SDIFF set_2 set_1
1) "dance"
2) "sing"
```

### 2.6.4 有序集合 sorted set

Redis有序集合和Redis集合类似，是不包含相同字符串的合集。

它们的差别是，每个有序集合的成员都关联着一个双精度浮点型的评分

这个评分用于把有序集合中的成员按最低分到最高分排序。

有序集合的成员不能重复,但评分可以重复,一个有序集合中最多的成员数为 2^32 - 1=4294967295个， 经常用于排行榜的场景。

![image-20240506145956412](images\image-20240506145956412.png)

有序集合特点

- 有序
- 无重复元素
- 每个元素都是由SCORE和VALUE组成
- score可以重复
- value不可以重复

#### 2.6.4.1：创建有序集合

```bash
127.0.0.1:6379> ZADD zset1 1 v1 #分数为1
(integer) 1
127.0.0.1:6379> ZADD zset1 2 v2
(integer) 1
127.0.0.1:6379> ZADD zset1 2 v3  #分数可重复，元素值不可以重复
(integer) 1
127.0.0.1:6379> ZADD zset1 3 v4
(integer) 1
127.0.0.1:6379> type zset1
zset


#一次生成多个数据：
127.0.0.1:6379> ZADD zset2 1 v1 2 v2 3 v3 4 v4 5 v5
(integer) 5
```

#### 2.6.4.2: 实现排名

```bash
127.0.0.1:6379> ZADD course 90 linux 99 go 60 python 50 cloud
(integer) 4
127.0.0.1:6379> ZRANGE course 0 -1  #正序排序后显示集合内所有的key,按score从小到大显示
1) "cloud"
2) "python"
3) "linux"
4) "go"
127.0.0.1:6379> ZREVRANGE course 0 -1 #倒序排序后显示集合内所有的key,score从大到小显示
1) "go"
2) "linux"
3) "python"
4) "cloud"
127.0.0.1:6379> ZRANGE course 0 -1 WITHSCORES  #正序显示指定集合内所有key和得分情况
1) "cloud"
2) "50"
3) "python"
4) "60"
5) "linux"
6) "90"
7) "go"
8) "99"
127.0.0.1:6379> ZREVRANGE course 0 -1 WITHSCORES  #倒序显示指定集合内所有key和得分情况
1) "go"
2) "99"
3) "linux"
4) "90"
5) "python"
6) "60"
7) "cloud"
8) "50"
```

#### 2.6.4.3 查看集合的成员个数

```bash
zset
127.0.0.1:6379> ZCARD zset1
(integer) 4
```

#### 2.6.4.4 基于索引查找数据

```bash
127.0.0.1:6379> ZRANGE course 0 2
1) "cloud"
2) "python"
3) "linux"
127.0.0.1:6379> ZRANGE course 0 10  #超出范围不报错
1) "cloud"
2) "python"
3) "linux"
4) "go"
127.0.0.1:6379> ZRANGE zset1 1 3
1) "v2"
2) "v3"
3) "v4"
127.0.0.1:6379> ZRANGE zset1 0 2
1) "v1"
2) "v2"
3) "v3"
127.0.0.1:6379> ZRANGE zset1 2 2
1) "v3"
```

#### 2.6.4.5 查询指定数据的排名

```bash
127.0.0.1:6379> ZADD course 90 linux 99 go 60 python 50 cloud
(integer) 4
127.0.0.1:6379> ZRANK course go
(integer) 3   #第4个
127.0.0.1:6379> ZRANK course python
(integer) 1   #第2个
```

#### 2.6.4.6 获取分数

```bash
127.0.0.1:6379> zscore course cloud
"30"
```

#### 2.6.4.7 删除元素

```bash
127.0.0.1:6379> ZADD course 90 linux 199 go 60 python 30 cloud
(integer) 4
127.0.0.1:6379> ZRANGE course 0 -1
1) "cloud"
2) "python"
3) "linux"
4) "go"
127.0.0.1:6379> ZREM course python go
(integer) 2
127.0.0.1:6379> ZRANGE course 0 -1
1) "cloud"
2) "linux"
```

### 2.6.5: 哈希hash

hash 即字典, 用于保存字符串字段field和字符串值value之间的映射，即key/value做为数据部分

hash特别适合用于存储对象场景。

一个hash最多可以包含2^32-1 个key/value键值对。

哈希特点：

- 无序

- K/V对

- 适用于存放相关的数据

  ![image-20240506151103579](images\image-20240506151103579.png)

![image-20240506151119265](images\image-20240506151119265.png)

![image-20240506151132108](images\image-20240506151132108.png)

#### 2.6.5.1 创建 hash

格式：

```http
HSET hash field value
时间复杂度： O(1)
将哈希表 hash 中域 field 的值设置为 value 。

如果给定的哈希表并不存在， 那么一个新的哈希表将被创建并执行 HSET 操作。
如果域 field 已经存在于哈希表中， 那么它的旧值将被新值 value 覆盖。
```

范例：

```bash
127.0.0.1:6379> HSET user name wanglei age 30 gender male
(integer) 3

#查看所有字段的值
127.0.0.1:6379> hgetall user
1) "name"
2) "wanglei"
3) "age"
4) "30"
5) "gender"
6) "male"


#增加字段
127.0.0.1:6379> hset user job cloudnative
(integer) 1
127.0.0.1:6379> hgetall user
1) "name"
2) "wanglei"
3) "age"
4) "30"
5) "gender"
6) "male"
7) "job"
8) "cloudnative"
```

#### 2.6.5.2 查看hash的指定field的value

```bash
127.0.0.1:6379> HGET user name
"wanglei"
127.0.0.1:6379> HGET user age
"30"
127.0.0.1:6379> HMGET user name age
1) "wanglei"
2) "30"
```

#### 2.6.5.3 删除hash 的指定的 field/value

```bash
127.0.0.1:6379> HDEL user age
(integer) 1
127.0.0.1:6379> HGET user age
(nil)
```

#### 2.6.5.4 批量设置hash key的多个field和value

```bash
127.0.0.1:6379> HMSET 9527 name zhouxingxing age 50 city hongkong
OK
127.0.0.1:6379> HGETALL 9527
1) "name"
2) "zhouxingxing"
3) "age"
4) "50"
5) "city"
6) "hongkong"
```

#### 2.6.5.5 查看hash指定field的value

```bash
127.0.0.1:6379> HMSET 9527 name zhouxingxing age 50 city hongkong
OK
127.0.0.1:6379> HMGET 9527 name age 
1) "zhouxingxing"
2) "50"
127.0.0.1:6379> 
```

#### 2.6.5.6 查看hash的所有field

```bash
127.0.0.1:6379> HKEYS user
1) "name"
2) "gender"
3) "job"
```

#### 2.6.5.7 查看hash 所有value

```bash
127.0.0.1:6379> HVALS user
1) "wanglei"
2) "male"
3) "cloudnative"
```

#### 2.6.5.8 查看指定 hash的所有field及value

```bash
127.0.0.1:6379> HGETALL user
1) "name"
2) "wanglei"
3) "gender"
4) "male"
5) "job"
6) "cloudnative"
```

#### 2.6.5.9:  删除 hash

```bash
127.0.0.1:6379> DEL user
(integer) 1
127.0.0.1:6379> HGETALL user
(empty array)
```

## 2.7: 消息队列

消息队列: 把要传输的数据放在队列中,从而实现应用之间的数据交换

常用功能：可以实现多个应用系统之间的解耦，异步，削峰/限流

常用的消息队列应用：Kafka，RabbitMQ，Redis

![image-20240506152549372](images\image-20240506152549372.png)

消息队列分为两种：

- 生产者/消费者模式: Producer/Consumer
- 发布者/订阅者模式: Publisher/Subscriber

### 2.7.1: 生产者消费者模式

#### 2.7.1.1 模式说明

生产者消费者模式下，多个消费者同时监听一个频道（Redis用队列实现），但是生产者产生的一个消息只能被最先抢到消息的一个消费者消费一次，队列的消息可以由多个生产者写入，也可以由不同的消费者取出进行消费处理，此模式应用广泛。

![image-20240506152958867](images\image-20240506152958867.png)

![image-20240506153020716](images\image-20240506153020716.png)

#### 2.7.1.2 生产者生成消息

```bash
127.0.0.1:6379> LPUSH channel1 message1 #从管道的左侧写入
(integer) 1
127.0.0.1:6379> LPUSH channel1 message2
(integer) 2
127.0.0.1:6379> LPUSH channel1 message3
(integer) 3
127.0.0.1:6379> LPUSH channel1 message4
(integer) 4
127.0.0.1:6379> LPUSH channel1 message5
(integer) 5
```

#### 2.7.1.3 获取所有消息

```bash
127.0.0.1:6379> LRANGE channel1 0 -1
1) "message5"
2) "message4"
3) "message3"
4) "message2"
5) "message1"
```

#### 2.7.1.4 消费者消费消息

```bash
127.0.0.1:6379> RPOP channel1  #基于实现消息队列的先进先出原则,从管道的右侧消费
"message1"
127.0.0.1:6379> RPOP channel1
"message2"
127.0.0.1:6379> RPOP channel1
"message3"
127.0.0.1:6379> RPOP channel1
"message4"
127.0.0.1:6379> RPOP channel1
"message5"
127.0.0.1:6379> RPOP channel1
(nil)
```

#### 2.7.1.5 验证队列消息消费完成

```bash
127.0.0.1:6379> LRANGE channel1 0 -1
(empty array) #验证队列中的消息全部消费完成
```

### 2.7.2 发布者订阅模式

#### 2.7.2.1 模式说明

在发布者订阅者Pub/Sub模式下，发布者Publisher将消息发布到指定的频道channel，事先监听此channel的一个或多个订阅者Subscriber都会收到相同的消息。即一个消息可以由多个订阅者获取到。对于社交应用中的群聊，群发，群公告等场景适用于此模式。

![image-20240506164637916](images\image-20240506164637916.png)

#### 2.7.2.2 订阅者订阅频道

```bash
127.0.0.1:6379> SUBSCRIBE channel01   #订阅者事先订阅指定的频道，之后发布的消息才能收到
Reading messages... (press Ctrl-C to quit)
1) "subscribe"
2) "channel01"
3) (integer) 1

```

#### 2.7.2.3 发布者发布消息

```bash
127.0.0.1:6379> PUBLISH channel01 message1   #发布者发布信息到指定频道
(integer) 1    #订阅者个数
127.0.0.1:6379> PUBLISH channel01 message2
(integer) 1
```

#### 2.7.2.4 各个订阅者都能收到消息

```bash
root@redis01:~# redis-cli -a 123456
Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
127.0.0.1:6379> SUBSCRIBE channel01 
Reading messages... (press Ctrl-C to quit)
1) "subscribe"
2) "channel01"
3) (integer) 1
1) "message"
2) "channel01"
3) "message1"
1) "message"
2) "channel01"
3) "message2"
```

#### 2.7.2.5 订阅多个频道

```bash
#订阅指定的多个频道
127.0.0.1:6379> SUBSCRIBE channel01 channel02
```

#### 2.7.2.6 订阅所有频道

```bash
127.0.0.1:6379> PSUBSCRIBE *  #支持通配符*
```

#### 2.7.2.7 订阅匹配的频道

```bash
127.0.0.1:6379> PSUBSCRIBE chann* #匹配订阅多个频道
```

#### 2.7.2.8 取消订阅频道

```bash
127.0.0.1:6379> unsubscribe channel01
1) "unsubscribe"
2) "channel01"
3) (integer) 0
```

# 3: Redis集群与高可用

Redis单机服务存在数据和服务的单点问题，而且单机性能也存在着上限，可以利用Redis的集群相关技术来解决这些问题。

![image-20240506165549085](images\image-20240506165549085.png)

## 3.1 Redis 主从复制

![image-20240506165638946](images\image-20240506165638946.png)

### 3.1.1.：Redis主从复制架构

Redis和MySQL的主从模式类似，也支持主从模式(MASTER/SLAVE)，可以事先Redis数据的跨主机的远程备份

常见客户端连接主从的架构:

程序APP先连接到高可用性 LB 集群提供的虚拟IP，再由LB调度将用户的请求至后端Redis 服务器来真正 提供服务。

![image-20240506165911532](images\image-20240506165911532.png)

**主从复制特点**

- 一个master可以有多个slave
- 一个slave只能有一个master
- 数据流向是从master到slave单向的
- master可读可写
- slave只读

### 3.1.2 主从复制实现

当master出现故障后，可以自动提升一个slave节点变成新master，因此Redis Slave需要设置和master相同的连接密码

此外当一个slave提升为新的master时需要通过持久化实现数据的恢复。

![image-20240506170327987](images\image-20240506170327987.png)

当配置Redis复制功能时，强烈建议打开主服务器的持久化功能。否则的话，由于延迟等问题，部署的主节点Redis服务应该避免自动启动。

参考案例：导致主从服务器数据全部丢失

```http
1.假设节点A为主服务器，并且关闭了持久化。并且节点B和节点C从节点A复制数据
2.节点A崩溃，然后由自动拉起服务重启了节点A.由于节点A的持久化被关闭了，所以重启之后没有任何数据
3.节点B和节点C将从节点A复制数据，但是A的数据是空的，于是就把自身保存的数据副本删除。
```

在关闭主服务器上的持久化，并同时开启自动拉起进程的情况，即便使用Sentinel来实现Redis的高i可用性，也是非常危险的。因为主服务器可能拉起的非常快，以至于Sentinel在配置的心跳时间间隔内没 有检测到主服务器已被重启，然后还是会发生上面描述的情况,导致数据丢失。

无论何时，数据安全都是极其重要的，所以应该禁止主服务器关闭持久化的同时自动启动。

#### 3.1.2.1 主从命令配置

##### 3.1.2.1.1 启用主从同步

Redis Server 默认为 master节点，如果要配置为从节点,需要指定master服务器的IP,端口及连接密码

在从节点执行 REPLICAOF MASTER_IP PORT 指令可以启用主从同步复制功能,早期版本使用 SLAVEOF  指令

```http
127.0.0.1:6379> REPLICAOF MASTER_IP PORT #新版推荐使用
127.0.0.1:6379> SLAVEOF MasterIP Port   #旧版使用，将被淘汰
127.0.0.1:6379> CONFIG SET masterauth <masterpass>
```

master和SLAVE安装都是采用前文脚本安装。

```bash
# 在master上设置key1
root@redis01:/apps/redis/etc# redis-cli -a 123456
127.0.0.1:6379> info replication
# Replication
role:master
connected_slaves:0
master_failover_state:no-failover
master_replid:521e153bfdebafb665e5258b3b8ebabe51c6d851
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:0
second_repl_offset:-1
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0
127.0.0.1:6379> SET key1 v1-master
OK
127.0.0.1:6379> keys *
1) "key1"
127.0.0.1:6379> get key1
"v1-master"




#以下都在slave上执行，登录
root@redis02:/apps/redis/etc# redis-cli -a 123456
127.0.0.1:6379> info replication
# Replication
role:master
connected_slaves:0
master_failover_state:no-failover
master_replid:9f82203d698dd69525ca578161c4797d9f04ae9d
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:0
second_repl_offset:-1
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0
127.0.0.1:6379> SET key1 v1-slave-18
OK
127.0.0.1:6379> get key1
"v1-slave-18"
127.0.0.1:6379> 


#在第二个slave,也设置相同的key1,但值不同
root@redis03:/apps/redis/etc# redis-cli -a 123456
127.0.0.1:6379> info replication
# Replication
role:master
connected_slaves:0
master_failover_state:no-failover
master_replid:8cf7ecd89d07dc51cd4c7bdbcacf6104a4155a07
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:0
second_repl_offset:-1
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0
127.0.0.1:6379> set key1 v1-slave-28
OK
127.0.0.1:6379> get key1
"v1-slave-28"


#在slave上设置master的IP和端口，4.0版之前的指令为slaveof
127.0.0.1:6379> REPLICAOF 192.168.58.167 6379  #仍可使用SLAVEOF MasterIP Port
OK
#在slave上设置master的密码，才可以同步
127.0.0.1:6379> CONFIG SET masterauth 123456
OK
127.0.0.1:6379> INFO replication
# Replication  #角色变为slave
role:slave
master_host:192.168.58.167 #指向master
master_port:6379
master_link_status:up
master_last_io_seconds_ago:6
master_sync_in_progress:0
slave_read_repl_offset:14
slave_repl_offset:14
slave_priority:100
slave_read_only:1
replica_announced:1
connected_slaves:0
master_failover_state:no-failover
master_replid:ff1081713cc8dc502b7dad36139a8aac60ee121b
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:14
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:14
#查看已经同步成功
127.0.0.1:6379> get key1
"v1-master"


# 在master上可以看到所有slave信息
127.0.0.1:6379> INFO replication
# Replication
role:master
connected_slaves:2
slave0:ip=192.168.58.168,port=6379,state=online,offset=350,lag=0  #slave信息
slave1:ip=192.168.58.169,port=6379,state=online,offset=350,lag=1
master_failover_state:no-failover
master_replid:ff1081713cc8dc502b7dad36139a8aac60ee121b
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:350
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:350
```

##### 3.1.2.1.2: 删除主从同步

在从节点执行 REPLICAOF NO ONE 或 SLAVEOF NO ONE 指令可以取消主从复制

取消复制 会断开和master的连接而不再有主从复制关联, 但不会清除slave上已有的数据

#### 3.1.2.2：修改slave节点配置文件

范例：

```bash
root@redis02:/apps/redis/etc# vim /apps/redis/etc/redis.conf
.......
# replicaof <masterip> <masterport>
replicaof 192.168.58.167 6379 #指定master的IP和端口号
......
# masterauth <master-password>
masterauth 123456     #如果密码需要设置
requirepass 123456    #和masterauth保持一致，用于将来从节点提升主后使用
.......
root@redis02:/apps/redis/etc# systemctl restart redis
```

#### 3.1.2.3 Master 和 Slave查看状态

```bash
#在master上查看状态
127.0.0.1:6379> info replication
# Replication
role:master
connected_slaves:2
slave0:ip=192.168.58.168,port=6379,state=online,offset=1190,lag=0
slave1:ip=192.168.58.169,port=6379,state=online,offset=1176,lag=1
master_failover_state:no-failover
master_replid:ff1081713cc8dc502b7dad36139a8aac60ee121b
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:1190
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:1190


#在slave上查看状态
127.0.0.1:6379> get key1   #同步成功后,slave原key信息丢失，获取master复制过来新的值
"v1-master"
127.0.0.1:6379> info replication
# Replication
role:slave
master_host:192.168.58.167
master_port:6379
master_link_status:up
master_last_io_seconds_ago:3  #如果主从复制通信正常，每10秒重新从0计数，此值无法修改，如果无法通信，当计数到60时，master_link_status显示为down
master_sync_in_progress:0  #0表示同步完成，1表示正在同步
slave_read_repl_offset:1260
slave_repl_offset:1260
slave_priority:100
slave_read_only:1
replica_announced:1
connected_slaves:0
master_failover_state:no-failover
master_replid:ff1081713cc8dc502b7dad36139a8aac60ee121b
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:1260
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:1260


# 停止master的redis服务：systemctl stop redis,在slave上可以观察到以下现象
127.0.0.1:6379> info replication
# Replication
role:slave
master_host:192.168.58.167
master_port:6379
master_link_status:down   #显示down，表示无法连接master
master_last_io_seconds_ago:-1
master_sync_in_progress:0
slave_read_repl_offset:1358
slave_repl_offset:1358
master_link_down_since_seconds:26
slave_priority:100
slave_read_only:1
replica_announced:1
connected_slaves:0
master_failover_state:no-failover
master_replid:ff1081713cc8dc502b7dad36139a8aac60ee121b
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:1358
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:1358
```

#### 3.1.2.4 Slave 日志

```bash
root@redis02:/apps/redis/etc# tail -f /apps/redis/log/redis-6379.log
14436:S 06 May 2024 10:48:22.699 * Master replied to PING, replication can continue...
14436:S 06 May 2024 10:48:22.701 * Trying a partial resynchronization (request ff1081713cc8dc502b7dad36139a8aac60ee121b:1359).
14436:S 06 May 2024 10:48:27.157 * Full resync from master: 980d2d7a79f2d01e8e2d3094e73880fba88cde32:0
14436:S 06 May 2024 10:48:27.167 * MASTER <-> REPLICA sync: receiving streamed RDB from master with EOF to disk
14436:S 06 May 2024 10:48:27.168 * Discarding previously cached master state.
14436:S 06 May 2024 10:48:27.168 * MASTER <-> REPLICA sync: Flushing old data
14436:S 06 May 2024 10:48:27.168 * MASTER <-> REPLICA sync: Loading DB in memory
14436:S 06 May 2024 10:48:27.173 * Loading RDB produced by version 7.0.15
14436:S 06 May 2024 10:48:27.173 * RDB age 0 seconds
14436:S 06 May 2024 10:48:27.173 * RDB memory usage when created 0.89 Mb
14436:S 06 May 2024 10:48:27.173 * Done loading RDB, keys loaded: 0, keys expired: 0.
14436:S 06 May 2024 10:48:27.173 * MASTER <-> REPLICA sync: Finished with success

```

#### 3.1.2.5 Master日志

```bash
root@redis01:/apps/redis/etc# tail -f /apps/redis/log/redis-6379.log 
15265:M 06 May 2024 10:48:22.751 * Delay next BGSAVE for diskless SYNC
15265:M 06 May 2024 10:48:27.206 * Starting BGSAVE for SYNC with target: replicas sockets
15265:M 06 May 2024 10:48:27.208 * Background RDB transfer started by pid 15283
15283:C 06 May 2024 10:48:27.216 * Fork CoW for RDB: current 0 MB, peak 0 MB, average 0 MB
15265:M 06 May 2024 10:48:27.216 # Diskless rdb transfer, done reading from pipe, 2 replicas still up.
15265:M 06 May 2024 10:48:27.220 * Background RDB transfer terminated with success
15265:M 06 May 2024 10:48:27.220 * Streamed RDB transfer with replica 192.168.58.169:6379 succeeded (socket). Waiting for REPLCONF ACK from slave to enable streaming
15265:M 06 May 2024 10:48:27.220 * Synchronization with replica 192.168.58.169:6379 succeeded
15265:M 06 May 2024 10:48:27.220 * Streamed RDB transfer with replica 192.168.58.168:6379 succeeded (socket). Waiting for REPLCONF ACK from slave to enable streaming
15265:M 06 May 2024 10:48:27.220 * Synchronization with replica 192.168.58.168:6379 succeeded
```

#### 3.1.6.7 Slave 只读状态

验证Slave节点为只读状态, 不支持写入

```bash
127.0.0.1:6379> set key2 test
(error) READONLY You can't write against a read only replica.
```

### 3.1.3 主从复制故障恢复

#### 3.1.3.1 主从复制故障恢复过程介绍

##### 3.1.3.1.1 Slave 节点故障和恢复

当slave节点故障时，将Redis Client指向另一个slave节点即可，并及时修复故障从节点

![image-20240506185252930](images\image-20240506185252930.png)





##### 3.1.3.1.2 Master 节点故障和恢复

当master节点故障时，需要提升slave为新的master

![image-20240506185359490](images\image-20240506185359490.png)



![image-20240506185413787](images\image-20240506185413787.png)



master故障后，当前还只能手动提升一个slave为新master，不能自动切换。

之后将其它的slave节点重新指定新的master为master节点

**Master的切换会导致master_replid发生变化，slave之前的master_replid就和当前master不一致从而 会引发所有 slave的全量同步。**

#### 3.1.3.2 主从复制故障恢复实现

假设当前主节点192.168.58.167故障，提升192.68.58.168为新的master

```bash
#查看当前192.68.58.168节点的状态为slave,master指向192.168.58.167
127.0.0.1:6379> info replication
# Replication
role:slave
master_host:192.168.58.167
master_port:6379
master_link_status:up
master_last_io_seconds_ago:0
master_sync_in_progress:0
slave_read_repl_offset:798
slave_repl_offset:798
slave_priority:100
slave_read_only:1
replica_announced:1
connected_slaves:0
master_failover_state:no-failover
master_replid:980d2d7a79f2d01e8e2d3094e73880fba88cde32
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:798
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:798
```

停止slave同步并提升为新的master

```bash
#将当前 slave 节点提升为 master 角色
127.0.0.1:6379> REPLICAOF NO ONE   #旧版使用SLAVEOF no one
OK
27.0.0.1:6379> info replication
# Replication
role:master
connected_slaves:0
master_failover_state:no-failover
master_replid:ba4bf4bca2a32e2fa49cf7da871b2fbef8699ab1
master_replid2:980d2d7a79f2d01e8e2d3094e73880fba88cde32
master_repl_offset:896
second_repl_offset:897
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:896
```

测试能否写入数据：

```bash
127.0.0.1:6379> set keytest1 vtest1
OK
```

修改所有slave指向新的master节点

```bash
#修改192.168.58.169节点指向新的master节点192.168.58.168
127.0.0.1:6379> replicaof 192.168.58.168 6379

# 查看log
root@redis03:/apps/redis/etc# tail -f /apps/redis/log/redis-6379.log
77238:S 06 May 2024 11:02:08.397 * Connecting to MASTER 192.168.58.168:6379
77238:S 06 May 2024 11:02:08.397 * MASTER <-> REPLICA sync started
77238:S 06 May 2024 11:02:08.397 * REPLICAOF 192.168.58.168:6379 enabled (user request from 'id=5 addr=127.0.0.1:35240 laddr=127.0.0.1:6379 fd=8 name= age=21 idle=0 flags=N db=0 sub=0 psub=0 ssub=0 multi=-1 qbuf=50 qbuf-free=20424 argv-mem=27 multi-mem=0 rbs=1024 rbp=0 obl=0 oll=0 omem=0 tot-mem=22323 events=r cmd=replicaof user=default redir=-1 resp=2')
77238:S 06 May 2024 11:02:08.398 * Non blocking connect for SYNC fired the event.
77238:S 06 May 2024 11:02:08.398 * Master replied to PING, replication can continue...
77238:S 06 May 2024 11:02:08.399 * Trying a partial resynchronization (request 980d2d7a79f2d01e8e2d3094e73880fba88cde32:1149).
77238:S 06 May 2024 11:02:13.973 * Full resync from master: ba4bf4bca2a32e2fa49cf7da871b2fbef8699ab1:896
77238:S 06 May 2024 11:02:13.976 * MASTER <-> REPLICA sync: receiving streamed RDB from master with EOF to disk
77238:S 06 May 2024 11:02:13.976 * Discarding previously cached master state.
77238:S 06 May 2024 11:02:13.976 * MASTER <-> REPLICA sync: Flushing old data
77238:S 06 May 2024 11:02:13.977 * MASTER <-> REPLICA sync: Loading DB in memory
```

在新master可看到slave

```bash
#在新master节点192.168.58.168上查看状态
127.0.0.1:6379> INFO replication
# Replication
role:master
connected_slaves:1
slave0:ip=192.168.58.169,port=6379,state=online,offset=1078,lag=0
master_failover_state:no-failover
master_replid:ba4bf4bca2a32e2fa49cf7da871b2fbef8699ab1
master_replid2:980d2d7a79f2d01e8e2d3094e73880fba88cde32
master_repl_offset:1078
second_repl_offset:897
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:1078
```

### 3.1.5 主从复制优化

#### 3.1.5.1 主从复制过程

Redis主从复制分为全量同步和增量同步

Redis的主从同步是非阻塞的，即同步过程不会影响主服务器的正常访问

注意：主节点重启会导致全量同步，从节点重启只会导致增量同步

```shell
从redis 2.8版本以前，并不支持部分同步，当主从服务器之间的连接断掉之后，master服务器和slave服
务器之间都是进行全量数据同步，从redis 2.8开始，即使主从连接中途断掉，也不需要进行全量同步，因为
从这个版本开始引入了部分同步。
```

##### 3.1.5.1.1 全量复制过程 Full resync

```bash
4.0之前版本的复制：run_id和复制偏移量来判断进行全量复制还是部分复制
4.0之后版本的复制：根据master_replid和复制偏移量来判断进行全量复制还是部分复制主从关系建立后master_replid，保存的是当前主节点的master_replidmaster_replid2保存的是上一个主节点的master_replid
```

![image-20240506201606004](images\image-20240506201606004.png)

- 主从节点建立连接，验证身份后，从节点向主节点发送psync命令
- 主节点向从节点发送FULLRESYNC命令,包括master_replid(runID)和offset
- 从节点保存主节点信息
- 主节点执行BGSAVE保存RDB文件，同时记录新的记录到BUFFER中
- 主节点发送RDB文件给从节点
- 主节点将新收到BUFFER中的记录发送给从节点
- 从节点删除本机的旧数据
- 从节点加载RDB
- 从节点同步主节点BUFFER信息

**全量复制发生在下面情况**

- 从节点首次连接主节点(无master_replid/runid)
- 从节点的复制偏移量不在复制积压缓冲区内
- 从节点无法连接主节点超过一定的时间

范例：查看RUNID

```bash
#Redis 重启服务后，RUNID会发生变化
127.0.0.1:6379> info server
# Server
redis_version:7.0.5
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:77bd58d092d1d003
redis_mode:standalone
os:Linux 5.4.0-124-generic x86_64
arch_bits:64
monotonic_clock:POSIX clock_gettime
multiplexing_api:epoll
atomicvar_api:c11-builtin
gcc_version:9.4.0
process_id:16407
process_supervised:systemd
run_id:9e954950c255644ef291f6be0c579ae893c16aad
tcp_port:6379
server_time_usec:1667276559043301
uptime_in_seconds:3463
uptime_in_days:0
hz:10
configured_hz:10
lru_clock:6332175
executable:/apps/redis/bin/redis-server
config_file:/apps/redis/etc/redis.conf
io_threads_active:0
```

##### 3.1.5.1.2 增量复制过程 partial resynchronization

![image-20240506202155306](images\image-20240506202155306.png)

在主从复制首次完成全量同步之后再次需要同步时，从服务器只要发送当前的offset位置(类似于MySQL的 binlog的位置)给主服务器，然后主服务器根据相应的位置将之后的数据(包括写在缓冲区的积压数据)发 送给从服务器,再次将其保存到从节点内存即可。

即首次全量复制,之后的复制基本增量复制实现

##### 3.1.5.1.3 主从同步完整过程

主从同步完整过程如下：

- slave发起连接master，验证通过后，发送psync命令
- master接收到PSYNC命令后，执行BGSAVE命令将全部数据保存至RDB文件中,并将后续发生的写 操作记录至buffer中
- master向所有slave发送RDB文件
- master向所有slave发送后续记录在buffer中写操作
- slave收到快照文件后丢弃所有旧数据
- slave加载收到的RDB到内存
- slave 执行来自master接收到的buffer写操作
- 当slave完成全量复制后,后续master只会先发送slave_repl_offset信息
- 以后slave比较自身和master的差异,只会进行增量复制的数据即可

![image-20240506202628152](images\image-20240506202628152.png)

复制缓冲区(环形队列)配置参数：

```bash
#master的写入数据缓冲区，用于记录自上一次同步后到下一次同步过程中间的写入命令，计算公式：replbacklog-size= 允许从节点最大中断时长 * 主实例offset每秒写入量，比如:master每秒最大写入64mb，最大允许60秒，那么就要设置为64mb*60秒=3840MB(3.8G),建议此值是设置的足够大，默认值为1M
repl-backlog-size 1mb 

#如果一段时间后没有slave连接到master，则backlog size的内存将会被释放。如果值为0则表示永远不释放这部份内存。 
repl-backlog-ttl   3600
```

![image-20240506202812281](images\image-20240506202812281.png)

##### 3.1.5.1.4 避免全量复制

- 第一次全量复制不可避免,后续的全量复制可以利用小主节点(内存小),业务低峰时进行全量
- 节点RUN_ID不匹配:主节点重启会导致RUN_ID变化,可能会触发全量复制,可以利用config命令动态 修改配置，故障转移例如哨兵或集群选举新的主节点也不会全量复制,而从节点重启动,不会导致全 量复制,只会增量复制。
- 复制积压缓冲区不足: 当主节点生成的新数据大于缓冲区大小,从节点恢复和主节点连接后,会导致全 量复制.解决方法将repl-backlog-size 调大

##### 3.1.5.1.5 避免复制风暴

- 单主节点复制风暴

  当主节点重启，多从节点复制

   解决方法:更换复制拓扑

  ![image-20240506203113708](images\image-20240506203113708.png)

- 单机器多实例复制风暴

  机器宕机后，大量全量复制 

  解决方法:主节点分散多机器

![image-20240506203212430](images\image-20240506203212430.png)

#### 3.1.5.2 主从同步优化配置

Redis在2.8版本之前没有提供增量部分复制的功能，当网络闪断或者slave Redis重启之后会导致主从之 间的全量同步，即从2.8版本开始增加了部分复制的功能。

**性能相关配置**

```bash
repl-diskless-sync no # 是否使用无盘方式进行同步RDB文件，默认为no(编译安装默认为yes)，no表示不使用无盘，需要将RDB文件保存到磁盘后再发送给slave，yes表示使用无盘，即RDB文件不需要保存至本地磁盘，而且直接通过网络发送给slave

repl-diskless-sync-delay 5 #无盘时复制的服务器等待的延迟时间

repl-ping-slave-period 10 #slave向master发送ping指令的时间间隔，默认为10s

repl-timeout 60 #指定ping连接超时时间,超过此值无法连接,master_link_status显示为down状态,并记录错误日志


repl-disable-tcp-nodelay no #是否启用TCP_NODELAY
#设置成yes，则redis会合并多个小的TCP包成一个大包再发送,此方式可以节省带宽，但会造成同步延迟时长的增加，导致master与slave数据短期内不一致
#设置成no，则master会立即同步数据


repl-backlog-size 1mb #master的写入数据缓冲区，用于记录自上一次同步后到下一次同步前期间的写入命令，计算公式：repl-backlog-size = 允许slave最大中断时长 * master节点offset每秒写入量，如:master每秒最大写入量为32MB，最长允许中断60秒，就要至少设置为32*60=1920MB,建议此值是设置的足够大,如果此值太小,会造成全量复制


repl-backlog-ttl 3600 #指定多长时间后如果没有slave连接到master，则backlog的内存数据将会过期。如果值为0表示永远不过期。


slave-priority 100 #slave参与选举新的master的优先级，此整数值越小则优先级越高。当master故障时将会按照优先级来选择slave端进行选举新的master，如果值设置为0，则表示该slave节点永远不会被选为master节点


min-replicas-to-write 1 #指定master的可用slave不能少于个数，如果少于此值,master将无法执行写操作,默认为0,生产建议设为1,


min-slaves-max-lag 20 #指定至少有min-replicas-to-write数量的slave延迟时间都大于此秒数时，master将不能执行写操作,默认为10s
```

### 3.1.6 常见主从复制故障

#### 3.1.6.1 主从硬件和软件配置不一致

主从节点的maxmemory不一致,主节点内存大于从节点内存,主从复制可能丢失数据 

rename-command 命令不一致,如在主节点启用flushdb,从节点禁用此命令,结果在master节点执行 flushdb后,导致slave节点不同步

#### 3.1.6.2 Master 节点密码错误

如果slave节点配置的master密码错误，导致验证不通过,自然将无法建立主从同步关系。

#### 3.1.6.3 Redis 版本不一致

不同的redis 版本之间尤其是大版本间可能会存在兼容性问题，如：Redis 3,4,5,6之间 因此主从复制的所有节点应该使用相同的版本

#### 3.1.6.4 安全模式下无法远程连接

如果开启了安全模式，并且没有设置bind地址和密码,会导致无法远程连接

## 3.2 Redis 哨兵 Sentinel

### 3.2.1：Redis集群介绍

主从架构和MYSQL的主从复制一样，无法实现master和slave角色的自动切换，即当master出现故障时，不能实现自动的将一个slave节点提升为新的master节点，即主从复制无法实现自动的故障转移功能，如果想实现转移，则需要手动修改配置，才能将slave服务器提升为新的master节点，此外只有一个主节点支持写操作，所以业务量很大时会导致Redis服务性能达到瓶颈。

需要解决主从复制以下存在的问题：

- master和slave角色的自动切换，且不影响业务
- 提升Redis服务整体性能，支持更高并发访问

### 3.2.2：哨兵Sentinel工作原理

哨兵Sentinel从Redis2.6版本开始引用，Redis 2.8版本之后稳定可用。生产环境如果要使用此功能建议使用Redis的2.8版本以上版本。

#### 3.2.2.1：**Sentinel** **架构和故障转移机制**

![image-20240509093152724](images\image-20240509093152724.png)

**Sentinel 架构**

![image-20240509093229407](images\image-20240509093229407.png)

**Sentinel 故障转移**

![image-20240509093335598](images\image-20240509093335598.png)

专门的Sentinel服务进程是用于监控redis集群中master工作的状态，当master主服务器发生故障的时候，可以实现master和slave角色的自动切换，从而实现系统的高可用性。

Sentinel是一个分布式系统，即需要在多个节点上各自同时运行一个sentinel进程，Sentienl 进程通过流 言协议(gossip protocols)来接收关于Master是否下线状态，并使用投票协议(Agreement Protocols)来 决定是否执行自动故障转移,并选择合适的Slave作为新的Master。

每个Sentinel进程会向其它Sentinel、Master、Slave定时发送消息，来确认对方是否存活，如果发现某 个节点在指定配置时间内未得到响应，则会认为此节点已离线，即为主观宕机Subjective Down，简称 为 SDOWN

如果哨兵集群中的多数Sentinel进程认为Master存在SDOWN，共同利用 is-master-down-by-addr 命令 互相通知后，则认为客观宕机Objectively Down， 简称 ODOWN

接下来利用投票算法，从所有slave节点中，选一台合适的slave将之提升为新Master节点，然后自动修改其他slave相关配置，指向新的master节点，最终实现故障转移failover

Redis Sentinel中的Sentinel节点个数应该为大于等于3且最好为奇数

客户端初始化连接的是Sentinel节点集合，不再是具体的Redis节点，即 Sentinel只是配置中心不是代 理。

Redis Sentinel 节点与普通 Redis 没有区别,要实现读写分离依赖于客户端程序

Sentinel 机制类似于MySQL中的MHA功能,只解决master和slave角色的自动故障转移问题，但单个  Master 的性能瓶颈问题并没有解决

Redis 3.0 之前版本中,生产环境一般使用哨兵模式较多,Redis 3.0后推出Redis cluster功能,可以支持更大 规模的高并发环境

#### 3.2.2.2：Sentinel中的三个定时任务

- 每10s每个sentinel对master和slave执行info

  发现slave节点

  确认主从关系

- 每2s每个sentinel通过master节点的channel交换信息(pub/sub)

  通过sentinel_:hello频道交互

  交互对节点的看法和自身信息

- 每1s每个sentinel对其他sentinel和redis执行ping

### 3.2.3: 实现哨兵架构

以下案例实现一主两从的基于哨兵的高可用Redis架构

![image-20240509094704035](images\image-20240509094704035.png)

#### 3.2.3.1：哨兵需要先实现主从复制

哨兵的前提是已经实现了Redis的主从复制

注意：master的配置文件中masterauth和slave的配置文件masterauth必须相同

**所有主从节点的 redis.conf 中关健配置**

```bash
# 在所有主从节点执行（前提redis已经安装，参照主从复制章节）
root@redis01:~# cat /apps/redis/etc/redis.conf |grep -E "bind|masterauth|requirepass" | grep -Ev "^#|^$"
bind 0.0.0.0
masterauth 123456
requirepass 123456

# 所有从节点配置
root@redis02:~# cat /apps/redis/etc/redis.conf |grep "replicaof"
replicaof 192.168.58.167 6379

#在所有主从节点执行
root@redis01:~# systemctl enable --now redis
```

**master服务器状态**

```bash
root@redis01:~# redis-cli -a 123456
127.0.0.1:6379> info replication
# Replication
role:master
connected_slaves:2
slave0:ip=192.168.58.169,port=6379,state=online,offset=350,lag=0
slave1:ip=192.168.58.168,port=6379,state=online,offset=350,lag=0
master_failover_state:no-failover
master_replid:802932a6f3db1eda7e0c160946837579888614f7
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:350
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:350
```

**slave1服务器状态**

```bash
root@redis02:~# redis-cli -a 123456 info replication
# Replication
role:slave
master_host:192.168.58.167
master_port:6379
master_link_status:up
master_last_io_seconds_ago:9
master_sync_in_progress:0
slave_read_repl_offset:420
slave_repl_offset:420
slave_priority:100
slave_read_only:1
replica_announced:1
connected_slaves:0
master_failover_state:no-failover
master_replid:802932a6f3db1eda7e0c160946837579888614f7
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:420
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:420
```

**slave2服务器状态**

```bash
root@redis03:~# redis-cli -a 123456 info replication
# Replication
role:slave
master_host:192.168.58.167
master_port:6379
master_link_status:up
master_last_io_seconds_ago:7
master_sync_in_progress:0
slave_read_repl_offset:476
slave_repl_offset:476
slave_priority:100
slave_read_only:1
replica_announced:1
connected_slaves:0
master_failover_state:no-failover
master_replid:802932a6f3db1eda7e0c160946837579888614f7
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:476
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:476
```

#### 3.2.3.2: 编辑哨兵模式

**sentinel配置**

Sentinel实际上是一个特殊的redis服务器，有些redis指令支持，但很多指令并不支持，默认监听在26379/tcp端口

哨兵服务可以和Redis服务器分开部署在不同的主机，但为了节约成本一般会部署在一起

所有redis节点使用相同的以下示例的配置文件

```bash
#如果是编译安装，在源码目录有sentinel.conf，复制到安装目录即可.
root@redis01:~# cp /usr/local/src/redis-7.0.15/sentinel.conf /apps/redis/etc/sentinel.conf
chown redis.redis /apps/redis/etc/sentinel.conf 

# 编译安装修改配置文件
root@redis01:~# grep -Ev "#|^$" /apps/redis/etc/sentinel.conf
protected-mode no
port 26379
daemonize yes
pidfile /apps/redis/run/redis-sentinel.pid
logfile /apps/redis/log/redis-sentinel.log
dir /tmp  #工作目录

sentinel monitor mymaster 192.168.58.167 6379 2
#mymaster是集群的名称，此行指定当前mymaster集群中master服务器的地址和端口
#2为法定人数限制(quorum)，即有几个sentinel认为master down了就进行故障转移，一般此值是所有sentinel节点(一般总数是>=3的 奇数,如:3,5,7等)的一半以上的整数值，比如，总数是3，即3/2=1.5，取整为2,是master的ODOWN客观下线的依据

sentinel auth-pass mymaster 123456
#mymaster集群中master的密码，注意此行要在上面行的下面

sentinel down-after-milliseconds mymaster 3000
#判断mymaster集群中所有节点的主观下线(SDOWN)的时间，单位：毫秒，建议3000

acllog-max-len 128

sentinel parallel-syncs mymaster 1
#发生故障转移后，可以同时向新master同步数据的slave的数量，数字越小总同步时间越长，但可以减轻新master的负载压力

sentinel failover-timeout mymaster 180000
#所有slaves指向新的master所需的超时时间，单位：毫秒

sentinel deny-scripts-reconfig yes #禁止修改脚本
SENTINEL resolve-hostnames no
SENTINEL announce-hostnames no
SENTINEL master-reboot-down-after-period mymaster 0
```

**三个哨兵服务器的配置都如下**

```bash
root@redis01:~# grep -Ev "#|^$" /apps/redis/etc/sentinel.conf
protected-mode no
port 26379
daemonize yes
pidfile /apps/redis/run/redis-sentinel.pid
logfile /apps/redis/log/redis-sentinel.log
dir /tmp
sentinel monitor mymaster 192.168.58.167 6379 2
sentinel auth-pass mymaster 123456
sentinel down-after-milliseconds mymaster 3000
acllog-max-len 128
sentinel parallel-syncs mymaster 1
sentinel failover-timeout mymaster 180000
sentinel deny-scripts-reconfig yes
SENTINEL resolve-hostnames no
SENTINEL announce-hostnames no
SENTINEL master-reboot-down-after-period mymaster 0


root@redis01:~# scp  /apps/redis/etc/sentinel.conf 192.168.58.168:/apps/redis/etc/sentinel.conf
root@redis01:~# scp  /apps/redis/etc/sentinel.conf 192.168.58.169:/apps/redis/etc/sentinel.conf
```

#### 3.2.3.3:启动哨兵服务

如果是编译安装,在所有哨兵服务器执行下面操作启动哨兵

```bash
#如果是编译安装，可以在所有节点生成新的service文件
root@redis01:~# cat  /lib/systemd/system/redis-sentinel.service 
[Unit]
Description=Redis Sentinel
After=network.target

[Service]
ExecStart=/apps/redis/bin/redis-sentinel /apps/redis/etc/sentinel.conf --supervised systemd
ExecStop=/bin/kill -s QUIT $MAINPID
User=redis
Group=redis
RuntimeDirectory=redis
RuntimeDirectoryMode=0755

[Install]
WantedBy=multi-user.target
#注意所有节点的目录权限,否则无法启动服务
[root@redis-master ~]#chown -R redis.redis /apps/redis/
[root@redis-master ~]#systemctl daemon-reload
[root@redis-master ~]#systemctl enable --now redis-sentinel.service
```

#### 3.2.3.4: 验证哨兵服务

##### 3.2.3.4.1 查看哨兵服务端口状态

```bash
root@redis01:~# ss -ntl
State                       Recv-Q                      Send-Q                                           Local Address:Port                                            Peer Address:Port                     Process                     
LISTEN                      0                           4096                                             127.0.0.53%lo:53                                                   0.0.0.0:*                                                    
LISTEN                      0                           128                                                    0.0.0.0:22                                                   0.0.0.0:*                                                    
LISTEN                      0                           128                                                  127.0.0.1:6010                                                 0.0.0.0:*                                                    
LISTEN                      0                           128                                                  127.0.0.1:6011                                                 0.0.0.0:*                                                    
LISTEN                      0                           128                                                  127.0.0.1:6012                                                 0.0.0.0:*                                                    
LISTEN                      0                           128                                                  127.0.0.1:6013                                                 0.0.0.0:*                                                    
LISTEN                      0                           511                                                    0.0.0.0:26379                                                0.0.0.0:*                                                    
LISTEN                      0                           511                                                    0.0.0.0:6379                                                 0.0.0.0:*                                                    
LISTEN                      0                           128                                                       [::]:22                                                      [::]:*                                                    
LISTEN                      0                           128                                                      [::1]:6010                                                    [::]:*                                                    
LISTEN                      0                           128                                                      [::1]:6011                                                    [::]:*                                                    
LISTEN                      0                           128                                                      [::1]:6012                                                    [::]:*                                                    
LISTEN                      0                           128                                                      [::1]:6013                                                    [::]:*                                                    
LISTEN                      0                           511                                                       [::]:26379                                                   [::]:*     
```

##### 3.2.3.4.2 查看哨兵日志

**master哨兵日志**

```bash
root@redis01:/apps/redis/bin# tail -f /apps/redis/log/redis-sentinel.log 
7474:X 09 May 2024 06:54:12.136 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
7474:X 09 May 2024 06:54:12.136 # Redis version=7.0.15, bits=64, commit=00000000, modified=0, pid=7474, just started
7474:X 09 May 2024 06:54:12.136 # Configuration loaded
7474:X 09 May 2024 06:54:12.136 * Increased maximum number of open files to 10032 (it was originally set to 1024).
7474:X 09 May 2024 06:54:12.136 * monotonic clock: POSIX clock_gettime
7474:X 09 May 2024 06:54:12.137 * Running mode=sentinel, port=26379.
7474:X 09 May 2024 06:54:12.137 # Sentinel ID is 2878c09e07177743ce68bfae31a42262d2c93a98
7474:X 09 May 2024 06:54:12.137 # +monitor master mymaster 192.168.58.167 6379 quorum 2
7474:X 09 May 2024 06:54:12.137 # systemd supervision error: NOTIFY_SOCKET not found!
7474:X 09 May 2024 06:54:12.137 # systemd supervision error: NOTIFY_SOCKET not found!
7474:X 09 May 2024 06:57:53.441 * +sentinel sentinel 9e2e4f9b828fab4680f356aee227ad5327ba473c 192.168.58.168 26379 @ mymaster 192.168.58.167 6379
7474:X 09 May 2024 06:57:53.466 * Sentinel new configuration saved on disk
7474:X 09 May 2024 06:58:00.355 * +sentinel sentinel 8025d1f8030c58e908ea59256b95be4f7eeda367 192.168.58.169 26379 @ mymaster 192.168.58.167 6379
7474:X 09 May 2024 06:58:00.362 * Sentinel new configuration saved on disk
```

**slave哨兵日志**

```bash
root@redis02:~# tail /apps/redis/log/redis-sentinel.log 
5546:X 09 May 2024 06:57:51.419 # Sentinel ID is 9e2e4f9b828fab4680f356aee227ad5327ba473c
5546:X 09 May 2024 06:57:51.419 # +monitor master mymaster 192.168.58.167 6379 quorum 2
5546:X 09 May 2024 06:57:51.420 * +slave slave 192.168.58.168:6379 192.168.58.168 6379 @ mymaster 192.168.58.167 6379
5546:X 09 May 2024 06:57:51.421 * Sentinel new configuration saved on disk
5546:X 09 May 2024 06:57:51.421 * +slave slave 192.168.58.169:6379 192.168.58.169 6379 @ mymaster 192.168.58.167 6379
5546:X 09 May 2024 06:57:51.422 * Sentinel new configuration saved on disk
5546:X 09 May 2024 06:57:52.237 * +sentinel sentinel 2878c09e07177743ce68bfae31a42262d2c93a98 192.168.58.167 26379 @ mymaster 192.168.58.167 6379
5546:X 09 May 2024 06:57:52.241 * Sentinel new configuration saved on disk
5546:X 09 May 2024 06:58:00.352 * +sentinel sentinel 8025d1f8030c58e908ea59256b95be4f7eeda367 192.168.58.169 26379 @ mymaster 192.168.58.167 6379
5546:X 09 May 2024 06:58:00.360 * Sentinel new configuration saved on disk
```

##### 3.2.3.4.3 当前sentinel状态

在sentinel状态中尤其是最后一行，涉及到masterip是多少，有几个slave，有几个sentinels，必须是符合全部服务器数量

```bash
root@redis01:~# redis-cli  -p  26379
127.0.0.1:26379> info Sentinel
# Sentinel
sentinel_masters:1
sentinel_tilt:0
sentinel_tilt_since_seconds:-1
sentinel_running_scripts:0
sentinel_scripts_queue_length:0
sentinel_simulate_failure_flags:0
master0:name=mymaster,status=ok,address=192.168.58.167:6379,slaves=2,sentinels=3 #两个slave,三个sentinel服务器,如果sentinels值不符合,检查myid可能冲突
```

##### 3.2.3.4.4: sentinel配置文件会自动生成集群节点信息

一旦，哨兵服务启动完成，`sentinel.conf`配置文件会自动生成一些信息。

```bash
root@redis01:~# cat /apps/redis/etc/sentinel.conf
...
# Generated by CONFIG REWRITE
supervised systemd
latency-tracking-info-percentiles 50 99 99.9
user default on nopass sanitize-payload ~* &* +@all
sentinel myid 2878c09e07177743ce68bfae31a42262d2c93a98
sentinel config-epoch mymaster 0
sentinel leader-epoch mymaster 0
sentinel current-epoch 0

sentinel known-replica mymaster 192.168.58.168 6379

sentinel known-replica mymaster 192.168.58.169 6379

sentinel known-sentinel mymaster 192.168.58.168 26379 9e2e4f9b828fab4680f356aee227ad5327ba473c

sentinel known-sentinel mymaster 192.168.58.169 26379 8025d1f8030c58e908ea59256b95be4f7eeda367



root@redis02:~# cat /apps/redis/etc/sentinel.conf
...
# Generated by CONFIG REWRITE
latency-tracking-info-percentiles 50 99 99.9
user default on nopass ~* &* +@all
sentinel myid 9e2e4f9b828fab4680f356aee227ad5327ba473c
sentinel config-epoch mymaster 0
sentinel leader-epoch mymaster 0
sentinel current-epoch 0

sentinel known-replica mymaster 192.168.58.168 6379

sentinel known-replica mymaster 192.168.58.169 6379

sentinel known-sentinel mymaster 192.168.58.169 26379 8025d1f8030c58e908ea59256b95be4f7eeda367

sentinel known-sentinel mymaster 192.168.58.167 26379 2878c09e07177743ce68bfae31a42262d2c93a98



root@redis03:~# cat /apps/redis/etc/sentinel.conf
...
# Generated by CONFIG REWRITE
latency-tracking-info-percentiles 50 99 99.9
user default on nopass ~* &* +@all
sentinel myid 8025d1f8030c58e908ea59256b95be4f7eeda367
sentinel config-epoch mymaster 0
sentinel leader-epoch mymaster 0
sentinel current-epoch 0

sentinel known-replica mymaster 192.168.58.169 6379

sentinel known-replica mymaster 192.168.58.168 6379

sentinel known-sentinel mymaster 192.168.58.167 26379 2878c09e07177743ce68bfae31a42262d2c93a98

sentinel known-sentinel mymaster 192.168.58.168 26379 9e2e4f9b828fab4680f356aee227ad5327ba473c
```

#### 3.2.3.5 停止 Master 节点实现故障转移

##### 3.2.3.5.1:  停止 Master 节点

```bash
root@redis01:~# killall redis-server
```

查看各节点上哨兵信息：

```bash
root@redis01:~# redis-cli -p 26379
127.0.0.1:26379> info sentinel
# Sentinel
sentinel_masters:1
sentinel_tilt:0
sentinel_tilt_since_seconds:-1
sentinel_running_scripts:0
sentinel_scripts_queue_length:0
sentinel_simulate_failure_flags:0
master0:name=mymaster,status=ok,address=192.168.58.168:6379,slaves=2,sentinels=3 #可以发现master已经故障转移到redis02这台节点
```

故障转移时sentinel的信息：

```bash
root@redis01:/apps/redis/bin# tail -f /apps/redis/log/redis-sentinel.log
7474:X 09 May 2024 07:20:04.963 * Sentinel new configuration saved on disk
7474:X 09 May 2024 07:20:04.963 # +vote-for-leader 8025d1f8030c58e908ea59256b95be4f7eeda367 1
7474:X 09 May 2024 07:20:05.023 # +odown master mymaster 192.168.58.167 6379 #quorum 3/2
7474:X 09 May 2024 07:20:05.023 # Next failover delay: I will not start a failover before Thu May  9 07:26:05 2024
7474:X 09 May 2024 07:20:05.431 # +config-update-from sentinel 8025d1f8030c58e908ea59256b95be4f7eeda367 192.168.58.169 26379 @ mymaster 192.168.58.167 6379
7474:X 09 May 2024 07:20:05.433 # +switch-master mymaster 192.168.58.167 6379 192.168.58.168 6379
7474:X 09 May 2024 07:20:05.433 * +slave slave 192.168.58.169:6379 192.168.58.169 6379 @ mymaster 192.168.58.168 6379
7474:X 09 May 2024 07:20:05.433 * +slave slave 192.168.58.167:6379 192.168.58.167 6379 @ mymaster 192.168.58.168 6379
7474:X 09 May 2024 07:20:05.435 * Sentinel new configuration saved on disk
7474:X 09 May 2024 07:20:08.501 # +sdown slave 192.168.58.167:6379 192.168.58.167 6379 @ mymaster 192.168.58.168 6379
```

##### 3.2.3.5.2: 验证故障转移

故障转移后redis.conf中的replicaof行的master IP会被修改

```bash
root@redis03:~# cat /apps/redis/etc/redis.conf |grep "replicaof"
# Master-Replica replication. Use replicaof to make a Redis instance a copy of
replicaof 192.168.58.168 6379
```

哨兵配置文件的sentinel monitor IP 同样也会被修改

```bash
root@redis02:~# grep "^[a-Z]" /apps/redis/etc/sentinel.conf
protected-mode no
port 26379
daemonize yes
pidfile "/apps/redis/run/redis-sentinel.pid"
logfile "/apps/redis/log/redis-sentinel.log"
dir "/tmp"
sentinel monitor mymaster 192.168.58.168 6379 2 #自动修改此行，指向新的master ip
sentinel auth-pass mymaster 123456
sentinel down-after-milliseconds mymaster 3000
acllog-max-len 128
sentinel deny-scripts-reconfig yes
sentinel resolve-hostnames no
sentinel announce-hostnames no
latency-tracking-info-percentiles 50 99 99.9
user default on nopass ~* &* +@all
sentinel myid 9e2e4f9b828fab4680f356aee227ad5327ba473c
sentinel config-epoch mymaster 1
sentinel leader-epoch mymaster 1
sentinel current-epoch 1
sentinel known-replica mymaster 192.168.58.167 6379
sentinel known-replica mymaster 192.168.58.169 6379
sentinel known-sentinel mymaster 192.168.58.169 26379 8025d1f8030c58e908ea59256b95be4f7eeda367
sentinel known-sentinel mymaster 192.168.58.167 26379 2878c09e07177743ce68bfae31a42262d2c93a98


root@redis03:~# grep "^[a-Z]" /apps/redis/etc/sentinel.conf
protected-mode no
port 26379
daemonize yes
pidfile "/apps/redis/run/redis-sentinel.pid"
logfile "/apps/redis/log/redis-sentinel.log"
dir "/tmp"
sentinel monitor mymaster 192.168.58.168 6379 2   #自动修改此行，指向新的master ip
sentinel auth-pass mymaster 123456
sentinel down-after-milliseconds mymaster 3000
acllog-max-len 128
sentinel deny-scripts-reconfig yes
sentinel resolve-hostnames no
sentinel announce-hostnames no
latency-tracking-info-percentiles 50 99 99.9
user default on nopass ~* &* +@all
sentinel myid 8025d1f8030c58e908ea59256b95be4f7eeda367
sentinel config-epoch mymaster 1
sentinel leader-epoch mymaster 1
sentinel current-epoch 1
sentinel known-replica mymaster 192.168.58.167 6379
sentinel known-replica mymaster 192.168.58.169 6379
sentinel known-sentinel mymaster 192.168.58.167 26379 2878c09e07177743ce68bfae31a42262d2c93a98
sentinel known-sentinel mymaster 192.168.58.168 26379 9e2e4f9b828fab4680f356aee227ad5327ba473c
```

##### 3.2.3.5.3 验证 Redis 各节点状态

**新master（192.168.58.168）状态**

```bash
root@redis02:~# redis-cli -a 123456
Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
127.0.0.1:6379> info replication
# Replication
role:master    #提升为master
connected_slaves:1
slave0:ip=192.168.58.169,port=6379,state=online,offset=448982,lag=1
master_failover_state:no-failover
master_replid:c3611d898f00c2eb0f3c224baa0b4cab1b3d661c
master_replid2:47c3c982cc6cdfc39ebbd7699e2b535dcc1d9c69
master_repl_offset:449268
second_repl_offset:297673
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:449268
```

**另一个slave(192.168.58.169)指向新的master**

```bash
root@redis03:~# redis-cli -a 123456
127.0.0.1:6379> info replication
# Replication
role:slave
master_host:192.168.58.168   #指向新的master
master_port:6379
master_link_status:up
master_last_io_seconds_ago:0
master_sync_in_progress:0
slave_read_repl_offset:482940
slave_repl_offset:482940
slave_priority:100
slave_read_only:1
replica_announced:1
connected_slaves:0
master_failover_state:no-failover
master_replid:c3611d898f00c2eb0f3c224baa0b4cab1b3d661c
master_replid2:47c3c982cc6cdfc39ebbd7699e2b535dcc1d9c69
master_repl_offset:482940
second_repl_offset:297673
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:482940
```

#### 3.2.3.6: 原master重新加入Redis集群

```bash
root@redis01:~# systemctl start redis
root@redis01:~# ss -ntl | grep -w 6379
LISTEN  0        511              0.0.0.0:6379           0.0.0.0:*

root@redis01:~# grep ^replicaof /apps/redis/etc/redis.conf 
# sentinel会自动修改下面行指向新的master
replicaof 192.168.58.168 6379
```

**在原master上观察状态**

```bash
root@redis01:~# redis-cli -a 123456
127.0.0.1:6379> info replication
# Replication
role:slave  # role变成slave
master_host:192.168.58.168  #指向新的master
master_port:6379
master_link_status:up
master_last_io_seconds_ago:1
master_sync_in_progress:0
slave_read_repl_offset:598262
slave_repl_offset:598262
slave_priority:100
slave_read_only:1
replica_announced:1
connected_slaves:0
master_failover_state:no-failover
master_replid:c3611d898f00c2eb0f3c224baa0b4cab1b3d661c
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:598262
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:546996
repl_backlog_histlen:51267

root@redis01:~# redis-cli -p 26379
127.0.0.1:26379> info sentinel
# Sentinel
sentinel_masters:1
sentinel_tilt:0
sentinel_tilt_since_seconds:-1
sentinel_running_scripts:0
sentinel_scripts_queue_length:0
sentinel_simulate_failure_flags:0
master0:name=mymaster,status=ok,address=192.168.58.168:6379,slaves=2,sentinels=3
```

### 3.2.4 Sentinel 运维

在Sentinel主机手动触发故障切换

```bash
#redis-cli   -p 26379
127.0.0.1:26379> sentinel failover <masterName>
```

范例: 手动故障转移

```bash
root@redis01:~# grep replica-priority /apps/redis/etc/redis.conf 
replica-priority 100 #指定优先级,值越小sentinel会优先将之选为新的master,默为值为100

#或者动态修改
root@redis01:~# redis-cli -a 123456
127.0.0.1:6379> CONFIG GET replica-priority
1) "replica-priority"
2) "100"
127.0.0.1:6379> CONFIG SET replica-priority 99
OK
127.0.0.1:6379> CONFIG GET replica-priority
1) "replica-priority"
2) "99"

root@redis01:~# redis-cli  -p 26379
127.0.0.1:26379> sentinel failover mymaster  #原主节点自动变成从节点
OK
```

### 3.2.5：应用程序连接Sentinel

Redis 官方支持多种开发语言的客户端：https://redis.io/clients

#### 3.2.5.1 客户端连接 Sentinel 工作原理

1、客户端获取Sentinel节点集合，选举出一个Sentinel

![image-20240509155653014](images\image-20240509155653014.png)

2、由这个sentinel通过mastername获取master节点信息，客户端通过sentinel get-master-addr-byname master-name这个api来获取对应主节点信息

![image-20240509155816174](images\image-20240509155816174.png)

3. 客户端发送role指令确认master的信息，验证当前获取的主节点是真正的主节点，这样的目的是为了防止故障转移期间主节点变化

   ![image-20240509160006660](images\image-20240509160006660.png)

4、客户端保持和Sentinel节点集合的联系，即订阅Sentinel节点相关频道，时刻获取关于主节点的相 关信息,获取新的master 信息变化,并自动连接新的master

![image-20240509160039751](images\image-20240509160039751.png)

#### 3.2.5.2 Python 连接 Sentinel 哨兵

```bash
root@redis01:~# apt -y install python3-redis
root@redis01:~# vim sentinel_test.py
#!/usr/bin/python3
import redis
from redis.sentinel import Sentinel

#连接哨兵服务器(主机名也可以用域名)
sentinel = Sentinel([('192.168.58.167', 26379),
                     ('192.168.58.168', 26379),
                     ('192.168.58.169', 26379)
             ],
                    socket_timeout=0.5)

redis_auth_pass='123456'

#mymaster 是运维人员配置哨兵模式的数据库名称，实际名称按照个人部署案例来填写
#获取主服务器地址
master = sentinel.discover_master('mymaster')
print(master)


#获取从服务器地址
slave = sentinel.discover_slaves('mymaster')
print(slave)



#获取主服务器进行写入
master = sentinel.master_for('mymaster', socket_timeout=0.5, password=redis_auth_pass, db=0)
w_ret = master.set('name', 'wanglei')
#输出：True


#获取从服务器进行读取（默认是round-roubin）
slave = sentinel.slave_for('mymaster', socket_timeout=0.5, password=redis_auth_pass, db=0)
r_ret = slave.get('name')
print(r_ret)
#输出：wanglei


#执行
root@redis01:~# python3 sentinel_test.py 
('192.168.58.168', 6379)
[('192.168.58.167', 6379), ('192.168.58.169', 6379)]
b'wanglei'
```

## 3.3 Redis Cluster

![image-20240509160912361](images\image-20240509160912361.png)

### 3.3.1：Redis Cluster介绍

使用哨兵sentinel只能解决Redis高可用问题，实现Redis的自动故障转移，但仍然无法解决Redis Master单节点的性能瓶颈问题

为了解决单机性能的瓶颈，提高Redis服务整体性能，可以收i用分布式集群的解决方案

**早期 Redis 分布式集群部署方案：**

- 客户端分区：由客户端程序自己实现写入分配，高可用管理和故障转移等，对客户端的开发实现较为复杂
- 代理服务：客户端不直接连接Redis，而先连接到代理服务，由代理服务实现响应的读写分配，当前代理服务都是第三方实现。此方案客户端无序实现特殊开发，实现容易，但是代理服务节点仍存有单点 故障和性能瓶颈问题。比如：Twitter开源Twemproxy,豌豆荚开发的 codis

Redis 3.0版本之后推出无中心架构的Redis Cluster，支持多个master节点并行写入和故障的自动转移功能。

### 3.3.2 Redis Cluster 架构

#### 3.3.2.1 Redis Cluster 架构

![image-20240509163117942](images\image-20240509163117942.png)

Redis cluster需要至少3个master节点才能实现,slave节点数量不限，当然一般每个master都至少对应的由一个slave节点

如果有三个主节点采用哈希槽hash slot的方式分配16384个槽位slot

此三个节点分别承担的slot区间可以是以下方式分配

```http
节点M1 0－5460
节点M2 5461－10922
节点M3 10923－16383
```

![image-20240509163701052](images\image-20240509163701052.png)



#### 3.3.2.2: Redis Cluster的工作原理

![image-20240509163818425](images\image-20240509163818425.png)

##### 3.3.2.2.1：数据分区

如果是单机存储的话，直接将数据存放在单机redis就行。但是如果是集群存储，就需要考虑到数据分区了。

![image-20240509164014717](images\image-20240509164014717.png)

数据分区通常采用顺序分布和hash分布。

| 分布方式   | 顺序分布 | 哈希分布 |
| ---------- | -------- | -------- |
| 数据分散度 | 分布倾斜 | 分布散列 |
| 顺序访问   | 支持     | 不支持   |

顺序分布保障了数据的有序性，但是离散性低，可能导致某个分区的数据热度高，其他分区数据的热度 低，分区访问不均衡。

哈希分布也分为多种分布方式，比如区域哈希分区，一致性哈希分区等。而redis cluster采用的是虚拟 槽分区的方式。

**虚拟槽分区**

redis cluster设置0~16383的槽，每个槽映射一个数据的子集，通过hash函数，将数据存放在不同的槽位中，每个集群的节点保存一部分槽。

每个key存储时，先经过哈希函数CRC16(key)得到一个整数，然后整数与16384取余，得到槽的数值，然后找到对应的节点，将数据存放到对应的槽。

![image-20240509164759998](images\image-20240509164759998.png)

**集群通信**

但是寻找槽的过程并不是一次命中的，比如上图key将要放到14396槽，但是并不是一次就锁定了node3节点，可能先去询问node1，然后才访问node3.

而集群中节点之间的通信，保证了最多两次就能命中对应槽所在的节点。因为在每个节点中，都保存了其他节点的信息，知道哪个槽由哪个节点负责，这样即使第一次访问没有命中槽，但是会知道客户端，该槽在哪个节点，这样访问对应节点就能精准命中。

![image-20240509165346933](images\image-20240509165346933.png)

1. 节点A对节点B发送一个meet操作，B返回后表示A和B之间能够进行沟通。
2. 节点A对节点C发送meet操作，C返回后，A和C之间也能进行沟通。
3.  然后B根据对A的了解，就能找到C，B和C之间也建立了联系。
4.  直到所有节点都能建立联系。

##### 3.3.2.2.2： 集群伸缩

集群并不是建立之后，节点数就固定不变的，也会由新的节点加入集群或者集群的节点下线，这就是集群的扩容和缩容。但是由于集群节点和槽息息相关，所以集群的伸缩也对应了槽和数据的迁移。

![image-20240509200839247](images\image-20240509200839247.png)

**集群扩容**

当有新节点准备好加入集群时，这个新节点还是孤立的节点，加入集群有两种方式。一个是通过集群节点执行命令来和孤立节点握手，另一个则是使用脚本来添加节点。

1. cluster_node_ip:port: cluster meet ip port new_node_ip:port

2.  redis-trib.rb add-node new_node_ip:port cluster_node_ip:port

通常这个新节点有两种身份，要么作为主节点，要么作为从节点：

- 主节点：分摊槽和数据
- 从节点：做故障转移备份

![image-20240509201223200](images\image-20240509201223200.png)

**其中槽的迁移有以下步骤**

![image-20240509201321135](images\image-20240509201321135.png)

**集群缩容**

![image-20240509201410169](images\image-20240509201410169.png)

**下线节点流程如下**

- 判断该节点是否持有槽，如果未持有槽就跳转下一步，持有槽则先迁移槽到其他节点
- 通知其他节点（**cluster forget**）忘记该下线节点
- 关闭下线节点服务

需要注意的是，如果下线主节点，再下线从节点，会进行故障转移，所以要先下线从节点。

##### 3.3.2.2.3 故障转移

除了手动下线节点外，也会面对突发故障。下面提到的主要是主节点的故障，因为从节点的故障并不影 响主节点工作，对应的主节点只会记住自己哪个从节点下线了，并将信息发送给其他节点。故障的从节 点重连后，继续官复原职，复制主节点的数据。

只有主节点才需要进行故障转移。在之前学习主从复制时，我们需要使用redis sentinel来实现故障转 移。而redis cluster则不需要redis sentinel，其自身就具备了故障转移功能。

根据前面我们了解到，节点之间是会进行通信的，节点之间通过ping/pong交互消息，所以借此就能发 现故障。集群节点发现故障同样是有主观下线和客观下线的

**主观下线**

![image-20240509201833910](images\image-20240509201833910.png)

对于每个节点有一个故障列表，故障列表维护了当前节点接收到的其他所有节点的信息。当半数以上的 持有槽的主节点都标记某个节点主观下线，就会尝试客观下线。

**客观下线**

![image-20240509201923669](images\image-20240509201923669.png)

**故障转移**

集群同样具备了自动转移故障的功能，和哨兵有些类似，在进行客观下线之后，就开始准备让故障节点 的从节点“上任”了。

首先是进行资格检查，只有具备资格的从节点才能参加选举：

- 故障节点的所有从节点检查和故障主节点之间的断线时间
- 超过cluster-node-timeout * cluster-slave-validati-factor(默认10)则取消选举资格

然后是准备选举顺序，不同偏移量的节点，参与选举的顺位不同。offset最大的slave节点，选举顺位最 高，最优先选举。而offset较低的slave节点，要延迟选举。

![image-20240509202043369](images\image-20240509202043369.png)



当有从节点参加选举后，主节点收到信息就开始投票。偏移量最大的节点，优先参与选举就更大可能获 得最多的票数，称为主节点。

![image-20240509202125093](images\image-20240509202125093.png)

当从节点走马上任变成主节点之后，就要开始进行替换主节点：

1. 让该slave节点执行replicaof no one变为master节点
2. 将故障节点负责的槽分配给该节点
3. 向集群中其他节点广播Pong消息，表明已完成故障转移
4. 故障节点重启后，会成为new_master的slave节点

#### 3.3.2.3 Redis Cluster 部署架构说明

**注意：建立Redis Cluster的节点需要清空数据，另外网络中不要有Redis哨兵的主从，否则也可能会干扰集群的创建和扩缩容**

测试环境：3台服务器，每台服务器启动6379和6380两个redis 服务实例，适用于测试环境

![image-20240510094512921](images\image-20240510094512921.png)

生产环境：6台服务器，分别是三组master/slave，适用于生产环境

![image-20240510094543716](images\image-20240510094543716.png)

**说明：Redis 5.X 和之前版本相比有较大变化，以下介绍两个版本5.X配置**

#### 3.3.2.4 部署方式介绍

redis cluster有多种部署方法

- 原生命令安装

  理解Redis Cluster架构

  生产环境不使用

- 官方工具安装

  高效、准确

  生产环境可以使用

- 自主研发

  可以实现可视化的自动化部署

### 3.3.3： 实战案例：基于Redis 5以上版本的Redis Cluster部署

官方文档：https://redis.io/topics/cluster-tutorial

**redis cluster 相关命令**

范例: 查看 --cluster 选项帮助

```bash
# redis-cli --cluster help
Cluster Manager Commands:
 create         host1:port1 ... hostN:portN
                 --cluster-replicas <arg>
 check         host:port
                 --cluster-search-multiple-owners
 info           host:port
 fix           host:port
                 --cluster-search-multiple-owners
 reshard       host:port
                 --cluster-from <arg>
                 --cluster-to <arg>
                 --cluster-slots <arg>
                 --cluster-yes
                 --cluster-timeout <arg>
                 --cluster-pipeline <arg>
                 --cluster-replace
 rebalance     host:port
                 --cluster-weight <node1=w1...nodeN=wN>
                 --cluster-use-empty-masters
                 --cluster-timeout <arg>
                 --cluster-simulate
                 --cluster-pipeline <arg>
                 --cluster-threshold <arg>
                 --cluster-replace
 add-node       new_host:new_port existing_host:existing_port
                 --cluster-slave
                 --cluster-master-id <arg>
 del-node       host:port node_id
 call           host:port command arg arg .. arg
 set-timeout   host:port milliseconds
 import         host:port
                 --cluster-from <arg>
                 --cluster-copy
                 --cluster-replace
 help           
For check, fix, reshard, del-node, set-timeout you can specify the host and port 
of any working node in the cluster. 
```

#### 3.3.3.1 创建 Redis Cluster 集群的环境准备

![image-20240510095325628](images\image-20240510095325628.png)

- 每个Redis节点采用相同的Redis版本，相同的密码，硬件配置

- 所有Redis服务器必须没有任何数据

- 准备6台主机，地址如下：

  ```http
  192.168.58.167 redis01
  192.168.58.168 redis02
  192.168.58.169 redis03
  192.168.58.170 redis04
  192.168.58.171 redis05
  192.168.58.172 redis06
  ```

#### 3.3.3.2 启用 Redis Cluster 配置

所有6台主机安装好redis.

- 每个节点修改redis配置，必须开启cluster功能参数

  ```bash
  #手动修改配置文件
  root@redis01:~# vim /apps/redis/etc/redis.conf
  bind 0.0.0.0
  masterauth 123456   #建议配置，否则后期的master和slave主从复制无法成功，还需再配置
  requirepass 123456
  cluster-enabled yes #取消此行注释,必须开启集群，开启后 redis 进程会有cluster标识 
  cluster-config-file nodes-6379.conf #取消此行注释,此为集群状态数据文件,记录主从关系及slot范围信息,由redis cluster 集群自动创建和维护 
  cluster-require-full-coverage no   #默认值为yes,设为no可以防止一个节点不可用导致整个cluster不可用
  
  
  #如果是编译安装，批量修改
  root@redis01:~# sed -i.bak -e '/masterauth/a masterauth 123456' -e '/# cluster-enabled yes/a cluster-enabled yes' -e '/# cluster-config-file nodes-6379.conf/a cluster-config-file nodes-6379.conf' -e '/cluster-require-full-coverage yes/a cluster-require-full-coverage no' /apps/redis/etc/redis.conf
  
  root@redis01:~# systemctl restart redis
  ```
  
- 验证当前Redis服务状态：

  ```bash
  #开启了16379的cluster的端口,实际的端口=redis port + 10000
  root@redis01:~# ss -ntl
  State                       Recv-Q                      Send-Q                                           Local Address:Port                                            Peer Address:Port                     Process                     
  LISTEN                      0                           511                                                    0.0.0.0:6379                                                 0.0.0.0:*                                                    
  LISTEN                      0                           4096                                             127.0.0.53%lo:53                                                   0.0.0.0:*                                                    
  LISTEN                      0                           128                                                    0.0.0.0:22                                                   0.0.0.0:*                                                    
  LISTEN                      0                           128                                                  127.0.0.1:6010                                                 0.0.0.0:*                                                    
  LISTEN                      0                           511                                                    0.0.0.0:16379                                                0.0.0.0:*                                                    
  LISTEN                      0                           128                                                  127.0.0.1:6011                                                 0.0.0.0:*                                                    
  LISTEN                      0                           511                                                      [::1]:6379                                                    [::]:*    
  
  #注意进程有[cluster]状态
  root@redis01:~# ps -ef | grep redis
  redis      28239       1  0 06:45 ?        00:00:00 /apps/redis/bin/redis-server 0.0.0.0:6379 [cluster]
  ```

#### 3.3.3.3：创建集群

```bash
#命令redis-cli的选项 --cluster-replicas 1 表示每个master对应一个slave节点，注意：所有节点数据必须清空
root@redis01:~# redis-cli -a 123456 --cluster create 192.168.58.167:6379 192.168.58.168:6379 192.168.58.169:6379 192.168.58.170:6379 192.168.58.171:6379 192.168.58.172:6379 --cluster-replicas 1
Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
>>> Performing hash slots allocation on 6 nodes...
Master[0] -> Slots 0 - 5460
Master[1] -> Slots 5461 - 10922
Master[2] -> Slots 10923 - 16383
Adding replica 192.168.58.171:6379 to 192.168.58.167:6379
Adding replica 192.168.58.172:6379 to 192.168.58.168:6379
Adding replica 192.168.58.170:6379 to 192.168.58.169:6379
M: 920473f718072bf4a90c43caf99e337cd2636ce7 192.168.58.167:6379  #带M的为master
   slots:[0-5460] (5461 slots) master                            #当前master的槽位
M: 2965f72832240748235821db8994433187debc59 192.168.58.168:6379
   slots:[5461-10922] (5462 slots) master
M: 6b26cbee6ee9a51e3a42b9167873b9fcdeb71856 192.168.58.169:6379
   slots:[10923-16383] (5461 slots) master
S: 31e35f09c5a38544ae907f8762fbbeb22acededc 192.168.58.170:6379   #带S的slave
   replicates 6b26cbee6ee9a51e3a42b9167873b9fcdeb71856
S: 30a6b9f4267309bace33f4f8d920bb5030f546bf 192.168.58.171:6379
   replicates 920473f718072bf4a90c43caf99e337cd2636ce7
S: abb691ec024863337a492b463a78103dcd7acb53 192.168.58.172:6379
   replicates 2965f72832240748235821db8994433187debc59
Can I set the above configuration? (type 'yes' to accept): yes   #输入yes自动创建集群
>>> Nodes configuration updated
>>> Assign a different config epoch to each node
>>> Sending CLUSTER MEET messages to join the cluster
Waiting for the cluster to join
.
>>> Performing Cluster Check (using node 192.168.58.167:6379)
M: 920473f718072bf4a90c43caf99e337cd2636ce7 192.168.58.167:6379
   slots:[0-5460] (5461 slots) master                     #已经分配的槽位
   1 additional replica(s)                                #分配了slave
S: 30a6b9f4267309bace33f4f8d920bb5030f546bf 192.168.58.171:6379
   slots: (0 slots) slave                                 #slave没有分配槽位
   replicates 920473f718072bf4a90c43caf99e337cd2636ce7    #对应master的ID
M: 2965f72832240748235821db8994433187debc59 192.168.58.168:6379
   slots:[5461-10922] (5462 slots) master
   1 additional replica(s)
S: abb691ec024863337a492b463a78103dcd7acb53 192.168.58.172:6379
   slots: (0 slots) slave
   replicates 2965f72832240748235821db8994433187debc59
M: 6b26cbee6ee9a51e3a42b9167873b9fcdeb71856 192.168.58.169:6379
   slots:[10923-16383] (5461 slots) master
   1 additional replica(s)
S: 31e35f09c5a38544ae907f8762fbbeb22acededc 192.168.58.170:6379
   slots: (0 slots) slave
   replicates 6b26cbee6ee9a51e3a42b9167873b9fcdeb71856
[OK] All nodes agree about slots configuration.          #所有节点槽位分配完成
>>> Check for open slots...                              #检查打开的槽位
>>> Check slots coverage...                              #检查插槽覆盖范围
[OK] All 16384 slots covered.                            #所有槽位(16384个)分配完成


# 观察以上结果，可以看到3组master/slave
master:192.168.58.167---slave:192.168.58.171
master:192.168.58.168---slave:192.168.58.172
master:192.168.58.169---slave:192.168.58.170

#如果节点少于3个会出下面提示错误
root@redis01:~# redis-cli -a 123456 --cluster create 192.168.58.167:6379 192.168.58.168:6379
Warning: Using a password with '-a' or '-u' option on the command line interface 
may not be safe.
*** ERROR: Invalid configuration for cluster creation.
*** Redis Cluster requires at least 3 master nodes.
*** This is not possible with 2 nodes and 0 replicas per node.
*** At least 3 nodes are required.
```

#### 3.3.3.4:  验证集群

##### 3.3.3.4.1: 查看主从状态

```bash
# master: 192.168.58.167
root@redis01:~# redis-cli -a 123456 -c INFO replication
# Replication
role:master
connected_slaves:1
slave0:ip=192.168.58.171,port=6379,state=online,offset=2072,lag=0
master_failover_state:no-failover
master_replid:ef799e60b326c4b2a3640a2a3da4a2f8ec76481e
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:2072
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:2072

#slave: 192.168.58.171
root@redis05:~# redis-cli -a 123456 -c INFO replication
# Replication
role:slave
master_host:192.168.58.167
master_port:6379
master_link_status:up
master_last_io_seconds_ago:10
master_sync_in_progress:0
slave_read_repl_offset:2436
slave_repl_offset:2436
slave_priority:100
slave_read_only:1
replica_announced:1
connected_slaves:0
master_failover_state:no-failover
master_replid:ef799e60b326c4b2a3640a2a3da4a2f8ec76481e
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:2436
second_repl_offset:-1
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:2436
```

##### 3.3.3.4.2：验证集群状态

```bash
root@redis01:~# redis-cli -a 123456 CLUSTER INFO
cluster_state:ok
cluster_slots_assigned:16384
cluster_slots_ok:16384
cluster_slots_pfail:0
cluster_slots_fail:0
cluster_known_nodes:6    #节点数
cluster_size:3           #三个master
cluster_current_epoch:6
cluster_my_epoch:1
cluster_stats_messages_ping_sent:2125
cluster_stats_messages_pong_sent:2153
cluster_stats_messages_sent:4278
cluster_stats_messages_ping_received:2148
cluster_stats_messages_pong_received:2124
cluster_stats_messages_meet_received:5
cluster_stats_messages_received:4277
total_cluster_links_buffer_limit_exceeded:0



#查看任意节点的集群状态
root@redis01:~# redis-cli -a 123456 --cluster info 192.168.58.167:6379
192.168.58.167:6379 (920473f7...) -> 0 keys | 5461 slots | 1 slaves.
192.168.58.168:6379 (2965f728...) -> 0 keys | 5462 slots | 1 slaves.
192.168.58.169:6379 (6b26cbee...) -> 0 keys | 5461 slots | 1 slaves.
[OK] 0 keys in 3 masters.
0.00 keys per slot on average.
```

##### 3.3.3.4.3: 查看对应关系

```bash
#以下命令查看指定master节点的slave节点信息，其中第一行的“920473f718072bf4a90c43caf99e337cd2636ce7” 为对应master ID

root@redis01:~# redis-cli -a 123456 cluster nodes 
30a6b9f4267309bace33f4f8d920bb5030f546bf 192.168.58.171:6379@16379 slave 920473f718072bf4a90c43caf99e337cd2636ce7 0 1715327139815 1 connected
2965f72832240748235821db8994433187debc59 192.168.58.168:6379@16379 master - 0 1715327137000 2 connected 5461-10922
abb691ec024863337a492b463a78103dcd7acb53 192.168.58.172:6379@16379 slave 2965f72832240748235821db8994433187debc59 0 1715327138743 2 connected
920473f718072bf4a90c43caf99e337cd2636ce7 192.168.58.167:6379@16379 myself,master - 0 1715327138000 1 connected 0-5460
6b26cbee6ee9a51e3a42b9167873b9fcdeb71856 192.168.58.169:6379@16379 master - 0 1715327139000 3 connected 10923-16383
31e35f09c5a38544ae907f8762fbbeb22acededc 192.168.58.170:6379@16379 slave 6b26cbee6ee9a51e3a42b9167873b9fcdeb71856 0 1715327138000 3 connected
```

#### 3.3.3.5: 测试集群写入数据

![image-20240510155809515](images\image-20240510155809515.png)

##### 3.3.3.5.1：redis cluster写入key

```bash
# 经过算法计算，当前key的槽位需要写入指定node
root@redis01:~# redis-cli -a 123456 set key1 value1
Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
(error) MOVED 9189 192.168.58.168:6379 #槽位不在当前node所以无法写入

#到对应槽所在的节点可以写入
root@redis02:~# redis-cli -a 123456 set key1 value1
OK
```

##### 3.3.3.5.2: redis cluster计算key所属的slot

```bash
root@redis02:~# redis-cli -a 123456 CLUSTER NODES
31e35f09c5a38544ae907f8762fbbeb22acededc 192.168.58.170:6379@16379 slave 6b26cbee6ee9a51e3a42b9167873b9fcdeb71856 0 1715328383119 3 connected
920473f718072bf4a90c43caf99e337cd2636ce7 192.168.58.167:6379@16379 master - 0 1715328380980 1 connected 0-5460
6b26cbee6ee9a51e3a42b9167873b9fcdeb71856 192.168.58.169:6379@16379 master - 0 1715328384190 3 connected 10923-16383
abb691ec024863337a492b463a78103dcd7acb53 192.168.58.172:6379@16379 slave 2965f72832240748235821db8994433187debc59 0 1715328383000 2 connected
2965f72832240748235821db8994433187debc59 192.168.58.168:6379@16379 myself,master - 0 1715328381000 2 connected 5461-10922
30a6b9f4267309bace33f4f8d920bb5030f546bf 192.168.58.171:6379@16379 slave 920473f718072bf4a90c43caf99e337cd2636ce7 0 1715328382000 1 connected


# 计算得到hello对应的slot
root@redis02:~# redis-cli -a 123456 cluster keyslot hello
(integer) 866
# hello对应的槽位是192.168.58.167这个master
root@redis01:~# redis-cli -a 123456 set hello world
OK

# 计算name对应的slot
root@redis01:~# redis-cli -a 123456 cluster keyslot name
(integer) 5798
# name对应的槽位是192.168.58.168这个master
root@redis02:~# redis-cli -a 123456 set name wanglei
OK


# 使用选项-c以集群模式连接，会自动redirect
root@redis02:~# redis-cli -a 123456 -c -h 192.168.58.167 set linux icloud2native
-> Redirected to slot [12299] located at 192.168.58.168:6379
OK
```

#### 3.3.3.6：Python程序实现Redis Cluster访问

官网：

```http
https://github.com/Grokzen/redis-py-cluster
```

范例：

```bash
root@redis01:~# apt -y install python3-pip
root@redis01:~# pip3 install redis-py-cluster

root@redis01:~# cat redis_cluster_test.py 
#!/usr/bin/env python3
from rediscluster import RedisCluster

startup_nodes = [
    {"host":"192.168.58.167", "port":6379},
    {"host":"192.168.58.168", "port":6379},
    {"host":"192.168.58.169", "port":6379},
    {"host":"192.168.58.170", "port":6379},
    {"host":"192.168.58.171", "port":6379},
    {"host":"192.168.58.172", "port":6379}
]

redis_conn= RedisCluster(startup_nodes=startup_nodes,password='123456', decode_responses=True)

for i in range(0, 10000):
    redis_conn.set('key'+str(i),'value'+str(i))
    print('key'+str(i)+':',redis_conn.get('key'+str(i)))
    
root@redis01:~# python3 redis_cluster_test.py

# 验证数据
root@redis01:~# redis-cli -a 123456 -h 192.168.58.167 dbsize
(integer) 3333
root@redis01:~# redis-cli -a 123456 -h 192.168.58.168 dbsize.
(integer) 3341
root@redis01:~# redis-cli -a 123456 -h 192.168.58.169 dbsize
(integer) 3331
```

#### 3.3.3.7：模拟故障实现故障转移

```bash
# 模拟redis02(192.168.58.168)节点故障，需要相应的数秒故障转移时间
root@redis02:~# systemctl stop redis

root@redis01:~# redis-cli -a 123456 --cluster info 192.168.58.167:6379
Could not connect to Redis at 192.168.58.168:6379: Connection refused
192.168.58.167:6379 (920473f7...) -> 3333 keys | 5461 slots | 1 slaves.
192.168.58.172:6379 (abb691ec...) -> 3341 keys | 5462 slots | 0 slaves. #192.168.58.172为新的master
192.168.58.169:6379 (6b26cbee...) -> 3331 keys | 5461 slots | 1 slaves.
[OK] 10005 keys in 3 masters.
0.61 keys per slot on average.

root@redis01:~# redis-cli -a 123456 -h 192.168.58.172 info replication  
# Replication
role:master         #已经变成master
connected_slaves:0
master_failover_state:no-failover
master_replid:bc9eb0f41e881e78e663eae5041e0fbc90c15068
master_replid2:954ccf513b0b314173569770d9c72379090d1867
master_repl_offset:142434
second_repl_offset:142435
repl_backlog_active:1
repl_backlog_size:1048576
repl_backlog_first_byte_offset:1
repl_backlog_histlen:142434


# 恢复故障节点redis02自动成为slave
root@redis02:~# systemctl start redis

# 查看自动生成的配置文件，可以查看node2自动成为slave节点
root@redis02:~# cat /apps/redis/data/nodes-6379.conf 
2965f72832240748235821db8994433187debc59 192.168.58.168:6379@16379 myself,slave abb691ec024863337a492b463a78103dcd7acb53 0 1715330203455 7 connected #已经变成slave节点
920473f718072bf4a90c43caf99e337cd2636ce7 192.168.58.167:6379@16379 master - 0 1715330203455 1 connected 0-5460
30a6b9f4267309bace33f4f8d920bb5030f546bf 192.168.58.171:6379@16379 slave 920473f718072bf4a90c43caf99e337cd2636ce7 0 1715330203455 1 connected
6b26cbee6ee9a51e3a42b9167873b9fcdeb71856 192.168.58.169:6379@16379 master - 0 1715330203455 3 connected 10923-16383
31e35f09c5a38544ae907f8762fbbeb22acededc 192.168.58.170:6379@16379 slave 6b26cbee6ee9a51e3a42b9167873b9fcdeb71856 0 1715330203455 3 connected
abb691ec024863337a492b463a78103dcd7acb53 192.168.58.172:6379@16379 master - 0 1715330203455 7 connected 5461-10922
```

### 3.3.5 Redis cluster 管理

#### 3.3.5.1：集群扩容

**扩容适用场景：**

当前客户量激增，现有的Redis Cluster架构已经无法满足越来越高的并发访问请求，为解决此问题，新购置两台服务器，要求其动态添加到现有集群，但不能影响业务的正常访问。

新版支持集群中有旧数据的情况扩容

注意: 生产环境一般建议master节点为奇数个,比如:3,5,7,以防止脑裂现象

![image-20240510164617694](images\image-20240510164617694.png)



![image-20240510164634453](images\image-20240510164634453.png)

##### 3.3.5.1.1：添加节点准备

增加Redis 新节点，需要与之前的Redis node版本和配置一致，然后分别再启动两台Redis node，应为 一主一从。

```http
192.168.58.173 redis07
192.168.58.174 redis08
```

以下两节点都要执行下面步骤：

```bash
# 部署redis
root@redis07:~# bash install_redis.sh

#如果是编译安装，批量修改
root@redis07:~# sed -i.bak -e '/masterauth/a masterauth 123456' -e '/# cluster-enabled yes/a cluster-enabled yes' -e '/# cluster-config-file nodes-6379.conf/a cluster-config-file nodes-6379.conf' -e '/cluster-require-full-coverage yes/a cluster-require-full-coverage no' /apps/redis/etc/redis.conf

root@redis07:~# systemctl restart redis
```

##### 3.3.5.1.2 添加新的master节点到集群

使用以下命令添加新节点，要添加的新redis节点IP和端口添加到的已有的集群的任意节点的IP:Port

```bash
add-node new_host:new_port existing_host:existing_port [--slave --master-id <arg>]

#说明：
new_host:new_port #指定新添加的主机的IP和端口
existing_host:existing_port #指定已有的集群中任意节点的IP和端口
```

**Redis 5 以上版本的添加命令：**

```bash
# 将一台新的主机192.168.58.173加入集群，
root@redis01:~# redis-cli -a 123456 --cluster add-node 192.168.58.173:6379 <当前任意集群节点>:6379
Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
>>> Adding node 192.168.58.173:6379 to cluster 192.168.58.167:6379
>>> Performing Cluster Check (using node 192.168.58.167:6379)
M: 920473f718072bf4a90c43caf99e337cd2636ce7 192.168.58.167:6379
   slots:[0-5460] (5461 slots) master
   1 additional replica(s)
S: 30a6b9f4267309bace33f4f8d920bb5030f546bf 192.168.58.171:6379
   slots: (0 slots) slave
   replicates 920473f718072bf4a90c43caf99e337cd2636ce7
S: 2965f72832240748235821db8994433187debc59 192.168.58.168:6379
   slots: (0 slots) slave
   replicates abb691ec024863337a492b463a78103dcd7acb53
M: abb691ec024863337a492b463a78103dcd7acb53 192.168.58.172:6379
   slots:[5461-10922] (5462 slots) master
   1 additional replica(s)
M: 6b26cbee6ee9a51e3a42b9167873b9fcdeb71856 192.168.58.169:6379
   slots:[10923-16383] (5461 slots) master
   1 additional replica(s)
S: 31e35f09c5a38544ae907f8762fbbeb22acededc 192.168.58.170:6379
   slots: (0 slots) slave
   replicates 6b26cbee6ee9a51e3a42b9167873b9fcdeb71856
[OK] All nodes agree about slots configuration.
>>> Check for open slots...
>>> Check slots coverage...
[OK] All 16384 slots covered.
>>> Getting functions from cluster
>>> Send FUNCTION LIST to 192.168.58.173:6379 to verify there is no functions in it
>>> Send FUNCTION RESTORE to 192.168.58.173:6379
>>> Send CLUSTER MEET to node 192.168.58.173:6379 to make it join the cluster.
[OK] New node added correctly.


#观察到该节点已经加入成功，但此节点没有 slot，也无slave节点，而且新节点是master
root@redis01:~# redis-cli -a 123456 --cluster info 192.168.58.167:6379
192.168.58.167:6379 (920473f7...) -> 3333 keys | 5461 slots | 1 slaves.
192.168.58.172:6379 (abb691ec...) -> 3341 keys | 5462 slots | 1 slaves.
192.168.58.173:6379 (89566a8f...) -> 0 keys | 0 slots | 0 slaves.
192.168.58.169:6379 (6b26cbee...) -> 3331 keys | 5461 slots | 1 slaves.
[OK] 10005 keys in 4 masters.

root@redis01:~# redis-cli -a 123456 cluster nodes
30a6b9f4267309bace33f4f8d920bb5030f546bf 192.168.58.171:6379@16379 slave 920473f718072bf4a90c43caf99e337cd2636ce7 0 1715331975004 1 connected
2965f72832240748235821db8994433187debc59 192.168.58.168:6379@16379 slave abb691ec024863337a492b463a78103dcd7acb53 0 1715331970000 7 connected
abb691ec024863337a492b463a78103dcd7acb53 192.168.58.172:6379@16379 master - 0 1715331972847 7 connected 5461-10922
920473f718072bf4a90c43caf99e337cd2636ce7 192.168.58.167:6379@16379 myself,master - 0 1715331971000 1 connected 0-5460
89566a8f6605dab8932297fdd76b3d3403ade148 192.168.58.173:6379@16379 master - 0 1715331972000 0 connected
6b26cbee6ee9a51e3a42b9167873b9fcdeb71856 192.168.58.169:6379@16379 master - 0 1715331973924 3 connected 10923-16383
31e35f09c5a38544ae907f8762fbbeb22acededc 192.168.58.170:6379@16379 slave 6b26cbee6ee9a51e3a42b9167873b9fcdeb71856 0 1715331973000 3 connected
```

##### 3.3.5.1.3 在新的master上重新分配槽位

新的node节点加到集群之后，默认是master节点，但没有slots，需要重新分配，否则没有槽位将无法访问

**注意: 旧版本重新分配槽位需要清空数据,所以需要先备份数据,扩展后再恢复数据,新版支持有数据直接扩 容**

Redis 5以上版本命令：

```bash
root@redis01:~# redis-cli -a 123456 --cluster reshard <当前任意集群节点>:6379
>>> Performing Cluster Check (using node 192.168.58.167:6379)
M: 920473f718072bf4a90c43caf99e337cd2636ce7 192.168.58.167:6379
   slots:[0-5460] (5461 slots) master
   1 additional replica(s)
S: 30a6b9f4267309bace33f4f8d920bb5030f546bf 192.168.58.171:6379
   slots: (0 slots) slave
   replicates 920473f718072bf4a90c43caf99e337cd2636ce7
S: 2965f72832240748235821db8994433187debc59 192.168.58.168:6379
   slots: (0 slots) slave
   replicates abb691ec024863337a492b463a78103dcd7acb53
M: abb691ec024863337a492b463a78103dcd7acb53 192.168.58.172:6379
   slots:[5461-10922] (5462 slots) master
   1 additional replica(s)
M: 89566a8f6605dab8932297fdd76b3d3403ade148 192.168.58.173:6379
   slots: (0 slots) master
M: 6b26cbee6ee9a51e3a42b9167873b9fcdeb71856 192.168.58.169:6379
   slots:[10923-16383] (5461 slots) master
   1 additional replica(s)
S: 31e35f09c5a38544ae907f8762fbbeb22acededc 192.168.58.170:6379
   slots: (0 slots) slave
   replicates 6b26cbee6ee9a51e3a42b9167873b9fcdeb71856
[OK] All nodes agree about slots configuration.
>>> Check for open slots...
>>> Check slots coverage...
[OK] All 16384 slots covered.
How many slots do you want to move (from 1 to 16384)? 4096 #新分配多少个槽位=16384/master个数
What is the receiving node ID? 89566a8f6605dab8932297fdd76b3d3403ade148 #新的master的ID
Please enter all the source node IDs.
  Type 'all' to use all the nodes as source nodes for the hash slots.
  Type 'done' once you entered all the source nodes IDs.
Source node #1: all #输入all,将哪些源主机的槽位分配给新的节点，all是自动在所有的redis node选择划分，如果是从redis cluster删除某个主机可以使用此方式将指定主机上的槽位全部移动到别的redis主机
......
Do you want to proceed with the proposed reshard plan (yes/no)?  yes #确认分配
......
Moving slot 12282 from 192.168.58.169:6379 to 192.168.58.173:6379: 
Moving slot 12283 from 192.168.58.169:6379 to 192.168.58.173:6379: .
Moving slot 12284 from 192.168.58.169:6379 to 192.168.58.173:6379: 
Moving slot 12285 from 192.168.58.169:6379 to 192.168.58.173:6379: .
Moving slot 12286 from 192.168.58.169:6379 to 192.168.58.173:6379: 
Moving slot 12287 from 192.168.58.169:6379 to 192.168.58.173:6379:



# 确定slot分配成功
root@redis01:~# redis-cli -a 123456 --cluster info 192.168.58.167:6379
192.168.58.167:6379 (920473f7...) -> 2512 keys | 4096 slots | 1 slaves.
192.168.58.172:6379 (abb691ec...) -> 2515 keys | 4096 slots | 1 slaves.
192.168.58.173:6379 (89566a8f...) -> 2476 keys | 4096 slots | 0 slaves.
192.168.58.169:6379 (6b26cbee...) -> 2502 keys | 4096 slots | 1 slaves.
[OK] 10005 keys in 4 masters.
```

##### 3.3.5.1.4 为新的master指定新的slave节点

当前Redis集群中新的master存在单点问题，还需要给其添加一个对应的slave节点，实现高可用功能

**Redis 5 以上版本添加命令：**

```http
redis-cli -a 123456 --cluster add-node new_slave_ip:6379 <任意集群节点>:6379 --
cluster-slave --cluster-master-id <对应master id>
```

```bash
root@redis01:~# redis-cli -a 123456 --cluster add-node 192.168.58.174:6379 192.168.58.167:6379 --cluster-slave --cluster-master-id 89566a8f6605dab8932297fdd76b3d3403ade148


# 验证是否成功
root@redis01:~# redis-cli -a 123456 cluster nodes
30a6b9f4267309bace33f4f8d920bb5030f546bf 192.168.58.171:6379@16379 slave 920473f718072bf4a90c43caf99e337cd2636ce7 0 1715332911000 1 connected
2965f72832240748235821db8994433187debc59 192.168.58.168:6379@16379 slave abb691ec024863337a492b463a78103dcd7acb53 0 1715332910000 7 connected
f71da88bcba2f55b34d6b8ba922c6c0908fd7ca8 192.168.58.174:6379@16379 slave 89566a8f6605dab8932297fdd76b3d3403ade148 0 1715332912000 8 connected
abb691ec024863337a492b463a78103dcd7acb53 192.168.58.172:6379@16379 master - 0 1715332912923 7 connected 6827-10922
920473f718072bf4a90c43caf99e337cd2636ce7 192.168.58.167:6379@16379 myself,master - 0 1715332908000 1 connected 1365-5460
89566a8f6605dab8932297fdd76b3d3403ade148 192.168.58.173:6379@16379 master - 0 1715332914001 8 connected 0-1364 5461-6826 10923-12287
6b26cbee6ee9a51e3a42b9167873b9fcdeb71856 192.168.58.169:6379@16379 master - 0 1715332910000 3 connected 12288-16383
31e35f09c5a38544ae907f8762fbbeb22acededc 192.168.58.170:6379@16379 slave 6b26cbee6ee9a51e3a42b9167873b9fcdeb71856 0 1715332909000 3 connected


root@redis01:~# redis-cli -a 123456 cluster info
Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
cluster_state:ok
cluster_slots_assigned:16384
cluster_slots_ok:16384
cluster_slots_pfail:0
cluster_slots_fail:0
cluster_known_nodes:8  #8个节点
cluster_size:4         #4组主从
cluster_current_epoch:8
cluster_my_epoch:1
cluster_stats_messages_ping_sent:7246
cluster_stats_messages_pong_sent:7356
cluster_stats_messages_auth-ack_sent:1
cluster_stats_messages_sent:14603
cluster_stats_messages_ping_received:7349
cluster_stats_messages_pong_received:11341
cluster_stats_messages_meet_received:7
cluster_stats_messages_fail_received:1
cluster_stats_messages_auth-req_received:1
cluster_stats_messages_update_received:1
cluster_stats_messages_received:18700
total_cluster_links_buffer_limit_exceeded:0
```

#### 3.3.5.2 集群缩容

支持集群中有旧数据的情况进行缩容

**缩容适用场景：**

随着业务萎缩用户量下降明显,和领导商量决定将现有Redis集群的8台主机中下线两台主机挪做它用,缩容 后性能仍能满足当前业务需求

**删除节点过程：**

扩容时是先添加node到集群，然后再分配槽位，而缩容时的操作相反，是先将被要删除的node上的槽 位迁移到集群中的其他node上，然后 才能再将其从集群中删除，如果一个node上的槽位没有被完全迁 移空，删除该node时也会提示有数据出错导致无法删除。

![image-20240510172455001](images\image-20240510172455001.png)

##### 3.3.5.2.1 迁移要删除的master节点上面的槽位到其它master

Redis 5版本以上命令

```bash
#查看当前状态
root@redis01:~# redis-cli -a 123456 --cluster check 192.168.58.167:6379
Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
192.168.58.167:6379 (920473f7...) -> 2512 keys | 4096 slots | 1 slaves.
192.168.58.172:6379 (abb691ec...) -> 2515 keys | 4096 slots | 1 slaves.
192.168.58.173:6379 (89566a8f...) -> 2476 keys | 4096 slots | 1 slaves.
192.168.58.169:6379 (6b26cbee...) -> 2502 keys | 4096 slots | 1 slaves.
[OK] 10005 keys in 4 masters.
0.61 keys per slot on average.
>>> Performing Cluster Check (using node 192.168.58.167:6379)
M: 920473f718072bf4a90c43caf99e337cd2636ce7 192.168.58.167:6379
   slots:[1365-5460] (4096 slots) master
   1 additional replica(s)
S: 30a6b9f4267309bace33f4f8d920bb5030f546bf 192.168.58.171:6379
   slots: (0 slots) slave
   replicates 920473f718072bf4a90c43caf99e337cd2636ce7
S: 2965f72832240748235821db8994433187debc59 192.168.58.168:6379
   slots: (0 slots) slave
   replicates abb691ec024863337a492b463a78103dcd7acb53
S: f71da88bcba2f55b34d6b8ba922c6c0908fd7ca8 192.168.58.174:6379
   slots: (0 slots) slave
   replicates 89566a8f6605dab8932297fdd76b3d3403ade148
M: abb691ec024863337a492b463a78103dcd7acb53 192.168.58.172:6379
   slots:[6827-10922] (4096 slots) master
   1 additional replica(s)
M: 89566a8f6605dab8932297fdd76b3d3403ade148 192.168.58.173:6379
   slots:[0-1364],[5461-6826],[10923-12287] (4096 slots) master
   1 additional replica(s)
M: 6b26cbee6ee9a51e3a42b9167873b9fcdeb71856 192.168.58.169:6379
   slots:[12288-16383] (4096 slots) master
   1 additional replica(s)
S: 31e35f09c5a38544ae907f8762fbbeb22acededc 192.168.58.170:6379
   slots: (0 slots) slave
   replicates 6b26cbee6ee9a51e3a42b9167873b9fcdeb71856
[OK] All nodes agree about slots configuration.
>>> Check for open slots...
>>> Check slots coverage...
[OK] All 16384 slots covered.



# 将1365个slot从192.168.58.173移动到第一个master节点192.168.58.172
root@redis01:~# redis-cli -a 123456 --cluster reshard 192.168.58.167:6379
>>> Performing Cluster Check (using node 192.168.58.167:6379)
M: 920473f718072bf4a90c43caf99e337cd2636ce7 192.168.58.167:6379
   slots:[1365-5460] (4096 slots) master
   1 additional replica(s)
S: 30a6b9f4267309bace33f4f8d920bb5030f546bf 192.168.58.171:6379
   slots: (0 slots) slave
   replicates 920473f718072bf4a90c43caf99e337cd2636ce7
S: 2965f72832240748235821db8994433187debc59 192.168.58.168:6379
   slots: (0 slots) slave
   replicates abb691ec024863337a492b463a78103dcd7acb53
S: f71da88bcba2f55b34d6b8ba922c6c0908fd7ca8 192.168.58.174:6379
   slots: (0 slots) slave
   replicates 89566a8f6605dab8932297fdd76b3d3403ade148
M: abb691ec024863337a492b463a78103dcd7acb53 192.168.58.172:6379
   slots:[6827-10922] (4096 slots) master
   1 additional replica(s)
M: 89566a8f6605dab8932297fdd76b3d3403ade148 192.168.58.173:6379
   slots:[0-1364],[5461-6826],[10923-12287] (4096 slots) master
   1 additional replica(s)
M: 6b26cbee6ee9a51e3a42b9167873b9fcdeb71856 192.168.58.169:6379
   slots:[12288-16383] (4096 slots) master
   1 additional replica(s)
S: 31e35f09c5a38544ae907f8762fbbeb22acededc 192.168.58.170:6379
   slots: (0 slots) slave
   replicates 6b26cbee6ee9a51e3a42b9167873b9fcdeb71856
[OK] All nodes agree about slots configuration.
>>> Check for open slots...
>>> Check slots coverage...
[OK] All 16384 slots covered.
How many slots do you want to move (from 1 to 16384)? 1365 #共4096/3分别给其它三个master节点
What is the receiving node ID? abb691ec024863337a492b463a78103dcd7acb53  #master 192.168.58.172
Please enter all the source node IDs.
  Type 'all' to use all the nodes as source nodes for the hash slots.
  Type 'done' once you entered all the source nodes IDs.
Source node #1: 89566a8f6605dab8932297fdd76b3d3403ade148 #输入要删除节点192.168.58.173 ID
Source node #2: done
......
Do you want to proceed with the proposed reshard plan (yes/no)? yes
...
Moving slot 1358 from 192.168.58.173:6379 to 192.168.58.172:6379: ..
Moving slot 1359 from 192.168.58.173:6379 to 192.168.58.172:6379: .
Moving slot 1360 from 192.168.58.173:6379 to 192.168.58.172:6379: .




# 非交互方式
# 再将将1365个slot从192.168.58.173移动到第一个master节点192.168.58.167上
root@redis01:~# redis-cli -a 123456 --cluster reshard 192.168.58.167:6379 --cluster-slots 1365 --cluster-from 89566a8f6605dab8932297fdd76b3d3403ade148 --cluster-to 920473f718072bf4a90c43caf99e337cd2636ce7 --cluster-yes


#最后的slot从192.168.58.173移动到第三个master节点192.168.58.169上
root@redis01:~# redis-cli -a 123456 --cluster reshard 192.168.58.167:6379 --cluster-slots 1365 --cluster-from 89566a8f6605dab8932297fdd76b3d3403ade148 --cluster-to 6b26cbee6ee9a51e3a42b9167873b9fcdeb71856 --cluster-yes
```

##### **3.3.5.2.2** **从集群中删除服务器**

上面步骤完成后,槽位已经迁移走，但是节点仍然还属于集群成员，因此还需从集群删除该节点

注意: 删除服务器前,必须清除主机上面的槽位,否则会删除主机失败

Redis 5以上版本命令：

```bash
#redis-cli -a 123456 --cluster del-node <任意集群节点的IP>:6379 89566a8f6605dab8932297fdd76b3d3403ade148
#89566a8f6605dab8932297fdd76b3d3403ade148是删除节点的ID
>>> Removing node cb028b83f9dc463d732f6e76ca6bbcd469d948a7 from cluster 
192.168.58.173:6379
>>> Sending CLUSTER FORGET messages to the cluster...
>>> SHUTDOWN the node.

#删除节点后,redis进程自动关闭
#删除节点信息
#rm -f /apps/redis/data/nodes-6379.conf



# 验证集群信息
root@redis01:~# redis-cli -a 123456 --cluster info 192.168.58.167:6379
```

#### **3.3.5.3 **集群偏斜**

redis cluster 多个节点运行一段时间后,可能会出现倾斜现象,某个节点数据偏多,内存消耗更大,或者接受

用户请求访问更多

发生倾斜的原因可能如下:

- 节点和槽分配不均
- 不同槽对应键值数量差异较大
- 包含bigkey,建议少用
- 内存相关配置不一致
- 热点数据不均衡 : 一致性不高时,可以使用本缓存和MQ

获取指定槽位中对应键key值的个数

```bash
#redis-cli cluster countkeysinslot {slot的值}
```

执行自动的槽位重新平衡分布,但会影响客户端的访问,此方法慎用

```bash
#redis-cli --cluster rebalance <集群节点IP:PORT>
```

获取bigkey ,建议在slave节点执行

```bash
#redis-cli --bigkeys
```

### **3.3.5 Redis Cluster** **的局限性**

#### **3.3.5.1** **集群的读写分离**

在集群模式下的从节点是只读连接的，也就是说集群模式中的从节点是拒绝任何读写请求的。当有命令

尝试从slave节点获取数据时，slave节点会重定向命令到负责该数据所在槽的节点。

为什么说是只读连接呢？因为slave可以执行命令：readonly，这样从节点就能读取请求，但是这只是在

这次连接中生效。也就是说，当客户端断开连接重启后，再次请求又变成重定向了。

集群模式下的读写分离更加复杂，需要维护不同主节点的从节点和对于槽的关系。

通常是不建议在集群模式下构建读写分离，而是添加节点来解决需求。不过考虑到节点之间信息交流带

来的带宽问题，官方建议节点数不超过1000个。

#### **3.3.5.2** **单机**,**哨兵和集群的选择**

- 大多数时客户端性能会”降低”
- 命令无法跨节点使用︰mget、keys、scan、flush、sinter等
- 客户端维护更复杂︰SDK和应用本身消耗(例如更多的连接池)
- 不支持多个数据库︰集群模式下只有一个db 0
- 不支持多个数据库︰集群模式下只有一个db 0
- Key事务和Lua支持有限∶操作的key必须在一个节点,Lua和事务无法跨节点使用

所以集群搭建还要考虑单机redis是否已经不能满足业务的并发量，在redis sentinel同样能够满足高可

用，且并发并未饱和的前提下，搭建集群反而是画蛇添足了。

# **4**: **常见面试题**

- Redis 做什么的,即在哪些场景下使用
- 如果监控 Redis 是否出现故障
- Redis客户端timeout报错突然增加，排查思路是怎样的？
- 请简单描述pipeline功能，为什么pipeline功能会提升redis性能?
- 本地redis-client访问远程Redis服务出错，说出几种常见的错误?
- key-value的大小超大或单key的qps超高，会对Redis本身造成什么样的影响、会对访问Redis的其
- 他客户端造成什么样的影响？
- Zabbix 监控 Redis 哪些监控项
- RDB和AOF持久化区别
- docker拉取一个Redis如何实现数据持久化保存
- Redis 支持哪些数据类型
- Redis 如何实现消息队列
- 描述下常见的redis集群架构有哪些，他们之间的优缺点对比
- 主从复制工作原理
- Redis 如何实现高可用
- 哨兵工作原理
- Redis 集群的工作原理
- Redis 集群如果避免脑裂
- Redis 集群最少几个节点为什么?
- Redis的集群槽位多少个
- Redis集群中某个节点缺少一个槽位是否能使用
- Redis数据写入的时候是怎么在各个节点槽位分配数据的
- Redis的数据存储是以什么样的方式存储
- Redis集群的各槽位和总槽位之间什么关系
- Redis集群中有一个节点内存使用明显偏大，可能是原因是什么？
- Redis部署有几种模式



























