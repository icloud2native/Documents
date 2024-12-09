# 1 WEB 服务和HTTP协议

## 1.1 Internet 因特网

因特网是"Internet”的中文译名，它起源于美国的五角大楼，它的前身是美国国防部高级研究计划局 （ARPA）主持研制的ARPAnet。20世纪50年代末，正处于冷战时期。当时美国军方为了自己的计算机 网络在受到袭击时,即使部分网络被摧毁，其余部分仍能保持通信联系，便由美国国防部的高级研究计划 局（ARPA）建设了一个军用网，叫做"阿帕网”（ARPAnet）。

1969年正式启用阿帕网，当时仅连接了4台计算机，供科学家们进行计算机联网实验用，这就是因特网 的前身。

到70年代，ARPAnet已经有了好几十个计算机网络，但是每个网络只能在网络内部的计算机之间互联通 信，不同计算机网络之间仍然不能互通。为此， ARPA又设立了新的研究项目，支持学术界和工业界进 行有关的研究，研究的主要内容就是想用一种新的方法将不同的计算机局域网互联，形成"互联网”。研 究人员称之为"internetwork”，简称"Internet”。在研究实现互联的过程中，计算机软件起了主要的作 用。

1974年，出现了连接分组网络的协议，其中就包括了TCP/IP协议。TCP/IP有一个非常重要的特点，就是 开放性，即TCP/IP的规范和Internet的技术都是公开的。目的就是使任何厂家生产的计算机都能相互通 信，使Internet成为一个开放的系统，这正是后来Internet得到飞速发展的重要原因。ARPA在1982年接 受了TCP/IP，选定Internet为主要的计算机通信系统，并把其它的军用计算机网络都转换到TCP/IP。 1983年，ARPAnet分成两部分：一部分军用，称为MILNET；另一部分仍称ARPAnet，供民用。

1974年，出现了连接分组网络的协议，其中就包括了TCP/IP协议。TCP/IP有一个非常重要的特点，就是 开放性，即TCP/IP的规范和Internet的技术都是公开的。目的就是使任何厂家生产的计算机都能相互通 信，使Internet成为一个开放的系统，这正是后来Internet得到飞速发展的重要原因。ARPA在1982年接 受了TCP/IP，选定Internet为主要的计算机通信系统，并把其它的军用计算机网络都转换到TCP/IP。 1983年，ARPAnet分成两部分：一部分军用，称为MILNET；另一部分仍称ARPAnet，供民用。

Internet的发展引起了商家的极大兴趣。1992年，美国IBM、MCI、MERIT三家公司联合组建了一个高级 网络服务公司（SNS），建立了一个新的网络，叫做SNSnet，成为Internet的另一个主干网。它与 SNSFnet不同，NSFnet是由国家出资建立的，而SNSnet则是SNS 公司所有，从而使Internet开始走向商 业化。

1995年4月30日，SNSFnet正式宣布停止运作。而此时Internet的骨干网已经覆盖了全球91个国家，主 机已超过400万台。而在当前，因特网仍以惊人的速度向前发展

在90年代，超文本标识语言（HTML），即一个可以获得因特网的图像信息的超文本因特网协议被采 用，使每一个人可以产生自己的图像页面（网址），然后成为一个巨大的虚拟超文本网络的组成部分。 这个增强型的因特网又被非正式地称为万维网，与此同时产生了数量庞大的新用户群。于是，许多人 用"因特网” 一词指这个网络的物理结构，包括连接所有事物的客户机、服务器和网络；而用"万维网”一 词指利用这个网络可以访问的所有网站和信息。

## 1.2 Internet 和中国

北京时间1987年9月14日，物理研究员钱天白建立起一个网络节点，通过电话拨号连接到国际互联网， 向他的德国朋友发出来自中国的第一封电子邮件：Across the Great Wall we can reach every corner in  the world，自此，中国与国际计算机网络开始连接在一起

![image-20241118141751705](images/image-20241118141751705.png)

1990年10月，钱天白教授代表中国正式在国际互联网络信息中心的前身DDN-NIC注册登记了我国的顶 级域名CN，并且从此开通了使用中国顶级域名CN的国际电子邮件服务。由于当时中国尚未正式连入 Internet，所以委托德国卡尔斯鲁厄大学运行CN域名服务器

1993年3月2日， 中国科学院高能物理研究所租用AT&T公司的国际卫星信道接入美国斯坦福线性加速器 中心（SLAC）的64K专线正式开通,专线开通后，美国政府以Internet上有许多科技信息和其它各种资 源，不能让社会主义国家接入为由，只允许这条专线进入美国能源网而不能连接到其它地方。尽管如 此，这条专线仍是我国部分连入Internet的第一根专线

1994年4月20日，中国通过一条64k的国际专线全功能接入国际互联网，成为国际互联网大家庭中的第 77个成员，正式开启了互联网时代。随后，中科院高能物理研究所推出第一个WWW网站和第一套网页

1994年5月21日， 在钱天白教授和德国卡尔斯鲁厄大学的协助下，中国科学院计算机网络信息中心完成 了中国国家顶级域名(CN)服务器的设置，改变了中国CN顶级域名服务器一直放在国外的历史

1995年5月17日， 第27个世界电信日，邮电部正式宣布，向国内社会开放计算机互联网接入服务

1995年5月，北京的中关村南大街上出现了一块巨大的广告牌，"中国离信息高速公路还有多远？向北 1500米。”那个位置就是一家叫"瀛海威”的网络科教馆，瀛海威正是information highway的音译，作为 中国第一个互联网接入服务商，瀛海威几乎就是当时互联网的代名词

1996年1月，中国互联网全国骨干网建成并正式开通，开始提供服务

1995年4月，马云凑了两万块钱，成立杭州海博网络公司，专门给企业做主页

1997年5月，丁磊创立网易

1998年2月， 张朝阳创立搜狐

1998年6月18日，刘强东在中关村创办京东公司，代理销售光磁产品

1998年11月，马化腾和张志东成立深圳市腾讯计算机系统有限公司，OICQ开通

1998年12月， 新浪网成立，关键人物：王志东

1999年5月18日，中国第一家电子商务企业8848.com成立，创始人王峻涛也曾被誉为"中国电子商务教 父”。2000年底，调查显示接近70%的人说上网买东西首选 8848

2000年1月，李彦宏创建了百度

2003年5月，阿里巴巴集团在创立淘宝网

2003年10月，淘宝网首次推出支付宝服务

2009年11月, 阿里开始举办双十一购物狂欢节

2012年1月11日淘宝商城正式更名为“天猫”

2014年9月19日阿里巴巴集团于纽约证券交易所正式挂牌上市

2004年1月，京东多媒体网正式开通，启用域名www.jdlaser.com

2010年4月，雷军创办小米

2011年1月21日，腾讯公司推出微信 (WeChat) 

2012年3月，今日头条由张一鸣于创建

2012年7月10日，北京小桔科技有限公司成立，滴滴司机端3个月后北京上线

2016年9月20日, 字节跳动上线抖音

**中国互联网连接世界**

1885年台湾建省，首任巡抚刘铭传派人与福州船政联系，使用船政电报学堂毕业生为技术人员，于1887 年铺设成功台湾淡水至福州川石海底电缆，全长117海里。这是我国自行设计安装的第一条海底电缆。 此电缆毁于第二次世界大战我国于1989年开始投入到全球海底光缆的投资与建设中来，并于1993年实现 了首条国际海底光缆的登陆（中日之间C-J海底光缆系统）；随后在1997年，我国参与建设的全球海底光 缆系统（FLAG）建成并投入运营，这也是第一条在我国登陆的洲际海底光缆中国连接世界目前共有8条 光缆，四个登陆站允许入境，目前我国的登陆站设立在三个城市的四个地区，分别是山东青岛登陆站 （隶属中国联通）、上海崇明登陆站（隶属中国电信）、上海南汇登陆站（隶属中国联通）和广东汕头 登陆站（隶属中国电信）

1993年3月2日，中国科学院高能物理研究所租用AT&T公司的国际卫星信道建立的接入美国SLAC国家实 验室的64K专线正式开通，成为我国连入Internet的第一根专线。

参考链接: http://www.ihep.cas.cn/kxcb/kpcg/jsywl/201407/t20140714_4156699.html

下图是海底光缆

![image-20241118142529981](images/image-20241118142529981.png)

## 1.3 HTTP 超文本传输协议

### 1.3.1 HTTP 相关概念

互联网：是网络的网络，是所有类型网络的母集。

因特网：世界上最大的互联网网络。即因特网概念从属于互联网概念。习惯上，大家把连接在因特网上 的计算机都成为主机。

万维网：WWW（world wide web）万维网并非某种特殊的计算机网络，是一个大规模的、联机式的信 息贮藏库，使用链接的方法能非常方便地从因特网上的一个站点访问另一个站点（超链技术），具有提 供分布式服务的特点。万维网是一个分布式的超媒体系统，是超文本系统的扩充，基于B/S架构实现

![image-20241118142643242](images/image-20241118142643242.png)

URL：万维网使用统一资源定位符（Uniform Resource Locator）来标志万维网上的各种文档，并使每 个文档在整个因特网的范围内具有唯一的标识符URL。

HTTP：为解决"用什么样的网络协议来实现整个因特网上的万维网文档”这一难题，就要使万维网客户程 序（以浏览器为主，但不限于浏览器）与万维网服务器程序之间的交互遵守严格的协议，即超文本传送 协议（HyperText Transfer Protocol）。HTTP是处于应用层的协议，使用TCP传输层协议进行可靠的传 送。因此，需要特别提醒的是，万维网是基于因特网的一种广泛因特网应用系统，且万维网采用的是 HTTP（80/TCP）和 HTTPS（443/TCP）的传输协议，但因特网还有其他的网络应用系统（如：FTP、 SMTP等等）。

HTML：为了解决"怎样使不同作者创作的不同风格的万维网文档，都能在因特网上的各种主机上显示出 来，同时使用户清楚地知道在什么地方存在着链接”这一问题，万维网使用超文本标记语言（HyperText  Markup Language），使得万维网页面的设计者可以很方便地用链接从页面的某处链接到因特网的任何 一个万维网页面，并且能够在自己的主机品目上将这些页面显示出来。HTML与txt一样，仅仅是是一种 文档，不同之处在于，这种文档专供于浏览器上为浏览器用户提供统一的界面呈现的统一规约。且具备 结构化的特征，这是txt所不具备的强制规定。

### 1.3.2 浏览器访问网站的过程

![image-20241118142853541](images/image-20241118142853541.png)



### 1.3.3 HTTP 协议通信过程

![image-20241118142920504](images/image-20241118142920504.png)

HTTP（HyperText Transfer Protocol，超文本传输协议）是一种用于分布式、协作式和超媒体信息系统 的应用层协议。HTTP是万维网的数据通信的基础设计HTTP最初的目的是为了提供一种远距离共享知识 的方式，借助多文档进行关联实现超文本，连成相互参阅的WWW（world wide web,万维网）

HTTP的发展是由蒂姆·伯纳斯-李（Tim Berners-Lee）于1989年在欧洲核子研究组织（CERN）所发起。 HTTP的标准制定由万维网协会（World Wide Web Consortium，W3C）和互联网工程任务组 （Internet Engineering Task Force，IETF）进行协调，最终发布了一系列的RFC，其中最著名的是 1999年6月公布的 RFC 2616，定义了HTTP协议中现今广泛使用的一个版本——HTTP 1.1版

**HTTP服务通信过程**

![image-20241118143050926](images/image-20241118143050926.png)

**HTTP协议分层**

![image-20241118143115004](images/image-20241118143115004.png)

### 1.3.4 HTTP 相关技术

#### 1.3.4.1 WEB 开发语言

**http：**Hyper Text Transfer Protocol 应用层协议，默认端口： 80/tcp

**WEB前端开发语言：**

- html
- css
- javascript

![image-20241118143240944](images/image-20241118143240944.png)

**html**

Hyper Text Markup Language 超文本标记语言，编程语言，主要负责实现页面的结构

范例：html语言

```html
<html>
<head>
<meta http-equiv=Content-Type content="text/html;charset=utf-8">
<title>HTML语言</title>
</head>
<body>
<img src="http://www.wang.com/wp-content/uploads/2017/09/logo.png" >
<h1 style="color:red">欢迎</h1>
<p><a href=http://www.wang.com>爱写代码的小奶还</a>欢迎你</p>
</body>
</html>
#注意:html文件编码为utf-8编码
```

**CSS**

Cascading Style Sheet 层叠样式表， 定义了如何显示（装扮） HTML 元素，比如：字体大小和颜色属 性等。样式通常保存在外部的 .css 文件中,用于存放一些HTML文件的公共属性,从而通过仅编辑一个简单 的 CSS 文档，可以同时改变站点中所有页面的布局和外观。 

范例 ：CSS

```html
#test.html 建议用Vscode创建文件,用记事本可能会出现乱码
<html>
<head>
<meta http-equiv=Content-Type content="text/html;charset=utf-8">
<link rel="stylesheet" type="text/css" href="mystyle.css" />
</head>
<body>
<h1>这是 heading 1</h1>
<p>这是一段普通的段落。请注意，该段落的文本是红色的。在 body 选择器中定义了本页面中的默认文本颜
色。</p>
<p class="ex">该段落定义了 class="ex"。该段落中的文本是蓝色的。</p>
</body>
</html>

#mystyle.css
body {color:red}
h1 {color:#00ff00}
p.ex {color:rgb(0,0,255)}
```

**JS**

javascript，实现网页的动画效果，但实属于静态资源

Java和javascript的关系: 周杰和周杰伦的关系

范例：javascript

```javascript
<!DOCTYPE html>
<html>
<head>
<meta http-equiv=Content-Type content="text/html;charset=utf-8">
</head>
<body>
<h2>我的第一个 JavaScript</h2>
<button type="button"
onclick="document.getElementById('demo').innerHTML = Date()">
点击这里来显示日期和时间
</button>
<p id="demo"></p>
</body>
</html>
```

#### 1.3.4.2 MIME

MIME : Multipurpose Internet Mail Extensions 多用途因特网邮件扩展

文件`/etc/mime.types`,来自于mailcap包

MIME格式：type/subtype txt html jpg bmp 

参考链接：

https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics_of_HTTP/MIME_Types

http://www.w3school.com.cn/media/media_mimeref.asp

 范例：

```bash
text/plain   txt asc text pm el c h cc hh cxx hxx f90 conf log
text/html     html htm
text/css
image/jpeg   jpg jpeg
image/png 
video/mp4 
application/javascript 
```

#### 1.3.4.3 URI和URL

参考链接

```http
https://developer.mozilla.org/zhCN/docs/Web/HTTP/Basics_of_HTTP/Identifying_resources_on_the_Web
```

URI： Uniform Resource Identifier 统一资源标识，分为URL 和 URN

URN：Uniform Resource Naming，统一资源命名

示例：P2P下载使用的磁力链接是URN的一种实现

```bash
magnet:?xt=urn:btih:1E45C21458681BFECBEB72D77A2500762D6F799F
```

URL：Uniform Resource Locator，统一资源定位符，用于描述某服务器某特定资源位置

两者区别：URN如同一个人的名称，而URL代表一个人的住址。换言之，URN定义某事物的身份，而 URL提供查找该事物的方法。URN仅用于命名，而不指定地址

URL组成

![image-20241118144215072](images/image-20241118144215072.png)



```http
<scheme>://<user>:<password>@<host>:<port>/<path>;<params>?<query>#<frag>
```

```http
scheme:方案，访问服务器以获取资源时要使用哪种协议
user:用户，某些方案访问资源时需要的用户名
password:密码，用户对应的密码，中间用：分隔
Host:主机，资源宿主服务器的主机名或IP地址
port:端口,资源宿主服务器正在监听的端口号，很多方案有默认端口号
path:路径,服务器资源的本地名，由一个/将其与前面的URL组件分隔
params:参数，指定输入的参数，参数为名/值对，多个参数，用;分隔
query:查询，传递参数给程序，如数据库，用？分隔,多个查询用&分隔
frag:片段,一小片或一部分资源的名字，此组件在客户端使用，用#分隔
```

**URL示例**

![image-20241118144455768](images/image-20241118144455768.png)

```http
https://list.jd.com/list.html?
cat=670,671,672&ev=14_2&sort=sort_totalsales15_desc&trans=1
http://apache.org/index.html#projects-list
```

#### 1.3.4.4 网站访问量

**网站访问量统计的重要指标**

- IP(独立IP)：即Internet Protocol,指独立IP数。一天内来自相同客户机IP 地址只计算一次，记录远 程客户机IP地址的计算机访问网站的次数，是衡量网站流量的重要指标
- PV(访问量)： 即Page View, 页面浏览量或点击量，用户每次刷新即被计算一次，PV反映的是浏览 某网站的页面数，PV与来访者的数量成正比，PV并不是页面的来访者数量，而是网站被访问的页 面数量
- UV(独立访客)：即Unique Visitor,访问网站的一台电脑为一个访客。一天内相同的客户端只被计算 一次。可以理解成访问某网站的电脑的数量。网站判断来访电脑的身份是通过cookies实现的。如 果更换了IP后但不清除cookies，再访问相同网站，该网站的统计中UV数是不变的

**网站统计：** http://www.alexa.cn/rank/ 

范例：网站访问统计

```bash
1. 甲乙丙三人在同一台通过 ADSL 上网的电脑上（中间没有断网），分别访问 www.wang.com 网站，并
且每人共用一个浏览器，各个浏览了2个页面，那么网站的流量统计是：
IP: 1 PV:6   UV：1

2. 若三人都是ADSL重新拨号后,各个使用不同的浏览器，分别浏览了2个页面，则
IP: 3 PV:6 UV：3
```

**网站访问量 PV,IP,UV统计方法**

- 使用文本工具, 比如awk提取IP，sort排序、uniq统计去重后统计IP数
- 第三方统计工具进行pv统计，比如: 百度统计、腾讯分析、piwik、开发自研统计平台。

### 1.3.5 HTTP工作机制

一次http事务包括：

- http请求：http request
- http响应：http response

**Web资源：** web resource， 一个网页由多个资源（文件）构成，打开一个页面，通常会有多个资源展 示出来，但是每个资源都要单独请求。因此，一个"Web 页面”通常并不是单个资源，而是一组资源的集 合

**资源类型：**

- 静态文件：无需服务端做出额外处理,服务器端和客户端的文件内容相同

  常见文件后缀：.html, .txt, .jpg, .js, .css, .mp3, .avi

- 动态文件：服务端执行程序，返回执行的结果,服务器端和客户端的文件内容不相同

  常见文件后缀：.php, .jsp ,.asp

**HTTP连接请求**

![image-20241118145444134](images/image-20241118145444134.png)

**串行和并行连接**

![image-20241118145643993](images/image-20241118145643993.png)

**串行,持久连接和管道**

![image-20241118145731410](images/image-20241118145731410.png)

**提高HTTP连接性能**

- 并行连接：通过多条TCP连接发起并发的HTTP请求
- 持久连接：keep-alive，重用TCP连接，以消除连接和关闭的时延,以事务个数和时间来决定是否关 闭连接
- 管道化连接：通过共享TCP连接，发起并发的多个HTTP请求,但需要也要按发起请求的顺序来接收 响应,实现难度很大,很多代理服务器和浏览器不支持
- 复用的连接：交替传送请求和响应报文（实验阶段）

### 1.3.6 HTTP 协议版本

#### 1.3.6.1 HTTP 1.X 协议

RFC Hypertext Transfer Protocol -- HTTP/1.1

```http
https://tools.ietf.org/html/rfc2616
```

![image-20241118150019225](images/image-20241118150019225.png)

**http/0.9：**

1991，原型版本，功能简陋，只有一个命令GET。GET /index.html ,服务器只能回应HTML格式字符 串，不能回应别的格式

**http/1.0**

1996年5月,支持cache, MIME, method

每个TCP连接只能发送一个请求，发送数据完毕，连接就关闭，如果还要请求其他资源，就必须再新建 一个连接。引入了POST命令和HEAD命令头信息是 ASCII 码，后面数据可为任何格式。服务器回应时会告 诉客户端，数据是什么格式，即Content-Type字段的作用。这些数据类型总称为MIME 多用途互联网邮 件扩展，每个值包括一级类型和二级类型，预定义的类型，也可自定义类型, 常见Content-Type值： text/xml image/jpeg audio/mp3

**http/1.1**

1997年1月，引入了持久连接（persistent connection），即TCP连接默认不关闭，可以被多个请求复 用，不用声明Connection: keep-alive。对于同一个域名，大多数浏览器允许同时建立6个持久连接引入 了管道机制，即在同一个TCP连接里，客户端可以同时发送多个请求，进一步改进了HTTP协议的效率

新增方法：PUT、PATCH、OPTIONS、DELETE

同一个TCP连接里，所有的数据通信是按次序进行的。服务器只能顺序处理回应，前面的回应慢，会有 许多请求排队，造成"队头堵塞"（Head-of-line blocking）

为避免上述问题，两种方法：一是减少请求数，二是同时多开持久连接。

网页优化技巧，如合并脚本和样式表、将图片嵌入CSS代码、域名分片（domain sharding）等

HTTP 协议不带有状态，每次请求都必须附上所有信息。请求的很多字段都是重复的，浪费带宽，影响 速度

**HTTP1.0和HTTP1.1的区别**

![image-20241118150543705](images/image-20241118150543705.png)

- 缓存处理，在HTTP1.0中主要使用header里的If-Modified-Since,Expires来做为缓存判断的标准， HTTP1.1则引入了更多的缓存控制策略例如Entity tag，If-Unmodified-Since, If-Match, If-NoneMatch等更多可供选择的缓存头来控制缓存策略
- 带宽优化及网络连接的使用，HTTP1.0中，存在一些浪费带宽的现象，例如：客户端只是需要某个 对象的一部分，而服务器却将整个对象送过来了，并且不支持断点续传功能，HTTP1.1则在请求头 引入了range头域，它允许只请求资源的某个部分，即返回码是206（Partial Content），方便了 开发者自由的选择以便于充分利用带宽和连接
- 错误通知的管理，在HTTP1.1中新增24个状态响应码，如409（Conflict）表示请求的资源与资源当 前状态冲突；410（Gone）表示服务器上的某个资源被永久性的删除
- Host 头处理，在HTTP1.0中认为每台服务器都绑定一个唯一的IP地址，因此，请求消息中的URL并 没有传递主机名（hostname）。但随着虚拟主机技术的发展，在一台物理服务器上可以存在多个 虚拟主机（Multi-homed Web Servers），并且它们共享一个IP地址。HTTP1.1的请求消息和响应 消息都应支持Host头域，且请求消息中如果没有Host头域会报告一个错误（400 Bad Request）
- 长连接，HTTP 1.1支持持久连接（PersistentConnection）和请求的流水线（Pipelining）处理， 在一个TCP连接上可以传送多个HTTP请求和响应，减少了建立和关闭连接的消耗和延迟，在 HTTP1.1中默认开启Connection： keep-alive，弥补了HTTP1.0每次请求都要创建连接的缺点

**HTTP1.0和1.1的问题 **

- HTTP1.x在传输数据时，每次都需要重新建立连接，无疑增加了大量的延迟时间，特别是在移动端 更为突出
- HTTP1.x在传输数据时，所有传输的内容都是明文，客户端和服务器端都无法验证对方的身份，无 法保证数据的安全性
- HTTP1.x在使用时，header里携带的内容过大，增加了传输的成本，并且每次请求header基本不 怎么变化，尤其在移动端增加用户流量
- 虽然HTTP1.x支持了keep-alive，来弥补多次创建连接产生的延迟，但是keep-alive使用多了同样会 给服务端带来大量的性能压力，并且对于单个文件被不断请求的服务(例如图片存放网站)，keepalive可能会极大的影响性能，因为它在文件被请求之后还保持了不必要的连接很长时间

**HTTPS协议：**

为解决安全问题，网景在1994年创建了HTTPS，并应用在网景导航者浏览器中。 最初，HTTP是与SSL一 起使用的；在SSL逐渐演变到TLS时（其实两个是一个东西，只是名字不同而已），最新的HTTPS也由在 2000年五月公布的RFC 2818正式确定下来。HTTPS就是安全版的HTTP，目前大型网站基本实现全站 HTTPS

**HTTPS特点**

- HTTPS协议需要到CA申请证书，一般免费证书很少，需要交费
- HTTP协议运行在TCP之上，所有传输的内容都是明文，HTTPS运行在SSL/TLS之上，SSL/TLS运行 在TCP之上，所有传输的内容都经过加密的
- HTTP和HTTPS使用的是不同的连接方式，端口不同，前者是80，后者是443
- HTTPS可以有效的防止运营商劫持，解决了防劫持的一个大问题
- HTTPS 实现过程降低用户访问速度，但经过合理优化和部署，HTTPS 对速度的影响还是可以接受 的

#### 1.3.6.2 HTTP 2.0 协议

**SPDY协议**

SPDY：2009年谷歌研发，综合HTTPS和HTTP两者有点于一体的传输协议，主要特点：

- 降低延迟，针对HTTP高延迟的问题，SPDY优雅的采取了多路复用（multiplexing）。多路复用通 过多个请求stream共享一个tcp连接的方式，解决了HOL blocking的问题，降低了延迟同时提高了 带宽的利用率
- 请求优先级（request prioritization）。多路复用带来一个新的问题是，在连接共享的基础之上有 可能会导致关键请求被阻塞。SPDY允许给每个request设置优先级，重要的请求就会优先得到响 应。比如浏览器加载首页，首页的html内容应该优先展示，之后才是各种静态资源文件，脚本文件 等加载，可以保证用户能第一时间看到网页内容
- header压缩。HTTP1.x的header很多时候都是重复多余的。选择合适的压缩算法可以减小包的大 小和数量
- 基于HTTPS的加密协议传输，大大提高了传输数据的可靠性
- 服务端推送（server push），采用了SPDY的网页，例如网页有一个sytle.css的请求，在客户端收 到sytle.css数据的同时，服务端会将sytle.js的文件推送给客户端，当客户端再次尝试获取sytle.js时 就可以直接从缓存中获取到，不用再发请求了

**HTTP2协议**

http/2.0：2015年发布，HTTP2.0是SPDY的升级版

- 头信息和数据体都是二进制，称为头信息帧和数据帧
- 复用TCP连接，在一个连接里，客户端和浏览器都可以同时发送多个请求或回应，且不用按顺序响 应，避免了"队头堵塞",此双向的实时通信称为多工（Multiplexing）
- 引入头信息压缩机制（header compression）,头信息使用gzip或compress压缩后再发送；客户端 和服务器同时维护一张头信息表，所有字段都会存入这个表，生成一个索引号，不发送同样字段， 只发送索引号，提高速度
- HTTP/2 允许服务器有新数据时未经请求，主动向客户端发送资源，而无需客户端拉取,即服务器推 送（server push）

**HTTP2.0和SPDY区别：**

- HTTP2.0 支持明文 HTTP 传输，而 SPDY 强制使用 HTTPS
- HTTP2.0 消息头的压缩算法采用 HPACK，而非 SPDY 采用的 DEFLATE

**HTTP 版本速度比较**

```http
https://http2.akamai.com/demo/http2-lab.html
```

#### 1.3.6.3 HTTP 3.0 协议

![image-20241118151859132](images/image-20241118151859132.png)

![image-20241118151909983](images/image-20241118151909983.png)

2020年发布 HTTP/3 的草案,2022年6月正式发布,使用QUIC(基于UDP协议)的新协议代替TCP

它在传输层引入流作为一等公民,多个QUIC流共享相同的快速连接,因此不需要额外的握手,来创建新连 接,QUIC流是独立交付的,在大多数情况下，丢包仅影响一个流,并不影响其他流,这就是QUIC 在传输层消 除队头阻塞的方法

QUIC是为移动互联网重度使用而设计的,携带智能手机的人们经常从一个网络切换到另一个网络,如果使 用TCP,从一个网络切换到另一个网络是很慢的

QUIC实现了一个称为连接ID的概念,它允许连接在IP地址和网络接口之间快速可靠地移动

尽管HTTP/3刚刚发布,号称已经有25%的网站开始使用,许多浏览器也支持它

![image-20241118152059997](images/image-20241118152059997.png)

QUIC的数据包格式

从协议栈可以看出:QUIC = HTTP/2 + TLS + UDP

![image-20241118152141065](images/image-20241118152141065.png)

![image-20241118152150811](images/image-20241118152150811.png)

QUIC的数据包分为Header和Data部分，其中Header是明文传输，包括Flags是标志位，Connection ID 是连接ID，可用于连接迁移，QUIC Version是QUIC的版本号，Packet Number是包序号，用于保证可 靠传输；Data部分是密文传输，是一些数据帧，有很多数据帧类型：Stream、ACK、Padding、 Blocked等，其中Stream帧传输应用数据。

Stream

![image-20241118152236474](images/image-20241118152236474.png)

### 1.3.7 HTTP 请求访问的完整过程

![image-20241118152305998](images/image-20241118152305998.png)

**一次完整的http请求处理过程**

1、建立连接：接收或拒绝连接请求

2、接收请求：接收客户端请求报文中对某资源的一次请求的过程

Web访问响应模型（Web I/O）

![image-20241118152432414](images/image-20241118152432414.png)

- 单进程I/O模型：启动一个进程处理用户请求，而且一次只处理一个，多个请求被串行响应
- 多进程I/O模型：并行启动多个进程,每个进程响应一个连接请求
- 复用I/O结构：启动一个进程，同时响应N个连接请求
- 复用的多进程I/O模型：启动M个进程，每个进程响应N个连接请求，同时接收M*N个请求

3、处理请求：服务器对请求报文进行解析，并获取请求的资源及请求方法等相关信息，根据方法，资 源，首部和可选的主体部分对请求进行处理

常用请求Method: GET、POST、HEAD、PUT、DELETE、TRACE、OPTIONS

4、访问资源：

   服务器获取请求报文中请求的资源web服务器，即存放了web资源的服务器，负责向请求者提供对方 请求的静态资源，或动态运行后生成的资源

5、构建响应报文：

   一旦Web服务器识别除了资源，就执行请求方法中描述的动作，并返回响应报文。响应报文中 包含 有响应状态码、响应首部，如果生成了响应主体的话，还包括响应主体

1）响应实体：如果事务处理产生了响应主体，就将内容放在响应报文中回送过去。响应报文中通常包 括：

​     描述了响应主体MIME类型的Content-Type首部

​     描述了响应主体长度的Content-Length 

​      实际报文的主体内容

2）URL重定向：web服务构建的响应并非客户端请求的资源，而是资源另外一个访问路径

3）MIME类型： Web服务器要负责确定响应主体的MIME类型。多种配置服务器的方法可将MIME类型 与资源管理起来

6、发送响应报文

   Web服务器通过连接发送数据时也会面临与接收数据一样的问题。服务器可能有很多条到各个客户 端的连接，有些是空闲的，有些在向服务器发送数据，还有一些在向客户端回送响应数据。服务器要记 录连接的状态，还要特别注意对持久连接的处理。对非持久连接而言，服务器应该在发送了整条报文之 后，关闭自己这一端的连接。对持久连接来说，连接可能仍保持打开状态，在这种情况下，服务器要正 确地计算Content-Length首部，不然客户端就无法知道响应什么时候结束

7、记录日志

  最后，当事务结束时，Web服务器会在日志文件中添加一个条目，来描述已执行的事务

## 1.4 HTTP 协议报文头部结构

http协议：http/0.9, http/1.0, http/1.1, http/2.0，http/3.0 

http协议：stateless 无状态, 服务器无法持续追踪访问者来源

解决http协议无状态方法

- cookie 客户端存放 
- session 服务端存放

http事务：一次访问的过程

- 请求：request 
- 响应：response

HTTP报文结构

协议查看或分析的工具：tcpdump, wireshark,tshark

参考资料：https://developer.mozilla.org/zh-CN/docs/Web/HTTP

### 1.4.1 HTTP 请求报文

![image-20241118153718936](images/image-20241118153718936.png)

**request报文格式**

```http
<method> <request-URL> <version>
<headers>
<entity-body>
```

范例：

```bash
GET / HTTP/1.1
Accept: */*
Accept-Encoding: gzip, deflate
Connection: keep-alive
Host: www.wanglei.org
User-Agent: HTTPie/0.9.4

```

### 1.4. 2  H T T P 响 应 报 文

![image-20241118154144339](images/image-20241118154144339.png)

**response报文格式**

```http
<version> <status> <reason-phrase>
<headers>
<entity-body>
```

范例：

```shell
HTTP/1.1 200 OK
Cache-Control: max-age=3, must-revalidate
Connection: keep-alive
Content-Encoding: gzip
Content-Type: text/html; charset=UTF-8
Date: Thu, 07 Nov 2024 03:44:14 GMT
Server: Tengine
Transfer-Encoding: chunked
Vary: Accept-Encoding
Vary: Accept-Encoding, Cookie
```

### 1.4.3 HTTP报文格式详解

#### 1.4.3.1 Method 方法

请求方法，标明客户端希望服务器对资源执行的动作，包括以下：

- GET： 从服务器获取一个资源
- HEAD： 只从服务器获取文档的响应首部
- POST： 向服务器输入数据，通常会再由网关程序继续处理
- PUT： 将请求的主体部分存储在服务器中，如上传文件
- DELETE： 请求删除服务器上指定的文档
- TRACE： 追踪请求到达服务器中间经过的代理服务器
- OPTIONS：请求服务器返回对指定资源支持使用的请求方法
- CONNECT：建立一个到由目标资源标识的服务器的隧道
- PATCH：用于对资源应用部分修改

#### 1.4.3.2 version版本

```http
HTTP/<major>.<minor>
```

范例：

```http
HTTP/1.1
```

#### 1.4.3.3 status 状态码

![image-20241118154626500](images/image-20241118154626500.png)

![image-20241118154648254](images/image-20241118154648254.png)

三位数字，标记请求处理过程中发生的情况

参考资料：https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status

**http协议状态码分类**

```http
1xx：100-101 信息提示
2xx：200-206 成功
3xx：300-307 重定向
4xx：400-415 错误类信息，客户端错误
5xx：500-505 错误类信息，服务器端错误
```

**http协议常用的状态码**

```http
200： 成功，请求数据通过响应报文的entity-body部分发送;OK
301： Moved Permanently,请求的URL指向的资源已经被删除；但在响应报文中通过首部Location指明
了资源现在所处的新位置
302： Moved Temporarily,响应报文Location指明资源临时新位置 
304： 客户端发出了条件式请求，但服务器上的资源未曾发生改变，则通过响应此响应状态码通知客户端；
Not Modified,但无需再发送原始数据即实体给客户端
307: 浏览器内部重定向，而无需再向服务器发送请求
401： 需要输入账号和密码认证方能访问资源；Unauthorized
403： 请求被禁止；Forbidden,一般是因为权限错误或主页文件不存在
404： 服务器无法找到客户端请求的资源；Not Found
405： 表明服务器禁止了使用当前 HTTP 方法的请求 ethod Not Allowed 
413： 上传的资源超过了最大限制值
499： 客户端主动断开连接。然而在实际业务开发中，当出现 HTTP 499 状态码时，大部分都是由于服务端
请求时间过长，导致客户端等的“不耐烦”了，因此断开了连接。比如：慢SQL问题，499是客户端读超时关闭
连接造成的，推荐从超时时间或者优化响应速度入手,web服务器发现客户端主动关闭连接后，记录到access
日志中的。可能是客户端接收响应超时了,可以先在客户端统计下是不是这个原因，再调查为什么会导致超时
500： 服务器内部错误；Internal Server Error,比如:cgi程序没有执行权限,或连接数据库失
败,rewrite死循环
502： Bad Gateway,代理服务器从后端服务器收到了一条错误响应或伪响应，如无法连接到网关；Bad 
Gateway,比如:后端服务端口没有打开,或后端服务不可用或关机,iptable -j REJECT,确定服务器是
down,相当于"确定人不存在了"
503： 服务不可用，临时服务器维护或过载，服务器无法处理请求,比如:超过连接数和连接频率
504： Gateway Timeout,网关超时,或者后端服务器无回应报文,比如:服务端口虽然打开,但服务返回结果
时间过长,iptable -j DROP,不确定服务器down,相当于"人失踪了,不确定存在或不存在"
```

#### 1.4.3.4 reason-phrase原因短语

状态码所标记的状态的简要描述

#### 1.4.3.5 headers首部字段头

首部字段包含的信息最为丰富。首部字段同时存在于请求和响应报文内，并涵盖 HTTP 报文相关的内容 信息。使用首部字段是为了给客服端和服务器端提供报文主体大小、所使用的语言、认证信息等内容

首部字段是由首部字段名和字段值构成的，中间用冒号"：”分隔字段值对应，即key/value 键/值对 

单个 HTTP 首部字段可以有多个值

参考资料：https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers

#### 1.4.3.6 entity-body实体

请求时附加的数据或响应时附加的数据，例如：登录网站时的用户名和密码，博客的上传文章，论坛上 的发言等。

#### 1.4.4 Cookie 和 Session

![image-20241118155621478](images/image-20241118155621478.png)

无状态协议是指协议对事物处理没有记忆能力。缺少状态意味着如果后续处理需要前面的信息，则必须 重传，这样可能导致每次连接传送的数据量增大。另一方面，在服务器不需要先前信息时它应答就很快。

HTTP是超本文传输协议，顾名思义，这个协议支持超文本的传输。什么是超文本？说白了就是使用 HTML编写的页面。通常，我们使用客户端浏览器访问服务器的资源，最常见的URL也是以html为后缀 的文件，因此可以说超文本是网络上最主要的资源。

既然HTTP协议的目的是在于支持超文本的传输，也就是资源的传输，那么客户端浏览器向HTTP服务器 发送请求，继而HTTP服务器将相信资源发回给客户端这样一个过程中，无论对于客户端还是服务器，都 没有必要记录这个过程，因为每一次请求和响应都是相对独立的，一般而言，一个URL对应着一个唯一 的超文本，正是因为这样的唯一性，使得记录用户的行为状态变得毫无意义，所以，HTTP协议被设计为 无状态的连接协议符合它本身的需求。

HTTP协议这种特性有优点也有缺点，优点在于解放了服务器，每一次请求"点到为止"，不会造成不必要 的连接占用，缺点在于如果为了保留状态，每次请求都会传输大量的重复信息内容。

可是随着 Web 的不断发展，很多业务都需要对通信状态进行保存.

如果是一次性会话的过程： 打开浏览器 -> 访问一些服务器内容 -> 关闭浏览器

但目前有很多WEB访问场景，并不是一次性会话，而是多次相关的会话，比如：

登录场景：

打开浏览器 -> 浏览到登陆页面 -> 输入用户名和密码 -> 访问到用户主页(显示用户名) -> 修改密码（输入 原密码）-> 修改收货地址....... 

问题：在此处登录会话过程中产生的数据（用户会话数据）如何保存下来呢？

购物场景：

打开浏览器 -> 浏览商品列表 -> 加入购物车(把商品信息保存下来) -> 关闭浏览器

打开浏览器-> 直接进入购物车 -> 查看到上次加入购物车的商品 -> 下订单 -> 支付

问题： 在购物会话过程中，如何保存商品信息？

以上场景都需要保留会话数据，需要会话管理机制。

会话管理： 管理浏览器客户端和服务器端之间会话过程中产生的会话数据。

为了会话管理，HTTP就需要传输大量重复信息内容的问题，造成大量的网络带宽消耗。于是 Cookie 和  Session 技术闪亮登场了，它们可以为用户进行会话管理，实现保存状态。

#### 1.4.4.1 Cookie

Cookie 又称为"小甜饼”。类型为"小型文本文件”，指某些网站为了辨别用户身份而储存在用户本地终端 （Client Side）上的数据（通常经过加密）。由网景公司的前雇员卢·蒙特利在1993年3月发明

因为HTTP协议是无状态的，即服务器不知道用户上一次做了什么，这严重阻碍了交互式Web应用程序的 实现。在典型的网上购物场景中，用户浏览了几个页面，买了一盒饼干和两瓶饮料。最后结帐时，由于 HTTP的无状态性，不通过额外的手段，服务器并不知道用户到底买了什么，所以Cookie就是用来绕开 HTTP的无状态性的"额外手段”之一。服务器可以设置或读取Cookies中包含信息，借此维护用户跟服务 器会话中的状态。

在上面的购物场景中，当用户选购了第一项商品，服务器在向用户发送网页的同时，还发送了一段 Cookie，记录着那项商品的信息。当用户访问另一个页面，浏览器会把Cookie发送给服务器，于是服务 器知道他之前选购了什么。用户继续选购饮料，服务器就在原来那段Cookie里追加新的商品信息。结帐 时，服务器读取发送来的Cookie就行了。

Cookie基于HTTP协议，也叫Web Cookie或浏览器Cookie，是服务器发送到用户浏览器并保存在客户端 本地的一小块数据，它会在浏览器下次向同一服务器再发起请求时被携带并发送到服务器上。通常，它 用于告知服务端两个请求是否来自同一浏览器，如保持用户的登录状态。Cookie使基于无状态的HTTP 协议记录稳定的状态信息成为了可能。

**cookie 的获取过程**

![image-20241118160510745](images/image-20241118160510745.png)



- 第一次请求过程

  浏览器第一次发送请求时,不会携带任何cookie信息

  服务器接收到请求之后，发现请求中没有任何cookie信息

  服务器生成和设置一个cookie，并将此cookie设置通过set_cookie的首部字段保存在响应报文中返 回给浏览器

  浏览器接收到这个响应报文之后,发现里面有cookie信息,浏览器会将cookie信息保存起来

- 第二次及其之后的过程

  当浏览器第二次及其之后的请求报文中自动 cookie的首部字段携带第一次响应报文中获取的cookie 信息

  服务器再次接收到请求之后,会发现请求中携带的cookie信息,这样的话就认识是谁发的请求了

  之后的响应报文中不会再添加set_cookie首部字段

 Cookie主要用于以下三个方面：

- 会话状态管理（如用户登录状态、购物车、游戏分数或其它需要记录的信息）
- 个性化设置（如用户自定义设置、主题等）
- 浏览器行为跟踪（如跟踪分析用户行为等）

使用 Cookie 的状态管理

Cookie 技术通过在请求和响应报文中写入 Cookie 信息来控制客户端的状态。当服务器收到HTTP请求 时，服务器可以在响应头里面添加一个Set-Cookie选项。浏览器收到响应后通常会保存下Cookie，之后 对该服务器每一次请求中都通过Cookie请求头部将Cookie信息发送给服务器。服务器端发现客户端发送 过来的 Cookie 后，会去检查究竟是从哪一个客户端发来的连接请求，然后对比服务器上的记录，最后 得到之前的状态信息.另外，Cookie的过期时间、域、路径、有效期、适用站点都可以根据需要来指定。

**Set-Cookie首部字段**

- NAME=VALUE 赋予 Cookie 的名称和其值,此为必需项

- expires=DATE Cookie 的有效期，若不明确指定则默认为浏览器关闭前为止

  **会话期Cookie**

  基于内存保存，会话期Cookie是最简单的Cookie：浏览器关闭之后它会被自动删除，也就是说它 仅在会话期内有效。会话期Cookie不需要指定过期时间（Expires）或者有效期（Max-Age）。需 要注意的是，有些浏览器提供了会话恢复功能，这种情况下即使关闭了浏览器，会话期Cookie也会 被保留下来，就好像浏览器从来没有关闭一样。

  **持久性Cookie**

  基于硬盘保存，和关闭浏览器便失效的会话期Cookie不同，持久性Cookie可以指定一个特定的过 期时间（Expires）或有效期（Max-Age）。

  ```http
  Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT;
  ```

  提示：当Cookie的过期时间被设定时，设定的日期和时间只与客户端相关，而不是服务端。

- path=PATH 指定了主机下的哪些路径可以接受Cookie（该URL路径必须存在于请求URL中）。若 不指定则默认为文档所在的文件目录,以字符 %x2F ("/") 作为路径分隔符，子路径也会被匹配。

  例如，设置 `Path=/docs `，则以下地址都会匹配：

  - `/docs`
  - `/docs/Web/`
  - `/docs/Web/HTTP`

- domain=域名 指定了哪些主机可以接受Cookie。如果不指定，默认为当前文档的主机（不包含 子域名）。如果指定了Domain，则一般包含子域名。

  例如，如果设置 Domain=wang.com，则Cookie也包含子域名（如：study.wang.com）

- Secure 标记为 Secure 的Cookie只应通过被HTTPS协议加密过的请求发送给服务端。但即便设置 了 Secure 标记，敏感信息也不应该通过Cookie传输，因为Cookie有其固有的不安全性，Secure  标记也无法提供确实的安全保障。从 Chrome 52 和 Firefox 52 开始，不安全的站点（http:）无法 使用Cookie的 Secure 标记。

- HttpOnly 加以限制使 Cookie 不能被 JavaScript 脚本访问,为避免跨域脚本 (XSS) 攻击，通过 JavaScript的 Document.cookie API无法访问带有 HttpOnly 标记的Cookie，它们只应该发送给服 务端。如果包含服务端 Session 信息的 Cookie 不想被客户端 JavaScript 脚本调用，那么就应该为 其设置 HttpOnly 标记

**浏览器对cookie的限制：**

Cookie 存储的限制是不一样的。例如：单个域名可存储的 Cookie 数量、Cookie 大小等。

![image-20241118161409738](images/image-20241118161409738.png)

在进行页面 Cookie 操作的时候，应该尽量保证 Cookie 的个数小于 20 个，总大小小于 4KB，这是一个 安全且保险的范围。

范例：响应报文中的set-cookie首部

```http
HTTP/1.0 200 OK
Content-type: text/html
Set-Cookie: yummy_cookie=choco
Set-Cookie: tasty_cookie=strawberry
```

范例：请求报文中的cookie首部字段

```http
GET /sample_page.html HTTP/1.1
Host: www.example.org
Cookie: yummy_cookie=choco; tasty_cookie=strawberry
```

范例：响应报文set-cookie中的Secure 和 HttpOnly

```http
Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT; Secure; HttpOnly
```

范例：浏览器查看cookie

![image-20241118161606486](images/image-20241118161606486.png)

范例：chrome 浏览器禁止cookie

![image-20241118161807758](images/image-20241118161807758.png)



![image-20241118161817741](images/image-20241118161817741.png)



范例：php语言实现cookie的管理

```php
#设置cookie
#cat setcookie.php 
<?php
setcookie('title','cto');    #有效期为会话级
setcookie('user','wang',time()+3600*12);  #有效期为12小时
echo "<h1>test setcookie </h1>"
?>
#说明：setcookie设置的cookie，只有下一次http请求才能生效

#显示cookie
cat showcookies.php
<?php
echo "<h1>test showcookie </h1>";
echo $_COOKIE["user"];    #显示user的这一个cookie
echo "<br />";
var_dump($_COOKIE);      #显示所有cookie 
//print_r($_COOKIE);     #不如上面方式详细
?>

#删除cookie，通过设置过期时间实现
#vim delcookie.php
<?php
setcookie('user','wang',time()-3600*12);
echo "<h1>cookie:user is deleted </h1>";
?>    
```

#### 1.4.4.2 Session

![image-20241118161929967](images/image-20241118161929967.png)

**session**

session是相对于cookie的另外一个状态保持的解决方案，它是通过服务器来保持状态的。session指的 是服务器上为每个客户端所开辟的独立存储空间，在其中保存的信息就是用于保存状态的。

Session是服务器端程序运行的过程中创建的，不同语言实现的应用程序有不同创建session的方法。在 创建了session的同时，服务器会为该session生成唯一的sessionId，而这个sessionId被创建了之后， 就可以调用session相关的方法往session中增加内容了，而这些内容只会保存在服务器中，每个 sessionid就像数据库中主键，可以根据SessionId 关联每个session的相关信息，比如：购物车里的商 器，登录用户等。但发送给客户端浏览器的只有sessionId。当客户端浏览器再次发送http请求时，会自 动地将这个sessionId 附加在请求报文中 ，服务器收到请求之后就会根据sessionId找到对应的 session，从而再次使用，使得用户的状态得以保持。

每个session都有一个sessionId，这个ID存放有两种方式：

1、通过URL存取，比如：Java程序中，URL会带上一个jsessionId=xxxxxx等，这样每次重新请求的时候 都传了sessionId给服务器,但此方式不安全,所以很少使用,所以一般session是依赖于cookie的.即如果浏 览器禁用了cookie,则session无法实现

2、通过cookie存取（Tomcat默认如此），这种cookie是session cookie，区别于persistent cookies也 就是我们常说的cookie，session cookie要注意的是存储在浏览器内存中，而不是写到硬盘上。程序一 开始执行，服务器就生成一个sessionId并通过cookie携带客户端浏览器的缓存中，当下一次访问的时 候，服务器先检测一下是否有这个cookie，如果有就取它的ID，如果没有就再生成一个。这就是为什么 关闭浏览器之后，再进去session已经没有了，其实在服务器端session并没有清空，而是sessionId变 了。

当将浏览器关闭，服务器保存的session数据不是立即释放的，此时数据还会存在一段时间（可以在程序 中加以设置，Tomcat默认15分钟），只要我们知道那个sessionId，就可以继续通过请求获得此session 的信息。session里面的数据都放在服务器端，通过sessionId保证不会访问错误，服务端自动对session 进行管理，如果在规定的时间内没有访问，则释放掉这个session。

最后提两点：

1、sessionId通常在浏览器地址中是看不到的，但是当我们把浏览器的cookie禁止之后，Web服务器会 采用URL重写的方式传递sessionId，这样就可以在地址栏看到sessionId了

2、session cookie不可以跨窗口使用，但可以跨同一个窗口的多个标签页。

**session 的工作流程**

第一次请求:

- 浏览器发起第一次请求的时候可以携带一些信息(比如: 用户名/密码) cookie中没有任何信息
- 当服务器接收到这个请求之后,进行用户名和密码的验证,验证成功后则可以设置session信息
- 在设置session信息的同时(session信息保存在服务器端) .服务器会在响应头中设置一个随机的 session id的cookie信息
- 客户端(浏览器)在接收到响应之后,会将cookie信息保存起来(保存session id的信息)

客户端(浏览器)在接收到响应之后,会将cookie信息保存起来(保存session id的信息)

- 第二次及其之后的请求都会携带session id信息
- 当服务器接收到这个请求之后,会获取到session id信息,然后进行验证
- 验证成功,则可以获取session信息(session信息保存在服务器端)

**范例：PHP的PHPSESSID**

```php
<?php
session_start(); 
echo session_id();
?>
#执行结果如下图
```

![image-20241118162558111](images/image-20241118162558111.png)

**范例：JAVA的JSESSIONID**

```bash
[root@centos8 ~]#cat /usr/local/tomcat/webapps/ROOT/session.jsp 
<h1>
sessionId: <%=request.getSession().getId()%> 
</h1>
```

![image-20241118162629263](images/image-20241118162629263.png)

![image-20241118162642149](images/image-20241118162642149.png)

![image-20241118162649821](images/image-20241118162649821.png)

#### 1.4.4.3 Cookie 和 Session 比较

cookie和session的相同和不同：

- cookie通常是在服务器生成,但也可以在客户端生成,session是在服务器端生成的
- session 将数据信息保存在服务器端，可以是内存，文件，数据库等多种形式,cookie 将数据保存在 客户端的内存或文件中
- 单个cookie保存的数据不能超过4K，每个站点cookie个数有限制，比如IE8为50个、Firefox为50 个、Opera为30个；session存储在服务器，没有容量限制 
- cookie存放在用户本地，可以被轻松访问和修改，安全性不高；session存储于服务器，比较安全
- cookie有会话cookie和持久cookie，生命周期为浏览器会话期的会话cookie保存在缓存，关闭浏 览器窗口就消失，持久cookie被保存在硬盘，知道超过设定的过期时间；随着服务端session存储 压力增大，会根据需要定期清理session数据 
- session中有众多数据，只将sessionID这一项可以通过cookie发送至客户端进行保留，客户端下次 访问时，在请求报文中的cookie会自动携带sessionID，从而和服务器上的的session进行关联

cookie缺点：

1、使用cookie来传递信息，随着cookie个数的增多和访问量的增加，它占用的网络带宽也很大，试想假 如cookie占用200字节，如果一天的PV有几个亿，那么它要占用多少带宽？

2、cookie并不安全，因为cookie是存放在客户端的，所以这些cookie可以被访问到，设置可以通过插 件添加、修改cookie。所以从这个角度来说，我们要使用sesssion，session是将数据保存在服务端的， 只是通过cookie传递一个sessionId而已，所以session更适合存储用户隐私和重要的数据

session 缺点：

1、不容易在多台服务器之间共享，可以使用session绑定，session复制，session共享解决

2、session存放在服务器中，所以session如果太多会非常消耗服务器的性能

cookie和session各有优缺点，在大型互联网系统中，单独使用cookie和session都是不可行的

## 1.5 Web 相关工具

### 1.5.1 links

格式：

```http
links [OPTION]... [URL]...
```

常用选项：

- -dump 非交互式模式，显示输出结果
- -source 打印源码

### 1.5.2 wget

格式：

```http
wget [OPTION]... [URL]...
```

常用选项：

```bash
#启动
-V, -version 显示wget的版本后退出
-h, -help 打印语法帮助
-b, -background 启动后转入后台执行
-e, -execute=COMMAND 执行`.wgetrc'格式的命令，wgetrc格式参见/etc/wgetrc或~/.wgetrc

#记录和输入文件
-o, -output-file=FILE 把记录写到FILE文件中
-a, -append-output=FILE 把记录追加到FILE文件中
-d, -debug 打印调试输出
-q, -quiet 安静模式(没有输出)
-v, -verbose 冗长模式(这是缺省设置)
-nv, -non-verbose 关掉冗长模式，但不是安静模式
-i, -input-file=FILE 下载在FILE文件中出现的URLs
-F, -force-html 把输入文件当作HTML格式文件对待
-B, -base=URL 将URL作为在-F -i参数指定的文件中出现的相对链接的前缀
-sslcertfile=FILE 可选客户端证书
-sslcertkey=KEYFILE 可选客户端证书的KEYFILE
-egd-file=FILE 指定EGD socket的文件名

#下载
-bind-address=ADDRESS
指定本地使用地址(主机名或IP，当本地有多个IP或名字时使用)
-t, -tries=NUMBER 设定最大尝试链接次数(0 表示无限制).
-O -output-document=FILE 把文档写到FILE文件中
-nc, -no-clobber 不要覆盖存在的文件或使用.#前缀
-c, -continue 接着下载没下载完的文件
-progress=TYPE 设定进程条标记
-N, -timestamping 不要重新下载文件除非比本地文件新
-S, -server-response 打印服务器的回应
-spider 不下载任何东西
-T, -timeout=SECONDS 设定响应超时的秒数
-w, -wait=SECONDS 两次尝试之间间隔SECONDS秒
-waitretry=SECONDS 在重新链接之间等待1…SECONDS秒
-random-wait 在下载之间等待0…2*WAIT秒
-Y, -proxy=on/off 打开或关闭代理
-Q, -quota=NUMBER 设置下载的容量限制
-limit-rate=RATE 限定下载输率


#目录
-nd -no-directories 不创建目录
-x, -force-directories 强制创建目录
-nH, -no-host-directories 不创建主机目录
-P, -directory-prefix=PREFIX 将文件保存到目录 PREFIX/…
-cut-dirs=NUMBER 忽略 NUMBER层远程目录

#HTTP 选项
-http-user=USER 设定HTTP用户名为 USER.
-http-passwd=PASS 设定http密码为 PASS.
-C, -cache=on/off 允许/不允许服务器端的数据缓存 (一般情况下允许).
-E, -html-extension 将所有text/html文档以.html扩展名保存
-ignore-length 忽略 `Content-Length'头域
-header=STRING 在headers中插入字符串 STRING
-proxy-user=USER 设定代理的用户名为 USER
-proxy-passwd=PASS 设定代理的密码为 PASS
-referer=URL 在HTTP请求中包含 `Referer: URL'头
-s, -save-headers 保存HTTP头到文件
-U, -user-agent=AGENT 设定代理的名称为 AGENT而不是 Wget/VERSION.
-no-http-keep-alive 关闭 HTTP活动链接 (永远链接).
-cookies=off 不使用 cookies.
-load-cookies=FILE 在开始会话前从文件 FILE中加载cookie
-save-cookies=FILE 在会话结束后将 cookies保存到 FILE文件中

#FTP 选项
-nr, -dont-remove-listing 不移走 `.listing'文件
-g, -glob=on/off 打开或关闭文件名的 globbing机制
-passive-ftp 使用被动传输模式 (缺省值).
-active-ftp 使用主动传输模式
-retr-symlinks 在递归的时候，将链接指向文件(而不是目录)

#递归下载
-r, -recursive 递归下载－－慎用!
-l, -level=NUMBER 最大递归深度 (inf 或 0 代表无穷).
-delete-after 在现在完毕后局部删除文件
-k, -convert-links 转换非相对链接为相对链接
-K, -backup-converted 在转换文件X之前，将之备份为 X.orig
-m, -mirror 等价于 -r -N -l inf -nr.
-p, -page-requisites 下载显示HTML文件的所有图片

#递归下载中的包含和不包含(accept/reject)
-A, -accept=LIST 分号分隔的被接受扩展名的列表
-R, -reject=LIST 分号分隔的不被接受的扩展名的列表
-D, -domains=LIST 分号分隔的被接受域的列表
-exclude-domains=LIST 分号分隔的不被接受的域的列表
-follow-ftp 跟踪HTML文档中的FTP链接
-follow-tags=LIST 分号分隔的被跟踪的HTML标签的列表
-G, -ignore-tags=LIST 分号分隔的被忽略的HTML标签的列表
-H, -span-hosts 当递归时转到外部主机
-L, -relative 仅仅跟踪相对链接
-I, -include-directories=LIST 允许目录的列表
-X, -exclude-directories=LIST 不被包含目录的列表
-np, -no-parent 不要追溯到父目录
```

常用选项: 

```bash
-q 静默模式
-c 断点续传
-P /path 保存在指定目录
-O filename 保存为指定文件名，filename 为 - 时，发送至标准输出
--limit-rate= 指定传输速率，单位K，M等
```

范例：

```bash
[root@centos8 ~]#wget --limit-rate 1M -P /data 
https://mirrors.aliyun.com/centos/8/isos/x86_64/CentOS-8-x86_64-1905-dvd1.iso
--2019-12-12 13:02:18-- https://mirrors.aliyun.com/centos/8/isos/x86_64/CentOS8-x86_64-1905-dvd1.iso
Resolving
 mirrors.aliyun.com (mirrors.aliyun.com)... 27.221.92.112, 
119.167.168.225, 61.240.128.248, ...
Connecting to mirrors.aliyun.com (mirrors.aliyun.com)|27.221.92.112|:443... 
connected.
HTTP request sent, awaiting response... 200 OK
Length: 7135559680 (6.6G) [application/octet-stream]
Saving to: ‘/data/CentOS-8-x86_64-1905-dvd1.iso’
CentOS-8-x86_64-1905-dvd1.iso              100%
[===============================================================================
=========>]   6.65G  1.04MB/s    in 1h 53m  
2019-12-12 14:55:45 (1024 KB/s) - ‘/data/CentOS-8-x86_64-1905-dvd1.iso’ saved 
[7135559680/7135559680]

[root@centos8 ~]#ls /data
CentOS-8-x86_64-1905-dvd1.iso
```

范例：实现浏览器功能

```bash
[root@centos8 ~]#wget -qO - http://10.0.0.6/
<h1>welcome to wang.org</1>
```

范例: 下载指定目录

```bash
[root@centos8 ~]#wget -r -np -nH -R index.html http://www.example.com/dir/
[root@centos8 ~]#wget -c -r -np -k -L -p http://www.example.com/dir/

-r : 遍历所有子目录
-np : 不到上一层子目录去
-nH : 不要将文件保存到主机名文件夹
-R index.html : 不下载 index.html 文件
```

### 1.5.3 curl

curl是基于URL语法在命令行方式下工作的文件传输工具，它支持FTP, FTPS, HTTP, HTTPS, GOPHER,  TELNET, DICT, FILE及LDAP等协议。curl支持HTTPS认证，并且支持HTTP的POST、PUT等方法， FTP上 传， kerberos认证，HTTP上传，代理服务器，cookies，用户名/密码认证， 下载文件断点续传，上载 文件断点续传, http代理服务器管道（ proxy tunneling），还支持IPv6，socks5代理服务器，通过http 代理服务器上传文件到FTP服务器等，功能十分强大

格式：

```bash
curl [options] [URL...]
```

常见选项：

```bash
-A/--user-agent <string> 设置用户代理发送给服务器
-e/--referer <URL> 来源网址
--cacert <file> CA证书 (SSL)
-k/--insecure   允许忽略证书进行 SSL 连接
--compressed 要求返回是压缩的格式
-H/--header "key:value” 自定义首部字段传递给服务器
-i 显示页面内容，包括报文首部信息
-I/--head 只显示响应报文首部信息
-D/--dump-header <file>将url的header信息存放在指定文件中
--basic 使用HTTP基本认证
-u/--user <user[:password]>设置服务器的用户和密码
-L   如果有3xx响应码，重新发请求到新位置
-O 使用URL中默认的文件名保存文件到本地
-o <file> 将网络文件保存为指定的文件中
--limit-rate <rate> 设置传输速度
-0/--http1.0 数字0，使用HTTP 1.0
-v/--verbose 更详细
-C 选项可对文件使用断点续传功能
-c/--cookie-jar <file name> 将url中cookie存放在指定文件中
-x/--proxy <proxyhost[:port]> 指定代理服务器地址
-X/--request <command> 向服务器发送指定请求方法
-U/--proxy-user <user:password> 代理服务器用户和密码
-T 选项可将指定的本地文件上传到FTP服务器上
--data/-d 方式指定使用POST方式传递数据
-s --silent   Silent mode
-b name=data 从服务器响应set-cookie得到值，返回给服务器
-w <format> 显示相应的指定的报文信息，如：%{http_code}，%{remote_ip}等
-m, --max-time <time> 允许最大传输时间
```

范例：利用curl 获取响应码和远程主机IP

```bash
[root@ubuntu ~]#curl -s -I -m10 -o /dev/null   -w %{http_code} 
http://www.baidu.com/
200
[root@ubuntu ~]#curl -s -I -m10 -o /dev/null   -w %{remote_ip} 
http://wangxiaochun.com/
58.87.87.99
[root@centos8 ~]#curl -s -I -m10 -o /dev/null -w %{local_ip} 
http://wangxiaochun.com/
10.0.0.8
[root@centos8 ~]#curl -s -I -m10 -o /dev/null -w %{local_port} 
http://wangxiaochun.com/
45304
[root@centos8 ~]#curl -s -I -m10 -o /dev/null -w %{remote_port} 
http://wangxiaochun.com/
80
```

### 1.5.4 httpie

![image-20241118164246040](images/image-20241118164246040.png)

HTTPie 工具是功能丰富的 HTTP 命令行客户端，它能通过命令行界面与 Web 服务进行交互。它提供一 个简单的 http 命令，允许使用简单而自然的语法发送任意的 HTTP 请求，并会显示彩色的输出

HTTPie 能用于测试、调试及与 HTTP 服务器交互。

主要特点：

- 具表达力的和直观语法
- 格式化的及彩色化的终端输出
- 内置 JSON 支持
- 表单和文件上传
- HTTPS、代理和认证
- 自定义头部
- 持久化会话
- 类似 wget 的下载
- 支持 Python 2.7 和 3.x

官方网站：https://httpie.org

安装: Ubuntu

```bash
[root@ubuntu2204 ~#apt update && apt -y install httpie
```

### 1.5.5 压力测试工具

httpd的压力测试工具：

- ab, webbench, http_load, seige
- Jmeter 开源
- Loadrunner 商业，有相关认证
- tcpcopy：网易，复制生产环境中的真实请求，并将之保存

ab 来自httpd-tools包

命令格式

```http
ab [OPTIONS] URL 
```

常见选项:

```http
-n：总请求数
-c：模拟的并发数
-k：以持久连接模式测试
```

说明：并发数高于1024时，需要用 ulimit -n # 调整能打开的文件数

## 1.6 Web 服务介绍

Netcraft公司于1994年底在英国成立，多年来一直致力于互联网市场以及在线安全方面的咨询服务，其 中在国际上最具影响力的当属其针对网站服务器，域名解析/主机提供商，以及SSL市场所做的客观严谨 的分析研究。

https://news.netcraft.com/

![image-20241118164721400](images/image-20241118164721400.png)

### 1.6.1 Apache 经典的 Web 服务端

Apache起初由美国的伊利诺伊大学香槟分校的国家超级计算机应用中心开发，目前经历了两大版本分别 是1.X和2.X，其可以通过编译安装实现特定的功能

官方网站：http://www.apache.org

Apache HTTP服务器最初是基于阻塞式 I/O 模型实现的。在阻塞式 I/O 模型中，每个连接都需要一个单 独的线程来处理它的 I/O 操作。因此，如果有大量的并发连接，服务器将会创建大量的线程，这会导致 服务器性能下降。

为了解决这个问题，Apache 2.0 引入了基于事件驱动的架构，以提高服务器的性能和可伸缩性。在基于 事件驱动的架构中，服务器使用一组事件处理程序来处理多个连接。这些事件处理程序使用基于 select  或 epoll 的多路复用技术来处理多个连接。这使得服务器可以使用更少的线程来处理大量的连接，从而 提高了服务器的性能和可伸缩性。

因此，Apache HTTP服务器在 2.0 版本及以后的版本中使用基于事件驱动的架构，并使用基于 select 或  epoll 的多路复用技术来处理多个连接。

Apache的MPM（Multi-Processing Module）是Apache服务器用来管理进程或线程的模块，它决定了 Apache服务器的工作方式，包括如何处理并发连接、如何分配资源等

MPM multi-processing module 有三种工作模式

#### 1.6.1.1 Apache prefork 模型

预派生模式，有一个主控制进程，然后生成多个子进程，每个子进程有一个独立的线程响应用户请求， 相对比较占用内存，但是比较稳定，可以设置最大和最小进程数，是最古老的一种模式，也是最稳定的 模式，适用于访问量不是很大的场景。

优点：稳定

缺点：每个用户请求需要对应开启一个进程,占用资源较多，并发性差,不适用于高并发场景

![image-20241118165041198](images/image-20241118165041198.png)

#### 1.6.1.2 Apache worker 模型

一种多进程和多线程混合的模型，有一个控制进程，启动多个子进程，每个子进程里面包含固定的线 程，使用线程程来处理请求，当线程不够使用的时候会再启动一个新的子进程，然后在进程里面再启动 线程处理请求，由于其使用了线程处理请求，因此可以承受更高的并发。

优点：相比prefork 占用的内存较少，可以同时处理更多的请求,可以基于select的IO多路复用技术实现 使用更少的线程支持更多的并发连接

缺点：使用keepalive的长连接方式，某个线程会一直被占据，即使没有传输数据，也需要一直等待到超 时才会被释放。如果过多的线程，被这样占据，也会导致在高并发场景下的无服务线程可用。（该问题 在prefork模式下，同样会发生）

![image-20241118165151716](images/image-20241118165151716.png)

#### 1.6.1.3 Apache event 模型

Apache中最新的模式，2012年发布的apache 2.4.X系列正式支持event 模型，属于事件驱动模型 (epoll)，

每个进程响应多个请求，在现在版本里的已经是稳定可用的模式。它和worker模式很像，最大 的区别在于，它解决了keepalive场景下，长期被占用的线程的资源浪费问题（某些线程因为被 keepalive，空挂在哪里等待，中间几乎没有请求过来，甚至等到超时）。event MPM中，会有一个专 门的线程来管理这些keepalive类型的线程，当有真实请求过来的时候，将请求传递给服务线程，执行完 毕后，又允许它释放。这样增强了高并发场景下的请求处理能力。

优点：单线程响应多请求，占据更少的内存，高并发下表现更优秀，会有一个专门的线程来管理keepalive类型的线程，当有真实请求过来的时候，将请求传递给服务线程，执行完毕后，又允许它释放,,可以 基于epoll 更加高效的IO多路复用技术实现使用更少的线程支持更多的并发连接

缺点：没有线程安全控制

![image-20241118165331850](images/image-20241118165331850.png)

### 1.6.2 Nginx 高性能的 Web 服务端

Nginx是由俄罗斯国立莫斯科鲍曼科技大学在1994年毕业的学生为俄罗斯rambler.ru公司开发的，开发 工作最早从2002年开始，第一次公开发布时间是2004年10月4日，版本号是0.1.0

2019年3月11日F5 与 NGINX达成协议,F5 将收购 NGINX 的所有已发行股票，总价值约为 6.7 亿美元。 6.7亿美金约合44.97亿人民币,nginx核心模块代码长度198430（包括空格、注释），所以一行代码约为 2.2万人民币

官网地址 www.nginx.org

Nginx历经十几年的迭代更新（https://nginx.org/en/CHANGES）， 目前功能已经非常完善且运行稳 定，分为社区版本和商业版，另外Nginx的社区版本分为开发版（奇数）、最新稳定版（偶数）和过期 版，nginx以功能丰富著称，它即可以作为http服务器，也可以作为反向代理服务器或者邮件服务器，能 够快速的响应静态网页的请求，支持FastCGI/SSL/Virtual Host/URL Rwrite/Gzip/HTTP Basic Auth/http 或者TCP的负载均衡(1.9版本以上且开启stream模块)等功能，并且支持第三方的功能扩展。

天猫 淘宝 京东 小米 163 新浪等一线互联网公司都在用Nginx或者进行二次开发

基于Nginx的工作场景：

![image-20241118165538145](images/image-20241118165538145.png)

### 1.6.3 用户访问体验和性能

#### 1.6.3.1 用户访问体验统计

互联网存在用户速度体验的1-3-10原则，即1秒最优，1-3秒较优，3~10秒比较慢，10秒以上用户无法接 受。用户放弃一个产品的代价很低，只是换一个URL而已。

![image-20241118165631502](images/image-20241118165631502.png)

全球最大搜索引擎 Google：慢500ms = 20% 将放弃访问。

全球最大的电商零售网站亚马逊：慢100ms = 1% 将放弃交易

有很多研究都表明，性能对用户的行为有很大的影响：

79%的用户表示不太可能再次打开一个缓慢的网站

47%的用户期望网页能在2秒钟以内加载

40%的用户表示如果加载时间超过三秒钟，就会放弃这个网站

页面加载时间延迟一秒可能导致转换损失7%，页面浏览量减少11%

8秒定律：用户访问一个网站时，如果等待网页打开的时间超过8秒，会有超过30%的用户放弃等待

#### 1.6.3.2 影响用户体验的因素

据说马云在刚开始创业在给客户演示时，打开一个网站花了不到四个小时。

```http
https://www.toutiao.com/article/6440287421317218562/?wid=1669189116646
https://www.shuimiao.net/NjHaO/

```

**影响用户体验的因素**

```http
#客户端
客户端硬件配置
客户端网络速率 
客户端与服务端距离
#服务器
服务端网络速率
服务端硬件配置
服务端架构设计
服务端应用程序工作模式
服务端并发数量
服务端响应文件大小及数量 buffer cache
服务端I/O压力
```

### 1.6.4 服务端 I/O 流程

I/O在计算机中指Input/Output， IOPS (Input/Output Per Second)即每秒的输入输出量(或读写次数)， 是衡量磁盘性能的主要指标之一。IOPS是指单位时间内系统能处理的I/O请求数量，一般以每秒处理的 I/O请求数量为单位，I/O请求通常为读或写数据操作请求。

一次完整的I/O是用户空间的进程数据与内核空间的内核数据的报文的完整交换，但是由于内核空间与用 户空间是严格隔离的，所以其数据交换过程中不能由用户空间的进程直接调用内核空间的内存数据，而 是需要经历一次从内核空间中的内存数据copy到用户空间的进程内存当中，所以简单说I/O就是把数据 从内核空间中的内存数据复制到用户空间中进程的内存当中。

Linux 的 I/O 

- 磁盘I/O
- 网络I/O : 一切皆文件,本质为对socket文件的读写

#### 1.6.4.1 磁盘 I/O

磁盘I/O是进程向内核发起系统调用，请求磁盘上的某个资源比如是html 文件或者图片，然后内核通过 相应的驱动程序将目标文件加载到内核的内存空间，加载完成之后把数据从内核内存再复制给进程内 存，如果是比较大的数据也需要等待时间

#### 1.6.4.2 网络 I/O

网络通信就是网络协议栈到用户空间进程的IO就是网络IO

![image-20241118170236009](images/image-20241118170236009.png)

网络I/O 处理过程

```http
获取请求数据，客户端与服务器建立连接发出请求，服务器接受请求（1-3）
构建响应，当服务器接收完请求，并在用户空间处理客户端的请求，直到构建响应完成（4）
返回数据，服务器将已构建好的响应再通过内核空间的网络 I/O 发还给客户端（5-7）
```

不论磁盘和网络I/O

```http
每次I/O，都要经由两个阶段：
第一步：将数据从文件先加载至内核内存空间（缓冲区），等待数据准备完成，时间较长
第二步：将数据从内核缓冲区复制到用户空间的进程的内存中，时间较短
```

## 1.7 I/O 模型

### 1.7.1 I/O 模型相关概念

#### 1.7.1.1 同步和异步

关注的是消息通信机制，即调用者在等待一件事情的处理结果时，被调用者是否提供完成状态的通知。

- 同步：synchronous，被调用者并不提供事件的处理结果相关的通知消息，需要调用者主动询问事 情是否处理完成
- 异步：asynchronous，被调用者通过状态、通知或回调机制主动通知调用者被调用者的运行状态

#### 1.7.1.2 阻塞和非阻塞

关注调用者在等待结果返回之前所处的状态

- 阻塞：blocking，指IO操作需要彻底完成后才返回到用户空间，调用结果返回之前，调用者被挂 起，干不了别的事情。
- 非阻塞：nonblocking，指IO操作被调用后立即返回给用户一个状态值，而无需等到IO操作彻底完 成，在最终的调用结果返回之前，调用者不会被挂起，可以去做别的事情。

### 1.7.2 网络 I/O 模型

阻塞型、非阻塞型、复用型、信号驱动型、异步

参看:《UNIX网络编程 卷1：套接字联网API 》(美)W. Richard Stevens 著

#### 1.7.2.1 阻塞型 I/O 模型（blocking IO）

![image-20241118171224681](images/image-20241118171224681.png)

阻塞IO模型是最简单的I/O模型，用户线程在内核进行IO操作时被阻塞

用户线程通过系统调用read发起I/O读操作，由用户空间转到内核空间。内核等到数据包到达后，然后将 接收的数据拷贝到用户空间，完成read操作

用户需要等待read将数据读取到buffer后，才继续处理接收的数据。整个I/O请求的过程中，用户线程是 被阻塞的，这导致用户在发起IO请求时，不能做任何事情，对CPU的资源利用率不够

优点：程序简单，在阻塞等待数据期间进程/线程挂起，基本不会占用 CPU 资源

缺点：每个连接需要独立的进程/线程单独处理，当并发请求量大时为了维护程序，内存、线程切换开销 较大，apache 的prefork使用的是这种模式。

```http
同步阻塞：程序向内核发送I/O请求后一直等待内核响应，如果内核处理请求的IO操作不能立即返回,则进程将
一直等待并不再接受新的请求，并由进程轮询查看I/O是否完成，完成后进程将I/O结果返回给Client，在IO
没有返回期间进程不能接受其他客户的请求，而且是有进程自己去查看I/O是否完成，这种方式简单，但是比
较慢，用的比较少。
```

#### 1.7.2.2 非阻塞型 I/O 模型 (nonblocking IO)

![image-20241118171526047](images/image-20241118171526047.png)

用户线程发起IO请求时立即返回。但并未读取到任何数据，用户线程需要不断地发起IO请求，直到数据 到达后，才真正读取到数据，继续执行。即 “轮询”机制存在两个问题：如果有大量文件描述符都要等， 那么就得一个一个的read。这会带来大量的Context Switch（read是系统调用，每调用一次就得在用户 态和核心态切换一次）。轮询的时间不好把握。这里是要猜多久之后数据才能到。等待时间设的太长， 程序响应延迟就过大;设的太短，就会造成过于频繁的重试，干耗CPU而已，是比较浪费CPU的方式，一 般很少直接使用这种模型，而是在其他IO模型中使用非阻塞IO这一特性。

```http
非阻塞：程序向内核发送请I/O求后一直等待内核响应，如果内核处理请求的IO操作不能立即返回IO结果，进
程将不再等待，而且继续处理其他请求，但是仍然需要进程隔一段时间就要查看内核I/O是否完成。
```

查看上图可知，在设置连接为非阻塞时，当应用进程系统调用 `recvfrom` 没有数据返回时，内核会立即 返回一个 `EWOULDBLOCK` 错误，而不会一直阻塞到数据准备好。如上图在第四次调用时有一个数据报准备 好了，所以这时数据会被复制到 应用进程缓冲区 ，于是 `recvfrom `成功返回数据

当一个应用进程这样循环调用` recvfrom` 时，称之为轮询 `polling` 。这么做往往会耗费大量CPU时间， 实际使用很少

#### 1.7.2.3 I/O 多路复用型 (I/O multiplexing)

网络I/O复用是指利用操作系统提供的一种机制，同时监控多个I/O事件（如可读、可写、异常等），当 有I/O事件发生时，通知应用程序进行相应的处理。

通常，一个应用程序需要对多个网络连接进行处理，传统的方法是使用多线程或多进程模型，为每个连 接创建一个线程或进程进行处理。这种方法存在一些问题，例如线程或进程的创建和销毁需要消耗大量 的系统资源，且容易导致线程或进程的数量过多，进而导致系统崩溃或运行缓慢。

相比于传统的多线程或多进程模型，网络I/O复用模型可以有效地减少线程或进程的数量，从而提高系统 的性能和稳定性。通过网络I/O复用模型，应用程序可以通过一个线程或进程同时监控多个网络连接，当 有网络I/O事件发生时，操作系统会通知应用程序进行相应的处理，从而实现多个网络连接的并发处理。

上面的模型中,每一个文件描述符对应的IO是由一个线程监控和处理,即如果一个I/O流进来，就开启一个 进程处理这个I/O流。那么假设现在有一百万个I/O流进来，那就需要开启一百万个进程一一对应处理这 些I/O流（——这就是传统意义下的多进程并发处理）。一百万个进程，CPU占有率会多高，所以提出了 I/O多路复用这个模型，一个线程，通过记录I/O流的状态来同时管理多个I/O，可以提高服务器的吞吐能 力 

多路复用IO指一个线程可以同时（实际是交替实现，即并发完成）监控和处理多个文件描述符对应各自 的IO，即复用同一个线程

一个线程之所以能实现同时处理多个IO,是因为这个线程调用了内核中的SELECT,POLL或EPOLL等系统调 用，从而实现多路复用IO

![image-20241118174109071](images/image-20241118174109071.png)

I/O multiplexing 主要包括:select，poll，epoll三种系统调用，select/poll/epoll的好处就在于单个 process就可以同时处理多个网络连接的IO。

它的基本原理就是select/poll/epoll这个function会不断的轮询所负责的所有socket，当某个socket有数 据到达了，就通知用户进程。

当用户进程调用了select，那么整个进程会被block，而同时，kernel会“监视”所有select负责的socket， 当任何一个socket中的数据准备好了，select就会返回。这个时候用户进程再调用read操作，将数据从 kernel拷贝到用户进程。

在Apache中，MPM模块可以使用select或epoll技术来实现并发连接的处理。具体来说，当Apache使用 Prefork模型时，它使用阻塞式I/O来处理连接，而在Worker和Event模型中，它们使用select或epoll来 实现并发连接的非阻塞I/O处理。

```http
IO多路复用（IO Multiplexing) ：是一种机制，程序注册一组socket文件描述符给操作系统，表示“我要
监视这些fd是否有IO事件发生，有了就告诉程序处理”
IO多路复用一般和NIO一起使用的。NIO和IO多路复用是相对独立的。NIO仅仅是指IO API总是能立刻返回，
不会被Blocking;而IO多路复用仅仅是操作系统提供的一种便利的通知机制。操作系统并不会强制这俩必须得
一起用，可以只用IO多路复用 + BIO，这时还是当前线程被卡住。IO多路复用和NIO是要配合一起使用才有
实际意义
IO多路复用是指内核一旦发现进程指定的一个或者多个IO条件准备读取，就通知该进程
多个连接共用一个等待机制，本模型会阻塞进程，但是进程是阻塞在select或者poll这两个系统调用上，而
不是阻塞在真正的IO操作上
用户首先将需要进行IO操作添加到select中，同时等待select系统调用返回。当数据到达时，IO被激活，
select函数返回。用户线程正式发起read请求，读取数据并继续执行
从流程上来看，使用select函数进行IO请求和同步阻塞模型没有太大的区别，甚至还多了添加监视IO，以及
调用select函数的额外操作，效率更差。并且阻塞了两次，但是第一次阻塞在select上时，select可以监
控多个IO上是否已有IO操作准备就绪，即可达到在同一个线程内同时处理多个IO请求的目的。而不像阻塞IO
那种，一次只能监控一个IO
虽然上述方式允许单线程内处理多个IO请求，但是每个IO请求的过程还是阻塞的（在select函数上阻塞），
平均时间甚至比同步阻塞IO模型还要长。如果用户线程只是注册自己需要的IO请求，然后去做自己的事情，等
到数据到来时再进行处理，则可以提高CPU的利用率
IO多路复用是最常使用的IO模型，但是其异步程度还不够“彻底”，因它使用了会阻塞线程的select系统调
用。因此IO多路复用只能称为异步阻塞IO模型，而非真正的异步IO
```

优缺点

- 优点：可以基于一个阻塞对象，同时在多个描述符上等待就绪，而不是使用多个线程(每个文件描述 符一个线程)，这样可以大大节省系统资源
- 缺点：当连接数较少时效率相比多线程+阻塞 I/O 模型效率较低，可能延迟更大，因为单个连接处 理需要 2 次系统调用，占用时间会有增加

IO多路复用适用如下场合：

- 当客户端处理多个描述符时（一般是交互式输入和网络套接口），必须使用I/O复用
- 当一个客户端同时处理多个套接字时，此情况可能的但很少出现
- 当一个服务器既要处理监听套接字，又要处理已连接套接字，一般也要用到I/O复用
- 当一个服务器即要处理TCP，又要处理UDP，一般要使用I/O复用
- 当一个服务器要处理多个服务或多个协议，一般要使用I/O复用

#### 1.7.2.4 信号驱动式 I/O 模型 (signal-driven IO)

![image-20241125140737183](images/image-20241125140737183.png)

信号驱动I/O的意思就是进程现在不用傻等着，也不用去轮询。而是让内核在数据就绪时，发送信号通知 进程。

调用的步骤是，通过系统调用 `sigaction` ，并注册一个信号处理的回调函数，该调用会立即返回，然后 主程序可以继续向下执行，当有I/O操作准备就绪,即内核数据就绪时，内核会为该进程产生一个` SIGIO `信号，并回调注册的信号回调函数，这样就可以在信号回调函数中系统调用 `recvfrom` 获取数据,将用户 进程所需要的数据从内核空间拷贝到用户空间

此模型的优势在于等待数据报到达期间进程不被阻塞。用户主程序可以继续执行，只要等待来自信号处 理函数的通知。

在信号驱动式 I/O 模型中，应用程序使用套接口进行信号驱动 I/O，并安装一个信号处理函数，进程继 续运行并不阻塞

当数据准备好时，进程会收到一个 SIGIO 信号，可以在信号处理函数中调用 I/O 操作函数处理数据。

优点：线程并没有在等待数据时被阻塞，内核直接返回调用接收信号，不影响进程继续处理其他请求因 此可以提高资源的利用率

缺点：信号 I/O 在大量 IO 操作时可能会因为信号队列溢出导致没法通知

```http
异步阻塞：程序进程向内核发送IO调用后，不用等待内核响应，可以继续接受其他请求，内核收到进程请求后
进行的IO如果不能立即返回，就由内核等待结果，直到IO完成后内核再通知进程。
```

#### 1.7.2.5 异步 I/O 模型 (asynchronous IO)

![image-20241125141027349](images/image-20241125141027349.png)



异步I/O 与 信号驱动I/O最大区别在于，信号驱动是内核通知用户进程何时开始一个I/O操作，而异步I/O 是由内核通知用户进程I/O操作何时完成，两者有本质区别,相当于不用去饭店场吃饭，直接点个外卖， 把等待上菜的时间也给省了

相对于同步I/O，异步I/O不是顺序执行。用户进程进行aio_read系统调用之后，无论内核数据是否准备 好，都会直接返回给用户进程，然后用户态进程可以去做别的事情。等到socket数据准备好了，内核直 接复制数据给进程，然后从内核向进程发送通知。IO两个阶段，进程都是非阻塞的。

信号驱动IO当内核通知触发信号处理程序时，信号处理程序还需要阻塞在从内核空间缓冲区拷贝数据到 用户空间缓冲区这个阶段，而异步IO直接是在第二个阶段完成后，内核直接通知用户线程可以进行后续 操作了

优点：异步 I/O 能够充分利用 DMA 特性，让 I/O 操作与计算重叠

缺点：要实现真正的异步 I/O，操作系统需要做大量的工作。目前 Windows 下通过 IOCP 实现了真正的 异步 I/O，在 Linux 系统下，Linux 2.6才引入，目前 AIO 并不完善，因此在 Linux 下实现高并发网络编 程时以 IO 复用模型模式+多线程任务的架构基本可以满足需求

Linux提供了AIO库函数实现异步，但是用的很少。目前有很多开源的异步IO库，例如libevent、libev、 libuv。

```http
异步非阻塞：程序进程向内核发送IO调用后，不用等待内核响应，可以继续接受其他请求，内核调用的IO如果
不能立即返回，内核会继续处理其他事物，直到IO完成后将结果通知给内核，内核在将IO完成的结果返回给进
程，期间进程可以接受新的请求，内核也可以处理新的事物，因此相互不影响，可以实现较大的同时并实现较
高的IO复用，因此异步非阻塞使用最多的一种通信方式。
```

### 1.7.3 五种 IO 对比

这五种 I/O 模型中，越往后，阻塞越少，理论上效率也是最优前四种属于同步 I/O，因为其中真正的 I/O  操作(recvfrom)将阻塞进程/线程，只有异步 I/O 模型才与 POSIX 定义的异步 I/O 相匹配

![image-20241125141335825](images/image-20241125141335825.png)

### 1.7.4 I/O 的具体实现方式

#### 1.7.4.1 I/O常见实现

网络I/O复用模型常见的机制包括`select`、`poll`、`epoll`等。这些机制都提供了一种高效的方式来同时监控 多个网络连接，从而提高系统的性能和稳定性。

Nginx支持在多种不同的操作系统实现不同的事件驱动模型，但是其在不同的操作系统甚至是不同的系 统版本上面的实现方式不尽相同，主要有以下实现方式：

```http
1、select：
select库是在linux和windows平台都基本支持的 事件驱动模型库，并且在接口的定义也基本相同，只是部
分参数的含义略有差异，最大并发限制1024，是最早期的事件驱动模型。I/O多路复用这个概念被提出来以
后， select于1983年第一个在BSD里面实现
2、poll：
在Linux 的基本驱动模型，windows不支持此驱动模型，是select的升级版，取消了最大的并发限制，在编
译nginx的时候可以使用--with-poll_module和--without-poll_module这两个指定是否编译select
库。poll出现在1997年
3、epoll：
epoll是库是Nginx服务器支持的最高性能的事件驱动库之一，是公认的非常优秀的事件驱动模型，它和
select和poll有很大的区别，epoll是poll的升级版，但是与poll有很大的区别.在2002年Davide 
Libenzi 实现了epoll.
epoll的处理方式是创建一个待处理的事件列表，然后把这个列表发给内核，返回的时候在去轮询检查这个
表，以判断事件是否发生，epoll支持一个进程打开的最大事件描述符的上限是系统可以打开的文件的最大
数，同时epoll库的I/O效率不随描述符数目增加而线性下降，因为它只会对内核上报的“活跃”的描述符进行
操作。
4、kqueue：
用于支持BSD系列平台的高校事件驱动模型，主要用在FreeBSD 4.1及以上版本、OpenBSD 2.0级以上版
本，NetBSD级以上版本及Mac OS X 平台上，该模型也是poll库的变种，因此和epoll没有本质上的区别，
效效率和epoll相似
5、IOCP：
Windows系统上的实现方式，对应第5种（异步I/O）模型。
6、/dev/poll:
用于支持unix衍生平台的高效事件驱动模型，主要在Solaris 平台、HP/UX，该模型是sun公司在开发
Solaris系列平台的时候提出的用于完成事件驱动机制的方案，它使用了虚拟的/dev/poll设备，开发人员将
要见识的文件描述符加入这个设备，然后通过ioctl()调用来获取事件通知，因此运行在以上系列平台的时候
请使用/dev/poll事件驱动机制。效率和epoll相似
7、rtsig：
不是一个常用事件驱动，最大队列1024，不是很常用
8、eventport：
该方案也是sun公司在开发Solaris的时候提出的事件驱动库，只是Solaris 10以上的版本，该驱动库可防
止内核崩溃等情况的发生。
```

#### 1.7.4.2 常用I/O实现比较

![image-20241125141958974](images/image-20241125141958974.png)

![image-20241125142007278](images/image-20241125142007278.png)

 上图中测试工具为deadcon. 横轴Dead connections 就是链接数，纵轴是每秒处理请求的数量

可以看到，epoll每秒处理请求的数量基本不会随着链接变多而下降的，poll 和/dev/poll 相对就很差 了。 

![image-20241125142051933](images/image-20241125142051933.png)

```http
Select：
实现过程 
1. 从用户空间将fd_set拷贝到内核空间
2. 注册回调函数
3. 调用其对应的poll方法
4. poll方法会返回一个描述读写是否就绪的mask掩码，根据这个mask掩码给fd_set赋值。
5. 如果遍历完所有的fd都没有返回一个可读写的mask掩码，就会让select的进程进入休眠模式，直到发现
可读写的资源后，重新唤醒等待队列上休眠的进程。如果在规定时间内都没有唤醒休眠进程，那么进程会被唤
醒重新获得CPU，再去遍历一次fd。
6. 将fd_set从内核空间拷贝到用户空间
优点:
POSIX所规定，目前几乎在所有的平台上支持，其良好跨平台支持也是它的一个优点
缺点:
单个进程能够监视的文件描述符的数量存在最大限制，在Linux上一般为1024，可以通过修改宏定义
FD_SETSIZE，再重新编译内核实现，但是这样也会造成效率的降低
单个进程可监视的fd数量被限制，默认是1024，修改此值需要重新编译内核
对socket是线性扫描，即采用轮询的方法，效率较低
select 采取了内存拷贝方法来实现内核将 FD 消息通知给用户空间，这样一个用来存放大量fd的数据结
构，这样会使得用户空间和内核空间在传递该结构时复制开销大 
```

```http
poll：
实现过程本质上和select没有区别，它将用户传入的数组拷贝到内核空间，然后查询每个fd对应的设备状态
其没有最大连接数的限制，原因是它是基于链表来存储的
大量的fd的数组被整体复制于用户态和内核地址空间之间，而不管这样的复制是不是有意义 
poll特点是“水平触发”，如果报告了fd后，没有被处理，那么下次poll时会再次报告该fd 
select是边缘触发即只通知一次
```

```http
epoll：
在Linux 2.6内核中提出的select和poll的增强版本
支持水平触发LT和边缘触发ET
最大的特点在于边缘触发，它只告诉进程哪些fd刚刚变为就绪态，并且只会通知一次 
使用“事件”的就绪通知方式，通过epoll_ctl注册fd，一旦该fd就绪，内核就会采用类似callback的回调
机制来激活该fd，epoll_wait便可以收到通知 
优点: 
1)没有最大并发连接的限制：能打开的FD的上限远大于1024(1G的内存能监听约10万个端口)，具体查
看/proc/sys/fs/file-max，此值和系统内存大小相关
2)效率提升：非轮询的方式，不会随着FD数目的增加而效率下降;只有活跃可用的FD才会调用callback函
数，即epoll最大的优点就在于它只管理“活跃”的连接，而跟连接总数无关
3)内存拷贝，利用mmap(Memory Mapping)加速与内核空间的消息传递;即epoll使用mmap减少复制开销 
缺点:
只有linux支持。在BSD上面对应的实现是kqueue。
```

总结：

```http
1、epoll只是一组API，比起select这种扫描全部的文件描述符，epoll只读取就绪的文件描述符
2、epoll比select等多路复用方式来说，减少了遍历循环及内存拷贝的工作量，因为活跃连接只占总并发连
接的很小一部分。
3、epoll基于事件的就绪通知机制，使用回调机制,所以性能比较好
4、基于epoll的IO多路复用减少了进程间切换的次数，使得操作系统少做了相对于用户任务来说的无用功。
```

#### 1.7.4.3 I/O 选择

-  完全跨平台，可以使用select、poll。但是性能较差
- 针对不同操作系统自行选择支持的最优技术，比如: Linux选用epoll,Mac选用kqueue,Windows 选 用IOCP,提高IO处理的性能

范例: 最大并发连接数和内存有直接关系

```bash
#内存1G
[root@centos8 ~]#free -h
             total       used       free     shared buff/cache   available
Mem:         952Mi       168Mi       605Mi       12Mi       178Mi       629Mi
Swap:         2.0Gi         0B       2.0Gi

[root@centos8 ~]#cat /proc/sys/fs/file-max
92953

#内存2G
[root@centos8 ~]#free -h
             total       used       free     shared buff/cache   available
Mem:          1.9Gi       258Mi       1.3Gi       12Mi       341Mi       1.6Gi
Swap:         2.0Gi         0B       2.0Gi
[root@centos8 ~]#cat /proc/sys/fs/file-max
195920
```

范例: 内核限制

```bash
[root@centos8 ~]#grep -R FD_SETSIZE linux-5.8/*
linux-5.8/Documentation/userspace-api/media/v4l/func-select.rst:   
 ``FD_SETSIZE``.
linux-5.8/include/uapi/linux/posix_types.h:#undef __FD_SETSIZE
linux-5.8/include/uapi/linux/posix_types.h:#define __FD_SETSIZE 1024 #单个进程能够
监视的文件描述符的文件最大数量
linux-5.8/include/uapi/linux/posix_types.h: unsigned long fds_bits[__FD_SETSIZE 
/ (8 * sizeof(long))];
linux-5.8/tools/include/nolibc/nolibc.h:#define FD_SETSIZE 256
linux-5.8/tools/include/nolibc/nolibc.h:typedef struct { uint32_t 
fd32[FD_SETSIZE/32]; } fd_set;
linux-5.8/tools/include/nolibc/nolibc.h: if (fd < 0 || fd >= FD_SETSIZE)
linux-5.8/tools/testing/selftests/net/nettest.c: rc = select(FD_SETSIZE, 
NULL, &wfd, NULL, tv);
```

范例: select 和epoll 帮助

```bash
[root@centos8 ~]#whatis epoll
epoll (7)            - I/O event notification facility
[root@centos8 ~]#whatis select
select (2)           - synchronous I/O multiplexing
select (3)           - synchronous I/O multiplexing
select (3p)          - synchronous I/O multiplexing

[root@centos8 ~]#whatis poll
poll (2)             - wait for some event on a file descriptor
poll (3p)            - input/output multiplexing

```

## 1.8 零拷贝

### 1.8.1 零拷贝介绍

#### 1.8.1.1 传统 Linux中 I/O 的问题

![image-20241125144257608](images/image-20241125144257608.png)

传统的 Linux 系统的标准 I/O 接口（read、write）是基于数据拷贝的，也就是数据都是 copy_to_user  或者 copy_from_user，这样做的好处是，通过中间缓存的机制，减少磁盘 I/O 的操作，但是坏处也很 明显，大量数据的拷贝，用户态和内核态的频繁切换，会消耗大量的 CPU 资源，严重影响数据传输的性 能，统计表明，在Linux协议栈中，数据包在内核态和用户态之间的拷贝所用的时间甚至占到了数据包整 个处理流程时间的57.1%

#### 1.8.1.2 什么是零拷贝

零拷贝就是上述问题的一个解决方案，通过尽量避免拷贝操作来缓解 CPU 的压力。零拷贝并没有真正做 到“0”拷贝，它更多是一种思想，很多的零拷贝技术都是基于这个思想去做的优化

### 1.8.2 零拷页相关技术

#### 1.8.2.1 MMAP ( Memory Mapping )

![image-20241125144505300](images/image-20241125144505300.png)

mmap()系统调用使得进程之间通过映射同一个普通文件实现共享内存。普通文件被映射到进程地址空 间后，进程可以向访问普通内存一样对文件进行访问。

mmap是一种内存映射文件的方法，即将一个文件或者其它对象映射到进程的地址空间，实现文件磁盘 地址和进程虚拟地址空间中一段虚拟地址的一一对映关系。

实现这样的映射关系后，进程就可以采用指针的方式读写操作这一段内存，而系统会自动回写脏页面到 对应的文件磁盘上，即完成了对文件的操作而不必再调用read,write等系统调用函数。相反，内核空间 对这段区域的修改也直接反映用户空间，从而可以实现不同进程间的文件共享。

内存映射减少数据在用户空间和内核空间之间的拷贝操作,适合大量数据传输

![image-20241125144646120](images/image-20241125144646120.png)

![image-20241125144651463](images/image-20241125144651463.png)



上面左图为传统读写,右图为MMAP.两者相比mmap要比普通的read系统调用少了一次copy的过程。因 为read调用，进程是无法直接访问kernel space的，所以在read系统调用返回前，内核需要将数据从内 核复制到进程指定的buffer。但mmap之后，进程可以直接访问mmap的数据(page cache)。

#### 1.8.2.2 SENDFILE

![image-20241125144724774](images/image-20241125144724774.png)

#### 1.8.2.3 DMA辅助的 SENDFILE

![image-20241125144805779](images/image-20241125144805779.png)

# 2 Nginx 架构和安装

## 2.1 Nginx 概述

### 2.1.1 Nginx 介绍

Nginx：engine X ，2002年开发，分为社区版和商业版(nginx plus )

2019年3月11日 F5 Networks 6.7亿美元的价格收购 

Nginx是免费的、开源的、高性能的HTTP和反向代理服务器、邮件代理服务器、以及TCP/UDP代理服务器 

解决C10K问题（10K Connections）

解决C1000K问题参考链接: http://www.ideawu.net/blog/archives/740.html

Nginx官网：http://nginx.org

nginx的其他二次发行版：

- Tengine

  由淘宝网发起的Web服务器项目。它在Nginx的基础上，针对大访问量网站的需求，添加了很多高 级功能和特性。Tengine的性能和稳定性已经在大型的网站如淘宝网，天猫商城等得到了很好的检 验。它的最终目标是打造一个高效、稳定、安全、易用的Web平台。从2011年12月开始，Tengine 成为一个开源项目

  官网： http://tengine.taobao.org/

- OpenResty

  基于 Nginx 与 Lua 语言的高性能 Web 平台， 章亦春团队开发

  官网：http://openresty.org/cn/

### 2.1.2 Nginx 功能介绍

- 静态的web资源服务器html，图片，js，css，txt等静态资源
- http/https协议的反向代理
- 结合FastCGI/uWSGI/SCGI等协议反向代理动态资源请求
- tcp/udp协议的请求转发（反向代理）
- imap4/pop3协议的反向代理

### 2.2.3 基础特性

- 模块化设计，较好的扩展性
- 高可靠性
- 支持热部署：不停机更新配置文件，升级版本，更换日志文件
- 低内存消耗：10000个keep-alive连接模式下的非活动连接，仅需2.5M内存
- event-driven,aio,mmap，sendfile

### 2.2.4 Web 服务相关的功能

- 虚拟主机（server）
- 支持 keep-alive 和管道连接(利用一个连接做多次请求)
- 访问日志（支持基于日志缓冲提高其性能）
- url rewirte
- 路径别名
- 基于IP及用户的访问控制
- 支持速率限制及并发数限制
- 重新配置和在线升级而无须中断客户的工作进程

## 2.2 Nginx架构和进程

### 2.2.1 Nginx 架构

![image-20241125145938494](images/image-20241125145938494.png)

### 2.2.2 Nginx 进程结构

nginx是多进程组织模型，而且是由一个master主进程和worker工作进程组成。

![image-20241125150147559](images/image-20241125150147559.png)

主进程(master process)的功能：

```http
对外接口：接收外部的操作（信号）
对内转发：根据外部的操作的不同，通过信号管理 Worker
监控：监控 worker 进程的运行状态，worker 进程异常终止后，自动重启 worker 进程
读取Nginx 配置文件并验证其有效性和正确性
建立、绑定和关闭socket连接
按照配置生成、管理和结束工作进程
接受外界指令，比如重启、升级及退出服务器等指令
不中断服务，实现平滑升级，重启服务并应用新的配置
开启日志文件，获取文件描述符
不中断服务，实现平滑升级，升级失败进行回滚处理
编译和处理perl脚本
```

工作进程（worker process）的功能：

```http
所有 Worker 进程都是平等的
实际处理：网络请求，由 Worker 进程处理
Worker进程数量：一般设置为核心数，充分利用CPU资源，同时避免进程数量过多，导致进程竞争CPU资源，
增加上下文切换的损耗
接受处理客户的请求
将请求依次送入各个功能模块进行处理
I/O调用，获取响应数据
与后端服务器通信，接收后端服务器的处理结果
缓存数据，访问缓存索引，查询和调用缓存数据
发送请求结果，响应客户的请求
接收主程序指令，比如重启、升级和退出等
```

### 2.2.3 Nginx 启动和 HTTP 连接建立

![image-20241125150653839](images/image-20241125150653839.png)

- Nginx 启动时，Master 进程，加载配置文件
- Master 进程，初始化监听的 socket
- Master 进程，fork 出多个 Worker 进程
- Worker 进程，竞争新的连接，获胜方通过三次握手，建立 Socket 连接，并处理请求

### 2.2.4 HTTP 处理过程

![image-20241125150816693](images/image-20241125150816693.png)

Nginx是一种高性能的Web服务器，可以处理大量的并发HTTP请求。Nginx在处理HTTP请求时采用了高 效的事件驱动模型，使用异步IO等技术实现了高性能、低延迟的请求处理。

在处理HTTP请求时，Nginx会通过以下步骤进行处理：

- 读取请求：当客户端发送HTTP请求时，Nginx会使用socket接口读取请求，包括请求头和请求体。
- 解析请求：Nginx会对请求进行解析，包括解析请求方法、请求路径、查询参数等信息。Nginx还 会对请求头进行解析，包括解析Host、User-Agent、Content-Type等字段，这些信息可以在后续 处理中使用
- 处理请求：根据解析得到的请求信息，Nginx会进行请求处理。比如，如果请求路径对应的是一个 静态文件，Nginx会直接返回文件内容；如果请求路径对应的是一个动态页面，Nginx会将请求转 发给对应的后端应用服务器。
- 处理请求体：如果请求包含请求体，Nginx会将请求体读取到内存中，以供后续处理使用。
- 处理响应：当请求处理完成后，Nginx会根据处理结果生成响应，并发送给客户端。Nginx会将响 应头和响应体一起发送给客户端，响应头中包含响应状态码、响应头字段等信息。
- 关闭连接：当请求处理完成后，Nginx会关闭连接，释放资源，等待下一个请求。

## 2.3 Nginx 模块介绍

nginx 有多种模块

- 核心模块：是 Nginx 服务器正常运行必不可少的模块，提供错误日志记录 、配置文件解析 、事件 驱动机制 、进程管理等核心功能
- 标准HTTP模块：提供 HTTP 协议解析相关的功能，比如： 端口配置 、 网页编码设置 、 HTTP响应 头设置等
- 可选HTTP模块：主要用于扩展标准的 HTTP 功能，让 Nginx 能处理一些特殊的服务，比如： Flash  多媒体传输 、解析 GeoIP 请求、 网络传输压缩 、 安全协议 SSL 支持等
- 邮件服务模块：主要用于支持 Nginx 的 邮件服务 ，包括对 POP3 协议、 IMAP 协议和 SMTP协议 的支持
- Stream服务模块: 实现反向代理功能,包括TCP协议代理
- 第三方模块：是为了扩展 Nginx 服务器应用，完成开发者自定义功能，比如： Json 支持、 Lua 支 持等

nginx高度模块化，但其模块早期不支持DSO机制;1.9.11 版本支持动态装载和卸载

模块分类：

```bash
核心模块：core module
标准模块：
 HTTP 模块： ngx_http_*
     HTTP Core modules   #默认功能
     HTTP Optional modules #需编译时指定
 Mail 模块: ngx_mail_*
 Stream 模块 ngx_stream_*
第三方模块
```

![image-20241125151422864](images/image-20241125151422864.png)

## 2.4 Nginx 安装

### 2.4.1 Nginx版本和安装方式

Nginx 分为社区版和商业版,一般是社区版

Nginx版本

- Mainline version 主要开发版本,一般为奇数版本号,比如1.19
- Stable version 当前最新稳定版,一般为偶数版本,如:1.20
- Legacy versions 旧的稳定版,一般为偶数版本,如:1.18

Nginx安装可以使用yum/apt或源码安装，但是推荐使用源码编译安装

- yum/apt的系统仓库版本比较旧
- 编译安装可以更方便自定义相关路径,使用源码编译可以自定义相关功能，更方便业务的上的使用
- docker 容器直接运行

### 2.4.2 包安装

#### 2.4.2.1 基于Ubuntu 包安装 Nginx

范例: Ubuntu 2204内置包安装

```bash
root@ubutun2204-1:~# apt list nginx
Listing... Done
nginx/jammy-updates 1.18.0-6ubuntu14.4 amd64
root@ubutun2204-1:~# apt update && apt -y install nginx
```

范例: 官方包仓库安装 Nginx

```bash
http://nginx.org/en/linux_packages.html
```

Install the prerequisites:

```bash
sudo apt install curl gnupg2 ca-certificates lsb-release ubuntu-keyring
```

Import an official nginx signing key so apt could verify the packages authenticity. Fetch the key:

```bash
curl https://nginx.org/keys/nginx_signing.key | gpg --dearmor \
    | sudo tee /usr/share/keyrings/nginx-archive-keyring.gpg >/dev/null
```

Verify that the downloaded file contains the proper key:

```bash
gpg --dry-run --quiet --no-keyring --import --import-options import-show /usr/share/keyrings/nginx-archive-keyring.gpg
```

The output should contain the full fingerprint `573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62` as follows:

> ```
> pub   rsa2048 2011-08-19 [SC] [expires: 2027-05-24]
>       573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62
> uid                      nginx signing key <signing-key@nginx.com>
> ```

Note that the output can contain other keys used to sign the packages.

To set up the apt repository for stable nginx packages, run the following command:

> ```
> echo "deb [signed-by=/usr/share/keyrings/nginx-archive-keyring.gpg] \
> http://nginx.org/packages/ubuntu `lsb_release -cs` nginx" \
>     | sudo tee /etc/apt/sources.list.d/nginx.list
> ```

查看支持的版本

```bash
[root@ubuntu2204 ~]#apt-cache madison nginx
     nginx | 1.22.1-1~jammy | http://nginx.org/packages/ubuntu jammy/nginx amd64 
Packages
     nginx | 1.22.0-1~jammy | http://nginx.org/packages/ubuntu jammy/nginx amd64 
Packages
     nginx | 1.20.2-1~jammy | http://nginx.org/packages/ubuntu jammy/nginx amd64 
Packages
     nginx | 1.18.0-6ubuntu14.3 | http://mirrors.ustc.edu.cn//ubuntu jammysecurity/main
 amd64 Packages
     nginx | 1.18.0-6ubuntu14.3 | http://mirrors.ustc.edu.cn/ubuntu jammyupdates/main
 amd64 Packages
     nginx | 1.18.0-6ubuntu14 | http://mirrors.ustc.edu.cn/ubuntu jammy/main 
amd64 Packages
     nginx | 1.18.0-6ubuntu14 | http://mirrors.ustc.edu.cn/ubuntu jammy/main 
Sources
     nginx | 1.18.0-6ubuntu14.3 | http://mirrors.ustc.edu.cn/ubuntu jammysecurity/main
 Sources
     nginx | 1.18.0-6ubuntu14.3 | http://mirrors.ustc.edu.cn/ubuntu jammyupdates/main
 Sources
```

指定安装的版本

```bash
[root@ubuntu2204 ~]#apt install nginx=1.22.0-1~jammy
```

### 2.4.3 Nginx 编译安装

Nginx是由C语言编写而成,所以Nginx源码安装需要提前准备标准的编译器GCC（GNU Compiler  collection），由GNU开发，并以GPL即LGPL许可，早期GCC原本只能处理C语言，所以原名为GNU C语 言编译器，后来得到快速发展，还可以处理C++,Fortran，pascal，objective-C，java以及Ada等其他语 言，此外还需要Automake工具，以完成自动创建Makefile文件，Nginx的一些模块需要依赖第三方库， 比如: pcre（支持rewrite），zlib（支持gzip模块）和openssl（支持ssl模块）等。

#### 2.4.3.1 编译安装 Nginx

官方源码包下载地址：

```http
https://nginx.org/en/download.html
```

范例: Ubuntu22.04和Ubuntu20.04编译安装

```bash
#安装依赖包
root@ubutun2204-1:~# apt update && apt -y install gcc make libpcre3 libpcre3-dev openssl libssl-dev zlib1g-dev

#创建用户和组
root@ubutun2204-1:~# useradd -s /sbin/nologin nginx

root@ubutun2204-1:~# cd /usr/local/src/
root@ubutun2204-1:/usr/local/src# wget https://nginx.org/download/nginx-1.26.2.tar.gz
root@ubutun2204-1:/usr/local/src# tar xf nginx-1.26.2.tar.gz 
root@ubutun2204-1:/usr/local/src# cd nginx-1.26.2/

#编译安装
root@ubutun2204-1:/usr/local/src/nginx-1.26.2# ./configure --prefix=/apps/nginx --user=nginx --group=nginx --with-http_ssl_module --with-http_v2_module --with-http_realip_module --with-http_stub_status_module --with-http_gzip_static_module --with-pcre --with-stream --with-stream_ssl_module --with-stream_realip_module

root@ubutun2204-1:/usr/local/src/nginx-1.26.2# make && make install

#修改权限
root@ubutun2204-1:~# chown -R nginx.nginx /apps/nginx
```

nginx完成安装以后，有四个主要的目录

```bash
# 生成目录
root@ubutun2204-1:~# ls -ltr /apps/nginx/
total 16
drwxr-xr-x 2 nginx nginx 4096 Nov 25 07:40 sbin
drwxr-xr-x 2 nginx nginx 4096 Nov 25 07:40 logs
drwxr-xr-x 2 nginx nginx 4096 Nov 25 07:40 html
drwxr-xr-x 2 nginx nginx 4096 Nov 25 07:40 conf

#conf：保存nginx所有的配置文件，其中nginx.conf是nginx服务器的最核心最主要的配置文件，其他的.conf则是用来配置nginx相关的功能的，例如fastcgi功能使用的是fastcgi.conf和fastcgi_params两个文件，配置文件一般都有一个样板配置文件，是以.default为后缀，使用时可将其复制并将default后缀去掉即可。
#html目录中保存了nginx服务器的web文件，但是可以更改为其他目录保存web文件,另外还有一个50x的web文件是默认的错误页面提示页面。
#logs：用来保存nginx服务器的访问日志错误日志等日志，logs目录可以放在其他路径，比如/var/logs/nginx里面。
#sbin：保存nginx二进制启动脚本，可以接受不同的参数以实现不同的功能。
```

#### 2.4.3.2 验证版本及编译参数

```bash
root@ubutun2204-1:~# ls /apps/nginx/sbin/
nginx
root@ubutun2204-1:~# ln -sv /apps/nginx/sbin/nginx /usr/sbin/
'/usr/sbin/nginx' -> '/apps/nginx/sbin/nginx'


# 查看版本
root@ubutun2204-1:~# nginx -v
nginx version: nginx/1.26.2

# 查看编译参数
root@ubutun2204-1:~# nginx -V
nginx version: nginx/1.26.2
built by gcc 11.4.0 (Ubuntu 11.4.0-1ubuntu1~22.04) 
built with OpenSSL 3.0.2 15 Mar 2022
TLS SNI support enabled
configure arguments: --prefix=/apps/nginx --user=nginx --group=nginx --with-http_ssl_module --with-http_v2_module --with-http_realip_module --with-http_stub_status_module --with-http_gzip_static_module --with-pcre --with-stream --with-stream_ssl_module --with-stream_realip_module
```

#### 2.4.3.3 启动和停止 nginx 测试访问 web 界面

```bash
#启动nginx
root@ubutun2204-1:~# nginx
root@ubutun2204-1:~# ss -ntl
State                        Recv-Q                       Send-Q                                               Local Address:Port                                               Peer Address:Port                       Process                       
LISTEN                       0                            128                                                        0.0.0.0:22                                                      0.0.0.0:*                                                        
LISTEN                       0                            511                                                        0.0.0.0:80                                                      0.0.0.0:*                                                        
LISTEN                       0                            128                                                      127.0.0.1:6010                                                    0.0.0.0:*                                                        
LISTEN                       0                            4096                                                 127.0.0.53%lo:53                                                      0.0.0.0:*                                                        
LISTEN                       0                            128                                                           [::]:22                                                         [::]:*                                                        
LISTEN                       0                            128                                                          [::1]:6010                                                       [::]:*     

#关闭nginx
root@ubutun2204-1:~# nginx -s stop
```

![image-20241125154939062](images/image-20241125154939062.png)

#### 2.4.3.4 创建 Nginx 自启动文件

```bash
#复制同一版本的nginx的yum安装生成的service文件
root@ubutun2204-1:~# vim /lib/systemd/system/nginx.service
[Unit]
Description=nginx - high performance web server
Documentation=http://nginx.org/en/docs/
After=network-online.target remote-fs.target nss-lookup.target
Wants=network-online.target

[Service]
Type=forking
#指定pid文件的目录,默认在logs目录下,可选配置
PIDFile=/apps/nginx/run/nginx.pid
ExecStart=/apps/nginx/sbin/nginx -c /apps/nginx/conf/nginx.conf
ExecReload=/bin/kill -s HUP $MAINPID
ExecStop=/bin/kill -s TERM $MAINPID
LimitNOFILE=100000

[Install]
WantedBy=multi-user.target

#创建pid文件存放的目录
root@ubutun2204-1:~# mkdir /apps/nginx/run/

#修改配置文件
root@ubutun2204-1:~# vim /apps/nginx/conf/nginx.conf
pid   /apps/nginx/run/nginx.pid;
```

#### 2.4.3.5 验证 Nginx 自启动文件

```bash
root@ubutun2204-1:~# systemctl daemon-reload
root@ubutun2204-1:~# systemctl enable --now nginx

root@ubutun2204-1:~# ll /apps/nginx/run/nginx.pid 
-rw-r--r-- 1 root root 5 Nov 25 07:57 /apps/nginx/run/nginx.pid

root@ubutun2204-1:~# systemctl stop nginx.service 
root@ubutun2204-1:~# systemctl status nginx.service 
○ nginx.service - nginx - high performance web server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: inactive (dead) since Mon 2024-11-25 07:58:25 UTC; 5s ago
       Docs: http://nginx.org/en/docs/
    Process: 5960 ExecStart=/apps/nginx/sbin/nginx -c /apps/nginx/conf/nginx.conf (code=exited, status=0/SUCCESS)
    Process: 5995 ExecStop=/bin/kill -s TERM $MAINPID (code=exited, status=0/SUCCESS)
   Main PID: 5961 (code=exited, status=0/SUCCESS)
        CPU: 32ms

Nov 25 07:57:27 ubutun2204-1 systemd[1]: Starting nginx - high performance web server...
Nov 25 07:57:27 ubutun2204-1 systemd[1]: Started nginx - high performance web server.
Nov 25 07:58:25 ubutun2204-1 systemd[1]: Stopping nginx - high performance web server...
Nov 25 07:58:25 ubutun2204-1 systemd[1]: nginx.service: Deactivated successfully.
Nov 25 07:58:25 ubutun2204-1 systemd[1]: Stopped nginx - high performance web server.

```

### 2.4.4 自动化部署 nginx

#### 2.4.4.1 实战案例: 一键安装 nginx 脚本

```bash
#!/bin/bash
#
****************************************************************

NGINX_VERSION=1.26.2
#NGINX_VERSION=1.22.0
#NGINX_VERSION=1.20.2
#NGINX_VERSION=1.18.0
NGINX_FILE=nginx-${NGINX_VERSION}.tar.gz
NGINX_URL=http://nginx.org/download/
NGINX_INSTALL_DIR=/apps/nginx
SRC_DIR=/usr/local/src
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


check () {
    [ -e ${NGINX_INSTALL_DIR} ] && { color "nginx 已安装,请卸载后再安装" 1; exit; }
    cd  ${SRC_DIR}
    if [  -e ${NGINX_FILE}${TAR} ];then
        color "相关文件已准备好" 0
    else
        color '开始下载 nginx 源码包' 0
        wget ${NGINX_URL}${NGINX_FILE}${TAR} 
        [ $? -ne 0 ] && { color "下载 ${NGINX_FILE}${TAR}文件失败" 1; exit; } 
    fi
} 

install () {
    color "开始安装 nginx" 0
    if id nginx  &> /dev/null;then
        color "nginx 用户已存在" 1 
    else
        useradd -s /sbin/nologin -r  nginx
        color "创建 nginx 用户" 0 
    fi
    color "开始安装 nginx 依赖包" 0
    if [ $ID == "centos" ] ;then
	    if [[ $VERSION_ID =~ ^7 ]];then
            yum -y  install  gcc  make pcre-devel openssl-devel zlib-devel perl-ExtUtils-Embed
		elif [[ $VERSION_ID =~ ^8 ]];then
            yum -y  install make gcc-c++ libtool pcre pcre-devel zlib zlib-devel openssl openssl-devel perl-ExtUtils-Embed 
		else 
            color '不支持此系统!'  1
            exit
        fi
     elif [ $ID == "rocky"  ];then
	    yum -y  install gcc make gcc-c++ libtool pcre pcre-devel zlib zlib-devel openssl openssl-devel perl-ExtUtils-Embed 
     else
        apt update
        apt -y install gcc make  libpcre3 libpcre3-dev openssl libssl-dev zlib1g-dev
     fi
     [ $? -ne 0 ] && { color "安装依赖包失败" 1; exit; } 
     cd $SRC_DIR
     tar xf ${NGINX_FILE}
     NGINX_DIR=`echo ${NGINX_FILE}| sed -nr 's/^(.*[0-9]).*/\1/p'`
     cd ${NGINX_DIR}
     ./configure --prefix=${NGINX_INSTALL_DIR} --user=nginx --group=nginx --with-http_ssl_module --with-http_v2_module --with-http_realip_module --with-http_stub_status_module --with-http_gzip_static_module --with-pcre --with-stream --with-stream_ssl_module --with-stream_realip_module 
     make -j $CPUS && make install 
     [ $? -eq 0 ] && color "nginx 编译安装成功" 0 ||  { color "nginx 编译安装失败,退出!" 1 ;exit; }
	 chown -R nginx.nginx ${NGINX_INSTALL_DIR}
     ln -s ${NGINX_INSTALL_DIR}/sbin/nginx /usr/local/sbin/nginx
     echo "PATH=${NGINX_INSTALL_DIR}/sbin:${PATH}" > /etc/profile.d/nginx.sh
     cat > /lib/systemd/system/nginx.service <<EOF
[Unit]
Description=The nginx HTTP and reverse proxy server
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=${NGINX_INSTALL_DIR}/logs/nginx.pid
ExecStartPre=/bin/rm -f ${NGINX_INSTALL_DIR}/logs/nginx.pid
ExecStartPre=${NGINX_INSTALL_DIR}/sbin/nginx -t
ExecStart=${NGINX_INSTALL_DIR}/sbin/nginx
ExecReload=/bin/kill -s HUP \$MAINPID
KillSignal=SIGQUIT
TimeoutStopSec=5
KillMode=process
PrivateTmp=true
LimitNOFILE=100000

[Install]
WantedBy=multi-user.target
EOF
     systemctl daemon-reload
     systemctl enable --now nginx &> /dev/null 
     systemctl is-active nginx &> /dev/null ||  { color "nginx 启动失败,退出!" 1 ; exit; }
     color "nginx 安装完成" 0
}

check

install
```

#### 2.4.4.2 利用 ansible 的 playbook 实现 nginx 编译安装

```bash
root@ubutun2204-1:~# cat nginx_install.yml
---
- hosts: webservers
  remote_user: root
  gather_facts: yes
  vars:
    nginx_verison: nginx-1.18.0
    suffix: .tar.gz
    down_dir: /usr/local/src/
    ins_dir: /apps/nginx/
    user: nginx
    group: nginx
    
   tasks:
    - name: install packages on centos8
      yum:
        name:
          - gcc
          - make
          - pcre-devel
          - openssl-devel
          - zlib-devel
        state: present
      when: 
        - ansible_facts['distribution'] == "CentOS" 
        - ansible_facts['distribution_major_version'] == "8"
    - name: install packages on centos7
      yum:
        name:
          - gcc
          - make
          - pcre-devel
          - openssl-devel
          - zlib-devel
          - perl-ExtUtils-Embed
        state: present
      when: 
        - ansible_facts['distribution'] == "CentOS" 
        - ansible_facts['distribution_major_version'] == "7"
    - name: install packages on ubuntu18.04
      apt:
        name:
          - gcc
          - make
          - libpcre3
          - libpcre3-dev
          - openssl
          - libssl-dev
          - zlib1g-dev
       state: present
      when: 
        - ansible_facts['distribution'] == "Ubuntu" 
        - ansible_facts['distribution_major_version'] == "18"
        
     - name: group "{{ group }}"
     group: name={{ group }} state=present system=yes
    - name: user "{{ user }}"
     user:
       name: "{{ user }}"
       shell: /sbin/nologin
       system: yes
       group: "{{ group }}"
       home: "/home/{{ user }}"
       create_home: no
    - name: unarchive
     unarchive:
       src: "http://nginx.org/download/{{ nginx_verison }}{{ suffix }}"
       dest: "{{ down_dir }}"
       remote_src: yes
    - name: configure
     shell: ./configure \
                --prefix={{ ins_dir }} \
                --user={{ user }} --group={{ group }} \
                --with-http_ssl_module \
                --with-http_realip_module \
                --with-http_v2_module \
                --with-http_stub_status_module \
                --with-http_gzip_static_module \
                --with-pcre \
                --with-stream \
                --with-stream_ssl_module \
                --with-stream_realip_module
     args:
       chdir: "{{ down_dir }}{{ nginx_verison }}/"
    - name: make
     shell: make -j "{{ ansible_processor_vcpus }}" && make install
     args:
       chdir: "{{ down_dir }}{{ nginx_verison }}/"
    - name: link
     file:
       src: "{{ ins_dir }}sbin/nginx"
       dest: /usr/sbin/nginx
       state: link
    - name: service file
     copy: content='[Unit]\nDescription=nginx - high performance web 
server\nDocumentation=http://nginx.org/en/docs/\nAfter=network-online.target 
remote-fs.target nss-lookup.target\nWants=networkonline.target\n\n[Service]\nType=forking\nPIDFile={{
 ins_dir 
}}run/nginx.pid\nExecStart=/usr/sbin/nginx -c {{ ins_dir 
}}conf//nginx.conf\nExecReload=/bin/sh -c "/bin/kill -s HUP $(/bin/cat {{ ins_dir 
}}run/nginx.pid)"\nExecStop=/bin/sh -c "/bin/kill -s TERM $(/bin/cat {{ ins_dir 
}}run/nginx.pid)"\nLimitNOFILE=100000\n[Install]\nWantedBy=multi-user.target' 
dest=/lib/systemd/system/nginx.service
    - name: change configure pid location and change worker_processes
     lineinfile:
       path: "{{ item.path }}"
       regexp: "{{ item.regexp }}"
       line: "{{ item.line }}"
     with_items:
        - { path: "{{ ins_dir }}conf/nginx.conf",regexp: 
'^worker_processes',line: "worker_processes {{ ansible_processor_vcpus }};" }
        - { path: "{{ ins_dir }}conf/nginx.conf",regexp: '^#pid',line: 'pid     
  run/nginx.pid;' }
    - name: create dir run and modify directory permission
     file: 
       path: "{{ ins_dir }}run"
       owner: "{{ user }}"
       group: "{{ group }}"
       state: directory
    - name: start serivce
      service: 
       name: nginx
       state: started
       enabled: yes
```

## 2.5 Nginx 命令和信号

### 2.5.1 nginx 命令

nginx 命令支持向其发送信号,实现不同功能

nginx格式

```http
nginx [-?hvVtTq] [-s signal] [-c filename] [-p prefix] [-g directives]
```

选项说明

```http
帮助: -? -h
使用指定的配置文件: -c
指定配置指令:-g
指定运行目录:-p
测试配置文件是否有语法错误:-t -T
打印nginx的版本信息、编译信息等:-v -V
发送信号: -s 示例: nginx -s reload
```

信号说明:

```http
立刻停止服务:stop,相当于信号SIGTERM,SIGINT
优雅的停止服务:quit,相当于信号SIGQUIT
平滑重启，重新加载配置文件: reload,相当于信号SIGHUP
重新开始记录日志文件:reopen,相当于信号SIGUSR1,在切割日志时用途较大
平滑升级可执行程序:发送信号SIGUSR2,在升级版本时使用
优雅的停止工作进程:发送信号SIGWINCH,在升级版本时使用
```

范例: 查看nginx帮助

```bash
root@ubutun2204-1:~# nginx -h
nginx version: nginx/1.26.2
Usage: nginx [-?hvVtTq] [-s signal] [-p prefix]
             [-e filename] [-c filename] [-g directives]

Options:
  -?,-h         : this help
  -v            : show version and exit
  -V            : show version and configure options then exit
  -t            : test configuration and exit
  -T            : test configuration, dump it and exit
  -q            : suppress non-error messages during configuration testing
  -s signal     : send signal to a master process: stop, quit, reopen, reload
  -p prefix     : set prefix path (default: /apps/nginx/)
  -e filename   : set error log file (default: logs/error.log)
  -c filename   : set configuration file (default: conf/nginx.conf)
  -g directives : set global directives out of configuration file
```

### 2.5.2 quit 实现worker进程优雅关闭

- 设置定时器: worker_shutdown_timeout

  ```bash
  http://nginx.org/en/docs/ngx_core_module.html#worker_shutdown_timeout
  
  Syntax: worker_shutdown_timeout time;
  Default: —
  Context: main
  This directive appeared in version 1.11.11.
  
  Configures a timeout for a graceful shutdown of worker processes. When the 
  time expires, nginx will try to close all the connections currently open to 
  facilitate shutdown.
  ```

- 关闭监听句柄

- 关闭空闲连接

- 在循环中等待全部连接关闭

- 退出nginx所有进程

### 2.5.3 reload 流程

![image-20241125161324726](images/image-20241125161324726.png)



![image-20241125161336717](images/image-20241125161336717.png)

利用 reload 可以实现平滑修改配置并生效

- 向master进程发送HUP信号(reload命令)
- master进程校验配置语法是否正确
- master进程打开新的监听端口
- master进程用新配置启动新的worker子进程
- master进程向老worker子进程发送QUIT信号，老的worker对已建立连接继续处理，处理完才会优 雅退出.未关闭的worker旧进程不会处理新来的请求
- 老worker进程关闭监听句柄，处理完当前连接后结束进程

# 3 Nginx 核心模块

## 3.1 配置文件说明

nginx 官方帮助文档

```http
http://nginx.org/en/docs/
```

tengine 帮助文档

```http
http://tengine.taobao.org/nginx_docs/cn/docs/
```

Nginx的配置文件的组成部分：

- 主配置文件：nginx.conf
- 子配置文件: include conf.d/*.conf
- fastcgi， uwsgi，scgi 等协议相关的配置文件
- mime.types：支持的mime类型，MIME(Multipurpose Internet Mail Extensions)多用途互联网邮 件扩展类型，MIME消息能包含文本、图像、音频、视频以及其他应用程序专用的数据，是设定某 种扩展名的文件用一种应用程序来打开的方式类型，当该扩展名文件被访问的时候，浏览器会自动 使用指定应用程序来打开。多用于指定一些客户端自定义的文件名，以及一些媒体文件打开方式。 MIME参考文档：https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics_of_HTTP/MIME_ Types

nginx配置文件格式说明

```http
配置文件由指令与指令块构成
每条指令以;分号结尾，指令与值之间以空格符号分隔
可以将多条指令放在同一行,用分号分隔即可,但可读性差,不推荐
指令块以{ }大括号将多条指令组织在一起,且可以嵌套指令块
include语句允许组合多个配置文件以提升可维护性
使用#符号添加注释，提高可读性
使用$符号使用变量
部分指令的参数支持正则表达式
```

Nginx主配置文件的配置指令方式：

```bash
directive value [value2 ...];

注意
(1) 指令必须以分号结尾
(2) 支持使用配置变量
    内建变量：由Nginx模块引入，可直接引用
    自定义变量：由用户使用set命令定义,格式: set variable_name value;
    引用变量：$variable_name
```

主配置文件结构：四部分

```bash
main block：主配置段，即全局配置段，对http,mail都有效

#事件驱动相关的配置
events {
 ...
}  

#http/https 协议相关配置段
http {
 ...
}

#默认配置文件不包括下面两个块
#mail 协议相关配置段
mail {
 ...
}   

#stream 服务器相关配置段
stream {
 ...
} 
```

**默认的nginx.conf配置文件格式说明**

```bash
#全局配置端，对全局生效，主要设置nginx的启动用户/组，启动的工作进程数量，工作模式，Nginx的PID路径，日志路径等。
user nginx nginx;
worker_processes  1;   #启动工作进程数数量

events { #events设置快，主要影响nginx服务器与用户的网络连接，比如是否允许同时接受多个网络连接，使用哪种事件驱动模型处理请求，每个工作进程可以同时支持的最大连接数，是否开启对多工作进程下的网络连接进行序列化等。
     worker_connections  1024;   #设置单个nginx工作进程可以接受的最大并发，作为web服务器的时候最大并发数为worker_connections * worker_processes，作为反向代理的时候为(worker_connections * worker_processes)/2
}


http { #http块是Nginx服务器配置中的重要部分，缓存、代理和日志格式定义等绝大多数功能和第三方模块都可以在这设置，http块可以包含多个server块，而一个server块中又可以包含多个location块，server块可以配置文件引入、MIME-Type定义、日志自定义、是否启用sendfile、连接超时时间和单个链接的请求上限等。
     include       mime.types;
     default_type application/octet-stream;
     sendfile       on; #作为web服务器的时候打开sendfile加快静态文件传输，指定是否使用sendfile系统调用来传输文件,sendfile系统调用在两个文件描述符之间直接传递数据(完全在内核中操作)，从而避免了数据在内核缓冲区和用户缓冲区之间的拷贝，操作效率很高，被称之为零拷贝，硬盘 >> kernel buffer (快速拷贝到kernelsocket buffer) >>协议栈。
     keepalive_timeout  65;  #长连接超时时间，单位是秒
     
     server { #设置一个虚拟机主机，可以包含自己的全局快，同时也可以包含多个location模块。比如本虚拟机监听的端口、本虚拟机的名称和IP配置，多个server 可以使用一个端口，比如都使用80端口提供web服务、
         listen       80;  #配置server监听的端口
         server_name localhost; #本server的名称，当访问此名称的时候nginx会调用当前serevr内部的配置进程匹配。 
         location / { #location其实是server的一个指令，为nginx服务器提供比较多而且灵活的指令，都是在location中体现的，主要是基于nginx接受到的请求字符串，对用户请求的UIL进行匹配，并对特定的指令进行处理，包括地址重定向、数据缓存和应答控制等功能都是在这部分实现，另外很多第三方模块的配置也是在location模块中配置。
               root   html; #相当于默认页面的目录名称，默认是安装目录的相对路径，可以使用绝对路径配置。
               index index.html index.htm; #默认的页面文件名称
         }
         error_page   500 502 503 504 /50x.html; #错误页面的文件名称
         location = /50x.html { #location处理对应的不同错误码的页面定义到/50x.html，这个跟对应其server中定义的目录下。
              root   html;  #定义默认页面所在的目录
         }
     }
     
     #导入其他路径的配置文件
     include /apps/nginx/conf.d/*.conf

}

#和邮件相关的配置
#mail {
#               ...
#       }         mail 协议相关配置段

#tcp代理配置，1.9版本以上支持
#stream {
#               ...
#       }       stream 服务器相关配置段

```

## 3.2 全局配置

Main 全局配置段常见的配置指令分类

- 正常运行必备的配置
- 优化性能相关的配置
- 用于调试及定位问题相关的配置
- 事件驱动相关的配置

**全局配置说明:**

```bash
user nginx nginx; #启动Nginx工作进程的用户和组
worker_processes [number | auto]; #启动Nginx工作进程的数量,一般设为和CPU核心数相同
worker_cpu_affinity 00000001 00000010 00000100 00001000 | auto ; #将Nginx工作进程绑定到指定的CPU核心, 默认Nginx是不进行进程绑定的，绑定并不是意味着当前nginx进程独占以一核心CPU，但是可以保证此进程不会运行在其他核心上，这就极大减少了nginx的工作进程在不同的cpu核心上的来回跳转，减少了CPU对进程的资源分配与回收以及内存管理等，因此可以有效的提升nginx服务器的性能。

CPU MASK: 00000001：0号CPU
          00000010：1号CPU
          10000000：7号CPU
          
#示例:
worker_cpu_affinity 0001 0010 0100 1000;第0号---第3号CPU
worker_cpu_affinity 1000 0100 0010 0001;
worker_cpu_affinity 0101 1010; 

#示例
worker_processes  4;
worker_cpu_affinity 00000010 00001000 00100000 10000000;
root@ubutun2204-1:# ps axo pid,cmd,psr | grep nginx
31093 nginx: master process /apps   1
 34474 nginx: worker process         1
 34475 nginx: worker process         3
 34476 nginx: worker process         5
 34477 nginx: worker process         7
 35751 grep nginx

#auto 绑定CPU
#The special value auto (1.9.10) allows binding worker processes automatically to available CPUs:
worker_processes auto; 
worker_cpu_affinity auto;
#The optional mask parameter can be used to limit the CPUs available for automatic binding:
worker_cpu_affinity auto 01010101;

#错误日志记录配置，语法：error_log file [debug | info | notice | warn | error | crit | alert | emerg]
#error_log logs/error.log;
#error_log logs/error.log notice;

error_log /apps/nginx/logs/error.log error; 

#pid文件保存路径
pid       /apps/nginx/logs/nginx.pid;

worker_priority 0; #工作进程优先级，-20~20(19)
worker_rlimit_nofile 65536; #所有worker进程能打开的文件数量上限,包括:Nginx的所有连接（例如与代理服务器的连接等），而不仅仅是与客户端的连接,另一个考虑因素是实际的并发连接数不能超过系统级别的最大打开文件数的限制.最好与ulimit -n 或者limits.conf的值保持一致,默认不限制

daemon off;  #前台运行Nginx服务用于测试、或者以容器运行时，需要设为off
master_process off|on; #是否开启Nginx的master-worker工作模式，仅用于开发调试场景,默认为on


events {
    worker_connections  65536;  #设置单个工作进程的最大并发连接数，默认512，生产建议根据性能修改更大的值
    use epoll; #使用epoll事件驱动，Nginx支持众多的事件驱动，比如:select、poll、epoll，只能设置在events模块中设置。
    accept_mutex on; #mutex互斥为on表示同一时刻一个请求轮流由worker进程处理,而防止被同时唤醒所有worker,避免多个睡眠进程被唤醒的设置，可以避免多个 worker 进程竞争同一连接而导致性能下降,也可以提高统的稳定性,默认为off，新请求会唤醒所有worker进程,此过程也称为"惊群"，在高并发的场景下多个worker进程可以各自同时接受多个新的连接请求，如果是多CPU和worker进程绑定,就可以提高吞吐量
    multi_accept on; #on时Nginx服务器的每个工作进程可以同时接受多个新的网络连接，此指令默认为off，即默认为一个工作进程只能一次接受一个新的网络连接，打开后几个同时接受多个。建议设置为on 
}
```

范例: 实现 nginx 的高并发配置

```bash
[root@centos7 ~]#ulimit -n 102400
[root@centos7 ~]#while true;do ab -c 5000 -n 10000 http://10.0.0.8/;sleep 0.5;done

#Ubuntu内核参数默认值比较高，无需调整
[root@ubuntu2204 ~]#cat /proc/3238/limits
Limit                     Soft Limit           Hard Limit           Units
Max cpu time             unlimited           unlimited           seconds
Max file size             unlimited           unlimited           bytes
Max data size             unlimited           unlimited           bytes
Max stack size            8388608             unlimited           bytes
Max core file size        0                   unlimited           bytes
Max resident set         unlimited           unlimited           bytes
Max processes             7310                 7310                 processes
Max open files            1024                 1048576             files
Max locked memory         254492672            254492672           bytes
Max address space         unlimited           unlimited           bytes
Max file locks           unlimited           unlimited           locks
Max pending signals       7310                 7310                 signals
Max msgqueue size         819200               819200               bytes
Max nice priority         0                    0
Max realtime priority     0                    0
Max realtime timeout     unlimited           unlimited           us

[root@ubuntu2004 ~]#cat /proc/25149/limits
Limit                     Soft Limit           Hard Limit           Units
Max open files            1024                 524288               files

#Rocky8默认值比较低，需要调整
[root@rocky8 ~]#cat /proc/25658/limits
Limit                     Soft Limit           Hard Limit           Units
Max open files            1024                 262144               files

#CentOS7默认值比较低，需要调整
[root@centos7 ~]#cat /proc/23682/limits
Limit                     Soft Limit           Hard Limit           Units
Max open files            1024                 4096                 files

#默认nginx配置不支持高并发,会出现以下错误日志
[root@centos8 conf]#tail /apps/nginx/logs/error.log
2020/09/24 21:19:33 [crit] 41006#0: *1105860 open() "/apps/nginx/html/50x.html" 
failed (24: Too many open files), client: 10.0.0.7, server: localhost, request: 
"GET / HTTP/1.0", host: "10.0.0.8"
2020/09/24 21:19:33 [crit] 41006#0: accept4() failed (24: Too many open files)
2020/09/24 21:19:33 [crit] 41006#0: *1114177 open() 
"/apps/nginx/html/index.html" failed (24: Too many open files), client: 10.0.0.7, 
server: localhost, request: "GET / HTTP/1.0", host: "10.0.0.8"


#如果systemd启动,则需要修改nginx.service文件中加LimitNOFILE=100000,才能有效
root@ubutun2204-1:#vim /lib/systemd/system/nginx.service
[Service]
......
LimitNOFILE=100000
.....

#如果非systemd启动,可以修改下面pam限制
root@ubutun2204-1:#vim /etc/security/limits.conf 
*               soft   nofile          1000000
*               hard   nofile          1000000

root@ubutun2204-1:#vim /apps/nginx/conf/nginx.conf
worker_rlimit_nofile 40000;  #由2核CPU*worker_connections 20000得出
events {
   worker_connections  20000; #每个worker进程最大连接数
   use epoll;
}

root@ubutun2204-1:/apps/nginx/conf# systemctl restart nginx.service
#验证进程优先级
root@ubutun2204-1:~# ps -axo pid,cmd,nice | grep nginx
   6142 nginx: master process /apps   0
   6143 nginx: worker process        19
   6144 nginx: worker process        19
```

## 3.3 Http 配置块

http 协议相关的配置结构

```bash
http {
     ...
     ...  #各server的公共配置
     server {    #每个server用于定义一个虚拟主机,第一个server为默认虚拟服务器
     	...
     }
     server {     
         ...
         server_name   #虚拟主机名
         root     #主目录
         alias     #路径别名
         location [OPERATOR] URL {     #指定URL的特性
             ...
             if CONDITION {
             ...
             }
         }
      }
}

```

http 协议配置说明

```bash
http {
    include       mime.types;  #导入支持的文件类型,是相对于/apps/nginx/conf的目录
    default_type  application/octet-stream; #除mime.types中文件类型外,设置其它文件默认类型，访问其它类型时会提示下载不匹配的类型文件

#日志部分
    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

#自定义优化参数
    sendfile        on;
    #tcp_nopush     on; #开启sendfile的情况下，合并请求后统一发送给客户端,必须开启sendfile，此选项只有send_file为on，才可以设置为on
    #tcp_nodelay   off; #开启keepalived模式下的连接是否启用TCP_NODELAY选项，为off时，延迟0.2s发送，默认On时，不延迟发送，立即发送用户响应报文。

    #keepalive_timeout  0;
    keepalive_timeout  65;  #设置会话保持时间

    #gzip  on;  #开启文件压缩

    server {
        listen       80 default_server; #设置监听地址和端口,多个虚拟机时当前是否是默认的虚拟主机，default_server表示是默认主机，否则排在前面server为默认主机

        server_name  localhost;  #设置server name，可以以空格隔开写多个并支持正则表达式，如:*.wang.com www.wang.* ~^www\d+\.wang\.com$ 示例: .wang.org 相当于 *.wang.org和wang.org

        #charset koi8-r; #设置编码格式，默认是俄语格式，建议改为utf-8
        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            root   html;
            index  index.html index.htm;
        }

        #error_page  404              /404.html;

        # redirect server error pages to the static page /50x.html
        #
        error_page   500 502 503 504  /50x.html; #定义错误页面
        location = /50x.html {
            root   html;
        }

        # proxy the PHP scripts to Apache listening on 127.0.0.1:80
        #
        #location ~ \.php$ { #以http的方式转发php请求到指定web服务器
        #    proxy_pass   http://127.0.0.1;
        #}

        # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
        #
        #location ~ \.php$ {  #以fastcgi的方式转发php请求到php处理
        #    root           html;
        #    fastcgi_pass   127.0.0.1:9000;
        #    fastcgi_index  index.php;
        #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
        #    include        fastcgi_params;
        #}

        # deny access to .htaccess files, if Apache's document root
        # concurs with nginx's one
        #
        #location ~ /\.ht { #拒绝web形式访问指定文件，如很多的网站都是通过.htaccess文件来改变自己的重定向等功能
        #    deny  all;
        #}
    }


    # another virtual host using mix of IP-, name-, and port-based configuration
    #
    #server { #自定义虚拟server
    #    listen       8000;
    #    listen       somename:8080;
    #    server_name  somename  alias  another.alias;

    #    location / {
    #        root   html;
    #        index  index.html index.htm; #指定默认网页文件，此指令由ngx_http_index_module模块提供

    #    }
    #}


    # HTTPS server
    #
    #server { #https服务器配置
    #    listen       443 ssl;
    #    server_name  localhost;

    #    ssl_certificate      cert.pem;
    #    ssl_certificate_key  cert.key;

    #    ssl_session_cache    shared:SSL:1m;
    #    ssl_session_timeout  5m;

    #    ssl_ciphers  HIGH:!aNULL:!MD5;
    #    ssl_prefer_server_ciphers  on;

    #    location / {
    #        root   html;
    #        index  index.html index.htm;
    #    }
    #}

}
```

### 3.3.1 MIME

```bash
#在响应报文中将指定的文件扩展名映射至MIME对应的类型
include           /etc/nginx/mime.types;
default_type     application/octet-stream;#除mime.types中的类型外，指定其它文件的默认MIME类型，浏览器一般会提示下载
types {
   text/html html;
   image/gif gif;
   image/jpeg jpg;
}

#MIME参考文档：
https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics_of_HTTP/MIME_Types
```

范例：识别php文件为text/html

```bash
root@ubutun2204-1:~# cat   /apps/nginx/html/test.php
<?php
phpinfo();
?>

root@ubutun2204-1:~# curl -I 192.168.159.104/test.php
HTTP/1.1 200 OK
Server: nginx/1.26.2
Date: Mon, 25 Nov 2024 09:21:57 GMT
Content-Type: application/octet-stream #为默认的mime.type
Content-Length: 20
Last-Modified: Mon, 25 Nov 2024 09:21:20 GMT
Connection: keep-alive
ETag: "67444190-14"
Accept-Ranges: bytes


#修改默认的mime.type
root@ubutun2204-1:~# vim /apps/nginx/conf/nginx.conf
http {
   include       mime.types;
   default_type text/html;
......


root@ubutun2204-1:~# systemctl restart nginx.service

root@ubutun2204-1:~# curl -I 192.168.159.104/test.php
HTTP/1.1 200 OK
Server: nginx/1.26.2
Date: Mon, 25 Nov 2024 09:24:14 GMT
Content-Type: text/html
Content-Length: 20
Last-Modified: Mon, 25 Nov 2024 09:21:20 GMT
Connection: keep-alive
ETag: "67444190-14"
Accept-Ranges: bytes
```

### 3.3.2 指定响应报文server首部

```bash
#是否在响应报文的Server首部显示nginx版本
server_tokens on | off | build | string;
```

范例: 修改server字段

```bash
如果想自定义响应报文的nginx版本信息，需要修改源码文件，重新编译:

如果server_tokens on，修改 src/core/nginx.h 修改第13-14行，如下示例
#define NGINX_VERSION     "1.68.9"
#define NGINX_VER         "wanglei/" NGINX_VERSION

如果server_tokens off，修改 src/http/ngx_http_header_filter_module.c 
第49行，如下示例：
static char ngx_http_server_string[] = "Server: nginx" CRLF;
把其中的nginx改为自己想要的文字即可,如：wanginx 

```

范例: 修改 Server 头部信息

```bash
# server_tokens 为on
root@ubutun2204-1:~# vim /usr/local/src/nginx-1.26.2/src/core/nginx.h
#define NGINX_VERSION     "1.68.9"
#define NGINX_VER         "wanginx/" NGINX_VERSION 

root@ubutun2204-1:~# curl -I 192.168.159.104
HTTP/1.1 200 OK
Server: wanginx/1.68.9 #已经修改了
Date: Thu, 24 Sep 2020 07:44:05 GMT
Content-Type: text/html
Content-Length: 8
Last-Modified: Wed, 23 Sep 2020 14:39:21 GMT
Connection: keep-alive
ETag: "5f6b5e19-8"
Accept-Ranges: bytes

# server_tokens 为off
root@ubutun2204-1:~#vim /apps/nginx/conf/conf.d/pc.conf 
server {
     ......
     server_tokens off; 
     ......

root@ubutun2204-1:~# vim nginx-1.18.0/src/http/ngx_http_header_filter_module.c
static u_char ngx_http_server_string[] = "Server: wang-nginx" CRLF;

[root@centos7 ~]#curl -I 192.168.159.104
HTTP/1.1 200 OK
Server: wang-nginx #已经修改了
Date: Thu, 24 Sep 2020 07:44:59 GMT
Content-Type: text/html
Content-Length: 8
Last-Modified: Wed, 23 Sep 2020 14:39:21 GMT
Connection: keep-alive
ETag: "5f6b5e19-8"
Accept-Ranges: bytes
```

### 3.3.3 指定字符集

指定字符集utf-8，防止网页显示乱码

```bash
#是否在响应报文中的Content-Type显示指定的字符集，默认off不显示
charset charset | off;

#示例
charset utf-8;
```

## 3.4 常见核心模块配置

基于不同的IP、不同的端口以及不用得域名实现不同的虚拟主机，依赖于核心模块

**ngx_http_core_module**实现。

### 3.4.1 新建 PC Web 站点

```bash
#定义子配置文件路径
root@ubutun2204-1:~# mkdir /apps/nginx/conf/conf.d
root@ubutun2204-1:~# vim /apps/nginx/conf/nginx.conf
http {
 ......
 include /apps/nginx/conf/conf.d/*.conf; #在配置文件的最后面添加此行,注意不要放在最前面,会导致前面的命令无法生效
}

#创建PC网站配置
root@ubutun2204-1:~# cat /apps/nginx/conf/conf.d/pc.conf
server {
 listen 80 default_server;
 server_name www.wanglei.org;
 root /data/nginx/html/pc;
 }

root@ubutun2204-1:~# mkdir -p /data/nginx/html/pc
root@ubutun2204-1:~# echo "pc web" > /data/nginx/html/pc/index.html

#访问测试
root@ubutun2204-1:~# systemctl reload nginx.service 
root@ubutun2204-1:~# curl -H "Host: www.wanglei.org" 192.168.159.104
pc web
```

### 3.4.2 新建 Mobile Web 站点

![image-20241125174219515](images/image-20241125174219515.png)

```bash
root@ubutun2204-1:~# cat /apps/nginx/conf/conf.d/mobile.conf 
server {
 listen 80;
 server_name m.wanglei.org;
 root /data/nginx/html/mobile;
}

oot@ubutun2204-1:~# mkdir -p /data/nginx/html/mobile 
root@ubutun2204-1:~# echo "mobile web" >> /data/nginx/html/mobile/index.html


root@ubutun2204-1:~# systemctl reload nginx.service 
root@ubutun2204-1:~# curl -H "Host: m.wanglei.org" 192.168.159.104
mobile web
```

### 3.4.3 root 与 alias 指令

root：指定web的家目录，在定义location的时候，文件的绝对路径等于` root+location`

范例：

```bash
root@ubutun2204-1:~# cat /apps/nginx/conf/conf.d/pc.conf
server {
     listen 80;
     server_name www.wang.org;
     location / {
       root /data/nginx/html/pc;
     }
     location /about {
       root /opt/html; #必须要在html目录中创建一个名为about的目录才可以访问，否则报错。
     }
}

root@ubutun2204-1:~# mkdir -p /opt/html/about
root@ubutun2204-1:~# echo about > /opt/html/about/index.html

#重启Nginx并访问测试
```

alias：定义路径别名，会把访问的路径重新定义到其指定的路径,文档映射的另一种机制;仅能用于 location上下文,此指令使用较少

范例：

```bash
root@ubutun2204-1:~# cat /apps/nginx/conf/conf.d/pc.conf
server {
     listen 80;
     server_name www.wang.org;
     location / {
       root /data/nginx/html/pc;
     }
     location /about { #注意about后不要加/ , 使用alias的时候uri后面如果加了斜杠,则下面的路径配置必须加斜杠，否则403
       alias /opt/html/about; #当访问about的时候，会显示alias定义的/opt/html/about里面的内容。
     }
}
#重启Nginx并访问测试
```

注意：location中使用root指令和alias指令的意义不同

```http
root 给定的路径对应于location中的/uri 左侧的/
alias 给定的路径对应于location中的/uri 的完整路径 
```

### 3.4.4 location 指令

在一个server中location配置段可存在多个，用于实现从uri到文件系统的路径映射；ngnix会根据用户请 求的URI来检查定义的所有location，按一定的优先级找出一个最佳匹配，而后应用其配置

在没有使用正则表达式的时候，nginx会先在server中的多个location选取匹配度最高的一个uri，uri是 用户请求的字符串，即域名后面的web文件路径，然后使用该location模块中的正则url和字符串，如果 匹配成功就结束搜索，并使用此location处理此请求。

location官方帮助：

```http
http://nginx.org/en/docs/http/ngx_http_core_module.html#location
```

```bash
#语法规则：
location [ = | ~ | ~* | ^~ ] uri { ... }

=   #用于标准uri前，需要请求字串与uri精确匹配，大小敏感,如果匹配成功就停止向下匹配并立即处理请求
^~  #用于标准uri前，表示包含正则表达式,并且匹配以指定的正则表达式开头,对uri的最左边部分做匹配检查，不区分字符大小写
~   #用于标准uri前，表示包含正则表达式,并且区分大小写
~*  #用于标准uri前，表示包含正则表达式,并且不区分大写
不带符号 #匹配起始于此uri的所有的 uri
\   #用于标准uri前，表示包含正则表达式并且转义字符。可以将 . * ?等转义为普通符号

#匹配优先级从高到低：
=, ^~, ~/~*, 不带符号
```

官方范例

```bash
location = / {
   [ configuration A ]
}
location / {
   [ configuration B ]
}
location /documents/ {
   [ configuration C ]
}
location ^~ /images/ {
   [ configuration D ]
}
location ~* \.(gif|jpg|jpeg)$ {
   [ configuration E ]
}

The “/” request will match configuration A(?), the “/index.html” request will 
match configuration B,
the “/documents/document.html” request will match configuration C, the 
“/images/1.gif” request will match configuration D, and the “/documents/1.jpg” 
request will match configuration E.
```

范例：

```bash
# cat /etc/nginx/conf.d/www.wang.org.conf
server {
     listen 80;
     server_name location.wang.org;
     location = / {
         default_type text/html;
         return 200 'location = /';
     }
     location / {
         default_type text/html;
         return 200 'location /';
     }
     location /documents/ {
         default_type text/html;
         return 200 'location /documents/';
     }
     location ^~ /images/ {
         default_type text/html;
         return 200 'location ^~ /images/';
     }
     location ~* \.(gif|jpg|jpeg)$ {
         default_type text/html;
         return 200 'location ~* \.(gif|jpg|jpeg)';
     }
}


#测试结果如下,建议是curl测试
#1.请求 http://location.wang.org/ 会被 location =/ 匹配
#2.请求 http://location.wang.org/index.html 会被 location / 匹配
#3.请求 http://location.wang.org/documents/1.html 会被 location /documents/ 匹配
#4.请求 http://location.wang.org/images/1.gif 会被 location ^~ /images/ 匹配
#5.请求 http://location.wang.org/documents/1.jpg 会被 location ~* \.(gif|jpg|jpeg)$匹配

```

#### 3.4.4.1 匹配案例-精确匹配

在server部分使用location配置一个web界面，例如：当访问nginx 服务器的/logo.jpg的时候要显示指定 html文件的内容

精确匹配一般用于匹配组织的logo等相对固定的URL,匹配优先级最高

范例: 精确匹配 logo

```bash
cat /apps/nginx/conf/conf.d/pc.conf
server {
     listen 80;
     server_name www.wanglei.org;
     location / {
       root /data/nginx/html/pc;
     }
     location = /logo.jpg {
       root /data/nginx/images;
       index index.html;
     }
}

#上传logo.jpg图片到/data/nginx/images，重启Nginx并访问测试
#访问测试：http://www.wang.org/logo.jpg
```

#### 3.4.4.2 匹配案例-区分大小写

~ 实现区分大小写的模糊匹配. 以下范例中, 如果访问uri中包含大写字母的JPG，则以下location匹配 Ax.jpg条件不成功，因为 ~ 区分大小写，当用户的请求被执行匹配时发现location中定义的是小写的 jpg，本次访问的uri匹配失败，后续要么继续往下匹配其他的location（如果有），要么报错给客户端

```bash
location ~ /A.?\.jpg { #匹配字母A开头的jpg图片，后面?表示A后面零次或一个字符
   index index.html;
   root /data/nginx/html/image;
}

#重启Nginx并访问测试
#将只能访问以小写字符的jpg图片，不能识别大写的JPG结尾的图片
```

![image-20241125180604892](images/image-20241125180604892.png)

![image-20241125180613896](images/image-20241125180613896.png)

#### 3.4.4.3 匹配案例-不区分大小写

`~*` 用来对用户请求的uri做模糊匹配，uri中无论都是大写、都是小写或者大小写混合，此模式也都会匹 配，通常使用此模式匹配用户request中的静态资源并继续做下一步操作,此方式使用较多

注意: 此方式中,对于Linux文件系统上的文件仍然是区分大小写的,如果磁盘文件不存在,仍会提示404 

```bash
#正则表达式匹配
location ~* /A.?\.jpg {
   index index.html;
   root /opt/nginx/html/image;
 }

#重启Nginx并访问测试
对于不区分大小写的location，则可以访问任意大小写结尾的图片文件,如区分大小写则只能访问Aa.jpg此
类文件，不区分大小写则可以访问除了aa.jpg以外,还有其它的资源比如Aa.JPG、aA.jPG这样的混合名称文
件，但是还同时也要求nginx服务器的资源目录有相应的文件，比如:必须有Aa.JPG,aA.jPG这样文件存在。
```

![image-20241129092246751](images/image-20241129092246751.png)



#### 3.4.4.4 匹配案例-URI开始

```bash
root@ubutun2204-1:/apps/nginx/conf/conf.d# cat pc.conf 
server {
 listen 80 default_server;
 server_name www.wanglei.org;
 location ^~ /images {
   root /data/nginx/;
   index index.html;
 }
 location /api {
   alias /data/nginx/api;
   index index.html;
 }
}

# 创建文件
root@ubutun2204-1:/apps/nginx/conf/conf.d# mkdir -p /data/nginx/images
root@ubutun2204-1:/apps/nginx/conf/conf.d# mkdir -p /data/nginx/api
root@ubutun2204-1:/apps/nginx/conf/conf.d# echo "images" > /data/nginx/images/index.html
root@ubutun2204-1:/apps/nginx/conf/conf.d# echo "api" > /data/nginx/api/index.html

#重启Nginx并访问测试，实现效果是访问/images和/api返回不同的结果
root@ubutun2204-1:/apps/nginx/conf# curl -H "Host: www.wanglei.org" http://192.168.159.104/images/
images
root@ubutun2204-1:/apps/nginx/conf# curl -H "Host: www.wanglei.org" http://192.168.159.104/api/
api
```

#### 3.4.4.5 匹配案例-文件名后缀

```bash
root@ubutun2204-1:/apps/nginx/conf# mkdir /data/nginx/static
#上传一个图片到/data/nginx/static
 location ~* \.(gif|jpg|jpeg|bmp|png|tiff|tif|ico|wmf|js|css)$ {
   root /data/nginx/static;
   index index.html;
 }
#重启Nginx并访问测试
```

#### 3.4.4.6 匹配案例-优先级

```bash
location = /1.jpg {
   root /data/nginx/static1;
   index index.html;
 }
 location /1.jpg {
   root /data/nginx/static2;
   index index.html;
}
 location ~* \.(gif|jpg|jpeg|bmp|png|tiff|tif|ico|wmf|js)$ {
   root /data/nginx/static3;
   index index.html;
 }

#匹配优先级：=, ^~, ～/～*，/
location优先级：(location =) > (location ^~ 路径) > (location ~,~* 正则顺序) > 
(location 完整路径) > (location 部分起始路径) > (/)
```

#### 3.4.4.7 生产使用案例

```bash
#直接匹配网站根会加速Nginx访问处理
location = /index.html {
   ......;
}

location / {
   ......;
}

#静态资源配置方法1
location ^~ /static/ {
   ......;
}
#静态资源配置方法2,应用较多
location ~* \.(gif|jpg|jpeg|png|css|js|ico)$ {
   ......;
}

#多应用配置
location ~* /app1 {
     ......;
}
location ~* /app2 {
     ......;
}
```

#### 3.4.4.8 Location @重定向

`location @name` 这样的location不用于常规请求处理，而是用于请求重定向

范例：

```bash
# cat /etc/nginx/conf.d/www.wanglei.org.conf
server {
 listen 80;
 server_name www.wanglei.org;
 root /data/www;
 location / {
     index index.html;
 }
 #如果出现异常,则重新定向到@error_404这个location上
 error_page 404 @error_404;
 location @error_404 {
     default_type text/html;
     charset utf8;
     return 200 '你访问的页面可能走丢了!';
 }
}
```

# 4 Nginx 常见模块

## 4.1 四层访问控制

访问控制基于模块`ngx_http_access_module`实现，可以通过匹配客户端源IP地址进行限制

注意: 如果能在防火墙设备控制,最好就不要在nginx上配置,可以更好的节约资源

官方帮助：

```http
http://nginx.org/en/docs/http/ngx_http_access_module.html
```

![image-20241129100317749](images/image-20241129100317749.png)

范例：

```bash
location = /login/ {
   root /data/nginx/html/pc;
   allow 10.0.0.0/24;
   deny all;
 }

location /about {
   alias /data/nginx/html/pc;
   index index.html;
   deny  192.168.1.1;
   allow 192.168.1.0/24;
   allow 10.1.1.0/16;
   allow 2001:0db8::/32;
   deny all;              #按先小范围在前，大范围在后排序
 }
```

## 4.2 账户认证功能

由 `ngx_http_auth_basic_module` 模块提供此功能

官方帮助:

```http
https://nginx.org/en/docs/http/ngx_http_auth_basic_module.html
```

范例：

```bash
#Ubuntu安装包
root@ubutun2204-1:~# apt -y install apache2-utils

#创建用户
#-b 非交互式方式提交密码
root@ubutun2204-1:~# htpasswd -cb /apps/nginx/conf/.htpasswd wanglei 123456
Adding password for user wanglei
root@ubutun2204-1:~# tail /apps/nginx/conf/.htpasswd
wanglei:$apr1$COkGqj6M$4q6lTrKW9qYJGySy.VdTc1

# 安全加固
root@ubutun2204-1:~# chown nginx.nginx /apps/nginx/conf/.htpasswd
root@ubutun2204-1:~# chmod 600 /apps/nginx/conf/.htpasswd

root@ubutun2204-1:~# vim /apps/nginx/conf/conf.d/pc.conf
server {
 listen 80 default_server;
 server_name www.wanglei.org;
 location = /login/ {
   root /data/nginx/html/pc;
   index index.html;
   auth_basic "login password";
   auth_basic_user_file /apps/nginx/conf/.htpasswd; #相对路径是相于/apps/nginx/conf的路径
 }
}

#重启Nginx并访问测试
```

![image-20241129104047968](images/image-20241129104047968.png)



## 4.3 自定义错误页面

自定义错误页，同时也可以用指定的响应状态码进行响应, 可用位置：`http`, `server`,` location`, `if in  location`

```http
http://nginx.org/en/docs/http/ngx_http_core_module.html#error_page

Syntax: error_page code ... [=[response]] uri;
Default: —
Context: http, server, location, if in location
```

范例: 

```bash
listen 80;
server_name www.wang.org;
error_page  500 502 503 504 /error.html;
location = /error.html {
   root /data/nginx/html;
}

#重启nginx并访问不存在的页面进行测试
```

范例: 自定义错误页面

```bash
error_page 404 /40x.html;
location = /40x.html {
 root /data/html/ ;
}
```

范例: 如果404,就转到主页

```bash
#404转为302
#error_page 404 /index.html;
error_page  404  =302 /index.html; 
error_page 500 502 503 504 /50x.html;
     location = /50x.html {
}
```

范例: 浏览器"截胡"

使用360浏览器访问基于IP的web主机上面的不存在的页面时,会自动用广告页面代替错误页面

![image-20241129105055588](images/image-20241129105055588.png)

## 4.4 自定义错误日志

 可以自定义错误日志

```bash
Syntax: error_log file [level];
Default: 
error_log logs/error.log error;
Context: main, http, mail, stream, server, location
level: debug, info, notice, warn, error, crit, alert, emerg

#关闭错误日志
error_log /dev/null;
```

范例: 

```bash
server { 
 listen 80;
 server_name www.wanglei.org;
 error_page  500 502 503 504 404 /error.html; 
 access_log /apps/nginx/logs/wanglei.org_access.log; 
 error_log /apps/nginx/logs/wanglei.org_error.log; #定义错误日志
 location = /error.html {
   root   html;
 }
}
#重启nginx并访问不存在的页面进行测试并验证是在指定目录生成新的日志文件
```

范例:

```bash
server {
   listen 80 default_server;
   server_name www.wanglei.org;
   root /data/nginx/html/pc;
   index index.html;
   error_log /apps/nginx/logs/www.wanglei.org-error.log; #全局配置启用错误日志路径
   location /login {
       error_log /dev/null;  #针对/login目录的错误日志不记录
   }
}
```

范例: 

```bash
# cat /etc/nginx/conf.d/www.wang.org.conf
server {
 listen 80;
 server_name www.wang.org;
 root /data/www;
 location / {
     index index.html;
 }
 #如果出现异常,则重新定向到@error_404这个location上
 error_page 404 @error_404;
 location @error_404 {
     default_type text/html;
     charset utf8;
     return 200 '你访问的页面可走丢了!';
 }
}
```

## 4.5 检测文件是否存在

 `try_files` 会按顺序检查文件是否存在，返回第一个找到的文件或文件夹（结尾加斜线表示为文件夹）， 如果所有文件或文件夹都找不到，会进行一个内部重定向到最后一个参数。只有最后一个参数可以引起 一个内部重定向，之前的参数只设置内部URI的指向。最后一个参数是回退URI且必须存在，否则会出现 内部500错误。

语法格式

```http
http://nginx.org/en/docs/http/ngx_http_core_module.html#try_files
Syntax: try_files file ... uri;
try_files file ... =code;
Default: —
Context: server, location
```

范例： Ubuntu 包安装默认配置

```bash
[root@ubuntu2004 ~]#cat /etc/nginx/sites-enabled/default
   location / {
        # First attempt to serve request as file, then
        # as directory, then fall back to displaying a 404.
       try_files $uri $uri/ =404;
   }
```

范例：try_files举例理解

```bash
location /images/ {
    root /opt/html/;
    try_files $uri   $uri/  /images/default.gif; 
}


当请求 127.0.0.1/images/test.gif 会依次查找： (按指定的file顺序查找)
  1、文件127.0.0.1/opt/html/images/test.gif (查找路径按root为根路径来找)
  2、文件夹 127.0.0.1/opt/html/images/test.gif/下的index文件 ($uri/ 是把访问的链接作为一个文件 夹，请求它下面的index文件)
  3、请求127.0.0.1/images/default.gif （给出的file都没匹配到，重新请求最后一个参数给定的uri，就是新的location匹配）
```

## 4.6 长连接配置

```bash
http://nginx.org/en/docs/http/ngx_http_core_module.html#keepalive_timeout

Syntax: keepalive_requests number;
Default: 
keepalive_requests 1000;
Context: http, server, location
This directive appeared in version 0.8.0.

Syntax: keepalive_time time;
Default: 
keepalive_time 1h;
Context: http, server, location
This directive appeared in version 1.19.10.

Syntax: keepalive_timeout timeout [header_timeout];
Default: 
keepalive_timeout 75s;
Context: http, server, location

keepalive_time time;      #限制对一个连接中请求处理的最长时间,到时间后续的再有新的请求会断开连接,默认1h
keepalive_timeout timeout [header_timeout];  #设置保持空闲的连接超时时长，0表示禁止长连接，默认为75s，通常配置在http字段作为站点全局配置
keepalive_requests number;  #在一次长连接上所允许请求的资源的最大数量，默认为1000次
```

范例: 

```bash
keepalive_requests 3;
keepalive_timeout  65 60;
#开启长连接后，返回客户端的会话保持时间为60s，单次长连接累计请求达到指定次数请求或65秒就会被断开，第二个数字60为发送给客户端应答报文头部中显示的超时时间设置为60s：如不设置客户端将不显示超时时间。
Keep-Alive:timeout=60  #浏览器收到的服务器返回的报文

#如果设置为0表示关闭会话保持功能，将如下显示：
Connection:close  #浏览器收到的服务器返回的报文


#使用命令测试
root@ubutun2204-1:~# curl -I www.wanglei.org
# 相应报文
HTTP/1.1 200 OK
Server: nginx/1.26.2
Date: Fri, 29 Nov 2024 03:51:14 GMT
Content-Type: text/html
Content-Length: 615
Last-Modified: Mon, 25 Nov 2024 07:40:48 GMT
Connection: keep-alive
Keep-Alive: timeout=65 #返回给客户端timeout的时间
ETag: "67442a00-267"
Accept-Ranges: bytes

```

## 4.7 作为下载服务器配置

`ngx_http_autoindex_module`模块处理以斜杠字符 "/" 结尾的请求，并生成目录列表,可以做为下载服务 配置使用

官方文档：

```http
http://nginx.org/en/docs/http/ngx_http_autoindex_module.html
```

相关指令:

```bash
Syntax:	autoindex on | off;
Default:	
autoindex off;
Context:	http, server, location

autoindex on | off;#自动文件索引功能，默为off
autoindex_exact_size on | off;  #计算文件确切大小（单位bytes），off 显示大概大小（单位K、M)，默认on
autoindex_localtime on | off ; #显示本机时间而非GMT(格林威治)时间，默认off
charset charset | off;  #指定字符编码,默认为off,中文会乱码,指定为utf8
autoindex_format html | xml | json | jsonp; #显示索引的页面文件风格，默认html
limit_rate rate; #限制响应客户端传输速率(除GET和HEAD以外的所有方法)，单位B/s,即bytes/second，默认值0,表示无限制,此指令由ngx_http_core_module提供 
set $limit_rate 4k; #也可以通变量限速,单位B/s,同时设置,此项优级高.Rate limit can also be set in the $limit_rate variable, however, since version 1.17.0, this method is not recommended:
```

范例: 实现下载站点

```bash
#注意:download不需要index.html文件
root@ubutun2204-1:~# mkdir -p /data/nginx/html/pc/download

root@ubutun2204-1:~# cat  /apps/nginx/conf/conf.d/pc.conf
server {
 listen 80 default_server;
 server_name www.wanglei.org;
 location /download {
     autoindex on; #自动索引功能
     autoindex_exact_size on; #计算文件确切大小（单位bytes），此为默认值,off只显示大概大小（单位kb、mb、gb）
     autoindex_localtime on; #on表示显示本机时间而非GMT(格林威治)时间,默为为off显示GMT时间

     charset utf8;  #支持中文
     limit_rate 1024k; #限速,默认不限速
     root /data/nginx/html/pc;
 }
}

root@ubutun2204-1:~# dd if=/dev/zero bs=1024k count=1000 of=/data/nginx/html/pc/download/test.img
#重启Nginx并访问测试下载页面
```

![image-20241129120529046](images/image-20241129120529046.png)

## 4.8 作为上传服务器

```http
限制文件大小可以通过 client_max_body_size 指令来设置，该指令通常在 http、server 或
location 块中设置，如果不设置，默认上传大小为1M。
```

以下指令控制上传数据

```bash
client_max_body_size 1m; #设置允许客户端上传单个文件的最大值，默认值为1m,上传文件超过此值会出413错误
client_body_buffer_size size; #用于接收每个客户端请求报文的body部分的缓冲区大小;默认16k;超出此大小时，其将被暂存到磁盘上的由client_body_temp_path指令所定义的位置
client_body_temp_path path [level1 [level2 [level3]]];
#设定存储客户端请求报文的body部分的临时存储路径及子目录结构和数量，目录名为16进制的数字，使用hash之后的值从后往前截取1位、2位、2位作为目录名

#配置示例：
client_max_body_size 100m;               #如果太大，上传时会出现下图的413错误,注意:如果php上传,还需要修改php.ini的相关配置
client_body_buffer_size 1024k;
client_body_temp_path   /apps/nginx/client_body_temp/ 1 2 2; #上传时,Nginx会自动创建相关目录
```

范例: 

```bash
root@ubutun2204-1:~# vim /apps/nginx/conf/conf.d/pc.conf
server {
 listen 80 default_server;
 server_name www.wanglei.org;
 location /download {
     autoindex on;
     autoindex_exact_size on;
     autoindex_localtime on;
     charset utf8;
     limit_rate 1024k;
     root /data/nginx/html/pc;
 }
 location /upload {
     client_max_body_size 100m;
     client_body_buffer_size 1024k;
     client_body_temp_path /tmp 1 2 2;     
     root /tmp;
 }
}




#测试
root@ubutun2204-1:~# ll -h /data/nginx/html/pc/download/test.img
-rw-r--r-- 1 root root 1000M Nov 29 04:03 /data/nginx/html/pc/download/test.img
root@ubutun2204-1:~# curl -T /data/nginx/html/pc/download/test.img http://www.wanglei.org/upload
<html>
<head><title>413 Request Entity Too Large</title></head>
<body>
<center><h1>413 Request Entity Too Large</h1></center>
<hr><center>nginx/1.26.2</center>
</body>
</html>
```

## 4.9 限流限速

### 4.9.1 为什么要限速

限制某个用户在一定时间内能够产生的Http请求或者限制某个用户的下载速度。

防止个别用户对资源消耗过多,导致其它用户受影响.

启用限速后,如果超过指定的阈值,则默认提示503过载保护

### 4.9.2 限速相关模块

下载限速：限制用户下载资源的速度

```bash
ngx_http_core_module
```

请求限制：限制用户单位时间内所产生的Http请求数

```bash
ngx_http_limit_req_module
```

连接限制：限制同一时间的连接数，即并发数限制

```bash
ngx_http_limit_conn_module
```

### 4.9.3 请求频率限速原理

请求频率限速的工作原理类似于漏斗

先将请求放置缓存中，然后按指定速度持续处理。当请求速度超过了处理速度会导致缓存被占满

如果还有没有放入缓存的请求，则会被丢弃。

```bash
root@ubutun2204-1:~# cat   /apps/nginx/conf/conf.d/pc.conf
server {
 listen 80 default_server;
 server_name www.wanglei.org;
 location /download {
     autoindex on;
     autoindex_exact_size on;
     autoindex_localtime on;
     charset utf8;
     limit_rate_after 100m; #下载达到100MB数据后开始限速
     limit_rate 1024k;     #限速100k
     root /data/nginx/html/pc;
 }
}
```

![image-20241129143412860](images/image-20241129143412860.png)

### 4.9.5 限制请求数

限制同一个IP的同时发起的最大请求数

指令

```bash
http://nginx.org/en/docs/http/ngx_http_limit_req_module.html

Syntax: limit_req_zone key zone=name:size rate=rate [sync];
Default: —
Context: http

Syntax: limit_req zone=name [burst=number] [nodelay | delay=number];
Default: —
Context: http, server, location

Syntax: limit_req_status code;
Default: 
limit_req_status 503;
Context: http, server, location


#示例
http {
   limit_req_zone $binary_remote_addr zone=one:10m rate=10r/s;
   ...
   server {
       ...
       location /search/ {
           limit_req zone=one burst=5;
           limit_req_status 500; #默认503,可以指定其它状态码
       }
       
# 参数说明
limit_req_zone定义在http块中，$binary_remote_addr表示以客户端IP地址的二进制形式为限流依据的key
zone=区域名字:区域大小,Zone为存放IP及URL访问频率的共享内存区域。8000个IP地址的状态信息约占用内存空间1MB，上面示例区域可以存储80000个IP地址。
rate=最大请求速率。示例中速率不能超过每秒10个请求。超过此速率的请求放入burst队列做延迟处理
burst=队列大小,当此队列满后,会中断请求报错
nodelay: 表示超过请求速率并且缓存区满后不延迟处理,立即返回503错误,不设置此项则排队

#常见的limit_req指令用法。例如，以下配置将限制来自单个 IP 地址的请求的处理速率，同时限制虚拟服务器的请求处理速率
limit_req_zone $binary_remote_addr zone=perip:10m rate=1r/s;
limit_req_zone $server_name zone=perserver:10m rate=10r/s;

server {
   ...
   limit_req zone=perip burst=5 nodelay;
   limit_req zone=perserver burst=10;
}
```

范例: 基于来源IP对下载速率限制，限制每秒处理1次请求，缓存区请求突发队列为10个

```bash
# http标签段定义请求限制, rate限制速率，限制一秒钟最多一个IP请求
#注意:$remote_addr和$binary_remote_addr的不同

http {
   limit_req_zone $binary_remote_addr  zone=req_one:10m rate=1r/s;

    server {
       listen 80;
       server_name mirrors.wang.org;
        #请求超过1r/s的请求放入burst队列被延迟处理,burst队列中请求数超过burst定义的数量，则返回
    503
       limit_req zone=req_one burst=10 nodelay;
       location / {
           root /data/mirrors/;
           index index.html;
       }
    }
 }  
 
 
 
limit_req_zone $binary_remote_addr zone=req_one:10m rate=1r/s;
#第一个参数：$binary_remote_addr表示通过这个标识来做限制，限制同一客户端ip地址。
#第二个参数：zone=req_one:10m表示生成一个大小为10M，名为req_one的内存区域用来存储访问频次信息
#第三个参数：rate=1r/s表示允许相同标识的客户端的访问频次，此处限制的是每秒1次。

limit_req zone=req_one burst=10 nodelay;
#第一个参数：zone=req_one 设置使用哪个配置区域来做限制，与上面limit_req_zone的name对应。
#第二个参数：burst=10，设置一个大小为10的缓冲区，当有大量请求过来时，超过了访问频次限制的请求可以先放到这个缓冲区内。
#第三个参数：nodelay，超过访问频次并且缓冲区也满了的时候，则会返回503，如果没有设置，则所有请求会等待排队。
```

### 4.9.6 限制并发连接数

限制同一个IP的同时发起的最大并发连接数

指令

```bash
Syntax: limit_conn_zone key zone=name:size;
Default: —
Context: http

Syntax: limit_conn zone number;
Default: —
Context: http, server, location
```

范例: 设置共享内存区域和给定键值的最大允许个连接数。超过此限制时服务器将返回503错误

```bash
# cat /etc/nginx/conf.d/mirrors.wang.org.conf

limit_conn_zone $binary_remote_addr zone=conn_zone:10m;

server {
 listen 80;
 server_name mirrors.wang.org;
 root /data/mirrors/;
 charset utf8;
 autoindex on;
 autoindex_exact_size off;
 autoindex_localtime on;
 limit_conn conn_zone 2; #限制并发2个连接
 limit_rate 100k;
 location / {
 index index.html;
 }
}
```

### 4.9.7 综合实战

实现百度云盘非会员限速限流功能:

- 当下载超过100M则限制下载速度为500k
- 限制web服务器请求数处理为1秒一个，触发值为5、限制用户仅可同时下载2个文件。
- 如果同时下载超过2个资源，则返回提示 "请联系管理员进行会员充值" 并跳转到其他页面

范例：

```bash
root@ubutun2204-1:~# cat   /apps/nginx/conf/conf.d/pc.conf
limit_req_zone $binary_remote_addr zone=req_zone:10m rate=1r/s;
limit_conn_zone $binary_remote_addr zone=conn_zone:10m;
server {
 listen 80 default_server;
 server_name www.wanglei.org;
 limit_req zone=req_zone burst=5 nodelay;
 limit_conn conn_zone 2;
 error_page 503 @error_page;
 
 location /download {
     autoindex on;
     autoindex_exact_size on;
     autoindex_localtime on;
     charset utf8;
     limit_rate_after 100m;
     limit_rate 500k;
     root /data/nginx/html/pc;
 }

 location @error_page {
     default_type text/html;
     charset utf8; 
     return 200 '温馨提示:请联系管理员进行会员充值!';
     #return https://pan.baidu.com/buy/center?tag=8&from=loginpage#/svip; 
 }
}

#先建立两次连接，再执行下面可以看到如果提示
root@ubutun2204-1:~# curl www.wanglei.org/download/test.img -v
*   Trying 192.168.159.104:80...
* Connected to www.wanglei.org (192.168.159.104) port 80 (#0)
> GET /download/test.img HTTP/1.1
> Host: www.wanglei.org
> User-Agent: curl/7.81.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 503 Service Temporarily Unavailable
< Server: nginx/1.26.2
< Date: Fri, 29 Nov 2024 06:57:51 GMT
< Content-Type: application/octet-stream
< Content-Length: 50
< Connection: keep-alive
< Keep-Alive: timeout=65
< 
* Connection #0 to host www.wanglei.org left intact
温馨提示:请联系管理员进行会员充值!
```

## 4.10 Nginx 状态页

基于 nginx 模块` ngx_http_stub_status_module` 实现，在编译安装nginx的时候需要添加编译参数 -- with-http_stub_status_module，否则配置完成之后监测会是提示语法错误

注意: 状态页显示的是整个服务器的状态,而非虚拟主机的状态

指令

```bash
http://nginx.org/en/docs/http/ngx_http_stub_status_module.html

Syntax: stub_status;
Default: —
Context: server, location
```

范例:

```bash
#配置示例：
location /nginx_status {
   stub_status;
   auth_basic           "auth login";
   auth_basic_user_file /apps/nginx/conf/.htpasswd;
   allow 192.168.0.0/16;
   allow 127.0.0.1;
   deny all;
   access_log off;
}


#状态页用于输出nginx的基本状态信息：
#输出信息示例：
Active connections: 291
server accepts handled requests
    16630948 16630948 31070465 
 上面三个数字分别对应accepts,handled,requests三个值
Reading: 6 Writing: 179 Waiting: 106

Active connections： #当前处于活动状态的客户端连接数，包括连接等待空闲连接数=reading+writing+waiting
accepts：#统计总值，Nginx自启动后已经接受的客户端请求连接的总数。
handled：#统计总值，Nginx自启动后已经处理完成的客户端请求连接总数，通常等于accepts，除非有因worker_connections限制等被拒绝的失败连接,即失败连接数=accepts-handled
requests：#统计总值，Nginx自启动后客户端发来的总的请求数。因为长连接的原因此值大于上面的accept数
Reading：#当前状态，正在读取客户端请求报文首部的连接的连接数,数值越大,说明排队现象严重,性能不足
Writing：#当前状态，正在向客户端发送响应报文过程中的连接数,数值越大,说明访问量很大
Waiting：#当前状态，正在等待客户端发出请求的空闲连接数，开启keep-alive时,Waiting+reading+writing=active connections
```

范例: 分析网站当前访问量

```bash
[root@centos7 ~]#curl -s http://wang:123456@www.wanglei.com/nginx_status 
|awk -F: 'NR==1{print $NF}'

```

![image-20241129150723028](images/image-20241129150723028.png)

## 4.11 Nginx 第三方模块

 第三模块是对nginx 的功能扩展，第三方模块需要在编译安装Nginx 的时候使用参数-`-addmodule=PATH`指定路径添加，有的模块是由公司的开发人员针对业务需求定制开发的，有的模块是开 源爱好者开发好之后上传到github进行开源的模块，nginx的第三方模块需要从源码重新编译进行支持

### 4.11.1 nginx-module-vts 模块实现流量监控

```bash
https://github.com/vozlt/nginx-module-vts
```

范例：

```bash
root@ubutun2204-1:~# cd /usr/local/src/
root@ubutun2204-1:/usr/local/src# git clone https://github.com/vozlt/nginx-module-vts.git
root@ubutun2204-1:/usr/local/src/nginx-1.26.2# ./configure --prefix=/apps/nginx --user=nginx --group=nginx --with-http_ssl_module --with-http_v2_module --with-http_realip_module --with-http_stub_status_module --with-http_gzip_static_module --with-pcre --with-stream --with-stream_ssl_module --with-stream_realip_module --add-module=/usr/local/src/nginx-module-vts
root@ubutun2204-1:/usr/local/src/nginx-1.26.2# make && make install
http {
     ......
     vhost_traffic_status_zone;
     ......
     server {
     ......
     location /status {
       vhost_traffic_status_display;
     vhost_traffic_status_display_format html; #默认不加此行，是Json格式
     }
     ......
     }
}
root@ubutun2204-1:#systemctl restart nginx
#浏览器访问:http://<nginx_ip>/status 可以看到下面显示
```

![image-20241129152806886](images/image-20241129152806886.png)

![image-20241129152811790](images/image-20241129152811790.png)

### 4.11.2 echo 模块实现信息显示

开源的echo模块可以用来打印信息,变量等

```http
https://github.com/openresty/echo-nginx-module
```

范例: 

```bash
root@ubutun2204-1:~# vim /apps/nginx/conf/conf.d/pc.conf
location /main {
     echo "hello wanglei";
     echo $remote_addr;
     echo_reset_timer;  #将计时器开始时间重置为当前时间
 }


root@ubutun2204-1:~# cd /usr/local/src/
root@ubutun2204-1:/usr/local/src# git clone https://github.com/openresty/echo-nginx-module.git
root@ubutun2204-1:/usr/local/src/nginx-1.26.2# ./configure --prefix=/apps/nginx --user=nginx --group=nginx --with-http_ssl_module --with-http_v2_module --with-http_realip_module --with-http_stub_status_module --with-http_gzip_static_module --with-pcre --with-stream --with-stream_ssl_module --with-stream_realip_module --add-module=/usr/local/src/nginx-module-vts --add-module=/usr/local/src/echo-nginx-module
root@ubutun2204-1:/usr/local/src/nginx-1.26.2# make && make install

#确认语法检测通过
root@ubutun2204-1:/usr/local/src/nginx-1.26.2# nginx -t
nginx: the configuration file /apps/nginx/conf/nginx.conf syntax is ok
nginx: configuration file /apps/nginx/conf/nginx.conf test is successful


#编译新模块需要重启nginx才能访问测试，不支持reload
root@ubutun2204-1:/usr/local/src/nginx-1.26.2# systemctl restart nginx.service

#测试查看结果
root@ubutun2204-1:~# curl http://www.wanglei.org/main
hello wanglei
192.168.159.104
```

## 4.12 Nginx 变量使用

nginx的变量可以在配置文件中引用，作为功能判断或者日志等场景使用

变量可以分为内置变量和自定义变量

内置变量是由nginx模块自带，通过变量可以获取到众多的与客户端访问相关的值。

### 4.12.1 内置变量

官方文档

```http
http://nginx.org/en/docs/varindex.html
```

常用内置变量

```bash
$remote_addr; 
#存放了客户端的地址，注意是客户端的公网IP

$proxy_add_x_forwarded_for
#此变量表示将客户端IP追加请求报文中X-Forwarded-For首部字段,多个IP之间用逗号分隔,如果请求中没有X-Forwarded-For,就使用$remote_addr
the “X-Forwarded-For” client request header field with the $remote_addr variable 
appended to it, separated by a comma. If the “X-Forwarded-For” field is not 
present in the client request header, the $proxy_add_x_forwarded_for variable is 
equal to the $remote_addr variable.


$args; 
#变量中存放了URL中的所有参数，例如:http://www.wang.org/main/index.do?
id=20190221&partner=search
#返回结果为: id=20190221&partner=search

$is_args
#如果有参数为? 否则为空
“?” if a request line has arguments, or an empty string otherwise

$document_root; 
#保存了针对当前资源的请求的系统根目录,例如:/apps/nginx/html。

$document_uri;
#和$uri相同,保存了当前请求中不包含参数的URI，注意是不包含请求的指令，比
如:http://www.wang.org/main/index.do?id=20190221&partner=search会被定义
为/main/index.do 
#返回结果为:/main/index.do

$host; 
#存放了请求的host名称

limit_rate 10240;
echo $limit_rate;
#如果nginx服务器使用limit_rate配置了显示网络速率，则会显示，如果没有设置， 则显示0

$remote_port;
#客户端请求Nginx服务器时随机打开的端口，这是每个客户端自己的端口

$remote_user;
#已经经过Auth Basic Module验证的用户名

$request_body_file;
#做反向代理时发给后端服务器的本地资源的名称

$request_method;
#请求资源的方式，GET/PUT/DELETE等

$request_filename;
#当前请求的资源文件的磁盘路径，由root或alias指令与URI请求生成的文件绝对路径，
如:/apps/nginx/html/main/index.html

$request_uri;
#全路径，包含请求参数的原始URI，包含查询字符串,不包含主机名，相当于:$document_uri?$args,例如：/main/index.do?id=20190221&partner=search 

$scheme;
#请求的协议，例如:http，https,ftp等

$server_protocol;
#保存了客户端请求资源使用的协议的版本，例如:HTTP/1.0，HTTP/1.1，HTTP/2.0等

$server_addr;
#保存了服务器的IP地址

$server_name;
#请求的服务器的主机名

$server_port;
#请求的服务器的端口号

$http_user_agent;
#客户端浏览器的详细信息

$http_cookie;
#客户端的所有cookie信息

$cookie_<name>
#name为任意请求报文首部字部cookie的key名

$http_<name>
#name为任意请求报文首部字段,表示记录请求报文的首部字段，ame的对应的首部字段名需要为小写，如果有
横线需要替换为下划线
arbitrary request header field; the last part of a variable name is the field 
name converted to lower case with dashes replaced by underscores #用下划线代替横线


#示例
echo $http_user_agent; 
echo $http_host;

$sent_http_<name>
#name为响应报文的首部字段，name的对应的首部字段名需要为小写，如果有横线需要替换为下划线,此变量有问题
echo $sent_http_server;

$arg_<name>
#此变量存放了URL中的指定参数，name为请求url中指定的参数
echo $arg_id;

$uri;
#和$document_uri相同
```

范例：

```bash
root@ubutun2204-1:~# /apps/nginx/conf/conf.d/www.conf
.....
 location /echo {
    echo hello ;
    echo $binary_remote_addr;
    echo $remote_addr;
        echo $request;
        echo $proxy_add_x_forwarded_for;
        echo $args;
        echo $document_uri;
        echo $request_uri;
        echo $document_root;
        echo $host;
        echo $request_method;
        echo $request_filename;
        echo $scheme;
        set  $test $http_host;
        echo $test;
        echo $http_User_Agent;
        echo $http_cookie;
        echo $cookie_key1;
   }
}

root@ubutun2204-1:~# curl -b 'key1=v1;key2=v2' --output - 
"http://www.wang.org/echo/index.html?id=123456&partner=search"
GET /echo/index.html?id=123456&partner=search HTTP/1.1
hello

10.0.0.7
id=123456&partner=search
/echo/index.html
/echo/index.html?id=123456&partner=search
/data/nginx/html/pc
www.wang.org
GET
/data/nginx/html/pc/echo/index.html
http
www.wang.org
curl/7.29.0
key1=v1;key2=v2
v1
```

### 4.12.2 自定义变量

假如需要自定义变量名称和值，使用指令 `set $variable value;`

语法格式：

```bash
Syntax: set $variable value;
Default: —
Context: server, location, if
```

范例:

```bash
set $name wang;
echo $name;
set $my_port $server_port;
echo $my_port;
echo "$server_name:$server_port";

#输出信息如下
root@ubutun2204-1:~#  curl www.wang.org/main
wang
80
www.wang.org:80
```

## 4.13 Nginx 自定义访问日志

 访问日志是记录客户端即用户的具体请求内容信息，而在全局配置模块中的error_log是记录nginx服务 器运行时的日志保存路径和记录日志的level，因此两者是不同的，而且Nginx的错误日志一般只有一 个，但是访问日志可以在不同server中定义多个，定义一个日志需要使用access_log指定日志的保存路 径，使用log_format指定日志的格式，格式中定义要保存的具体日志内容。

访问日志由` ngx_http_log_module` 模块实现

官方帮助文档: 

```http
http://nginx.org/en/docs/http/ngx_http_log_module.html
```

语法格式

```bash
Syntax: access_log path [format [buffer=size] [gzip[=level]] [flush=time] 
[if=condition]];
access_log off; #关闭访问日志,比如在反向代理上可以关闭日志功能
Default: 
access_log logs/access.log combined;
Context: http, server, location, if in location, limit_except
```

日志格式的常见变量

```bash
$remote_addr # 记录客户端IP地址 
$remote_user # 记录客户端用户名
$time_local # 记录通用的本地时间
$time_iso8601 # 记录ISO8601标准格式下的本地时间
$request # 记录请求的方法以及请求的http协议
$status # 记录请求状态码(用于定位错误信息)
$body_bytes_sent # 发送给客户端的资源字节数，不包括响应头的大小
$bytes_sent # 发送给客户端的总字节数$msec # 日志写入时间。单位为秒，精度是毫秒。
$http_referer # 记录从哪个页面链接访问过来的
$http_user_agent # 记录客户端浏览器相关信息
$http_x_forwarded_for #记录客户端IP地址
$request_length # 请求的长度（包括请求行，请求头和请求正文）。
$request_time # 请求花费的时间，单位为秒，精度毫秒
# 注:如果Nginx位于负载均衡器，nginx反向代理之后，web服务器无法直接获取到客 户端真实的IP地址。
# $remote_addr获取的是反向代理的IP地址。 反向代理服务器在转发请求的http头信息中，增加X-Forwarded-For信息，用来记录客户端IP地址和客户端请求的服务器地址
```

默认日志格式

```bash
http {
   log_format main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';
   access_log /var/log/nginx/access.log main;
```

### 4.13.1 自定义默认格式日志

如果是要保留日志的源格式，只是添加相应的日志内容，则配置如下：

```bash
#注意:此指令只支持http块,不支持server块
log_format access_log_format  '$remote_addr - $remote_user [$time_local] 
"$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"'
                      '$server_name:$server_port';

#注意:此指令一定要在放在log_format命令后
access_log logs/access.log   access_log_format;

#重启nginx并访问测试日志格式
==> /apps/nginx/logs/access.log <==
10.0.0.1 - - [22/Feb/2019:08:44:14 +0800] "GET /favicon.ico HTTP/1.1" 404 162 "-
" "Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:65.0) Gecko/2
0100101 Firefox/65.0" "-"www.wang.org:80

```

### 4.13.2 自定义 json 格式日志

Nginx 的默认访问日志记录内容相对比较单一，默认的格式也不方便后期做日志统计分析，生产环境中 通常将nginx日志转换为json日志，然后配合使用ELK做日志收集,统计和分析。

```bash
log_format access_json '{"@timestamp":"$time_iso8601",'
        '"host":"$server_addr",'
        '"clientip":"$remote_addr",'
        '"size":$body_bytes_sent,'
        '"responsetime":$request_time,' #总的处理时间
        '"upstreamtime":"$upstream_response_time",' #后端应用服务器处理时间
        '"upstreamhost":"$upstream_addr",'   
        '"http_host":"$host",'
        '"uri":"$uri",'
        '"xff":"$http_x_forwarded_for",'
        '"referer":"$http_referer",'
        '"tcp_xff":"$proxy_protocol_addr",'
        '"http_user_agent":"$http_user_agent",'
        '"status":"$status"}';
     access_log /apps/nginx/logs/access_json.log access_json;

#重启Nginx并访问测试日志格式,参考链接:http://json.cn/
{"@timestamp":"2019-02-
22T08:55:32+08:00","host":"10.0.0.8","clientip":"10.0.0.1","size":162,"responset
ime":0.000,"upstreamtime":"-","upstreamhost":"-
","http_host":"www.wang.org","uri":"/favicon.ico","xff":"-","referer":"-
","tcp_xff":"","http_user_agent":"Mozilla/5.0 (Windows NT 6.1; Win64; x64; 
rv:65.0) Gecko/20100101 Firefox/65.0","status":"404"}
```

### 4.13.3 Json格式的日志访问统计

```bash
#!/usr/bin/env python3
#coding:utf-8

status_200=[]
status_404=[]
with open("access_json.log") as f:
     for line in f.readlines():
         line = eval(line)
         if line.get("status") == "200":
             status_200.append(line.get)
         elif line.get("status") == "404":
             status_404.append(line.get)
         else:
             print("状态码 ERROR")
         print((line.get("clientip")))    
f.close()  
```

### 4.13.4 不记录访问日志

一个网站会包含很多元素，尤其是有大量的images、js、css等静态资源。这样的请求可以不用记录日志

```bash
#请求 favicon.ico 时，不记录日志
location /favicon.ico {
 access_log off;
 return 200;
}

#当有人访问gif、png等资源时，将日志丢入空
location ~* .*\.(gif|jpg|png|css|js)$ {
   access_log /dev/null;
}
```

## 4.14 关于 favicon.ico

favicon.ico 文件是浏览器收藏网址时显示的图标，当客户端使用浏览器问页面时，浏览器会自己主动发 起请求获取页面的favicon.ico文件，但是当浏览器请求的favicon.ico文件不存在时，服务器会记录404日 志，而且浏览器也会显示404报错

解决办法：

```bash
#方法一：服务器不记录访问日志：
location = /favicon.ico {
   log_not_found off;
   access_log off;
}

#方法二：将图标保存到指定目录访问：
#location ~ ^/favicon\.ico$ {
location = /favicon.ico {
     root   /data/nginx/html/pc/images;
     expires 365d;  #设置文件过期时间
     access_log off;
}
```

![image-20241129163523340](images/image-20241129163523340.png)

## 4.15 Nginx 压缩功能

Nginx支持对指定类型的文件进行压缩然后再传输给客户端，而且压缩还可以设置压缩比例，压缩后的 文件大小将比源文件显著变小，这样有助于降低出口带宽的利用率，降低企业的IT支出，不过会占用相 应的CPU资源。

Nginx对文件的压缩功能是依赖于模块 ngx_http_gzip_module,默认是内置模块

官方文档： https://nginx.org/en/docs/http/ngx_http_gzip_module.html

配置指令：

```bash
#启用或禁用gzip压缩，默认关闭
gzip on | off; 

#压缩比由低到高从1到9，默认为1
gzip_comp_level level;

#禁用IE6 gzip功能
gzip_disable "MSIE [1-6]\."; 

#gzip压缩的最小文件，小于设置值的文件将不会压缩
gzip_min_length 1k; 

#启用压缩功能时，协议的最小版本，默认HTTP/1.1
gzip_http_version 1.0 | 1.1; 

#指定Nginx服务需要向服务器申请的缓存空间的个数和大小,平台不同,默认:32 4k或者16 8k;
gzip_buffers number size; 

#指明仅对哪些类型的资源执行压缩操作;默认为gzip_types text/html，不用显示指定，否则出错
gzip_types mime-type ...; 

#如果启用压缩，是否在响应报文首部插入“Vary: Accept-Encoding”,一般建议打开
gzip_vary on | off; 

#预压缩，即直接从磁盘找到对应文件的gz后缀的式的压缩文件返回给用户，无需消耗服务器CPU
#注意: 来自于ngx_http_gzip_static_module模块
gzip_static on | off;
```

范例：

```bash
# 进行访问测试压缩功能
root@ubutun2204-1:~# cp /apps/nginx/logs/access.log /data/nginx/html/pc/m.txt
root@ubutun2204-1:~# echo "test" > /data/nginx/html/pc/test.html #小于1k的文件测试是否会压缩
root@ubutun2204-1:~# vim /apps/nginx/conf/nginx.conf
gzip on;
gzip_comp_level 5;
gzip_min_length 1k;
gzip_types text/plain application/javascript application/x-javascript text/css 
application/xml text/javascript application/x-httpd-php image/gif image/png;   
 
gzip_vary on;



# 重启nginx并访问测试
root@ubutun2204-1:~# curl --head --compressed http://www.wanglei.org/m.txt
HTTP/1.1 200 OK
Server: nginx/1.26.2
Date: Fri, 29 Nov 2024 08:47:15 GMT
Content-Type: text/plain
Last-Modified: Fri, 29 Nov 2024 08:42:00 GMT
Connection: keep-alive
Keep-Alive: timeout=65
Vary: Accept-Encoding
ETag: W/"67497e58-43d1"
Content-Encoding: gzip #压缩传输

#当文件小于1k不压缩
root@ubutun2204-1:~# curl --head --compressed http://www.wanglei.org/test.html
HTTP/1.1 200 OK
Server: nginx/1.26.2
Date: Fri, 29 Nov 2024 08:48:30 GMT
Content-Type: text/html
Content-Length: 5
Last-Modified: Fri, 29 Nov 2024 08:42:24 GMT
Connection: keep-alive
Keep-Alive: timeout=65
ETag: "67497e70-5"
Accept-Ranges: bytes

```

![image-20241129165013185](images/image-20241129165013185.png)



## 4.16 HttpS 加密

![image-20241129165156612](images/image-20241129165156612.png)



```http
https 实现过程如下：

1.客户端发起HTTPS请求：
客户端访问某个web端的https地址，一般都是443端口
2.服务端的配置：
采用https协议的服务器必须要有一套证书，可以通过一些组织申请，也可以自己制作，目前国内很多网站都
自己做的，当你访问一个网站的时候提示证书不可信任就表示证书是自己做的，证书就是一个公钥和私钥匙，
就像一把锁和钥匙，正常情况下只有你的钥匙可以打开你的锁，你可以把这个送给别人让他锁住一个箱子，里
面放满了钱或秘密，别人不知道里面放了什么而且别人也打不开，只有你的钥匙是可以打开的。
3.传送证书：
服务端给客户端传递证书，其实就是公钥，里面包含了很多信息，例如证书得到颁发机构、过期时间等等。
4.客户端解析证书：
这部分工作是有客户端完成的，首先回验证公钥的有效性，比如颁发机构、过期时间等等，如果发现异常则会
弹出一个警告框提示证书可能存在问题，如果证书没有问题就生成一个随机值，然后用证书对该随机值进行加
密，就像2步骤所说把随机值锁起来，不让别人看到。
5.传送4步骤的加密数据：
就是将用证书加密后的随机值传递给服务器，目的就是为了让服务器得到这个随机值，以后客户端和服务端的
通信就可以通过这个随机值进行加密解密了。
6.服务端解密信息：
服务端用私钥解密5步骤加密后的随机值之后，得到了客户端传过来的随机值(私钥)，然后把内容通过该值进
行对称加密，对称加密就是将信息和私钥通过算法混合在一起，这样除非你知道私钥，不然是无法获取其内部
的内容，而正好客户端和服务端都知道这个私钥，所以只要机密算法够复杂就可以保证数据的安全性。
7.传输加密后的信息:
服务端将用私钥加密后的数据传递给客户端，在客户端可以被还原出原数据内容
8.客户端解密信息：
客户端用之前生成的私钥获解密服务端传递过来的数据，由于数据一直是加密的，因此即使第三方获取到数据
也无法知道其详细内容。
```

### 4.16.1 Https 配置参数

nginx 的https 功能基于模块ngx_http_ssl_module实现，因此如果是编译安装的nginx要使用参数

ngx_http_ssl_module开启ssl功能，但是作为nginx的核心功能，yum安装的nginx默认就是开启的，编 译安装的nginx需要指定编译参数--with-http_ssl_module开启

官方文档：

```http
https://nginx.org/en/docs/http/ngx_http_ssl_module.html
```

配置参数如下：

```bash
ssl on | off;  
#为指定的虚拟主机配置是否启用ssl功能，此功能在1.15.0废弃，使用listen [ssl]替代
listen 443 ssl http2;

ssl_certificate /path/to/file;
#指向包含当前虚拟主机和CA的两个证书信息的文件，一般是crt文件

ssl_certificate_key /path/to/file;
#当前虚拟主机使用的私钥文件，一般是key文件

ssl_protocols [SSLv2] [SSLv3] [TLSv1] [TLSv1.1] [TLSv1.2]; 
#支持ssl协议版本，早期为ssl现在是TLS，默认为后三个,最新的浏览器已经不再支持TLS1.0和TLS1.1

ssl_session_cache off | none | [builtin[:size]] [shared:name:size];
#配置ssl缓存
   off： #关闭缓存
   none:  #通知客户端支持ssl session cache，但实际不支持
   builtin[:size]：#使用OpenSSL内建缓存，为每worker进程私有,使用此内置缓存可能会导致内存碎片
   [shared:name:size]：#在各worker之间使用一个共享的缓存，需要定义一个缓存名称和缓存空间大小，1M可以存储4000个会话信息，多个虚拟主机可以使用相同的缓存名称
   
ssl_session_timeout time; #客户端连接可以复用ssl session cache中缓存的有效时长，默认5分钟
```

示例: 官方性能优化

```bash
https://nginx.org/en/docs/http/ngx_http_ssl_module.html
To reduce the processor load it is recommended to
set the number of worker processes equal to the number of processors,
enable keep-alive connections,
enable the shared session cache,
disable the built-in session cache,
and possibly increase the session lifetime (by default, 5 minutes):

worker_processes auto;

http {
   ...
   server {
       listen              443 ssl http2;
       keepalive_timeout   70;
       ssl_protocols       TLSv1 TLSv1.1 TLSv1.2;
       ssl_ciphers         AES128-SHA:AES256-SHA:RC4-SHA:DES-CBC3-SHA:RC4-MD5;
       ssl_certificate     /usr/local/nginx/conf/cert.pem;
       ssl_certificate_key /usr/local/nginx/conf/cert.key;
       ssl_session_cache   shared:SSL:10m;
       ssl_session_timeout 10m;
       ...
   }

```

### 4.16.2 自签名证书

```bash
#自签名CA证书
root@ubutun2204-1:/apps# cd /apps/nginx/
root@ubutun2204-1:/apps/nginx# mkdir certs
root@ubutun2204-1:/apps/nginx# cd certs/
root@ubutun2204-1:/apps/nginx/certs# openssl req -newkey rsa:4096 -nodes -sha256 -keyout ca.key -x509 -days 3650 -out ca.crt #自签名CA证书
Generating a 4096 bit RSA private key
.................++
.....
Country Name (2 letter code) [XX]:CN #国家代码
State or Province Name (full name) []:BeiJing   #省份
Locality Name (eg, city) [Default City]:Beijing #城市名称
Organization Name (eg, company) [Default Company Ltd]:wang.Ltd #公司名称   
Organizational Unit Name (eg, section) []:wang #部门
Common Name (eg, your name or your server's hostname) []:ca.wang.org #通用名称
Email Address []: #邮箱

#自制key和csr文件
root@ubutun2204-1:/apps/nginx/certs# openssl req -newkey rsa:4096 -nodes -sha256 -keyout www.wang.org.key  -out www.wang.org.csr
root@ubutun2204-1:/apps/nginx/certs# openssl req -newkey rsa:4096 -nodes -sha256 -keyout www.wang.org.key  -out www.wang.org.csr
Generating a 4096 bit RSA private key
........................................................................++
......
Country Name (2 letter code) [XX]:CN
State or Province Name (full name) []:BeiJing
Locality Name (eg, city) [Default City]:BeiJing
Organization Name (eg, company) [Default Company Ltd]:wang.org
Organizational Unit Name (eg, section) []:wang.org
Common Name (eg, your name or your server's hostname) []:www.wang.org
Email Address []:2973707860@qq.com
Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:      
An optional company name []:
root@ubutun2204-1:/apps/nginx/certs# ll
-rw-r--r--  1 root  root  2000 Nov 29 09:08 ca.crt
-rw-------  1 root  root  3272 Nov 29 09:08 ca.key
-rw-r--r--  1 root  root  1712 Nov 29 09:11 www.wang.org.csr
-rw-------  1 root  root  3272 Nov 29 09:10 www.wang.org.key

#签发证书
root@ubutun2204-1:/apps/nginx/certs# openssl x509 -req -days 3650 -in www.wang.org.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out www.wang.org.crt
Certificate request self-signature ok
subject=C = AU, ST = Some-State, O = Internet Widgits Pty Ltd, CN = www.wang.org

#验证证书内容
root@ubutun2204-1:/apps/nginx/certs# openssl x509 -in www.wang.org.crt -noout -text 
Certificate:
    Data:
        Version: 1 (0x0)
        Serial Number:
            2f:07:3b:4d:66:2e:68:5e:5f:ce:42:dd:91:47:a5:14:b4:cf:b2:ec
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = AU, ST = Some-State, O = Internet Widgits Pty Ltd, CN = ca.wang.org
        Validity
            Not Before: Nov 29 09:12:31 2024 GMT
            Not After : Nov 27 09:12:31 2034 GMT
        Subject: C = AU, ST = Some-State, O = Internet Widgits Pty Ltd, CN = www.wang.org
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                Public-Key: (4096 bit)
......

#合并CA和服务器证书成一个文件,注意服务器证书必须在前,ca证书在后,否则会出错
root@ubutun2204-1:/apps/nginx/certs# cat www.wang.org.crt ca.crt > www.wang.org.pem
```

### 4.16.3 Https 配置

```bash
root@ubutun2204-1:/apps/nginx# cat conf/conf.d/https.conf 
server {
 listen 80;
 listen 443 ssl http2;
 server_name www.wang.org;
 ssl_certificate /apps/nginx/certs/www.wang.org.pem;
 ssl_certificate_key /apps/nginx/certs/www.wang.org.key;
 ssl_session_cache shared:sslcache:20m;
 ssl_session_timeout 10m;
 root /data/nginx/html; 
}

#重启nginx，浏览器访问
```

![image-20241129171826687](images/image-20241129171826687.png)

![image-20241129172007618](images/image-20241129172007618.png)



### 4.16.4 实现多域名 Https

Nginx 支持基于单个IP实现多域名的功能，并且还支持单IP多域名的基础之上实现HTTPS，其实是基于 Nginx的 SNI（Server Name Indication）功能实现，SNI是为了解决一个Nginx服务器内使用一个IP绑定 多个域名和证书的功能，其具体功能是客户端在连接到服务器建立SSL链接之前先发送要访问站点的域名 （Hostname），这样服务器再根据这个域名返回给客户端一个合适的证书。

```bash
# 制作m.wang.org证书和之前一样

#nginx配置
#Nginx 配置
[root@centos8 certs]# cat /apps/nginx/conf/conf.d/mobile.conf 
server {
     listen 80 default_server;
     server_name m.wang.org;
     rewrite ^(.*)$ https://$server_name$1 permanent;
}
server {
     listen 443 ssl http2;
     server_name m.wang.org;
     ssl_certificate /apps/nginx/certs/m.wang.org.pem;
     ssl_certificate_key /apps/nginx/certs/m.wang.org.key;
     ssl_session_cache shared:sslcache:20m;
     ssl_session_timeout 10m;
     location / {
       root "/data/nginx/html/mobile";
     }
    location /mobile_status {
       stub_status;
 }
}

```

### 4.16.5 实现 HSTS

**HTTP Strict Transport Security** (通常简称为*HSTS*) 是一个安全功能，它告诉浏览器只能通过HTTPS访问当前资源, 禁止[HTTP](https://developer.mozilla.org/en/HTTP)方式

官方文档:

```http
https://www.nginx.com/blog/http-strict-transport-security-hsts-and-nginx/
```

**注意: 配置rewrite才能实现http跳转到https**

范例: 

```bash
server {
   listen 443 ssl http2;
   server_name www.wang.org;
   add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" 
always;
   location / {
       if ( $scheme = http ) {
         rewrite ^/(.*)$ https://www.wang.org/$1 redirect;                     
                          
       }
   .....
   }
}
```

范例:

```bash
root@ubutun2204-1:/apps/nginx# vim  conf/conf.d/https.conf
server {
 listen 80;
 listen 443 ssl http2;
 server_name www.wang.org;
 ssl_certificate /apps/nginx/certs/www.wang.org.pem;
 ssl_certificate_key /apps/nginx/certs/www.wang.org.key;
 ssl_session_cache shared:sslcache:20m;
 ssl_session_timeout 10m;
 error_log /apps/nginx/logs/wang.org_error.log;
 access_log /apps/nginx/logs/wang.org_access.log;
 add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
 location / {
   root /data/nginx/html/pc;
   if ( $scheme = http ) {
         rewrite ^/(.*)$ https://www.wang.org/$1 redirect;
   }
 }
}


root@ubutun2204-1:/apps/nginx# systemctl restart nginx.service

root@ubutun2204-1:/apps/nginx# curl -ikL https://www.wang.org
HTTP/2 200 
server: nginx/1.26.2
date: Fri, 29 Nov 2024 09:55:28 GMT
content-type: text/html
content-length: 7
last-modified: Mon, 25 Nov 2024 09:39:26 GMT
etag: "674445ce-7"
strict-transport-security: max-age=31536000; includeSubDomains
accept-ranges: bytes

pc web
```

## 4.17 升级 OpenSSL 版本

OpenSSL 程序库当前广泛用于实现互联网的传输层安全（TLS）协议。心脏出血（Heartbleed），也简 称为心血漏洞，是一个出现在加密程序库OpenSSL的安全漏洞，此漏洞于2012年被引入了软件中， 2014年4月首次向公众披露。只要使用的是存在缺陷的OpenSSL实例，无论是服务器还是客户端，都可 能因此而受到攻击。此问题的原因是在实现TLS的心跳扩展时没有对输入进行适当验证（缺少边界检 查），因此漏洞的名称来源于“心跳”（heartbeat）。该程序错误属于缓冲区过读，即可以读取的数据比 应该允许读取的还多。

范例: 升级OpenSSL解决安全漏洞

```bash
#准备OpenSSL源码包：
[root@centos8 ~]#cd /usr/local/src
[root@centos8 src]#wget https://www.openssl.org/source/openssl-1.1.1h.tar.gz
[root@centos8 src]#tar xvf openssl-1.1.1h.tar.gz

#编译安装Nginx并制定新版本OpenSSL路径：
[root@centos8 ~]#cd /usr/local/src/nginx-1.18.0/
[root@centos8 nginx-1.18.0]#./configure --prefix=/apps/nginx --user=nginx --
group=nginx --with-http_ssl_module --with-http_v2_module --withhttp_realip_module
 --with-http_stub_status_module --with-http_gzip_static_module 
--with-pcre --with-stream --with-stream_ssl_module --with-stream_realip_module --
add-module=/usr/local/src/echo-nginx-module --withopenssl=/usr/local/src/openssl-1.1.1h

[root@centos8 nginx-1.18.0]#make && make install

#验证并启动Nginx：
[root@centos8 ~]#nginx -t 
nginx: the configuration file /apps/nginx/conf/nginx.conf syntax is ok
nginx: configuration file /apps/nginx/conf/nginx.conf test is successful
[root@centos8 ~]#systemctl restart nginx

[root@centos8 ~]#nginx -V
nginx version: wanginx/1.68.9
built by gcc 8.3.1 20191121 (Red Hat 8.3.1-5) (GCC) 
built with OpenSSL 1.1.1h  22 Sep 2020
TLS SNI support enabled
configure arguments: --prefix=/apps/nginx --user=nginx --group=nginx --withhttp_ssl_module
 --with-http_v2_module --with-http_realip_module --withhttp_stub_status_module
 --with-http_gzip_static_module --with-pcre --with-stream 
--with-stream_ssl_module --with-stream_realip_module --addmodule=/usr/local/src/echo-nginx-module
--with-openssl=/usr/local/src/openssl1.1.1h


#Ubuntu22.04编译OpenSSL 3.0.7版,注意:较低版本的nginx不支持OpenSSL3.X版,只支持OpenSSL 
1.X版本
[root@ubuntu2204 ~]#nginx -V
nginx version: nginx/1.22.1
built by gcc 11.3.0 (Ubuntu 11.3.0-1ubuntu1~22.04) 
built with OpenSSL 3.0.7 1 Nov 2022
TLS SNI support enabled
configure arguments: --prefix=/apps/nginx --user=nginx --group=nginx --withhttp_ssl_module
 --with-http_v2_module --with-http_realip_module --withhttp_stub_status_module
 --with-http_gzip_static_module --with-pcre --with-stream 
--with-stream_ssl_module --with-stream_realip_module --addmodule=/usr/local/src/nginx-module-vts-master
--add-module=../echo-nginx-modulemaster
--with-openssl=/usr/local/src/openssl-3.0.7
```

## 4.18 Rewrite 模块

Nginx 利用 `ngx_http_rewrite_module` 模块解析和处理rewrite请求，此功能依靠 PCRE(perl  compatible regular expression)，因此编译之前要安装PCRE库

rewrite是nginx服务器的重要功能之一，用于实现常用的URL的重写，比如可以在改变网站结构之后， 不需要客户端修改原来的书签，也无需修改其它网站的链接地址，仍可继续访问原有内容，另外还可以 在一定程度上提高网站的安全性。

比如: 利用rewrite 模块可以实现下面网站URL的跳转

```http
http://www.58.com/bj --> http://beijing.58.com
http://baoji.58.com
http://www.58.com/sz --> http://shenzhen.58.com
http://suzhou.58.com 

http://www.360buy.com --> http://www.jd.com/
```

### 4.18.1 ngx_http_rewrite_module 模块指令

官方文档：https://nginx.org/en/docs/http/ngx_http_rewrite_module.html

#### 4.18.1.1 if 指令

```http
https://nginx.org/en/docs/http/ngx_http_rewrite_module.html#if
```

用于条件匹配判断，并根据条件判断结果选择不同的Nginx配置，可以配置在server或location块中进行 配置，Nginx的if语法仅能使用if做单次判断，不支持使用if else或者if elif这样的多重判断

语法如下：

```bash
yntax:	if (condition) { ... }
Default:	—
Context:	server, location
```

使用正则表达式对变量进行匹配，匹配成功时if指令认为条件为true，否则认为false，变量与表达式之 间使用以下符号链接：

```bash
= #比较变量和字符串是否相等，相等时if指令认为该条件为true，反之为false
!=  #比较变量和字符串是否不相等，不相等时if指令认为条件为true，反之为false
~ #区分大小写字符，可以通过正则表达式匹配，满足匹配条件为真，不满足匹配条件为假
!~ #区分大小写字符,判断是否匹配，不满足匹配条件为真，满足匹配条件为假

~* #不区分大小写字符，可以通过正则表达式匹配，满足匹配条件为真，不满足匹配条件为假
!~* #不区分大小字符,判断是否匹配，满足匹配条件为假，不满足匹配条件为真

-f 和 !-f #判断请求的文件是否存在和是否不存在
-d 和 !-d #判断请求的目录是否存在和是否不存在
-x 和 !-x #判断文件是否可执行和是否不可执行
-e 和 !-e #判断请求的文件或目录是否存在和是否不存在(包括文件，目录，软链接)

#注意：
#如果$变量的值为空字符串或0，则if指令认为该条件为false，其他条件为true。
#nginx 1.0.1之前$变量的值如果以0开头的任意字符串会返回false

#官方示例
if ($http_user_agent ~ MSIE) {
   rewrite ^(.*)$ /msie/$1 break;
}

if ($http_cookie ~* "id=([^;]+)(?:;|$)") {
    set $id $1;
}

if ($request_method = POST) {
   return 405;
}

if ($slow) {
   limit_rate 10k;
}

if ($invalid_referer) {
   return 403;
}
```

范例:

```bash
server {
   listen 80;
   listen 443 ssl;
   server_name www.wang.org;
   root /data/nginx/html/pc;
   ssl_certificate /apps/nginx/ssl/www.wang.org.pem;
   ssl_certificate_key /apps/nginx/ssl/www.wang.org.key;
   location /if {
       index index.html;
       default_type text/html;
        echo "if-----> $scheme";
        if (!-e $request_filename) {
            echo "$request_filename is not exist";
            #return 409;
       }
   }
}
```

范例: 拒绝curl的访问

```bash
server {
.....
   location / {
        if ($http_user_agent ~ curl) {
           return 403;
       }
       root /data/nginx/html/pc;
   }
....
}
```

#### 4.18.1.2 set 指令

指定key并给其定义一个变量，变量可以调用Nginx内置变量赋值给key，另外set定义格式为set $key  value，value可以是text, variables和两者的组合。

语法如下：

```bash
Syntax:	set $variable value;
Default:	—
Context:	server, location, if
```

范例:

```bash
location /set {
   root /data/nginx/html/pc;
   index index.html;
   default_type text/html;
    set $name wang;
    echo $name;
    set $my_port $server_port;
    echo $my_port;
}
```

范例：根据网络判断是否限速

```bash
server {
 .....
 location /set {
        set $slow 1; #如果为0,则不限速，非0限速
        if ($slow) {
           limit_rate 10k;
       }
   }
}
```

#### 4.18.1.3 break 指令

用于中断当前相同作用域(location)中的其他Nginx配置，与该指令处于同一作用域(location)的Nginx配置中，位 于它前面的配置生效，位于后面的 `ngx_http_rewrite_module` 模块中指令就不再执行，Nginx服务器 在根据配置处理请求的过程中遇到该指令的时候，回到上一层作用域继续向下读取配置，该指令可以在 server块和locationif块中使用

**注意: 如果break指令在location块中后续指令还会继续执行,只是不执行` ngx_http_rewrite_module `模 块的指令,其它指令还会执行**

语法如下：

```bash
Syntax: break;
Default: —
Context: server, location, if
```

范例：

```bash
if ($slow) {
   limit_rate 10k;
   break;
}

	location /break {
       default_type text/html;
        set $name wang;
        echo "break_before:name=$name" ;
        break;   #location块中break后面指令还会执行
        set $my_port $server_port; # set指令将不会执行
        echo "break_after:my_port=$my_port" ;
        echo "break_after:name=$name" ;
    }
    
# 测试及如果
[root@centos7 ~]#curl http://www.wang.org/break/
break_before:name=wang
break_after:my_port= 
break_after:name=wang
```

#### 4.18.1.4 return 指令

return用于完成对请求的处理，并直接向客户端返回响应状态码，比如:可以指定重定向URL(对于特殊重 定向状态码，301/302等) 或者是指定提示文本内容(对于特殊状态码403/500等)，处于此指令后的所有 配置都将不被执行，return可以在server、if 和 location块进行配置

语法：

```bash
Syntax:	return code [text];
		return code URL;
		return URL;
Default:	—
Context:	server, location, if

return code; #返回给客户端指定的HTTP状态码
return code [text]; #返回给客户端的状态码及响应报文的实体内容，可以调用变量,其中text如果有空格,需要用单或双引号
return code URL; #返回给客户端的URL地址
return URL; #302跳转返回给客户端的URL地址，注意：URL必须是完整的URL包括scheme，如:http://www.wang.org/
```

范例：

```bash
location / {
   root /data/nginx/html/pc;
   default_type text/html;
   index index.html;
    if ( $scheme = http ){
        #return 666;
        #return 666 "not allow http";
        #return 301 http://www.baidu.com;
       return 500 "service error";
        echo "if-----> $scheme"; #return后面的将不再执行
     }
     if ( $scheme = https ){
        echo "if ----> $scheme";
   }
}
```

范例: return 

```http
location /test {
     default_type application/json;
     return 200 '{"status:"success"}';
}
```

范例:  防止压力测试等工具访问

```bash
if ( $http_user_agent ~* "Wget|apachebench" ) {
 	set $user_agent_deny 1;
}
if ( $user_agent_deny =1 ) {
 	return 403;
}
```

范例: http跳转到https

```bash
# 方法0：死循环，不要使用
server {
   listen 80 ;
   listen 443 ssl;
   ssl_certificate /apps/nginx/ssl/www.wang.org.crt;
   ssl_certificate_key /apps/nginx/ssl/www.wang.org.key;
   ssl_session_cache shared:sslcache:20m;
   ssl_session_timeout 10m;
   server_name www.wang.org ;
   root /data/nginx/html/pc;
   return https://www.wang.org/;
}


#方法1
server {
     listen 80;
     server_name www.wang.org;
     return 302 https://$server_name$request_uri;
}
server {
 listen 443 ssl http2;
 server_name www.wang.org;
 ssl_certificate   /etc/nginx/ssl/www.wang.org.crt;
 ssl_certificate_key /etc/nginx/ssl/www.wang.org.key;
 location / {
     root /data/www/html; 
 }
}

#方法2
server {
   listen 80 ;
   listen 443 ssl;
   ssl_certificate /apps/nginx/ssl/www.wang.org.crt;
   ssl_certificate_key /apps/nginx/ssl/www.wang.org.key;
   ssl_session_cache shared:sslcache:20m;
   ssl_session_timeout 10m;
   server_name www.wang.org ;
   root /data/nginx/html/pc;
    if ($scheme = http) {
       return https://$server_name$request_uri;;
   }
   location = /nginx_status {
       stub_status;
   }
}   
```

### 4.18.2 rewrite 指令

通过正则表达式的匹配来改变URI，可以同时存在一个或多个指令，按照顺序依次对URI进行匹配， rewrite主要是针对用户请求的URL或者是URI做具体处理

官方文档：

```http
https://nginx.org/en/docs/http/ngx_http_rewrite_module.html#rewrite
```

`rewrite`可以配置在 `server`、`location`、`if`

语法：

```bash
Syntax:	rewrite regex replacement [flag];
Default:	—
Context:	server, location, if
```

 rewrite将用户请求的URI基于regex所描述的模式进行检查，匹配到时将其替换为表达式指定的新的  URI

**注意：如果在同一级配置块中存在多个rewrite规则，那么会自下而下逐个检查;被某条件规则替换完成 后，会重新一轮的替换检查，隐含有循环机制,但不超过10次;如果超过，提示500响应码，`[flag]`所表示 的标志位用于控制此循环机制**

如果替换后的URL是以http://或https://开头，则替换结果会直接以重定向返回给客户端, 即永久重定向  301

**正则表达式格式**

```bash
. #匹配除换行符以外的任意字符
\w #匹配字母或数字或下划线或汉字
\s #匹配任意的空白符
\d #匹配数字,相当于[0-9]
\b #匹配单词的开始或结束
^ #匹配字付串的开始
$ #匹配字符串的结束
a* #匹配重复零次或更多次
+ #匹配重复一次或更多次
? #匹配重复零次或一次
(n) #匹配重复n次
{n,} #匹配重复n次或更多次
{n,m} #匹配重复n到m次
*? #匹配重复任意次，但尽可能少重复
+? #匹配重复1次或更多次，但尽可能少重复
?? #匹配重复0次或1次，但尽可能少重复
{n,m}? #匹配重复n到m次，但尽可能少重复
{n,}? #匹配重复n次以上，但尽可能少重复
\W  #匹配任意不是字母，数字，下划线，汉字的字符
\S #匹配任意不是空白符的字符
\D #匹配任意非数字的字符
\B #匹配不是单词开头或结束的位置
[^x] #匹配除了x以外的任意字符
[^wang] #匹配除了wang 这几个字母以外的任意字符
```

官方示例

```bash
http://nginx.org/en/docs/http/ngx_http_rewrite_module.html#rewrite
Example:

server {
   ...
   rewrite ^(/download/.*)/media/(.*)\..*$ $1/mp3/$2.mp3 last;
   rewrite ^(/download/.*)/audio/(.*)\..*$ $1/mp3/$2.ra last;
   return  403;
   ...
}
But if these directives are put inside the “/download/” location, the last flag 
should be replaced by break, or otherwise nginx will make 10 cycles and return 
the 500 error:

location /download/ {
   rewrite ^(/download/.*)/media/(.*)\..*$ $1/mp3/$2.mp3 break;
   rewrite ^(/download/.*)/audio/(.*)\..*$ $1/mp3/$2.ra break;
   return  403;
}
If a replacement string includes the new request arguments, the previous request 
arguments are appended after them. If this is undesired, putting a question mark 
at the end of a replacement string avoids having them appended, for example:

rewrite ^/users/(.*)$ /show?user=$1? last;
```

#### 4.18.2.1 rewrite flag 使用介绍

利用nginx的rewrite的指令，可以实现url的重新跳转，rewrite有四种不同的flag，分别是redirect(临时 重定向302)、permanent(永久重定向301)、break和last。

其中前两种是跳转型的flag，后两种是代理型

- 跳转型指由客户端浏览器重新对新地址进行请求,客户端的浏览器地址信息会发生变化,如:301,302
- 代理型是在WEB服务器内部实现跳转,客户端的浏览器地址信息不会发生变化,如: last,break

rewrite 格式

```bash
Syntax: rewrite regex replacement [flag]; #通过正则表达式处理用户请求并返回替换后的数据包。
Default: —
Context: server, location, if
```

flag 说明:

```bash
redirect;
#临时重定向，重写完成后以临时重定向方式直接返回重写后生成的新URL给客户端，由客户端重新发起请求;使用相对路径,或者http://或https://开头，状态码：302

permanent;
#重写完成后以永久重定向方式直接返回重写后生成的新URL给客户端，由客户端重新发起请求，状态码：301

break;
#重写完成后,停止对当前URL在当前location中后续的其它重写操作，而后直接跳转至重写规则配置块之后的其它配置;不会执行其他location{}指令，结束循环，建议在location中使用
#适用于一个URL一次重写

last;
#重写完成后,停止对当前URI在当前location中后续的其它重写操作，而后对新的URL启动新一轮重写检查，不建议在location中使用
#适用于一个URL多次重写，要注意避免出现超过十次以及URL重写后返回错误的给用户
```

范例: 测试代码

```bash
root@centos8 ~]#cat /apps/nginx/conf.d/www.wang.org.conf
server {
   listen 80;
   server_name www.wang.org;
   root /data/site;
   location / {
       rewrite /1.html /2.html;  #如果没有flag，rewrite会继续执行后面的指令
       rewrite /2.html /3.html;
   }
   location /2.html {
       rewrite /2.html /a.html;
   }
   location /3.html {
       rewrite /3.html /b.html;
   }
}

#准备对应代码
[root@centos8 ~]#mkdir -p /data/site
[root@centos8 ~]# echo "1.html" >/data/site/1.html
[root@centos8 ~]# echo "2.html" >/data/site/2.html
[root@centos8 ~]# echo "3.html" >/data/site/3.html
[root@centos8 ~]# echo "a.html" >/data/site/a.html
[root@centos8 ~]# echo "b.html" >/data/site/b.html

#测试结果: 
当请求http://www.wang.org/1.html，最终将会访问/b.html
当请求http://www.wang.org/2.html，最终将会访问/a.htm
```

#### 4.18.2.2 break 与 last

##### 4.18.2.2.1 break 案例

范例：break案例

```bash
[root@centos8 ~]#cat /apps/nginx/conf.d/www.wang.org.conf
server {
  listen 80;
   server_name www.wang.org;
   root /data/site;
   location / {
       rewrite /1.html /2.html break;
       rewrite /2.html /3.html;
        #echo break;
   }
   location /2.html {
       rewrite /2.html /a.html;
   }
   location /3.html {
       rewrite /3.html /b.html;
   }
}

#测试结果
当请求/1.html，最终会访问/2.html
#原因:在location{}内部，遇到break，本location{}内以及后面的所有location{}内的所有指令都不再执行。
```

##### 4.18.2.2.2 last 案例

**`last`**：对某个location的URL匹配成功后,会停止当前location的后续rewrite规则，并结束当前location，

然后将匹配生成的新URL跳转至其他location继续匹配，直到没有location可匹配后, 将最后一次location 的数据返回给客户端。

ast 适用于要不改变客户端访问方式但是需做多次目的URL重写的场景

范例：last案例

```bash
[root@centos8 ~]#cat /apps/nginx/conf.d/www.wang.org.conf
server {
   listen 80;
   server_name www.wang.org;
   root /data/site;
   location / {
       rewrite /1.html /2.html last;
       rewrite /2.html /3.html;
   }
   location /2.html {
       rewrite /2.html /a.html;
   }
   location /3.html {
       rewrite /3.html /b.html;
   }
}

# 测试结果：当请求/1.html，最终会访问/a.html
# 原因：在location{}内部，遇到last，本location{}内后续指令不再执行，
# 而重写后的url会对所在的server{...}标签重新发起请求，从头到尾匹配一遍规则，哪个匹配则执行哪个。
```

范例: last 案例死循环

```bash
[root@centos8 ~]#cat /apps/nginx/conf.d/www.wang.org.conf
server {
   listen 80;
   server_name www.wang.org;
   root /data/site;
   location / {
       rewrite /1.html /2.html last;
       rewrite /2.html /1.html last;
   }
   location /3.html {
       rewrite /3.html /b.html;
   }
}
# 当访问/1.html 出现500的错误
# 原因: 死循环
```

##### 4.18.2.2.3 break 和 last 区别

- rewrite指令中的break和last都属于服务器内部跳转,客户端链接地址不变,客户端无感知
- 当rewrite规则遇到break指令后，本location{}后续的指令与其他location{}的所有指令都不执行。
- 当rewrite规则遇到last指令后，本location{}里后续规则不执行，但重写后的url会再次从头开始匹 配所有Location，也包括本location,哪个location先匹配到就执行哪个,可能会造成死循环500错误

#### 4.18.2.3 永久与临时重定向

域名的临时的调整，后期可能会变，之前的域名或者URL可能还用、或者跳转的目的域名和URL还会跳 转，这种情况浏览器不 会`缓存跳转`,`临时重定向不会缓存域名解析记录(A记录)`，`但是永久重定向会缓存`。

示例: 因业务需要，将访问源域名 www.wang.org 的请求永久重定向到 www.wang.com

```bash
location / {
   root /data/nginx/html/pc;
   index index.html;
   rewrite / http://www.wang.com permanent;
    #rewrite / http://www.wang.com redirect;
 }
#重启Nginx并访问域名 http://www.wang.org 进行测试
```

##### 4.18.2.3.1 永久重定向301

域名永久型调整，即域名永远跳转至另外一个新的域名，之前的域名再也不使用，跳转记录可以缓存到 客户端浏览器

永久重定向会缓存DNS解析记录, 浏览器中有 `from disk cache `信息,即使nginx服务器无法访问,浏览 器也会利用缓存进行重定向

比如: 京东早期的域名 www.360buy.com 由于与360公司类似，于是后期永久重定向到了 www.jd.com 

![image-20241201142433966](images/image-20241201142433966.png)

范例: permanent 301永久重定向

```bash
[root@centos8 ~]#cat /apps/nginx/conf.d/www.wang.org.conf
server {
   listen 80;
   server_name www.wang.org;
   root /data/site;
   location / {
       rewrite /1.html /2.html permanent;
       rewrite /2.html /3.html;
   }
}

#测试结果: 当请求/1.html，最终会访问/2.html
#原因:在location{}内部遇到permanent，客户端会重新发起新请求到新的重定向地址进行访问,而且url会修改为后面的新URL
```

##### 4.18.2.3.2 临时重定向302

域名临时重定向，告诉浏览器域名不是固定重定向到当前目标域名，后期可能随时会更改，因此浏览器 不会缓存当前域名的解析记录，而浏览器会缓存永久重定向的DNS解析记录，`这也是临时重定向与永久 重定向最大的本质区别。`

**即当nginx服务器无法访问时,浏览器不能利用缓存,而导致重定向失败**

范例: redirect 302 临时重定向

```bash
[root@centos8 ~]#cat /apps/nginx/conf.d/www.wang.org.conf
server {
   listen 80;
   server_name www.wang.org;
   root /data/site;
   location / {
       rewrite /1.html /2.html redirect ;
       rewrite /2.html /3.html;
   }
}

#测试结果: 当请求/1.html，最终会访问/2.html
#原因:在location{}内部遇到redirect，客户端会重新发起新请求到新的重定向地址进行访问,而且url会修改为后面的新URL
```

##### 4.18.2.3.3 redirect与permanent区别

redirect与permanent都会导致客户端上重新发起的请求,链接地址会发生变化,客户端可以感知到变化

| Flag      | 状 态 码 | 说明        | 特点                                                         |
| --------- | -------- | ----------- | ------------------------------------------------------------ |
| permanent | 301      | 永 久 跳 转 | 旧网站排名会被清空，新跳转网站继承原网站的排名，跳转会缓 存下来,主要用于旧域名废弃和新域名网站启用时使用 |
| redirect  | 302      | 临 时 跳 转 | 旧网站无影响，新网站会有排名,跳转不会缓存                    |

### 4.18.3 案例

#### 4.18.3.1 自动跳转 HTTPS

案例：基于通信安全考虑公司网站要求全站 https，因此要求将在不影响用户请求的情况下将http请求全 部自动跳转至 https，另外也可以实现部分 location 跳转

范例：两个 Server 实现自动跳转 HTTPS

```bash
server {
 listen 80;
 server_name www.wang.org;
 return 302 https://$server_name$request_uri;
}
server {
 listen 443 ssl http2;
 server_name www.wang.org;
 ssl_certificate   /etc/nginx/ssl/www.wang.org.crt;
 ssl_certificate_key /etc/nginx/ssl/www.wang.org.key;
 location / {
 root /data/www/html; 
 }
}
```

范例: 一个Server块和特定的URL实现自动跳转 HTTPS

```bash
[root@centos8 ~]#vim /apps/nginx/conf.d/pc.conf
server {
     listen 80;
     listen 443 ssl;
     server_name www.wang.org;
     ssl_certificate /apps/nginx/certs/www.wang.org.crt;
     ssl_certificate_key /apps/nginx/certs/www.wang.org.key;
     ssl_session_cache shared:sslcache:20m;
     ssl_session_timeout 10m;

     location / {    #针对全站跳转
       root /data/nginx/html/pc;
       index index.html;
        if ($scheme = http ){  #如果没有加条件判断，会导致死循环
           return https://www.wang.org$request_uri; #默认302
           #return 301 https://www.wang.org$request_uri;
           #return 302 https://$server_name$request_uri; #更好
           #return 301 https://$http_host$request_uri;
           #rewrite ^/(.*) https://$host/$1 redirect; #302
           #rewrite ^/(.*) https://$host/$1 permanent; #301
           #rewrite ^/(.*) https:/$server_name/$1 redirect; #更好
        }  
     }
     
     
     location /login {     #针对特定的URL进行跳转https 
     if ($scheme = http ){  #如果没有加条件判断，会导致死循环
           rewrite ^/(.*) https://$host/$1 redirect;  #302
           #rewrite / https://$host/login redirect;
       } 
     }
}



#重启Nginx并访问测试 
[root@centos7 ~]#curl -ikL www.wang.org
HTTP/1.1 302 Moved Temporarily
Server: nginx/1.26.0
Date: Thu, 08 Oct 2024 15:23:48 GMT
Content-Type: text/html
Content-Length: 145
Connection: keep-alive
Location: https://www.wang.org

HTTP/1.1 200 OK
Server: nginx/1.26.0
Date: Thu, 08 Oct 2024 15:23:48 GMT
Content-Type: text/html
Content-Length: 7
Last-Modified: Sat, 26 Sep 2024 01:18:32 GMT
Connection: keep-alive
ETag: "5f6e96e8-7"
Accept-Ranges: bytes

pc web
```

#### 4.18.3.2 判断文件是否存在

案例：当用户访问到公司网站的时输入了一个错误的URL，可以将用户重定向至官网首页

```bash
[root@centos8 ~]#vim /apps/nginx/conf.d/pc.conf
server {
   listen 80;
   server_name www.wang.org;
   location / {
   root /data/nginx/html/pc;
   index index.html;
    if (!-e $request_filename) {
       rewrite .*  http://www.wang.org/index.html; #实现客户端浏览器的302跳转
        #rewrite .* /index.html; #web服务器内部跳转
   }
 }
}
#重启Nginx并访问测试
```

#### 4.18.3.3 指定客户端类型跳转新的域名

```bash
#需求：用户通过手机设备访问 www.wang.org，跳转至m.wang.org
[root@centos8 ~]#vim /apps/nginx/conf.d/www.wang.org.conf
server {
   listen 80;
   server_name www.wang.org;
   root /data/nginx/html/pc;
    if ($http_user_agent ~* "android|iphone|ipad") {
       rewrite ^/(.*)$ http://m.wang.org/$1 redirect;
       #return 302 http://m.wang.org$request_uri ;
   }
}
```

#### 4.18.3.4 网站维护跳转

```bash
#需求: 公司网站在停机维护时，指定的IP能够正常访问，其他的IP跳转到维护页。
[root@centos8 ~]# cat /apps/nginx/conf.d/www.wang.org.conf
server {
   listen 80;
   server_name www.wang.org;
   root /data/site;
   index index.html;
    #在server层下设定ip变量值为0
    set $ip 0;
    #如果来源IP是10.0.0.101或102则设定变量为ip变量为1。
    if ($remote_addr = 10.0.0.101) {
        set $ip 1;
     }
    if ($remote_addr = 10.0.0.102) {
        set $ip 1;
   }
    #如果来源IP不是10.0.0.101或102、则跳转至/data/site/maintain.html这个页面,否则不做任
何处理
    if ($ip = 0) {
       rewrite ^(.*)$ /maintain.html break;
     }
     #如果想针对某个location进行操作，则将如上配置写入location中即可
}

```

#### 4.18.3.5 其它案例

```bash
#案例1:如果客户端浏览器包含MSIE，则rewrite客户端请求到/msie目录下
if ( $http_user_agent ~ MSIE){
 rewrite ^(.*)$ /msie/$1 break;
} 

#案例2: 更换目录访问方式,目录转换为对象存储形式
#要求:
#/20200106/static ->/static?id=20200106
#/20200123/image ->/image?id=20200123
rewrite ^/(\d+)/(.+)/   /$2?id=$1 redirect;

#案例3:多目录转换访问方式
#要求: www.wang.com/images/20200106/1.jpg => www.wang.com/index.do?
name=images&dir=20200106=&file=1.jpg
#规则配置:
if ($host ~* (.*)\.wang\.com) {
 rewrite ^/(.*)/(\d+)/(.*)$   /index.do?name=$1&dir=$2&file=$3 redirect; 
}
```

## 4.19 Nginx 防盗链

防盗链基于客户端携带的referer实现，referer是记录打开一个页面之前记录是从哪个页面跳转过来的标 记信息，如果别人只链接了自己网站图片或某个单独的资源，而不是打开了网站的整个页面，这就是盗 链，referer就是之前的那个网站域名

正常通过搜索引擎搜索web 网站并访问该网站的referer信息如下：

json格式日志:

```bash
#通过搜索引擎访问web网站的referer信息：
==> /apps/nginx/logs/access_json.log <==
{"@timestamp":"2019-02-
28T13:58:46+08:00","host":"10.0.0.100","clientip":"10.0.0.1","siz
e":0,"responsetime":0.000,"upstreamtime":"-","upstreamhost":"-
","http_host":"www.wang.org","uri":"/index.html","domain":"www.wang.org","xff":"
-","referer":"https://www.baidu.com/s?ie=utf8&f=8&rsv_bp=1&rsv_idx=1&tn=baidu&wd=www.wang.org&oq=www.wange.net&rsv_pq=d63060
680002eb69&rsv_t=de01TWnmyTdcJqph7SfI1hXgXLJxSSfUPcQ3QkWdJk%2FLNrN95ih3XOhbRs4&r
qlang=cn&rsv_enter=1&inputT=321&rsv_sug3=41&rsv_sug2=0&rsv_sug4=1626","tcp_xff":
"","http_user_agent":"Mozilla/5.0
 (Windows NT 6.1; Win64; x64) 
AppleWebKit/537.36 (KHTML, like Gecko) Chrome/72.0.3626.119 
Safari/537.36","status":"304"}
```

### 4.19.1 实现盗链

在一个web 站点盗链另一个站点的资源信息，比如:图片、视频等

```bash
#新建一个主机www.wange.org,盗取另一台主机www.wang.org的图片
[root@centos8 conf.d]# pwd
/apps/nginx/conf/conf.d

#盗链服务器配置如下
[root@centos8 conf.d]# cat wange.org.conf 
server {
     listen 80;
     server_name www.wange.org;
     location / {
       index index.html;
       root "/data/nginx/html/wange";
       access_log /apps/nginx/logs/www.wange.org_access.log main;
     }
}


#准备盗链web页面：
[root@centos8 conf.d]# mkdir /data/nginx/html/wange
[root@centos8 conf.d]# cat /data/nginx/html/wange/daolian.html 
<html>
<head>
<meta http-equiv=Content-Type content="text/html;charset=utf-8">
<title>盗链</title>
</head>
<body>
<img src="http://www.wang.org/images/logo.jpg" >
<h1 style="color:red">欢迎大家</h1>
<p><a href=http://www.wang.org>爱写代码的小男孩</a>欢迎你</p>
</body>
</html>


#重启Nginx并访问http://www.wange.org/daolian.html 测试
#验证两个域名的日志，是否会在被盗链的web站点的日志中出现以下盗链日志信息：
[root@centos8 ~]#tail /apps/nginx/logs/wang.org_access.log
10.0.0.1 - - [11/Oct/2020:09:50:07 +0800] "GET /images/logo.png HTTP/1.1" 200 
5934 "http://www.wange.org/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) 
AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.75 Safari/537.36 
Edg/86.0.622.38" "-"
```

### 4.19.2 实现防盗链

基于访问安全考虑，nginx支持通过`ngx_http_referer_module`模块,检查访问请求的referer信息是否有 效实现防盗链功能

文档：

```http
https://nginx.org/en/docs/http/ngx_http_referer_module.html
```

语法：

```bash
Syntax: valid_referers none | blocked | server_names | string ...;
Default: —
Context: server, location

none：#请求报文首部没有referer首部，比如用户直接在浏览器输入域名访问web网站，就没有referer信息。
blocked：#请求报文有referer首部，但无有效值，比如为空。
server_names：#referer首部中包含本主机名及即nginx 监听的server_name。
arbitrary_string：#自定义指定字符串，但可使用*作通配符。示例: *.wang.org www.wang.*
regular expression：#被指定的正则表达式模式匹配到的字符串,要使用~开头，例如： ~.*\.wang\.com
```

示例：

```bash
location   /images {
   root /data/nginx/html/pc;
   index index.html;
   valid_referers none blocked server_names
         *.example.com example.* www.example.org/galleries/
         ~\.google\.;
          
    if ($invalid_referer) {
     	return 403;
   }
}
```

范例: 定义防盗链：

```bash
[root@centos8 ~]# vim /apps/nginx/conf/conf.d/pc.conf
server {
   index index.html;
   valid_referers none blocked server_names *.wang.com *.wang.org   ~\.google\. 
~\.baidu\. ~\.bing\. ~\.so\. ~\.sogou\. ; #定义有效的referer
    if ($invalid_referer) { #假如是使用其他的无效的referer访问
         return 403 "Forbidden Access"; #返回状态码403
         #rewrite ^(.*)$ /testdir/images/daotu.jpg break;#或者返回错误图片
   }
......
}


#加载Nginx配置并访问测试
[root@centos8 ~]#nginx -s reload

#指定referer为http://www.baidu.com进行访问
[root@centos7 ~]# curl -e 'http://www.baidu.com' www.wang.org

#指定referer为http://www.xxx.com进行访问,被拒绝
[root@centos7 ~]# curl -e 'http://www.xxx.com' www.wang.org

#不加http的referer不会拒绝
[root@centos7 ~]# curl -e 'www.xxx.com' www.wang.org
```

在被盗链的nginx服务器查看日志

```bash
[root@centos8 ~]#tail /apps/nginx/logs/wang.org_access.log 
10.0.0.1 - - [11/Oct/2024:09:55:26 +0800] "GET /images/logo.png HTTP/1.1" 403 16 
"http://www.wange.org/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) 
AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.75 Safari/537.36 
Edg/86.0.622.38" "-"
```

# 5 Nginx 反向代理

**代理Proxy有两种**

- 正向代理：代理客户端访问服务器,可以实现缓存,科学上网,访问控制等功能
- 反向代理：reverse proxy，指的是代理外网用户的请求到内部的指定的服务器，并将数据返回给 用户的一种方式，这是用的比较多的一种方式。

![image-20241201150140896](images/image-20241201150140896.png)

Nginx 除了可以在企业提供高性能的web服务之外，另外还可以将 nginx 本身不具备的请求通过某种预 定义的协议转发至其它服务器处理，不同的协议就是Nginx服务器与其他服务器进行通信的一种规范， 主要在不同的场景使用以下模块实现不同的功能

```bash
ngx_http_proxy_module： #将客户端的请求以http协议转发至指定服务器进行处理
ngx_http_upstream_module #用于定义为proxy_pass,fastcgi_pass,uwsgi_pass等指令引用的后端服务器分组

ngx_stream_proxy_module：#将客户端的请求以tcp协议转发至指定服务器处理 
ngx_http_fastcgi_module：#将客户端对php的请求以fastcgi协议转发至指定服务器处理
ngx_http_uwsgi_module： #将客户端对Python的请求以uwsgi协议转发至指定服务器处理
```

**生产环境部署结构：**

![image-20241201150420623](images/image-20241201150420623.png)

**访问逻辑图：**

![image-20241201150530677](images/image-20241201150530677.png)

**四层(LVS)和七层(Nginx)反向代理的区别**

- 监听端口
- 参与三次握手和四次挥手
- 异构协议
- 应用数据修改
- 后端是否能看到客户端真实地址
- 性能
- 端口修改

![image-20241201150748689](images/image-20241201150748689.png)

- 工作层：LVS四层，Nginx七层
- 监听端口：LVS不监听，Nginx监听端口
- 后端服务器看到客户端地址：LVS可以，Nginx不可以
- 连接（三次握手）：LVS 不参与连接，只负责转发，Nginx代替后端服务器和客户建立连接

## 5.1 实现 Http 反向代理

### 5.1.1 Http 协议反向代理

Nginx 可以基于`ngx_http_proxy_modul`e模块提供http协议的反向代理服务

文档：

```http
https://nginx.org/en/docs/http/ngx_http_proxy_module.html
```

#### 5.1.1.1 反向代理配置参数

```bash
#官方文档：https://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_pass 
Syntax: proxy_pass URL;
Default: —
Context: location, if in location, limit_except

#用来设置将客户端请求转发给的后端服务器的主机，可以是主机名(将转发至后端服务做为主机头首部)、
IP:port 方式
#说明: proxy_pass http://FQDN/ 中的FQDN决定转发至后端哪个虚拟主机,而与用户请求的URL无关
#如果转到后端的哪个服务器由用户请求决定,可以向后端服务转发请求的主机头实现
#示例: proxy_set_header Host $http_host;

#示例:
  location /web {
   index index.html;
   proxy_pass http://10.0.0.18:8080; #8080后面无uri,即无 / 符号,需要将location后面 url 附加到proxy_pass指定的url后面,此行为类似于root
   #proxy_pass指定的uri不带斜线将访问的/web,等于访问后端服务器http://10.0.0.18:8080/web/index.html，即后端服务器配置的站点根目录下要有web目录才可以被访问
   
   # http://nginx/web/index.html ==> http://10.0.0.18:8080/web/index.html
   
   proxy_pass http://10.0.0.18:8080/;   #8080后面有uri,即有 / 符号,相当于置换,即访问/web时实际返回proxy_pass后面uri内容.此行为类似于alias 
   #proxy_pass指定的uri带斜线，等于访问后端服务器的http://10.0.0.18:8080/index.html 内容返回给客户端
 }  # http://nginx/web/index.html ==> http://10.0.0.18:8080

#重启Nginx测试访问效果：
#curl -L http://www.wang.org/web


#如果location定义其uri时使用了正则表达式模式(包括~,~*,但不包括^~)，则proxy_pass之后必须不能使用uri; 即不能有/ ,用户请求时传递的uri将直接附加至后端服务器之后
server {
     ...
     server_name HOSTNAME;
     location ~|~* /uri/ {
     proxy_pass http://host:port; #proxy_pass后面的url 不能加/
     }
     ...
 }
http://HOSTNAME/uri/ --> http://host/uri/


proxy_hide_header field;
#用于nginx作为反向代理的时候，在返回给客户端http响应时，隐藏后端服务器相应头部的信息，可以设置在http,server或location块


#示例: 隐藏后端服务器ETag首部字段
 location /web {
   index index.html;
   proxy_pass http://10.0.0.18:8080/; 
   proxy_hide_header ETag;
 }

proxy_pass_header field;
#默认nginx在响应报文中不传递后端服务器的首部字段Date, Server, X-Pad, X-Accel等参数，如果要传递的话则要使用 proxy_pass_header field声明将后端服务器返回的值传递给客户端
#field 首部字段大小不敏感

#示例:透传后端服务器的Server和Date首部给客户端,同时不再响应报中显示前端服务器的Server字段
proxy_pass_header Server;
proxy_pass_header Date;

proxy_pass_request_body on | off; 
#是否向后端服务器发送HTTP实体部分,可以设置在http,server或location块，默认即为开启

proxy_pass_request_headers on | off; 
#是否将客户端的请求头部转发给后端服务器，可以设置在http,server或location块，默认即为开启

proxy_set_header; 
#可更改或添加客户端的请求头部信息内容并转发至后端服务器，比如在后端服务器想要获取客户端的真实IP的时候，就要更改每一个报文的头部

#示例: 
#proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
$proxy_add_x_forwarded_for
the “X-Forwarded-For” client request header field with the $remote_addr variable 
appended to it, separated by a comma. If the “X-Forwarded-For” field is not 
present in the client request header, the $proxy_add_x_forwarded_for variable is 
equal to the $remote_addr variable.

proxy_set_header X-Real-IP  $remote_addr;  
#添加HOST到报文头部，如果客户端为NAT上网那么其值为客户端的共用的公网IP地址，常用于在日之中记录客户端的真实IP地址。
#在后端httpd服务器修改配置,添加日志记录X-Forwarded-For字段
LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\" \"%{XReal-IP}i\"" combined  


#在后端服务器查看日志
[root@centos8 ~]#tail /var/log/httpd/access_log   -f
10.0.0.8 - - [09/Oct/2024:21:50:57 +0800] "HEAD /static/index.html HTTP/1.0" 200 
- "-" "curl/7.29.0" "10.0.0.7"


proxy_connect_timeout time;
#配置nginx服务器与后端服务器尝试建立连接的超时时间，默认为60秒，用法如下：
proxy_connect_timeout 6s; 
#6s为自定义nginx与后端服务器建立连接的超时时间,超时会返回客户端504响应码

proxy_read_timeout time;
#配置nginx服务器向后端服务器或服务器组发起read请求后，等待的超时时间，默认60s

proxy_send_timeout time; 
#配置nginx项后端服务器或服务器组发起write请求后，等待的超时 时间，默认60s

proxy_http_version 1.0; 
#用于设置nginx提供代理服务的HTTP协议的版本，默认http 1.0,建议修改1.1支持长连接
#注意:需要配合实现proxy_set_header Connection "" 实现长连接，否则在高并发时，可能会造成server端出现大量TIME_WAIT

proxy_ignore_client_abort off; 
#当客户端网络中断请求时，nginx服务器中断其对后端服务器的请求。即如果此项设置为on开启，则服务器会忽略客户端中断并一直等着代理服务执行返回，如果设置为off，则客户端中断后Nginx也会中断客户端请求并立即记录499日志，默认为off

proxy_headers_hash_bucket_size 128;
#当配置了 proxy_hide_header和proxy_set_header的时候，用于设置nginx保存HTTP报文头的hash表的上限

proxy_headers_hash_max_size 512; 
#设置proxy_headers_hash_bucket_size的最大可用空间

server_names_hash_bucket_size 512; 
#server_names的hash表申请空间大小

server_names_hash_max_size  512; 
#设置服务器名称hash表的上限大小

proxy_next_upstream error | timeout | invalid_header | http_500 | http_502 | 
http_503 | http_504;
#当一台后端朋务器出错,超时,无效首部,500等时,切换至下一个后端服务器提供服务
```

#### 5.1.1.2 实战案例: 反向代理单台 Web 服务器

要求：将用户对域www.wanglei.org的请求转发给后端服务器处理

```bash
root@ubutun2204-1:~# cat /apps/nginx/conf/conf.d/pc.conf
server {
 listen 80;
 server_name www.wang.org;
 location / {
     proxy_pass http://10.0.0.18/; # http://10.0.0.18/ 最后的 / 可加或不加
     proxy_set_header Host  $http_host; #转发主机头至后端服务器
     proxy_connect_timeout 10s;
 }
}
#重启Nginx 并访问测试
```

如果后端服务器无法连接,比如:iptables -AINPUT -s nginx_ip -j REJECT或者systemctl stop httpd)，关机 (无后端服务器arp缓存), 会出现下面提示

![image-20241201153645287](images/image-20241201153645287.png)

默认在1分钟内后端服务器无法响应, 比如:iptables -AINPUT -s nginx_ip -j DROP或关机(有后端服务器的 arp缓存),会显示下面的504超时提示

![image-20241201153702298](images/image-20241201153702298.png)

#### 5.1.1.3 实战案例: 指定 location 实现反向代理

##### 5.1.1.3.1 针对指定的 location

```bash
# nginx服务配置
root@ubutun2204-1:~# vim /apps/nginx/conf/conf.d/pc.conf
server {
     listen 80 default_server;
     server_name www.wanglei.org;
     limit_req zone=req_zone burst=5 nodelay;
     limit_conn conn_zone 2;
     error_page 503 @error_page;

     location / {
        index index.html index.php;
        root /data/nginx/html/pc;
     }

     location /static {
        proxy_pass http://192.168.159.105:80; #后面没有 / , 表示附加http://192.168.159.105/static
 }


#后端web服务器必须要有相对于的访问URL
root@ubutun2204-1:~# mkdir /var/www/html/static
root@ubutun2204-1:~# echo "web2 page for apache" > /var/www/html/static/index.html

#重启nginx服务器访问测试
root@ubutun2204-1:~# curl -kL http://www.wang.org/
pc web
root@ubutun2204-1:~# curl -L http://www.wang.org/static
web2 page for apache

#后端web服务器log
root@backend01:~# tail /var/log/nginx/access.log 
192.168.159.104 - - [02/Dec/2024:10:59:08 +0000] "GET /static/ HTTP/1.1" 200 21 "-" "curl/7.81.0"
```

##### 5.1.1.3.2 针对特定的资源实现代理

![image-20241202190058014](images/image-20241202190058014.png)``



```bash
root@ubutun2204-1:~# vim /apps/nginx/conf/conf.d/pc.conf
server {
     listen 80 default_server;
     server_name www.wanglei.org;
     limit_req zone=req_zone burst=5 nodelay;
     limit_conn conn_zone 2;
     error_page 503 @error_page;

     location / {
        index index.html index.php;
        root /data/nginx/html/pc;
     }

     location ~ \.(jpe?g|png|bmp|gif)$  {
        proxy_pass http://192.168.159.105;     #如果加/ 语法出错
 }
```

#### 5.1.1.4 反向代理示例: 缓存功能

缓存功能默认关闭状态,需要先动配置才能启用

```bash
proxy_cache_path;
#定义可用于proxy功能的缓存;Context:http 
proxy_cache_path path [levels=levels] [use_temp_path=on|off] 
keys_zone=zone_name:size [inactive=time] [max_size=size] [manager_files=number] 
[manager_sleep=time] [manager_threshold=time] [loader_files=number] 
[loader_sleep=time] [loader_threshold=time] [purger=on|off] 
[purger_files=number] [purger_sleep=time] [purger_threshold=time];


#示例：在http配置定义缓存信息
proxy_cache_path /var/cache/nginx/proxy_cache #定义缓存保存路径，proxy_cache会自动创建
	levels=1:2:2 #定义缓存目录结构层次，1:2:2可以生成2^4x2^8x2^8=2^20=1048576个目录
	 keys_zone=proxycache:20m #指内存中缓存的大小，主要用于存放key和metadata（如：使用次数）,一般1M可存放8000个左右的key
     inactive=120s  #缓存有效时间
     max_size=10g; #最大磁盘占用空间，磁盘存入文件内容的缓存空间最大值
```

```bash
proxy_cache zone_name | off; 默认off
#指明调用的缓存，或关闭缓存机制;Context:http, server, location
#zone_name 表示缓存的名称.需要由proxy_cache_path事先定义
```

```bash
proxy_cache_key string;
#缓存中用于“键”的内容，默认值：proxy_cache_key $scheme$proxy_host$request_uri; 
```

```bash
proxy_cache_valid [code ...] time;
#定义对特定响应码的响应内容的缓存时长，定义在http{...}中
    示例:
     proxy_cache_valid 200 302 10m;
     proxy_cache_valid 404 1m;

```

```bash
#调用缓存功能，需要定义在相应的配置段，如server{...};或者location等
proxy_cache proxycache;
proxy_cache_key $request_uri; #对指定的数据进行MD5的运算做为缓存的key
proxy_cache_valid 200 302 301 10m; #指定的状态码返回的数据缓存多长时间
proxy_cache_valid any 1m;   #除指定的状态码返回的数据以外的缓存多长时间,必须设置,否则不会缓存
```

```bash
proxy_cache_use_stale error | timeout | invalid_header | updating | http_500 | 
http_502 | http_503 | http_504 | http_403 | http_404 | off ; #默认是off
#在被代理的后端服务器出现哪种情况下，可直接使用过期的缓存响应客户端

#示例
proxy_cache_use_stale error http_502 http_503;
```

```bash
proxy_cache_methods GET | HEAD | POST ...;
#对哪些客户端请求方法对应的响应进行缓存，GET和HEAD方法总是被缓存
```

**扩展知识: 清理缓存**

```bash
方法1: rm -rf 缓存目录
方法2: 第三方扩展模块ngx_cache_purge
```

##### 5.1.1.4.1 非缓存场景压测

```bash
#准备后端nginx服务器
root@backend01:~# cd /var/www/html/static/
root@backend01:/var/www/html/static# cat /var/log/syslog  > ./log.html
root@ubutun2204-1:~#  ab -n 2000 -c200 http://www.wang.org/static/log.html
Concurrency Level:      200
Time taken for tests:   0.265 seconds
Complete requests:      2000
Failed requests:        3
   (Connect: 0, Receive: 0, Length: 3, Exceptions: 0)
Non-2xx responses:      1997
Total transferred:      4435823 bytes
HTML transferred:       4065589 bytes
Requests per second:    7553.78 [#/sec] (mean)
Time per request:       26.477 [ms] (mean)
Time per request:       0.132 [ms] (mean, across all concurrent requests)
Transfer rate:          16360.96 [Kbytes/sec] received
```

##### 5.1.1.4.2 准备缓存配置

```bash
root@ubutun2204-1:~# vim +39 /apps/nginx/conf/nginx.conf
http{
	.....
	proxy_cache_path /data/nginx/proxycache levels=1:1:1 keys_zone=proxycache:20m inactive=120s max_size=1g;
	......
}

root@ubutun2204-1:~# vim /apps/nginx/conf/conf.d/pc.conf
server {
	......
	location /static { #要缓存的URL 或者放在server配置项对所有URL都进行缓存
        proxy_cache proxycache;
        proxy_cache_key $request_uri;
        proxy_cache_valid 200 302 301 10m;
        proxy_cache_valid any 5m; #必须指定哪些响应码的缓存
        proxy_set_header Host  $http_host; #转发主机头至后端服务器
        proxy_pass http://192.168.159.105:80;
     }
     ......
}

root@ubutun2204-1:~# systemctl restart nginx.service

#/data/nginx/proxycache/ 目录会自动生成
root@ubutun2204-1:~# tree  /data/nginx/proxycache/
/data/nginx/proxycache/

0 directories, 0 files
```

##### 5.1.1.4.3 访问并验证缓存文件

```BASH
#访问web并验证缓存目录
root@ubutun2204-1:~# curl http://www.wang.org/static/log.html
root@ubutun2204-1:~# ab -n2000 -c200 http://www.wang.org/static/log.html
Concurrency Level:      200
Time taken for tests:   0.162 seconds
Complete requests:      2000
Failed requests:        6
   (Connect: 0, Receive: 0, Length: 6, Exceptions: 0)
Non-2xx responses:      1994
Total transferred:      8609022 bytes
HTML transferred:       8284416 bytes
Requests per second:    12350.10 [#/sec] (mean) #性能提高近一倍
Time per request:       16.194 [ms] (mean)
Time per request:       0.081 [ms] (mean, across all concurrent requests)
Transfer rate:          51915.18 [Kbytes/sec] received


#验证缓存目录结构及文件大小
root@ubutun2204-1:~# tree /data/nginx/proxycache/
/data/nginx/proxycache/
└── d
    └── b
        └── e
            └── a971fce2cfaae636d54b5121d7a74ebd

3 directories, 1 file
```

#### 5.1.1.5 添加响应报文的头部信息

nginx基于模块`ngx_http_headers_module`可以实现对后端服务器响应给客户端的报文中添加指定的响 应首部字段

参考链接: https://nginx.org/en/docs/http/ngx_http_headers_module.html

```bash
Syntax: add_header name value [always];
Default: —
Context: http, server, location, if in location

#添加响应报文的自定义首部：
add_header name value [always]; 

#示例:
add_header X-Via   $server_addr; #当前nginx主机的IP
add_header X-Cache $upstream_cache_status; #缓存命中HIT，未命中MISS
add_header X-Accel $server_name; #客户访问的FQDN


#添加自定义响应信息的尾部，使用较少,1.13.2版后支持 
add_trailer name value [always];
```

##### 5.1.1.5.1 Nginx 配置

```bash
root@ubutun2204-1:~# vim /apps/nginx/conf/conf.d/pc.conf

server {
	......
	location /static { #要缓存的URL 或者放在server配置项对所有URL都进行缓存
        proxy_cache proxycache;
        proxy_cache_key $request_uri;
        proxy_cache_valid 200 302 301 10m;
        proxy_cache_valid any 5m; #必须指定哪些响应码的缓存
        proxy_set_header Host  $http_host; #转发主机头至后端服务器
        proxy_pass http://192.168.159.105:80;
        
        add_header X-Via  $server_addr;
        add_header X-Cache $upstream_cache_status;
        add_header X-Accel $server_name;
     }
     ......
}
```

##### 5.1.1.5.2 验证头部信息

```bash
root@ubutun2204-1:~# curl http://www.wang.org/static/log.html -I
HTTP/1.1 200 OK
Server: nginx/1.26.2
Date: Mon, 02 Dec 2024 11:38:55 GMT
Content-Type: text/html
Content-Length: 1321913
Connection: keep-alive
Keep-Alive: timeout=65
Vary: Accept-Encoding
Last-Modified: Mon, 02 Dec 2024 11:15:24 GMT
ETag: "674d96cc-142bb9"
X-Via:  192.168.159.104
X-Cache: MISS   #第一次无缓存
X-Accel: www.wanglei.org
Accept-Ranges: bytes


root@ubutun2204-1:~# curl http://www.wang.org/static/log.html -I
HTTP/1.1 200 OK
Server: nginx/1.26.2
Date: Mon, 02 Dec 2024 11:39:54 GMT
Content-Type: text/html
Content-Length: 1321913
Connection: keep-alive
Keep-Alive: timeout=65
Vary: Accept-Encoding
Last-Modified: Mon, 02 Dec 2024 11:15:24 GMT
ETag: "674d96cc-142bb9"
X-Via:  192.168.159.104
X-Cache: HIT  #第一次无缓存
X-Accel: www.wanglei.org
Accept-Ranges: bytes
```

#### 5.1.1.6 实现反向代理客户端 IP 透传

##### 5.1.1.6.1 一级代理实现客户端IP透传

![image-20241202194046047](images/image-20241202194046047.png)

```bash
root@ubutun2204-1:~# vim /apps/nginx/conf/conf.d/pc.conf
server {

	location /static {
        proxy_cache proxycache;
        proxy_cache_key $request_uri;
        proxy_cache_valid 200 302 301 10m;
        proxy_cache_valid any 5m;
        proxy_set_header Host  $http_host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;  #添加客户端IP和反向代理服务器IP到请求报文头部
        proxy_pass http://192.168.159.105:80;
    }
}
#说明$proxy_add_x_forwarded_for
#此变量表示将客户端IP追加请求报文中X-Forwarded-For首部字段,多个IP之间用逗号分隔,如果请求中没有X-Forwarded-For,就使用$remote_addr

#重启nginx
root@ubutun2204-1:~# systemctl restart nginx

#后端Nginx配置：
root@backend01:~# cat /etc/nginx/nginx.conf
"$http_x_forwarded_for"' #默认日志格式就有此配置

#重启nginx访问web界面并验证日志格式：
10.0.0.8 - - [04/Dec/2024:16:40:51 +0800] "GET / HTTP/1.0" 200 24 "-" 
"Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) 
Chrome/72.0.3626.119 Safari/537.36" "10.0.0.1"
```

##### 5.1.1.6.2 多级代理实现客户端 IP 透传

范例: 多级代理实现IP透传

![image-20241202194751256](images/image-20241202194751256.png)

```bash
#第一个代理服务器
[root@nginx1 ~]#vim /apps/nginx/conf/nginx.conf 
#开启日志格式,记录x_forwarded_for
http {
   include       mime.types;
   default_type application/octet-stream;
   proxy_cache_path /data/nginx/proxycache   levels=1:1:1 keys_zone=proxycache:20m inactive=120s  max_size=1g;
   log_format main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log logs/access.log main;
    
#定义反向代理
[root@nginx1 ~]#vim /apps/nginx/conf/conf.d/pc.conf 
server {
   location / {
     proxy_pass http://10.0.0.18;
     proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;               
            }
   .......   
}

#第二个代理服务器
[root@nginx2 ~]#vim /apps/nginx/conf/nginx.conf 
#开启日志格式,记录x_forwarded_for
http {
   include       mime.types;
   default_type application/octet-stream;
   proxy_cache_path /data/nginx/proxycache   levels=1:1:1 
 keys_zone=proxycache:20m inactive=120s  max_size=1g;
   log_format main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';
   access_log logs/access.log main;


#定义反向代理
[root@nginx2 ~]#vim /etc/nginx/nginx.conf
 server {
       location / {
         proxy_pass http://10.0.0.28;
         proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;           
                            
       }
       .....
}


#在第一个proxy上面查看日志
[root@nginx1 ~]#tail /apps/nginx/logs/access.log -f
10.0.0.7 - - [11/Dec/2024:14:37:00 +0800] "GET /index.html HTTP/1.1" 200 11 "-" 
"curl/7.58.0" "-"

#在第二个proxy上面查看日志
[root@nginx2 ~]#tail /apps/nginx/logs/access.log -f
10.0.0.8 - - [11/Dec/2024:14:37:00 +0800] "GET /index.html HTTP/1.0" 200 11 "-" 
"curl/7.58.0" "10.0.0.7"


#后端服务器配置日志格式
root@backend01:~# vim /etc/httpd/conf/httpd.conf
LogFormat "\"%{x-Forwarded-For}i\" %h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%
{User-Agent}i\"" testlog
CustomLog "logs/access_log" testlog

#测试访问
[root@centos7 ~]#curl www.wang.org/


#后端服务器查看日志
[root@centos8 ~]#tail -f /var/log/httpd/access_log
"10.0.0.7, 10.0.0.8"  10.0.0.18 - - [11/Dec/2024:14:37:00 +0800] "GET 
/index.html HTTP/1.0" 200 34 "-" "curl/7.29.0"
```

#### 5.1.1.7 利用 Nginx 解决跨域问题

##### 5.1.1.7.1 跨域问题说明

**什么是跨域**

当一个请求URL的`协议`、`域名`、`端口`三者之间任意一个与当前页面URL不同即为跨域。

| 当前页面URL          | 被请求页面URL                   | 是否跨域 | 说明                         |
| -------------------- | ------------------------------- | -------- | ---------------------------- |
| http://www.test.com/ | http://www.test.com/index.html  | 否       | 同源(协议、域名、端口号 相同 |
| http://www.test.com/ | https://www.test.com/index.html | 跨域     | 协议不同(http/https)         |
| http://www.test.com/ | http://www.baidu.com/           | 跨域     | 域名不同(test/baidu)         |
| http://www.test.com/ | http://blog.test.com            | 跨域     | 域名不同(www/blog)           |
| http://www.test.com  | http://www.test.com:8080        | 跨域     | 端口号不同(80/8080)          |

![image-20241202195824528](images/image-20241202195824528.png)

通常由于同域安全策略（the same-origin security policy），浏览器会禁止跨域请求。

**值得注意的是：虽然因为跨域的原因会导致浏览器禁止访问而获取数据失败，但返回的状态码仍为200**

常见的解决方案有：CORS，JSONP，Nginx反向代理等

采用CORS（Cross-Origin Resource Sharing 跨域资源共享）技术，可以允许当前域的Web相关资源被 其他域的脚本请求访问

CORS是一种基于HTTP头的机制，该机制允许使用AJAX发送跨域请求，只要HTTP响应头中包含了相应的 CORS响应头。CORS需要浏览器和服务器同时支持，CORS机制在老版本的浏览器中不支持，现代浏览 器都支持CORS。在使用CORS发送AJAX请求时浏览器端代码和过去一致，服务器端需要配置CORS的响 应头。

参考链接

```http
https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS
```

![image-20241202201139304](images/image-20241202201139304.png)

```bash
fetch("https://www.baidu.com")
fetch("https://www.taobao.com")
```

![image-20241202201415994](images/image-20241202201415994.png)

![image-20241202201425247](images/image-20241202201425247.png)

##### 5.1.1.7.2 使用 Nginx 反向代理功能解决跨域问题案例

```bash
# www.xiaochun.net一个web服务器，端口8080

#在www.wang.org主机的创建页面文件，此文件存在跨域问题
[root@ubuntu2004 ~]#cat /usr/share/nginx/html/cors.html
<!DOCTYPE html>
<html lang="en">
<head>
   <meta charset="UTF-8">
   <title>Cross-origin resource sharing</title>
</head>
<body>
   <script src="https://code.jquery.com/jquery-2.2.4.min.js"></script>
   <script>
       $.ajax({
       url:'http://www.xiaochun.net:8080/api/', #指向第二个域名的资源
       type:'get',
       data:{},
       success:function(res){
           //res = JSON.parse(res);
           console.log('请求成功',res)
       },
       error:function(er){
           console.log('请求错误')
       }
     })
   </script>
</body>
</html>

#访问http://www.wang.org/cors.html,可以观察到如下情况，响应码虽然返回为200，但是浏览器阻止了数据，无法正常显示
```

![image-20241202201629546](images/image-20241202201629546.png)

![image-20241202201653177](images/image-20241202201653177.png)

![image-20241202201701910](images/image-20241202201701910.png)

![image-20241202201758581](images/image-20241202201758581.png)

![image-20241202201811687](images/image-20241202201811687.png)

范例: 配置Nginx 解决跨域问题

```bash
#在www.wang.org主机的nginx反向代理解决跨域
[root@ubuntu2004 ~]#vim /etc/nginx/nginx.conf
server {
   listen 80;
   server_name www.wang.org;
   root /usr/share/nginx/html;
 location /api/ {
     proxy_pass http://www.xiaochun.net:8080; #指向第二个域
 }
}

#在www.wang.org主机上修改网页如下
[root@ubuntu2004 ~]#cat /usr/share/nginx/html/cors.html
<!DOCTYPE html>
<html lang="en">
<head>
   <meta charset="UTF-8">
   <title>Cross-origin resource sharing</title>
</head>
<body>
   <script src="https://code.jquery.com/jquery-2.2.4.min.js"></script>
   <script>
       $.ajax({
       url:'http://www.wang.org/api/', #只修改此行指向网页所在的同一个域名
       type:'get',
       data:{},
       success:function(res){
           //res = JSON.parse(res);
           console.log('请求成功',res)
       },
       error:function(er){
           console.log('请求错误')
       }
     })
   </script>
</body>
</html>
```

### 5.1.2 Http 反向代理负载均衡

在上一个节中Nginx可以将客户端的请求转发至单台后端服务器但是无法转发至特定的一组的服务器， 而且不能对后端服务器提供相应的服务器状态监测

Nginx 可以基于`ngx_http_upstream_module`模块提供服务器分组转发、权重分配、状态监测、调度算 法等高级功能

官方文档：https://nginx.org/en/docs/http/ngx_http_upstream_module.html

#### 5.1.2.1 http upstream 配置参数

```bash
#自定义一组服务器，配置在http块内
upstream name {
	server .....
    ......
}

# 示例
upstream backend {
   server backend1.example.com weight=5;
   server 127.0.0.1:8080  max_fails=3 fail_timeout=30s;
   server unix:/tmp/backend3;
   
   server backup1.example.com backup;
}

server address [parameters];
#配置一个后端web服务器，配置在upstream内，至少要有一个server服务器配置

#server支持的parameters如下：
weight=number #设置权重，默认为1,实现类似于LVS中的WRR,WLC等
max_conns=number  #给当前后端server设置最大活动链接数，默认为0表示没有限制
max_fails=number  #后端服务器的下线条件,当客户端访问时,对本次调度选中的后端服务器连续进行检测多少次,如果都失败就标记为不可用,默认为1次,当客户端访问时,才会利用TCP触发对探测后端服务器健康性检查,而非周期性的探测
fail_timeout=time #后端服务器的上线条件,对已经检测到处于不可用的后端服务器,每隔此时间间隔再次进行检测是否恢复可用，如果发现可用,则将后端服务器参与调度,默认为10秒
backup  #设置为备份服务器，当所有后端服务器不可用时,才会启用此备用服务器，和ip_hash指令冲突，不能同时使用
	#注意:此指令指向地址是自已的虚拟主机server,可能会造成死循环而出现500错误,应该指向另一个虚拟主机的server
down    #标记为down状态,可以平滑下线后端服务器,新用户不再调度到此主机,正在访问的旧用户不受影响	
```

```bash
ip_hash;
#源地址hash调度方法，基于的客户端的remote_addr(源地址IPv4的前24位或整个IPv6地址)做hash计算，以实现会话保持,注意:如果是局域网可能会导致调度到同一台主机
#hash $remote_addr 则是对全部32bit的IPv4进行hash计算
#注意:和backup指令冲突，不能同时使用
```

```bash
least_conn; 
#最少连接调度算法，优先将客户端请求调度到当前连接最少的后端服务器,相当于LVS中的WLC
```

```bash
hash KEY [consistent];
#基于指定请求报文中首部字段或者URI等key做hash计算，使用consistent参数，将使用ketama一致性hash算法，适用于后端是Cache服务器（如varnish）时使用，consistent定义使用一致性hash运算，一致性hash基于取模运算

#示例
hash $request_uri consistent; #基于用户请求的uri做hash,可以实现调度到后端缓存服务器功能
hash $remote_addr consistent; #则是对全部32bit的IPv4进行一致性hash计算
hash $cookie_sessionid        #基于cookie中的sessionid这个key进行hash调度,实现会话绑定
```

```bash
Syntax: keepalive connections;
Default: —
Context: upstream
This directive appeared in version 1.1.4.

keepalived  #该connections参数设置保留在每个工作进程缓存中的上游服务器的最大空闲保活连接数。当超过这个数字时，最近最少使用的连接将被关闭。

Syntax: keepalive_timeout timeout;
Default: 
keepalive_timeout 60s;
Context: upstream
This directive appeared in version 1.15.3.

keepalive_timeout #设置一个超时时间，在此期间与上游服务器的空闲保活连接将保持打开状态。
```

**基于 hash 的调度算法**

```http
#对总权重3取模得出以下结果，再进行调度至后端服务器
{3,6,9}%3=0
{1,4,7,10}%3=1
{2,5,8}%3=2
```

![image-20241209132358987](images/image-20241209132358987.png)

**添加节点后,会导致很多的调度的缓存信息失效**

```bash
#对总权重4取模得出以下结果，再进行调度至后端服务器，和上面对3取模结果差异很大,80%都发生了变化
{4,8}%4=0
{1,5,7}%4=1
{2,6,10}%4=2
{3,7}%4=3
```

![image-20241209132503459](images/image-20241209132503459.png)



**一致性hash 算法**

![image-20241209132611230](images/image-20241209132611230.png)

#### 5.1.2.2 反向代理示例: 后端多台 Web 服务器

![image-20241209132805047](images/image-20241209132805047.png)



环境说明：

```bash
192.168.159.103  #Nginx 代理服务器
192.168.159.104  #后端web A，Nginx部署
192.168.159.105 #后端web B，Nginx部署
```

##### 5.1.2.2.1 部署后端 Apache 服务器

```bash
root@web01:~# apt install nginx
root@web01:~# echo "web01 192.168.159.105" >/var/www/html/index.html

root@web02:~# apt install nginx
root@web02:~# echo "web02 192.168.159.106" >/var/www/html/index.html

#访问测试
root@web01:~# curl 127.0.0.1
web01 192.168.159.105
root@web02:~# curl 127.0.0.1
web02 192.168.159.106
```

##### 5.1.2.2.2 配置 nginx 反向代理

**注意: 本节实验过程中先关闭缓存**

```bash
root@ubutun2204-1:~# cat /apps/nginx/conf/conf.d/pc.conf 
upstream webserver {
   #hash $request_uri consistent;
   #hash $cookie_sessionid；
   #ip_hash;
   #least_conn;
   server 192.168.159.105:80 weight=1 fail_timeout=5s max_fails=3; #后端服务器状态监测
   server 192.168.159.106:80 weight=1 fail_timeout=5s max_fails=3;
   server 127.0.0.1:80 weight=1 fail_timeout=5s max_fails=3 backup;
   keepalive 100; #该connections参数设置保留在每个工作进程缓存中的上游服务器的最大空闲保活连接数。当超过这个数字时，最近最少使用的连接将被关闭。
   keepalive_timeout 60s; #空闲连接超时时长

}

server{
    listen 80;
    server_name www.wanglei.org;
    location / {
	    index index.html index.php;
	    root /data/nginx/html/pc;
    }


    location /web {
        index index.html;
	    proxy_pass http://webserver/;
        proxy_set_header Host  $http_host; #转发主机头至后端服务器
	    proxy_next_upstream error timeout invalid_header http_500 http_502 http_503 http_504;
	proxy_http_version 1.1; #指定使用http1.1版本才能支持长连接
	proxy_set_header Connection ""; #和上面的keepalived指令配合实现代理和后端服务器的长连接功能
    
    }
}


#重启nginx 并访问测试
root@ubutun2204-1:~# curl http://www.wanglei.org/web
web01 192.168.159.105
root@ubutun2204-1:~# curl http://www.wanglei.org/web
web02 192.168.159.106
```

#### 5.1.2.3 实战案例: 基于Cookie 实现会话绑定

```bash
[root@centos8 ~]#vim /apps/nginx/conf/nginx.conf
http {
     upstream websrvs {
         hash $cookie_hello;  #hello是cookie的key的名称
         server 10.0.0.101:80 weight=2;
         server 10.0.0.102:80 weight=1;
     }
}

[root@centos8 ~]# vim /apps/nginx/conf/conf.d/pc.conf
server {
   location /{
 		#proxy_cache mycache;
 		proxy_pass http://websrvs;
  		proxy_set_header Host  $http_host; #转发主机头至后端服务器
   }
}

# 测试
[root@centos8 ~]#curl -b hello=wang http://www.wang.org/
[root@centos8 ~]#curl -b hello=wange http://www.wang.org/
```

#### 5.1.2.5 实战案例: 实现 HTTPS 的负载均衡

![image-20241209141131841](images/image-20241209141131841.png)

```bash
# 方法一
[root@centos8 ~]#vim /apps/nginx/conf.d/proxy.conf
upstream websrvs {
     server 10.0.0.101:80 ;
     server 10.0.0.102:80 ;
}
server {
     listen 80;
     server_name www.wanglei.org;
     return 302 https://$server_name$request_uri;
}
server {
     listen 443 ssl;
     server_name www.wanglei.org;
     ssl_certificate   /apps/nginx/ssl/www.wanglei.org.pem;
     ssl_certificate_key /apps/nginx/ssl/www.wanglei.org.key;
     ssl_session_cache shared:sslcache:20m;
     ssl_session_timeout 10m;
     location / {
     proxy_pass http://websrvs;
           proxy_set_header Host  $http_host;
     }
}


#方法二：
[root@ubuntu2204 conf.d]#vim www.wang.org.conf
upstream webservers{
   server 10.0.0.201;
   server 10.0.0.202;
}
server {
   listen 80;
   listen 443 ssl;
   server_name www.wang.org;
   root /data/nginx/html/pc;
   ssl_certificate /apps/nginx/conf/conf.d/ssl/www.wang.org.pem ;
   ssl_certificate_key   /apps/nginx/conf/conf.d/ssl/www.wang.org.key ;
   access_log logs/www.wang.org-access.log main;
   location / {
       proxy_pass http://webservers;
       proxy_set_header host $http_host;
       #root /data/nginx/html/pc;
       index index.html;
        if ($scheme = http ) {
            #return 302 https://$server_name$request_uri;
           rewrite ^/(.*) https://$server_name/$1 redirect;
       }
   }
}
```

## 5.2 实现 Nginx 四层负载均衡

Nginx在1.9.0版本开始支持tcp模式的负载均衡，在1.9.13版本开始支持udp协议的负载，udp主要用于 DNS的域名解析，其配置方式和指令和http 代理类似，其基于`ngx_stream_proxy_module`模块实现tcp 负载，另外基于模块`ngx_stream_upstream_module`实现后端服务器分组转发、权重分配、状态监测、 调度算法等高级功能。

如果编译安装,需要指定 `--with-stream `选项才能支持ngx_stream_proxy_module模块

官方文档：

```http
https://nginx.org/en/docs/stream/ngx_stream_proxy_module.html
http://nginx.org/en/docs/stream/ngx_stream_upstream_module.html
```

### 5.2.1 TCP协议负载均衡配置参数

```bash
stream { #定义stream相关的服务；Context:main
	upstream backend { #定义后端服务器
       hash $remote_addr consistent; #定义调度算法,当后端服务器可用时此算法才生效，不可用时，可能调度其它可用的主机
       server backend1.example.com:12345 weight=5; #定义具体server
       server 127.0.0.1:12345      max_fails=3 fail_timeout=30s;
       server unix:/tmp/backend3;
   }
   
   upstream dns {  #定义后端服务器
       server 10.0.0.1:53535;  #定义具体server
       server dns.example.com:53;
   }

   server { #定义server
       listen 12345; #监听IP:PORT
       proxy_connect_timeout 1s; #连接超时时间
       proxy_timeout 3s; #转发超时时间
       proxy_pass backend; #转发到具体服务器组
   }

   server {
       listen 127.0.0.1:53 udp reuseport;
       proxy_timeout 20s;
       proxy_pass dns;
   }
   
   server {
       listen [::1]:12345;
       proxy_pass unix:/tmp/stream.socket;
   }

   server {
   listen 2222;
   proxy 10.0.0.8:22; # 只实现四层代理,无负载均衡功能
   }
}
```

### 5.2.2 负载均衡实例 : Redis

![image-20241209142941272](images/image-20241209142941272.png)

#### 5.2.2.1 后端服务器安装 redis

```bash
# 安装两台redis服务器
root@web01:~# apt install redis -y
root@web01:~# sed -i '/^bind /c bind 0.0.0.0' /etc/redis/redis.conf

oot@web01:~# systemctl restart redis
root@web01:~# ss -ntl | grep 6379
LISTEN 0      511          0.0.0.0:6379      0.0.0.0:*          
root@web01:~# ss -ntlp | grep 6379
LISTEN 0      511          0.0.0.0:6379      0.0.0.0:*    users:(("redis-server",pid=46576,fd=6))
```

#### 5.2.2.2 nginx 配置

```bash
root@ubutun2204-1:~# vim /apps/nginx/conf/nginx.conf
include /apps/nginx/conf/tcp/tcp.conf; #注意此处的include与http模块平级


root@ubutun2204-1:~# vim /apps/nginx/conf/tcp/tcp.conf
root@ubutun2204-1:~# cat /apps/nginx/conf/tcp/tcp.conf
stream {
	upstream redis_server {
	   #hash $remote_addr consistent;
           server 192.168.159.105:6379 max_fails=3 fail_timeout=30s;
           server 192.168.159.106:6379 max_fails=3 fail_timeout=30s;
	}
        
	server {
	   listen 192.168.159.104:6379;
	   proxy_connect_timeout 3s;
	   proxy_timeout 3s;
	   proxy_pass redis_server;
	}


}


# 重启nginx 
root@ubutun2204-1:~# nginx -s reload
root@ubutun2204-1:~# ss -tnl | grep 6379
LISTEN     0      128    192.168.159.104:6379                     *:* 

#测试通过nginx 负载连接redis：
root@ubutun2204-1:~# redis-cli -h 192.168.159.104 info
# Server
redis_version:6.0.16
redis_git_sha1:00000000
redis_git_dirty:0
redis_build_id:a3fdef44459b3ad6
redis_mode:standalone
os:Linux 5.15.0-112-generic x86_64
arch_bits:64
multiplexing_api:epoll
atomicvar_api:atomic-builtin
gcc_version:11.2.0
......
```

### 5.2.3 负载均衡实例: MySQL

![image-20241209145036420](images/image-20241209145036420.png)



#### 5.2.3.1 后端服务器安装MySQL

```bash
#安装MySQL服务
root@web01:~# apt install mariadb-server
root@web01:~# systemctl enable --now mariadb
root@web01:~# mysql
MariaDB [(none)]> create user wang@'192.168.159.%' identified by '123456';
MariaDB [(none)]> FLUSH PRIVILEGES;
MariaDB [(none)]> exit
```

#### 5.2.3.2 nginx配置

```bash
root@ubutun2204-1:~# vim /apps/nginx/conf/tcp/tcp.conf
stream {
	upstream redis_server {
	   #hash $remote_addr consistent;
           server 192.168.159.105:6379 max_fails=3 fail_timeout=30s;
           server 192.168.159.106:6379 max_fails=3 fail_timeout=30s;
	}
       
        upstream mysql_server {
           #hash $remote_addr consistent;
           server 192.168.159.105:3306 max_fails=3 fail_timeout=30s;
           server 192.168.159.106:3306 max_fails=3 fail_timeout=30s;
        }

	server {
	   listen 192.168.159.104:6379;
	   proxy_connect_timeout 3s;
	   proxy_timeout 3s;
	   proxy_pass redis_server;
	}

        server {
           listen 192.168.159.104:3306;
           proxy_connect_timeout 3s;
           proxy_timeout 3s;
           proxy_pass mysql_server;
        }
}

#重启nginx并访问测试：
root@ubutun2204-1:~# nginx -s reload

#测试通过nginx负载连接MySQL：
root@ubutun2204-1:~# mysql -uwang -p123456 -h192.168.159.104 -e "show databases;"
+--------------------+
| Database           |
+--------------------+
| information_schema |
+--------------------+
```

### 5.2.4 UDP协议负载均衡实例: DNS

```bash
stream { 
  upstream dns_servers { 
    server 10.0.0.7:53; 
    server 10.0.0.17:53; 
   } 
   server { 
     listen 53 udp; 
     proxy_pass dns_servers; 
   } 
}
```

# 6 Nginx 二次开发版本

## 6.1 Tengine

### 6.1.1 Tengine 介绍

 ![image-20241209163204452](images/image-20241209163204452.png)

Tengine是由淘宝网发起的Web服务器项目。它在Nginx的基础上，针对大访问量网站的需求，添加了很 多高级功能和特性。Tengine的性能和稳定性已经在大型的网站如淘宝网，天猫商城等得到了很好的检 验。它的最终目标是打造一个高效、稳定、安全、易用的Web平台。

官网：

```http
https://tengine.taobao.org/
```

官方文档：

```http
https://tengine.taobao.org/documentation.html
```

Tengine 特性

```http
继承Nginx-1.16.0的所有特性，兼容nginx的配置
支持HTTP的CONNECT方法，可用于正向代理场景
支持异步OpenSSL，可使用硬件如:QAT进行HTTPS的加速与卸载
增强相关运维、监控能力,比如异步打印日志及回滚,本地DNS缓存,内存监控等
Stream模块支持server_name指令
更加强大的负载均衡能力，包括一致性hash模块、会话保持模块，还可以对后端的服务器进行主动健康检查，
根据服务器状态自动上线下线，以及动态解析upstream中出现的域名
输入过滤器机制支持。通过使用这种机制Web应用防火墙的编写更为方便
支持设置proxy、memcached、fastcgi、scgi、uwsgi在后端失败时的重试次数
动态脚本语言Lua支持。扩展功能非常高效简单
支持按指定关键字(域名，url等)收集Tengine运行状态
组合多个CSS、JavaScript文件的访问请求变成一个请求
自动去除空白字符和注释从而减小页面的体积
自动根据CPU数目设置进程个数和绑定CPU亲缘性;
监控系统的负载和资源占用从而对系统进行保护
显示对运维人员更友好的出错信息，便于定位出错机器
更强大的防攻击（访问速度限制）模块
更方便的命令行参数，如列出编译的模块列表、支持的指令等
可以根据访问文件类型设置过期时间
```

### 6.1.2 动态模块

```http
http://tengine.taobao.org/document_cn/dso_cn.html
```

模块说明

```bash
这个模块主要是用来运行时动态加载模块，而不用每次都要重新编译Tengine.
如果想要编译官方模块为动态模块，需要在configure的时候加上类似这样的指令(-withhttp_xxx_module=shared),./configure --help可以看到更多的细节.
如果只想要安装官方模块为动态模块(不安装Nginx)，那么就只需要configure之后，执行 make dso_install命令.
动态加载模块的个数限制为128个.
如果已经加载的动态模块有修改，那么必须重启Tengine才会生效.
只支持HTTP模块.
模块 在Linux/FreeBSD/MacOS下测试成功.


例子:
worker_processes  1;

dso {
   load ngx_http_lua_module.so;
   load ngx_http_memcached_module.so;
}

events {
   worker_connections  1024;
}

#注意
在Tengine-2.3.0版本后废弃Tengine的dso_tool工具以及dso配置指令，若之前有使用Tengine的dso功
能、则可以切换到Nginx官方的load_module指令,详细文档
```

#### 6.1.2.1 编译安装 tengine-2.4.1

```bash
root@ubutun2204-1:~# apt update && apt -y install gcc make libpcre3 libpcre3-dev openssl libssl-dev zlib1g-dev

root@ubutun2204-1:~# groupadd -g 666 -r nginx
root@ubutun2204-1:~# useradd -g nginx -u 666 -r -s /sbin/nologin nginx
root@ubutun2204-1:~# cd /usr/local/src/
root@ubutun2204-1:/usr/local/src# wget https://tengine.taobao.org/download/tengine-2.4.1.tar.gz
root@ubutun2204-1:/usr/local/src# tar xf tengine-2.4.1.tar.gz 
root@ubutun2204-1:/usr/local/src# cd tengine-2.4.1/

root@ubutun2204-1:/usr/local/src/tengine-2.4.1# ./configure --prefix=/apps/tengine --user=nginx --group=nginx --with-http_ssl_module --with-http_v2_module --with-http_realip_module --with-http_stub_status_module --with-http_gzip_static_module --with-pcre --with-stream --with-stream_ssl_module --with-stream_realip_module

root@ubutun2204-1:/usr/local/src/tengine-2.4.1# make && make install
root@ubutun2204-1:~# tree /apps/tengine/
/apps/tengine/
├── conf
│   ├── fastcgi.conf
│   ├── fastcgi.conf.default
│   ├── fastcgi_params
│   ├── fastcgi_params.default
│   ├── koi-utf
│   ├── koi-win
│   ├── mime.types
│   ├── mime.types.default
│   ├── nginx.conf
│   ├── nginx.conf.default
│   ├── scgi_params
│   ├── scgi_params.default
│   ├── uwsgi_params
│   ├── uwsgi_params.default
│   └── win-utf
├── html
│   ├── 50x.html
│   └── index.html
├── logs
└── sbin
    └── nginx

root@ubutun2204-1:~# ln -s /apps/tengine/sbin/* /usr/sbin/
root@ubutun2204-1:~# nginx -v
Tengine version: Tengine/2.4.1
nginx version: nginx/1.22.1

root@ubutun2204-1:~# nginx
root@ubutun2204-1:~# ps aux | grep nginx
root        5847  0.0  0.0  10320   976 ?        Ss   09:01   0:00 nginx: master process nginx
nginx       5848  0.0  0.1  11072  3632 ?        S    09:01   0:00 nginx: worker process
root@ubutun2204-1:~# ss -ntl | grep 80
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*

root@ubutun2204-1:~# curl 192.168.159.106
<!DOCTYPE html>
<html>
<head>
<title>Welcome to tengine!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to tengine!</h1>
<p>If you see this page, the tengine web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://tengine.taobao.org/">tengine.taobao.org</a>.</p>

<p><em>Thank you for using tengine.</em></p>
</body>
</html>


root@ubutun2204-1:~#cat /lib/systemd/system/tengine.service
[Unit]
Description=The nginx HTTP and reverse proxy server
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=/apps/tengine/logs/nginx.pid
ExecStartPre=/bin/rm -f /apps/tengine/logs/nginx.pid
ExecStartPre=/apps/tengine/sbin/nginx -t
ExecStart=/apps/tengine/sbin/nginx
ExecReload=/bin/kill -s HUP $MAINPID
KillSignal=SIGQUIT
TimeoutStopSec=5
KillMode=process
PrivateTmp=true
LimitNOFILE=100000

[Install]
WantedBy=multi-user.target

root@ubutun2204-1:~#systemctl daemon-reload 
root@ubutun2204-1:~#systemctl enable --now tengine.service
```

![image-20241209170400419](images/image-20241209170400419.png)

### 6.1.3 Tengine配置文件

tengine兼容Nginx指定版本的配置参数

```bash
#tengine配置文件：
[root@centos8 ~]# cat /apps/tenginx/conf/conf.d/pc.conf
server {
   listen 80;
   server_name www.wang.org *.www.wang.org pc.wang.org;
   location / {
     concat on;
     root html;
     index index.html index.htm;
   }
   location ~ \.php$ {
     root /data/php;
     fastcgi_pass 10.0.0.18:9000;
     fastcgi_index index.php;
     #fastcgi_param SCRIPT_FILENAME /data/nginx/php$fastcgi_script_name;
     fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
     include fastcgi_params;
   }
}
```

## 6.2 OpenResty

### 6.2.1 OpenResty 介绍

![image-20241209170903138](images/image-20241209170903138.png)

Nginx 是俄罗斯人发明的， Lua 是巴西几个教授发明的，中国人章亦春把 LuaJIT VM 嵌入到 Nginx 中， 实现了 OpenResty 这个高性能服务端解决方案

OpenResty® 是一个基于 Nginx 与 Lua 的高性能 Web 平台，其内部集成了大量精良的 Lua 库、第三方 模块以及大多数的依赖项。用于方便地搭建能够处理超高并发、扩展性极高的动态 Web 应用、Web 服 务和动态网关。

OpenResty® 通过汇聚各种设计精良的 Nginx 模块（主要由 OpenResty 团队自主开发），从而将  Nginx 有效地变成一个强大的通用 Web 应用平台。这样，Web 开发人员和系统工程师可以使用 Lua 脚 本语言调动 Nginx 支持的各种 C 以及 Lua 模块，快速构造出足以胜任 10K 乃至 1000K 以上单机并发连 接的高性能 Web 应用系统。

OpenResty® 的目标是让你的Web服务直接跑在 Nginx 服务内部，充分利用 Nginx 的非阻塞 I/O 模 型，不仅仅对HTTP 客户端请求,甚至于对远程后端诸如 MySQL、PostgreSQL、Memcached 以及 Redis  等都进行一致的高性能响应。

OpenResty 由于有功能强大且方便的的API,可扩展性更强,如果需要实现定制功能,OpenResty是个不错 的选择

官网: http://openresty.org/cn/

### 6.2.2 编译安装 openresty

范例: Ubuntu22.04 编译安译安装Openresty

```bash
root@ubutun2204-1:~# apt update && apt -y install gcc make libpcre3 libpcre3-dev openssl libssl-dev zlib1g-dev

root@ubutun2204-1:~# groupadd -g 666 -r nginx
root@ubutun2204-1:~# useradd -g nginx -u 666 -r -s /sbin/nologin nginx
root@ubutun2204-1:~# cd /usr/local/src

root@ubutun2204-1:/usr/local/src# wget https://openresty.org/download/openresty-1.27.1.1.tar.gz
root@ubutun2204-1:/usr/local/src# tar xf openresty-1.27.1.1.tar.gz 
root@ubutun2204-1:/usr/local/src# cd openresty-1.27.1.1/

root@ubutun2204-1:/usr/local/src/openresty-1.27.1.1# ./configure --prefix=/apps/openresty --user=nginx --group=nginx --with-http_ssl_module --with-http_v2_module --with-http_realip_module --with-http_stub_status_module --with-http_gzip_static_module --with-pcre --with-stream --with-stream_ssl_module --with-stream_realip_module
root@ubutun2204-1:/usr/local/src/openresty-1.27.1.1# make && make install

root@ubutun2204-1:/usr/local/src/openresty-1.27.1.1# ln -s /apps/openresty/bin/* /usr/local/bin/
root@ubutun2204-1:/usr/local/src/openresty-1.27.1.1# openresty -v
nginx version: openresty/1.27.1.1

root@ubutun2204-1:/usr/local/src/openresty-1.27.1.1# openresty 


# 测试访问
root@ubutun2204-1:~# curl 192.168.159.105 -I
HTTP/1.1 200 OK
Server: openresty/1.27.1.1
Date: Mon, 09 Dec 2024 09:24:05 GMT
Content-Type: text/html
Content-Length: 128646
Last-Modified: Mon, 09 Dec 2024 09:21:09 GMT
Connection: keep-alive
ETag: "6756b685-1f686"
Accept-Ranges: bytes
```

![image-20241209172448298](images/image-20241209172448298.png)

# 7 常见面试题

- http 协议的各个版本和区别
- 响应码200，但是仍无法访问，原因是什么?
- 说明各种响应码分类,499的原因,502和504的区别
- 比较nginx 和 apache 的特性
- nginx 的功能
- 常见的nginx 性能优化方法
- location的优先级
- rewrite 中 redirect,permanent, break和last区别
- 如何获取客户端真实IP
- nginx的常见模块
- nginx的反向代理的调度算法
- 比较nginx，haprorxy和LVS的区别
- http的常见的响应码
- 访问web页面时出现502和504错误，请简述—下排查思路
- 有同事反应，网站访问速度很慢，有时候会出现打不开网站的情况，刷新等待好长时间后又正常打 开，请分析并说一说故障排查思路?
- 上家公司的服务各做了哪些优化，NGINX做了哪些优化
