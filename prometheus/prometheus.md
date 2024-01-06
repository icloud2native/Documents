# 一：监控及prometheus简介

监控的重要性：

通过业务监控系统，全满掌握业务环境运行状态，通过白盒监控能够提前预知业务瓶颈，通过黑盒监控能够第一时间发现业务故障并通过告警告知运维人员进行紧急恢复，从而将业务影响降低到最低。

```bash
黑盒监控，关注的是实时的状态，一般都是正在发生的事件，比如nginx界面打开503.黑盒监控的重点在于能够对正在发生的故障进行告警。

白盒监控，关注的是原因，也就是系统内部暴露一些指标数据，比如nginx后端服务器的响应时长，磁盘I/O负载值等。
```

## 1.1：监控逻辑布局

![image-20231223142555353](images\image-20231223142555353.png)

## 1.2：常见的监控方案

开源监控软件：cacti，nagios，zabbix，smokeping，open-falcon等。

### 1.2.1：Cacti

https://github.com/Cacti/cacti

https://www.cacti.net/

```tex
Cacti是基于LAMP平台展现的网络流量监测及分析工具，通过snmp或者自定义脚本从目标设备/主机获取监控指标值，其次进行数据存储，调用模板将数据存到数据库，使用rrdtool存储和更新数据，通过rrdtool绘制结果图形；最后进行数据展现，通过web方式将监控结果展现出来，常用于在数据中心监控网络设备。
```

### 1.2.2：Nagios

https://www.nagios.org/

```te
Nagios用来监控系统和网络的开源应用软件，利用其众多的插件实现对本机和远端服务的监控，当被监控对象发生异常，会及时向管理员告警，提供一批预设好的监控插件，用户可以调用，也可以自定义shell脚本监控服务，适合各企业的业务监控，可通过web页面显示对象状态，日志，告警信息，分层告警机制及自定义监控相对薄弱。
```

### 1.2.3：Smokeping

https://oss.oetiker.ch/smokeping/

```tex
Smokeping是一款用于网络性能检测的开源监控软件，主要用于对IDC的网络状况，网络质量，稳定性做检测，通过rrdtool绘制方式，图像化的展示网络延迟情况，进而能够清楚的判断出网络的即使通信情况。
```

### 1.2.4：Open-falcon

https://www.open-falcon.org/

```tex
小米公司开源的监控软件，监控能力和性能较强。
```

### 1.2.5：夜莺

https://n9e.didiyun.com/

```tex
一款经过大规模生产环境验证的，分布式高性能的运维监控系统。由滴滴基于open-falcon二次开发后开源的分布式监控系统。
```

### 1.2.6：Zabbix

https://www.zabbix.com/cn/

```tex
目前使用较多的开源监控软件，可横向扩展，自定义监控项，支持多种监控方式，可监控网络和服务等。
```

### 1.2.7：Prometheus

https://prometheus.io/

```tex
云原生下的监控解决方案。
```

### 1.2.8：商业监控软件

监控宝：https://www.jiankongbao.com/

听云：https://www.tingyun.com/

## 1.3：prometheus简介

https://prometheus.io/

Prometheus是基于go语言开发的一套监控，报警和时间序列数据库的组合，是由SoundCloud公司开发的开源监控系统。Prometheus于2016年加入CNCF，2018年8.9prometheus成为CNCF既kubernetes之后毕业的第二个项目，prometheus在容器和微服务领域中得到了广泛的应用，其特点如下：

```tex
使用key-value的多维度格式保存数据
数据不使用MYSQL这样的传统数据库，而是使用时序性数据库，目前是使用TEDB
支持第三方dashboard实现更高的图形界面，如granafa
组件模块化
不需要依赖存储，数据可以本地保存也可以远程保存
平均每个采样点占3.5bytes，且一个prometheus server可以处理数百万级别的metrics指标数据
支持服务自动化发现
强大的数据查询语句功能（PromQL）
数据可以直接进行算术运算
易于横向伸缩
众多官方和第三方的exporter实现不同的指标数据收集
```

### 1.3.1：为什么使用Prometheus

  容器监控的实现方式对比物理机和虚拟机有比较大的区别，比如容器在k8s环境可以任意横向扩缩容，那么就需要监控服务能够自动对新创建的容器进行监控，当容器删除后又能够及时的从监控服务中删除，而传统的zabbix的监控方式需要在每一个容器中安装agent，并且在容器自动发现注册和模板关联方面并没有比较好的实现方式。

### 1.3.2：Prometheus架构图

```tex
prometheus server：主服务，接受外部http请求，收集，存储和查询数据等
prometheus targets：静态收集的目标服务数据
service discovery: 动态发现服务
prometheus alarting:报警通知
push gateway：数据收集代理服务器（类似于zabbix proxy）
data visualization and export：数据可视化与数据导出
```

![image-20231223151118133](images\image-20231223151118133.png)

# 二：部署prometheus监控系统

可以通过不同的方式安装部署prometheus监控环境，虽然以下的多种安装方式演示了不同的部署方式，但是实际生产环境只需要根据实际需求选择其中一种方式部署即可。

```tex
https://prometheus.io/download/ #官方二进制下载及安装，prometheus server的监听端口为9090
https://prometheus.io/docs/prometheus/latest/installation/ #docker镜像直接启动
https://github.com/prometheus-operator/kube-prometheus #operator部署
```

## 2.1：Docker部署Prometheus Server

```yaml
# https://github.com/mohamadhoseinmoradi/Docker-Compose-Prometheus-and-Grafana

# docker-compose up -d 
```

## 2.2: Operator部署Prometheus监控系统

Operator部署是基于已经编写好的yaml文件，可以将prometheus server，alertmanager，granafa，node-exporter等组件一键批量部署。

```bash
部署环境：
kubernetes 1.27.1
kube-prometheus v0.13.0
```

### 2.2.1：clone项目并部署

```bash
# git clone https://github.com/prometheus-operator/kube-prometheus.git (v0.13.0)
# cd kube-prometheus/
# kubectl apply --server-side -f manifests/setup
# kubectl apply -f manifests/
```

### 2.2.2：验证Pod状态

![image-20231223154312163](images\image-20231223154312163.png)

### 2.2.3：通过NodePort访问Prometheus Server

【注】在 `release-0.11` 版本之后新增了 `NetworkPolicy` 默认是允许自己访问，如果了解 `NetworkPolicy` 可以修改一下默认的规则，可以用查看 `ls manifests/*networkPolicy*`，如果不修改的话则会影响到修改 `NodePort` 类型也无法访问，如果不会 `Networkpolicy` 可以直接删除就行。

```yaml
# cat manifests/prometheus-service.yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app.kubernetes.io/component: prometheus
    app.kubernetes.io/instance: k8s
    app.kubernetes.io/name: prometheus
    app.kubernetes.io/part-of: kube-prometheus
    app.kubernetes.io/version: 2.48.1
  name: prometheus-k8s
  namespace: monitoring
spec:
  type: NodePort
  ports:
  - name: web
    port: 9090
    targetPort: web
  - name: reloader-web
    port: 8080
    targetPort: reloader-web
  selector:
    app.kubernetes.io/component: prometheus
    app.kubernetes.io/instance: k8s
    app.kubernetes.io/name: prometheus
    app.kubernetes.io/part-of: kube-prometheus
  sessionAffinity: ClientIP
  
# kubectl apply -f  manifests/prometheus-service.yaml
service/prometheus-k8s configured

root@k-master01:~/kube-prometheus# kubectl get svc -n monitoring
NAME                    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                         AGE
alertmanager-main       ClusterIP   10.109.67.222    <none>        9093/TCP,8080/TCP               9m7s
alertmanager-operated   ClusterIP   None             <none>        9093/TCP,9094/TCP,9094/UDP      7m54s
blackbox-exporter       ClusterIP   10.105.174.233   <none>        9115/TCP,19115/TCP              9m6s
grafana                 ClusterIP   10.108.200.161   <none>        3000/TCP                        9m6s
kube-state-metrics      ClusterIP   None             <none>        8443/TCP,9443/TCP               9m6s
node-exporter           ClusterIP   None             <none>        9100/TCP                        9m6s
prometheus-adapter      ClusterIP   10.104.83.100    <none>        443/TCP                         9m5s
prometheus-k8s          NodePort    10.104.114.91    <none>        9090:30924/TCP,8080:30223/TCP   9m5s
prometheus-operated     ClusterIP   None             <none>        9090/TCP                        7m53s
prometheus-operator     ClusterIP   None             <none>        8443/TCP                        9m5s
```

### 2.2.4：验证prometheus web界面

![image-20231223202016836](images\image-20231223202016836.png)

### 2.2.5：通过NodePort访问Grafana

【注】在 `release-0.11` 版本之后新增了 `NetworkPolicy` 默认是允许自己访问，如果了解 `NetworkPolicy` 可以修改一下默认的规则，可以用查看 `ls manifests/*networkPolicy*`，如果不修改的话则会影响到修改 `NodePort` 类型也无法访问，如果不会 `Networkpolicy` 可以直接删除就行。

```yaml
# cat manifests/grafana-service.yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app.kubernetes.io/component: grafana
    app.kubernetes.io/name: grafana
    app.kubernetes.io/part-of: kube-prometheus
    app.kubernetes.io/version: 10.2.2
  name: grafana
  namespace: monitoring
spec:
  ports:
  - name: http
    port: 3000
    targetPort: http
  selector:
    app.kubernetes.io/component: grafana
    app.kubernetes.io/name: grafana
    app.kubernetes.io/part-of: kube-prometheus
root@k-master01:~/kube-prometheus/manifests# vim grafana-service.yaml 
root@k-master01:~/kube-prometheus/manifests# kubectl apply -f grafana-service.yaml 
service/grafana configured
root@k-master01:~/kube-prometheus/manifests# cat grafana-service.yaml 
apiVersion: v1
kind: Service
metadata:
  labels:
    app.kubernetes.io/component: grafana
    app.kubernetes.io/name: grafana
    app.kubernetes.io/part-of: kube-prometheus
    app.kubernetes.io/version: 10.2.2
  name: grafana
  namespace: monitoring
spec:
  type: NodePort
  ports:
  - name: http
    port: 3000
    targetPort: http
  selector:
    app.kubernetes.io/component: grafana
    app.kubernetes.io/name: grafana
    app.kubernetes.io/part-of: kube-prometheus
    

# root@k-master01:~/kube-prometheus/manifests# kubectl apply -f grafana-service.yaml 
service/grafana configured

root@k-master01:~/kube-prometheus/manifests# kubectl get svc -n monitoring
NAME                    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                         AGE
alertmanager-main       ClusterIP   10.104.222.11    <none>        9093/TCP,8080/TCP               8m37s
alertmanager-operated   ClusterIP   None             <none>        9093/TCP,9094/TCP,9094/UDP      8m33s
blackbox-exporter       ClusterIP   10.99.41.141     <none>        9115/TCP,19115/TCP              8m37s
grafana                 NodePort    10.96.36.202     <none>        3000:30620/TCP                  8m36s
kube-state-metrics      ClusterIP   None             <none>        8443/TCP,9443/TCP               8m36s
node-exporter           ClusterIP   None             <none>        9100/TCP                        8m36s
prometheus-adapter      ClusterIP   10.105.240.155   <none>        443/TCP                         8m35s
prometheus-k8s          NodePort    10.105.22.183    <none>        9090:30924/TCP,8080:31831/TCP   8m36s
prometheus-operated     ClusterIP   None             <none>        9090/TCP                        8m31s
prometheus-operator     ClusterIP   None             <none>        8443/TCP                        8m35s
```

### 2.2.6 :验证grafana界面

![image-20231223203701998](images\image-20231223203701998.png)

## 2.3：二进制部署Prometheus Server

```bash
部署环境：
prometheus server: 192.168.58.145
```

### 2.3.1：解压二进制程序

```bash
root@pro:~# mkdir /app
# cd /app
# wget https://mirror.ghproxy.com/https://github.com/prometheus/prometheus/releases/download/v2.48.1/prometheus-2.48.1.linux-amd64.tar.gz
# tar xf prometheus-2.48.1.linux-amd64.tar.gz
# ln -sv prometheus-2.48.1.linux-amd64 prometheus
# cd /app/prometheus
# ls -ltr
total 238524
-rwxr-xr-x 1 1001 127 125066649 Dec  8 23:35 prometheus #prometheus服务可执行文件
-rwxr-xr-x 1 1001 127 119151581 Dec  8 23:36 promtool #测试工具，用于检测prometheus配置文件，检测metrics数据等
-rw-r--r-- 1 1001 127       934 Dec  9 00:03 prometheus.yml # prometheus配置文件
-rw-r--r-- 1 1001 127      3773 Dec  9 00:03 NOTICE
-rw-r--r-- 1 1001 127     11357 Dec  9 00:03 LICENSE
drwxr-xr-x 2 1001 127      4096 Dec  9 00:03 consoles
drwxr-xr-x 2 1001 127      4096 Dec  9 00:03 console_libraries


# ./promtool check config prometheus.yml
Checking prometheus.yml
 SUCCESS: prometheus.yml is valid prometheus config file syntax
```

### 2.3.2：创建prometheus service启动脚本

```bash
# vim /etc/systemd/system/prometheus.service
[Unit]
Description=Prometheus Server
Documentation=https://prometheus.io/docs/introduction/overview/
After=network.target

[Service]
Restart=on-failure
WorkingDirectory=/app/prometheus/
ExecStart=/app/prometheus/prometheus --config.file=/app/prometheus/prometheus.yml

[Install]
WantedBy=multi-user.target
```

### 2.3.3：启动prometheus服务

```bash
root@pro:/app/prometheus# systemctl daemon-reload && systemctl restart prometheus && systemctl enable prometheus
Created symlink /etc/systemd/system/multi-user.target.wants/prometheus.service → /etc/systemd/system/prometheus.service.                                                   
```

### 2.3.4：验证prometheus web界面

![image-20231224145858914](images\image-20231224145858914.png)

## 2.4：二进制安装node-exporter

k8s各node节点使用daemonset方式安装node_exporter，用于收集各k8s node节点宿主机的监控数据，默认监听端口9100。

```bash
部署环境：
node1: 192.168.58.146
node2: 192.168.58.144
```

![image-20231224150615294](images\image-20231224150615294.png)

### 2.4.1：解压二进制程序

```bash
# cd /app
# wget https://github.com/prometheus/node_exporter/releases/download/v1.7.0/node_exporter-1.7.0.linux-amd64.tar.gz
# tar xf node_exporter-1.7.0.linux-amd64.tar.gz
# ln -sv node_exporter-1.7.0.linux-amd64 node_exporter
# cd /app/node_exporter
# ls -ltr
total 19476
-rwxr-xr-x 1 1001 1002 19925095 Nov 12 23:54 node_exporter
-rw-r--r-- 1 1001 1002      463 Nov 13 00:02 NOTICE
-rw-r--r-- 1 1001 1002    11357 Nov 13 00:02 LICENSE
```

### 2.4.2：创建node-exporter service启动文件

```bash
# vim /etc/systemd/system/node-exporter.service
[Unit]
Description=Prometheus Node Exporter
After=network.target

[Service]
ExecStart=/app/node_exporter/node_exporter

[Install]
WantedBy=multi-user.target
```

### 2.4.3：启动node-exporter服务

```bash
# systemctl daemon-reload && systemctl restart node-exporter && systemctl enable node-exporter
```

### 2.4.4：验证node exporter web界面

![image-20231224151656185](images\image-20231224151656185.png)

### 2.4.5：node-exporter指标数据

```bash
常见的指标：
node_boot_time_seconds：系统自启动以后的总时间
node_cpu：系统cpu使用率
node_disk*: 磁盘io
node_filesystem*: 系统文件用量
node_load1: 系统CPU负载
node_memory*: 内存使用量
node_network：网络带宽指标
node_time：当前系统时间
go_*：node exporter中go相关指标
process_*:node exporter自身进程相关运行指标
```

## 2.5：配置prometheus收集node-exporter指标数据

### 2.5.1：prometheus默认配置文件

```bash
root@pro:/app/prometheus# cat prometheus.yml 
# my global config
global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute. #数据收集间隔时间，不配置默认为1分钟
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute. # 规则扫描间隔时间，如果不配置默认为1分钟
  # scrape_timeout is set to the global default (10s).

# Alertmanager configuration
alerting:  # 报警通知配置
  alertmanagers:
    - static_configs:
        - targets:
          # - alertmanager:9093

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:  # 规则配置
  # - "first_rules.yml"
  # - "second_rules.yml"

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs: # 数据采集目标配置
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "prometheus"

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
      - targets: ["localhost:9090"]
```

### 2.5.2：添加Node节点数据收集

```bash
# vim /app/prometheus/prometheus.yml
    - job_name: "prometheus-node"
        static_configs:
          - targets: ["192.168.58.146:9100","192.168.58.144:9100"]
```

### 2.5.3：重启prometheus

```bash
root@pro:~# systemctl restart prometheus
```

### 2.5.4：验证prometheus server数据采集状态

![image-20231224153631358](images\image-20231224153631358.png)

### 2.5.5：验证Node数据

![image-20231224153724305](images\image-20231224153724305.png)

## 2.6：grafana部署

grafana是一个可视化组件，用于接收客户端浏览器的请求并连接到prometheus查询数据，最后经过渲染并在浏览器进行展示，需要注意的是，grafana查询数据类似于zabbix一样需要自定义模板，模板可以手动绘制也可以导入已有的模板。

```bash
https://grafana.com/ # 官网
https://grafana.com/grafana/dashboards/ #模板下载
```

![image-20231224154151300](images\image-20231224154151300.png)

### 2.6.1：安装grafana server

https://grafana.com/grafana/download # 下载地址

https://grafana.com/docs/grafana/latest/setup-grafana/installation/debian/ # 安装文档

```bash
部署要求：可以和prometheus server分离部署
部署环境：192.168.58.145 # grafana server

# sudo apt-get install -y adduser libfontconfig1 musl
# wget https://dl.grafana.com/enterprise/release/grafana-enterprise_10.2.3_amd64.deb
# sudo dpkg -i grafana-enterprise_10.2.3_amd64.deb
```

### 2.6.2：grafana server配置文件

```bash
# cat /etc/grafana/grafana.ini
[server]
# Protocol (http,https,socket)
protocol = http

# The ip address to bind to, empty will to all addresses
http_addr = 0.0.0.0

# The http port to use
http_port = 3000
```

### 2.6.3：启动grafana

```bash
# systemctl restart grafana-server && systemctl enable grafana-server
```

### 2.6.4：验证grafana web界面

#### 2.6.4.1：登录界面

`admin/admin`

![image-20231224155700901](images\image-20231224155700901.png)

#### 2.6.4.2：添加prometheus数据源

![image-20231224155901347](images\image-20231224155901347.png)

![image-20231224155949471](images\image-20231224155949471.png)

![image-20231224160118352](images\image-20231224160118352.png)

![image-20231224160139248](images\image-20231224160139248.png)

## 2.7：grafana导入模板

### 2.7.1：查找目标模板

![image-20231224160505594](images\image-20231224160505594.png)

### 2.7.2：grafana导入模板步骤

#### 2.7.2.1：点击import

![image-20231224160630053](images\image-20231224160630053.png)

#### 2.7.2.2：输入模板ID

![image-20231224160751759](images\image-20231224160751759.png)

#### 2.7.2.3：选择目的数据源

![image-20231224160850386](images\image-20231224160850386.png)

#### 2.7.2.4：验证模板图形

![image-20231224160937563](images\image-20231224160937563.png)

#### 2.7.2.5：插件管理

饼图插件未安装，需要提前安装

https://grafana.com/grafana/plugins/grafana-piechart-panel/

```bash
在线安装：
# grafana-cli plugins install grafana-piechart-panel


离线安装：
# pwd
/var/lib/grafana/plugins

# unzip grafana-piechart-panel-1.6.4.any.zip
# systemctl restart grafana-server
```

未安装饼图插件：（9894）

![](images\image-20231224162056388.png)

已安装饼图插件：

![image-20231224162343175](images\image-20231224162343175.png)

## 2.8：通过yaml文件在kubernetes部署prometheus

此安装方式通过yaml部署prometheus及node-exporter等组件。

```bash
环境说明：

k8s: v1.27.1
cadvisor: v0.45.0
node-exporter: v1.7.0
prometheus: v2.45.2
```

### 2.8.1：安装cadvisor

#### 2.8.1.1：通过daemonset运行cadvisor

```yaml
# kubectl create ns monitoring
namespace/monitoring created

# cat daemonset-cadvisor.yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: cadvisor
  namespace: monitoring
spec:
  selector:
    matchLabels:
      app: cAdvisor
  template:
    metadata:
      labels:
        app: cAdvisor
    spec:
      tolerations:    #污点容忍,忽略master的NoSchedule
        - effect: NoSchedule
          key: node-role.kubernetes.io/control-plane
      hostNetwork: true
      restartPolicy: Always   # 重启策略
      containers:
      - name: cadvisor
        image: gcr.io/cadvisor/cadvisor:v0.45.0
        imagePullPolicy: IfNotPresent  # 镜像策略
        ports:
        - containerPort: 8080
        volumeMounts:
          - name: root
            mountPath: /rootfs
          - name: run
            mountPath: /var/run
          - name: sys
            mountPath: /sys
          - name: docker
            mountPath: /var/lib/docker
      volumes:
      - name: root
        hostPath:
          path: /
      - name: run
        hostPath:
          path: /var/run
      - name: sys
        hostPath:
          path: /sys
      - name: docker
        hostPath:
          path: /var/lib/docker
```

查看pod运行状态：

```bash
root@k-master01:~/prometheus/k8s-prom# kubectl get pods -n monitoring 
NAME             READY   STATUS    RESTARTS   AGE
cadvisor-6bv27   1/1     Running   0          80s
cadvisor-r8l7z   1/1     Running   0          80s
cadvisor-wvf8p   1/1     Running   0          79s
```

#### 2.8.1.2：cadvisor指标数据

| 指标名称                               | 类型    | 含义                                     |
| -------------------------------------- | ------- | ---------------------------------------- |
| container_cpu_load_average_10s         | Gauge   | 过去10秒容器CPU的平均负载                |
| container_cpu_usage_seconds_total      | Counter | 容器在每个CPU上累计占用时间（单位：秒）  |
| container_cpu_system_seconds_total     | Counter | System CPU累计占用时间（单位：秒）       |
| container_cpu_user_seconds_total       | Counter | User CPU累计占用时间（单位：秒）         |
| container_fs_usage_bytes               | Gauge   | 容器中文件系统使用量（单位：字节）       |
| container_fs_limit_bytes               | Gauge   | 容器可以使用的文件系统总量（单位：字节） |
| container_fs_reads_bytes_total         | Counter | 容器累计读取数据总量（单位：字节）       |
| container_fs_writes_bytes_total        | Counter | 容器累计写入数据总量（单位：字节）       |
| container_memory_max_usage_bytes       | Gauge   | 容器的最大内存使用量（单位：字节）       |
| container_memory_usage_bytes           | Gauge   | 容器当前内存使用量（单位：字节）         |
| container_spec_memory_limit_bytes      | Gauge   | 容器的内存使用量限制                     |
| machine_memory_bytes                   | Gauge   | 当前主机内存总量                         |
| container_network_receive_bytes_total  | Counter | 容器网络累计接收数据总量（单位：字节）   |
| container_network_transmit_bytes_total | Counter | 容器网络累计传输数据总量（单位：字节）   |

```bash
当能够正常采集到cadvisor数据，通过以下表达式计算容器CPU的使用率：

（1）sum(irate(container_cpu_usage_seconds_total{image!=""}[1m])) without (cpu)
容器CPU的使用率

（2）container_memory_usage_bytes{image!=""}
查询容器内存使用量（单位：字节）

（3）sum(rate(container_network_receive_bytes_total{image!=""}[1m])) without (interface)
查询容器网络接受量（速率）（单位：字节/秒）

（4）sum(rate(container_network_transmit_bytes_total{image!=""}[1m])) without (interface)
容器网络传输量 字节/秒

（5）sum(rate(container_fs_reads_bytes_total{image!=""}[1m])) without (device)
容器文件系统读取速率 字节/秒

（6）sum(rate(container_fs_writes_bytes_total{image!=""}[1m])) without (device)
容器文件系统写入速率 字节/秒


cadvisor 常用容器监控指标
（1）网络流量
sum(rate(container_network_receive_bytes_total{name=~".+"}[1m])) by (name)
## 容器网络接收的字节数（1分钟内），根据名称查询name=~".+"

sum(rate(container_network_transmit_bytes_total{name=~".+"}[1m])) by (name)
## 容器网络传输的字节数（1分钟内），根据名称查询name=~".+"


（2）容器CPU相关
sum(rate(container_cpu_system_seconds_total[1m]))
## 所用容器system cpu的累计使用时间(1 min内)


sum(irate(container_cpu_system_seconds_total{image！=”“}[1m])) without (cpu)
## 每个容器system cpu的使用时间（1min内）



sum(rate(container_cpu_usage_seconds_total{name=~"。+"}[1m])) by (name) *100
## 每个容器的cpu使用率


sum(sum(rate(container_cpu_usage_seconds_total{name=~"。+"}[1m])) by (name) *100)
## 总容器的cpu使用率
```

### 2.8.2：安装node-exporter

#### 2.8.2.1：通过daemonset安装

```bash
root@k-master01:~/prometheus/k8s-prom# cat 02-node-exporter-ds.yaml 
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: node-exporter
  namespace: monitoring 
  labels:
    k8s-app: node-exporter
spec:
  selector:
    matchLabels:
        k8s-app: node-exporter
  template:
    metadata:
      labels:
        k8s-app: node-exporter
    spec:
      tolerations: #污点容忍,忽略master的NoSchedule
        - effect: NoSchedule
          key: node-role.kubernetes.io/control-plane
      containers:
      - image: quay.io/prometheus/node-exporter:v1.7.0 
        imagePullPolicy: IfNotPresent
        name: prometheus-node-exporter
        ports:
        - containerPort: 9100
          hostPort: 9100
          protocol: TCP
          name: metrics
        volumeMounts:
        - mountPath: /host/proc
          name: proc
        - mountPath: /host/sys
          name: sys
        - mountPath: /host
          name: rootfs
        args:
        - --path.procfs=/host/proc
        - --path.sysfs=/host/sys
        - --path.rootfs=/host
      volumes:
        - name: proc
          hostPath:
            path: /proc
        - name: sys
          hostPath:
            path: /sys
        - name: rootfs
          hostPath:
            path: /
      hostNetwork: true
      hostPID: true
---
apiVersion: v1
kind: Service
metadata:
  annotations:
    prometheus.io/scrape: "true"
  labels:
    k8s-app: node-exporter
  name: node-exporter
  namespace: monitoring 
spec:
  type: NodePort
  ports:
  - name: http
    port: 9100
    protocol: TCP
  selector:
    k8s-app: node-exporter
```

查看运行状态：

```bash
root@k-master01:~/prometheus/k8s-prom# kubectl get pods -n monitoring
NAME                  READY   STATUS    RESTARTS   AGE
cadvisor-6bv27        1/1     Running   0          174m
cadvisor-r8l7z        1/1     Running   0          174m
cadvisor-wvf8p        1/1     Running   0          174m
node-exporter-2r5zd   1/1     Running   0          2m1s
node-exporter-8lfcp   1/1     Running   0          2m1s
node-exporter-g6pr6   1/1     Running   0          2m1s
```

#### 2.8.2.2：node-exporter指标数据

```bash
常见的指标：
node_boot_time_seconds：系统自启动以后的总时间
node_cpu：系统cpu使用率
node_disk*: 磁盘io
node_filesystem*: 系统文件用量
node_load1: 系统CPU负载
node_memory*: 内存使用量
node_network：网络带宽指标
node_time：当前系统时间
go_*：node exporter中go相关指标
process_*:node exporter自身进程相关运行指标
```

### 2.8.3：安装prometheus server

#### 2.8.3.1：prometheus cfg

```bash
# cat 03-prometheus-cfg.yaml
---
kind: ConfigMap
apiVersion: v1
metadata:
  labels:
    app: prometheus
  name: prometheus-config
  namespace: monitoring 
data:
  prometheus.yml: |
    global:
      scrape_interval: 15s
      scrape_timeout: 10s
      evaluation_interval: 1m
    scrape_configs:
    - job_name: 'kubernetes-node'
      kubernetes_sd_configs:
      - role: node
      relabel_configs:
      - source_labels: [__address__]
        regex: '(.*):10250'
        replacement: '${1}:9100'
        target_label: __address__
        action: replace
      - action: labelmap
        regex: __meta_kubernetes_node_label_(.+)
    - job_name: 'kubernetes-node-cadvisor'
      kubernetes_sd_configs:
      - role:  node
      scheme: https
      tls_config:
        ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
      bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
      relabel_configs:
      - action: labelmap
        regex: __meta_kubernetes_node_label_(.+)
      - target_label: __address__
        replacement: kubernetes.default.svc:443
      - source_labels: [__meta_kubernetes_node_name]
        regex: (.+)
        target_label: __metrics_path__
        replacement: /api/v1/nodes/${1}/proxy/metrics/cadvisor

    - job_name: 'kubernetes-service-endpoints'
      kubernetes_sd_configs:
      - role: endpoints
      relabel_configs:
      - source_labels: [__meta_kubernetes_service_annotation_prometheus_io_scrape]
        action: keep
        regex: true
      - source_labels: [__meta_kubernetes_service_annotation_prometheus_io_scheme]
        action: replace
        target_label: __scheme__
        regex: (https?)
      - source_labels: [__meta_kubernetes_service_annotation_prometheus_io_path]
        action: replace
        target_label: __metrics_path__
        regex: (.+)
      - source_labels: [__address__, __meta_kubernetes_service_annotation_prometheus_io_port]
        action: replace
        target_label: __address__
        regex: ([^:]+)(?::\d+)?;(\d+)
        replacement: $1:$2
      - action: labelmap
        regex: __meta_kubernetes_service_label_(.+)
      - source_labels: [__meta_kubernetes_namespace]
        action: replace
        target_label: kubernetes_namespace
      - source_labels: [__meta_kubernetes_service_name]
        action: replace
        target_label: kubernetes_name



    - job_name: 'kubernetes-apiserver'
      kubernetes_sd_configs:
      - role: endpoints
      scheme: https
      tls_config:
        ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
      bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
      relabel_configs:
      - source_labels: [__meta_kubernetes_namespace, __meta_kubernetes_service_name, __meta_kubernetes_endpoint_port_name]
        action: keep
        regex: default;kubernetes;https

# kubectl apply -f 03-prometheus-cfg.yaml
```

#### 2.8.3.2: prometheus deployment

```bash
# 将prometheus运行在node2上，提前准备数据目录并授权。这里实验环境采用hostpath使prometheus数据持久化存储，生产环境采用pv,pvc

root@k-node02:~# mkdir -p /data/prometheusdata
# chmod 777 /data/prometheusdata
#将prometheus运行在node03,提前创建好目录并授权

# kubectl create serviceaccount monitor -n monitoring # 创建监控账号
# kubectl create clusterrolebinding monitor-clusterrolebinding -n monitoring --clusterrole=cluster-admin --serviceaccount=monitoring:monitor # 对monitoring账号授权
```

```bash
# cat 04-prometheus-deploy.yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: prometheus-server
  namespace: monitoring
  labels:
    app: prometheus
spec:
  replicas: 1
  selector:
    matchLabels:
      app: prometheus
      component: server
    #matchExpressions:
    #- {key: app, operator: In, values: [prometheus]}
    #- {key: component, operator: In, values: [server]}
  template:
    metadata:
      labels:
        app: prometheus
        component: server
      annotations:
        prometheus.io/scrape: 'false'
    spec:
      nodeName: 192.168.58.135  # node2的ip地址
      serviceAccountName: monitor
      containers:
      - name: prometheus
        image: prom/prometheus:v2.45.2
        imagePullPolicy: IfNotPresent
        command:
          - prometheus
          - --config.file=/etc/prometheus/prometheus.yml
          - --storage.tsdb.path=/prometheus
          - --storage.tsdb.retention=720h
        ports:
        - containerPort: 9090
          protocol: TCP
        volumeMounts:
        - mountPath: /etc/prometheus/prometheus.yml
          name: prometheus-config
          subPath: prometheus.yml
        - mountPath: /prometheus/
          name: prometheus-storage-volume
      volumes:
        - name: prometheus-config
          configMap:
            name: prometheus-config
            items:
              - key: prometheus.yml
                path: prometheus.yml
                mode: 0644
        - name: prometheus-storage-volume
          hostPath:
           path: /data/prometheusdata
           type: Directory
---
---
apiVersion: v1
kind: Service
metadata:
  name: prometheus
  namespace: monitoring
  labels:
    app: prometheus
spec:
  type: NodePort
  ports:
    - port: 9090
      targetPort: 9090
      nodePort: 30090
      protocol: TCP
  selector:
    app: prometheus
    component: server

```

#### 2.8.3.3：验证prometheus

```bash
# kubectl get pods -n monitoring
prometheus-server-54f586ff7d-6ctbz   1/1     Running   0          2m9s

# kubectl get svc -n monitoring
prometheus      NodePort   10.102.238.253   <none>        9090:30090/TCP   5m14s
```

![image-20231224203357034](images\image-20231224203357034.png)

# 三：prometheus的服务发现机制

   prometheus默认是采用pull方式拉取监控数据的，也就是定时去目标主机上抓取metrics数据，每一个被抓取的目标需要暴露一个HTTP接口，prometheus通过这个暴露的接口就可以获取到相应的指标数据，这种方式需要由目标服务决定采集的目标有哪些，通过配置在scrape_configs中的各种job来实现，无法动态感知新服务，如果后面增加了节点或者组件信息，就得手动修prometheus配置，并重启prometheus，很不方便，所以出现了动态服务发现。动态服务发现能够自动发现集群的新端点，并加入到配置中，通过服务发现，Prometheus能够查询需要监控的Target列表，然后轮询这些Target获取监控数据。

prometheus获取数据源target的方式有多种，如静态配置，prometheus支持多种服务发现，prometheus目前支持的服务发现有很多种，常用的主要分为以下几种：

```bash
kubernetes_sd_config: # Kubernetes服务发现，让prometheus动态发现kubernetes中监控的目标
static_config： # 静态服务发下女，基于prometheus配置文件指定的监控目标
dns_sd_configs: # DNS服务发现监控目标
consul_sd_config： # Consul服务发现，基于consul服务动态发现监控目标
file_sd_config： # 基于指定的文件实现服务发现，基于指定的文件发现监控目标
```

prometheus的静态服务发现`static_configs:` 每当有一个新的目标实例需要监控，都需要手动修改i配置文件配置目标target。

prometheus的consul服务发现`consul_sd_config:` Prometheus一直监视consul服务，当发现在consul中注册大服务有变化，prometheus就会自动监控到所有注册到consul中的目标资源。

prometheus的k8s服务发现`kubernetes_sd_config:` Prometheus与kubernetes的API进行交互，动态的发现kubernetes中部署的所有可监控的目标资源。

## 3.1：kubernetes_sd_config

https://prometheus.io/docs/prometheus/latest/configuration/configuration/#kubernetes_sd_config

```bash
Prometheus的relabeling（重新修改标签）功能很强大，它能够在抓取到目标示例之前把目标示例的元数据标签重新修改，动态添加或者覆盖标签。
Prometheus加载target成功之后，在Target实例中，都包含一些metadata标签信息，默认的标签有：
__address__: 以<host>:<port>格式显示目标target地址
__scheme__：采集的目标服务地址的scheme形式，HTTP或者HTTPS
__metrics_path__:采集的目标服务访问路径
```

### 3.1.1：基础功能-重新标记目的

为了更好的识别监控指标，便于后期调用数据绘图，告警等需求，prometheus支持对发现的你目标进行label修改，在两个阶段可以重新标记：

```bash
relabel_configs: 在采集之前（采集数据之前重新定义元标签），可以使用relabel_configs添加一些标签，也可以只采集特定目标或者过滤目标。

metric_relabel_configs：如果已经抓取到指标数据，可以使用metric_relabel_configs做最后的重新标记和过滤。
```

![image-20231225121344485](images\image-20231225121344485.png)

```yaml
scrape_configs:
  - job_name: "kubernetes-apiservers"  # job名称
    kubernetes_sd_configs: # 基于kubernetes_sd_configs实现服务发现
      - role: endpoints    #发现endpoints
    scheme: https          # 当前job使用的发现协议
    tls_config:            # 证书配置
      ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt #容器里面证书路径
    authorization:
      credentials_file: /var/run/secrets/kubernetes.io/serviceaccount/token # 容器里面token路径
    relabel_configs:  # 重新修改标签
      - source_labels:
          [
            __meta_kubernetes_namespace,
            __meta_kubernetes_service_name,
            __meta_kubernetes_endpoint_port_name,
          ]            # 源标签
        action: keep  # 定义了relabel的具体动作，action支持多种
        regex: default;kubernetes;https # 发现default名称空间kubernetees服务且是https协议
```

### 3.1.2：label详解

```bash
source_labels: 源标签，没有经过relabel处理之前的标签名字
target_label：通过action处理后的新的标签名字
regex: 正则表达式，匹配源标签
replacement：通过分组替换后标签(target_label)对应的值
```

### 3.1.3：action详解

https://prometheus.io/docs/prometheus/latest/configuration/configuration/#relabel_config

```bash
replace：替换标签值，根据regex正则匹配到源标签的值，使用replacement来引用表达式匹配的分组。
keep：满足regex正则条件的实例进行采集，把source_labels中没有匹配到的Target实例丢掉，即只采集匹配成功的实例。
drop：满足regex正则条件的实例不采集，把source_labels中匹配到的Target实例丢掉，即只采集没有匹配到的实例。

hashmod：使用hashmod计算source_labels的Hash值并进行对比，基于自定义模板取模，以实现对目标进行分类，重新赋值等功能。 Example:
labelmap：匹配regex所有标签名称，然后复制匹配标签的值进行分组，通过replacement分组引用(${1},${2},...)替代
labelkeep：匹配regex所有标签名称，其他不匹配的标签都将从标签集中删除
labelkeep：匹配regex所有标签名称，匹配的标签都将从标签集中删除
```

### 3.1.4：测试label功能

```yaml
# vim relabel/01-prometheus-cfg.yaml
# 删除下面82~85行
- job_name: 'kubernetes-apiserver'
 76       kubernetes_sd_configs:
 77       - role: endpoints
 78       scheme: https
 79       tls_config:
 80         ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
 81       bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
 82  #     relabel_configs:
 83  #     - source_labels: [__meta_kubernetes_namespace, __meta_kubernetes_service_name, __meta_kubernetes_endpoint_port_name]
 84  #       action: keep
 85  #       regex: default;kubernetes;https
```

```bash
# kubectl apply -f relabel/01-prometheus-cfg.yaml

重启prometheus，加载最新的配置文件
# kubectl rollout restart deploy prometheus-server -n monitoring
```

如下图：

好多down的，是因为做服务发现的时候没有进行过滤，所有的Pod被匹配成功并进行监控，但是Pod并没有提供metrics指标数据，所以不通：

![image-20231225144542620](images\image-20231225144542620.png)

### 3.1.5：查看prometheus server容器证书

```bash
# kubectl exec -it prometheus-server-5f64f4c8cd-mn9lr -n monitoring -- ls /var/run/secrets/kubernetes.io/serviceaccount
ca.crt     namespace  token
```

### 3.1.6：支持发现的目标类型

`kubernetes_sd_config`发现的类型：https://prometheus.io/docs/prometheus/latest/configuration/configuration/#kubernetes_sd_config

```bash
node
service
pod
endpoints
endpointslice # 对endpoint进行切片
ingress
```

### 3.1.7: 监控api-server实现

apiserver作为kubernetes最核心的组件，它的监控非常必要。对于apiserver的监控，我们可以直接通过kubernetes的service来获取：

```bash
# kubectl get svc
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   44h

# kubectl get ep
NAME         ENDPOINTS             AGE
kubernetes   192.168.58.133:6443   44h

# vim relabel/01-prometheus-cfg.yaml
- job_name: 'kubernetes-apiserver'
      kubernetes_sd_configs:
      - role: endpoints
      scheme: https
      tls_config:
        ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
      bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
      relabel_configs:
      - source_labels: [__meta_kubernetes_namespace, __meta_kubernetes_service_name, __meta_kubernetes_endpoint_port_name]
        action: keep
        regex: default;kubernetes;https # 含义为匹配到default的namespace,svc名称为kubernetes并且协议是https，匹配成功后进行保留，并且把regex作为source_labels相对应的值。即labels为key，regex为值。
        
# __meta_kubernetes_namespace=default, __meta_kubernetes_service_name=kubernetes, __meta_kubernetes_endpoint_port_name=https        
最终，匹配到api-server的地址
```

![image-20231225150825456](images\image-20231225150825456.png)

### 3.1.8：api-server指标数据

Apiserver组件是k8s集群的入口，所有请求都是从apiserver进来的，所以对apiserver指标做监控可以用来判断集群健康状态。

#### 3.1.8.1：apiserver_request_total

以下promQL语句为查询apiserver最近一分钟请求数量统计：

![image-20231225151428264](images\image-20231225151428264.png)

`irate和rate都会用于计算某个指标在一定时间内的变化率。但是它们的计算方法有所不同：irate取的是指定时间范围内最近两个数据点计算速率，而rate会取指定时间范围内所有数据点，算出一组速率，然后取平均值作为结果`

```bash
所以按照官方文档：irate适合快速变化的counter，而rate适合缓慢变化的counter。

根据以上算法我们也可以理解，对于快速变化的计数器，如果使用rate，因为使用了平均值，很容易把峰值削平。除非把时间间隔设置的足够小，就能够减弱这种效应。
```

#### 3.1.8.2：关于annotation_prometheus_io_scrape

在k8s中，基于prometheus的发现规则，需要在被发现的目的target定义注解匹配`annotation_prometheus_io_scrape=true`，且必须匹配成功该注解才会保留监控的target，然后进行数据抓取并进行标签替换，如`annotation_prometheus_io_scheme`标签为http或者https:

```yaml
# cat 03-prometheus-cfg.yaml
- job_name: 'kubernetes-service-endpoints' # job名称
      kubernetes_sd_configs:
      - role: endpoints  #角色，endpoints发现
      relabel_configs:   #标签重写配置
      # annotation_prometheus_io_scrape的值为true, 保留标签再向下执行
      - source_labels: [__meta_kubernetes_service_annotation_prometheus_io_scrape]
        action: keep
        regex: true
      # annotation_prometheus_io_scheme修改为__scheme__  
      - source_labels: [__meta_kubernetes_service_annotation_prometheus_io_scheme]
        action: replace
        target_label: __scheme__
        regex: (https?) # 正则匹配协议http或者https
      # 将源标签替换为__metrics_path__
      - source_labels: [__meta_kubernetes_service_annotation_prometheus_io_path]
        action: replace
        target_label: __metrics_path__
        regex: (.+) # 路径为1到任意长度
       # 地址发现及标签重写 
      - source_labels: [__address__, __meta_kubernetes_service_annotation_prometheus_io_port]
        action: replace
        target_label: __address__
        regex: ([^:]+)(?::\d+)?;(\d+)
        replacement: $1:$2 #格式为地址：端口
       # 发现新的label并用新的service name作为label，发现的值依然是新label的值 
      - action: labelmap
        regex: __meta_kubernetes_service_label_(.+) #通过正则匹配service name
      # 将__meta_kubernetes_namespace替换为kubernetes_namespace
      - source_labels: [__meta_kubernetes_namespace]
        action: replace
        target_label: kubernetes_namespace
      # 将__meta_kubernetes_service_nam替换为kubernetes_name
      - source_labels: [__meta_kubernetes_service_name]
        action: replace
        target_label: kubernetes_name
```

### 3.1.9：Kube-dns组件的服务发现

#### 3.1.9.1：查看kube-dns状态：

```bash
# kubectl describe  svc kube-dns -n kube-system
Name:              kube-dns
Namespace:         kube-system
Labels:            k8s-app=kube-dns
                   kubernetes.io/cluster-service=true
                   kubernetes.io/name=CoreDNS
Annotations:       prometheus.io/port: 9153 #注解标签，用于prometheus服务发现端口
                   prometheus.io/scrape: true #允许prometheus抓取数据
Selector:          k8s-app=kube-dns
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                10.96.0.10
IPs:               10.96.0.10
Port:              dns  53/UDP
TargetPort:        53/UDP
Endpoints:         10.244.84.129:53,10.244.84.130:53
Port:              dns-tcp  53/TCP
TargetPort:        53/TCP
Endpoints:         10.244.84.129:53,10.244.84.130:53
Port:              metrics  9153/TCP
TargetPort:        9153/TCP
Endpoints:         10.244.84.129:9153,10.244.84.130:9153
Session Affinity:  None
Events:            <none>
```

#### 3.1.9.2：修改副本数验证发现

验证：增加kube-dns的副本数，验证prometheus能否自动发现新pod

```bash
 kubectl scale deploy coredns --replicas=3 -n kube-system
```

![image-20231225155752214](images\image-20231225155752214.png)

### 3.1.10：node节点发现

#### 3.1.10.1：配置详解

```bash
# cat 03-prometheus-cfg.yaml
---
kind: ConfigMap
apiVersion: v1
metadata:
  labels:
    app: prometheus
  name: prometheus-config
  namespace: monitoring 
data:
  prometheus.yml: |
    global:
      scrape_interval: 15s
      scrape_timeout: 10s
      evaluation_interval: 1m
    scrape_configs:
    - job_name: 'kubernetes-node'  # job name
      kubernetes_sd_configs:       # 发现配置
      - role: node                 # 发现角色
      relabel_configs:             # 标签重写配置
      - source_labels: [__address__]  # 源标签
        regex: '(.*):10250'         # 通过正则匹配后缀为：10250的实例，10205是kubelet端口，默认发现的就是Kubelet端口
        replacement: '${1}:9100' # 将端口替换为node exporter的端口
        target_label: __address__ #将[__address__]替换为__address__
        action: replace #将[__address__]的值赋给__address__
      # 发现新的label并用新的servicename作为label，将发现的值赋给新label的值  
      - action: labelmap
        regex: __meta_kubernetes_node_label_(.+)
```

![image-20231225160826411](images\image-20231225160826411.png)

#### 3.1.10.2：node节点指标数据

```bash
# HELP:解释当前指标的含义
# 说明当前指标的数据类型

# HELP node_load1 1m load average.
# TYPE node_load1 gauge
node_load1 3.41
# HELP node_load15 15m load average.
# TYPE node_load15 gauge
node_load15 3.42
# HELP node_load5 5m load average.
# TYPE node_load5 gauge
node_load5 3.38
```

#### 3.1.10.3：常见监控指标

```bash
node_cpu: CPU相关指标
node_load1: 系统负载指标
node_load5
node_load15

node_memory_: 内存相关指标

node_network_:网络相关指标

node_disk_: 磁盘IO相关
node_filesystem_: 文件系统相关

node_boot_time_seconds：系统启动时间

go_*：node exporter运行过程中go相关的指标
process_*: node exporter运行进程指标
```

### 3.1.11：Pod发现及指标数据

#### 3.1.11.1：prometheus job配置

```bash
# cat 03-prometheus-cfg.yaml
    - job_name: 'kubernetes-node-cadvisor'  # job名称
          kubernetes_sd_configs:            # 基于k8s服务发现
          - role:  node                     # 角色
          scheme: https                     # 协议
          tls_config:                       # 证书配置
            ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
          bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
          relabel_configs:   # 标签重写配置
          - action: labelmap
            regex: __meta_kubernetes_node_label_(.+)
          # replacement指定替换后的标签值为：kubernetes.default.svc:443  
          - target_label: __address__
            replacement: kubernetes.default.svc:443
          # 将[__meta_kubernetes_node_name]重写为__metrics_path__  
          - source_labels: [__meta_kubernetes_node_name]
            regex: (.+)
            target_label: __metrics_path__
            replacement: /api/v1/nodes/${1}/proxy/metrics/cadvisor #替换值


# 注意：
tls_config配置的证书地址是每个Pod连接apiserver所用的地址，无论证书是否用得上，在pod启动的时候kubelet会给每一个pod自动注入ca的公钥，用于在访问apiserver被调用。
```

#### 3.1.11.2：pod监控指标

CPU

内存

磁盘

网卡

```bash
sum(rate(container_cpu_usage_seconds_total[1m])) by (pod)
sum(rate(container_memory_usage_bytes[1m])) by (pod)

sum(rate(container_fs_io_current[1m])) without (device)
sum(rate(container_fs_reads_bytes_total[1m])) without (device)
sum(rate(container_fs_writes_bytes_total[1m])) without (device)

sum(rate(container_network_receive_bytes_total[1m])) without (interface)
```

### 3.1.12: prometheus部署在k8s集群外实现服务发现

```bash
环境说明：
prometheus(二进制k8s集群外): 192.168.58.145
kubernetes: v1.27.1
```

#### 3.1.12.1：创建用户并授权

```bash
# cat 01-prom-rbac.yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: prometheus
  namespace: monitoring
---
apiVersion: v1
kind: Secret
metadata:
  name: secret-sa-prometheus
  namespace: monitoring
  annotations:
    kubernetes.io/service-account.name: "prometheus"   # 这里填写serviceAccountName
type: kubernetes.io/service-account-token
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: prometheus
rules:
- apiGroups:
  - ""
  resources:
  - nodes
  - services
  - endpoints
  - pods
  - nodes/proxy
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - "extensions"
  resources:
    - ingresses
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - ""
  resources:
  - configmaps
  - nodes/metrics
  verbs:
  - get
- nonResourceURLs:
  - /metrics
  verbs:
  - get
---
#apiVersion: rbac.authorization.k8s.io/v1beta1
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: prometheus
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: prometheus
subjects:
- kind: ServiceAccount
  name: prometheus
  namespace: monitoring


# kubectl apply -f 01-prom-rbac.yaml
```

#### 3.1.12.2：获取token

```bash
root@k-master01:~/prometheus/k8s-prom# kubectl describe secret secret-sa-prometheus -n monitoring
Name:         secret-sa-prometheus
Namespace:    monitoring
Labels:       <none>
Annotations:  kubernetes.io/service-account.name: prometheus
              kubernetes.io/service-account.uid: 8fc1e24b-5f5c-4777-a902-ea302ed7a199

Type:  kubernetes.io/service-account-token

Data
====
ca.crt:     1099 bytes
namespace:  10 bytes
token:      eyJhbGciOiJSUzI1NiIsImtpZCI6InBnQUFkQUFmQm1BOEpfRGEzeXlxcnF2ZG1iWHhnbTlUMTBBMUVrY2VzaFUifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJtb25pdG9yaW5nIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6InNlY3JldC1zYS1wcm9tZXRoZXVzIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6InByb21ldGhldXMiLCJrdWJlcm5ldGVzLmlvL3NlcnZpY2VhY2NvdW50L3NlcnZpY2UtYWNjb3VudC51aWQiOiI4ZmMxZTI0Yi01ZjVjLTQ3NzctYTkwMi1lYTMwMmVkN2ExOTkiLCJzdWIiOiJzeXN0ZW06c2VydmljZWFjY291bnQ6bW9uaXRvcmluZzpwcm9tZXRoZXVzIn0.ZCvfxslb9K2WRwq5ijoE9xDgevhWCrqQ1tYSaOMsGaWURuupZmtkou_A3IcgbQANaSsLGAyhJtc8Ynw_zEaVyBp9MY6RHIcDOmunmWbFuOlZJiDqSRlhW_ObF35nSFAwJ60gtDMdOLxxmOme8BbLTBHXHqjYhyjOynaBBibdxlc4GekdIkcojpqhjVBR4sFpZeNhCB9r3rfn8E8VfmUMVCz_VRq2PtYv8xHnXWK6DGJjvffktBmOA8gAWuSLVdnY4SuRY4SjNJCzWme0P_jrRFcFtTRSCAYz1olL6HCIF9y1tg2pFjlglLk91za8LDCEHEFhEQkgHINFnnqoxDIhCw
```

**将token保存到外部prometheus节点的k8s.token文件，后期用于权限认证。**

```bash
# vim /app/prometheus/k8s.token
```

#### 3.1.12.3：prometheus添加job

```bash
# cat /app/prometheus/prometheus.yml
# my global config
global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
  # scrape_timeout is set to the global default (10s).

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets:
          # - alertmanager:9093

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  # - "first_rules.yml"
  # - "second_rules.yml"

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  - job_name: 'kubernetes-apiservers-monitor' 
    kubernetes_sd_configs: 
    - role: endpoints
      api_server: https://192.168.58.133:6443
      tls_config: 
        insecure_skip_verify: true  
      bearer_token_file: /app/prometheus/k8s.token 
    scheme: https 
    tls_config: 
      insecure_skip_verify: true 
    bearer_token_file: /app/prometheus/k8s.token 
    relabel_configs: 
    - source_labels: [__meta_kubernetes_namespace, __meta_kubernetes_service_name, __meta_kubernetes_endpoint_port_name] 
      action: keep 
      regex: default;kubernetes;https 
    - target_label: __address__ 
      replacement: 192.168.58.133:6443
  - job_name: 'kubernetes-nodes-monitor' 
    scheme: http 
    tls_config: 
      insecure_skip_verify: true 
    bearer_token_file: /app/prometheus/k8s.token 
    kubernetes_sd_configs: 
    - role: node 
      api_server: https://192.168.58.133:6443
      tls_config: 
        insecure_skip_verify: true 
      bearer_token_file: /app/prometheus/k8s.token 
    relabel_configs: 
      - source_labels: [__address__] 
        regex: '(.*):10250' 
        replacement: '${1}:9100' 
        target_label: __address__ 
        action: replace 
      - source_labels: [__meta_kubernetes_node_label_failure_domain_beta_kubernetes_io_region] 
        regex: '(.*)' 
        replacement: '${1}' 
        action: replace 
        target_label: LOC 
      - source_labels: [__meta_kubernetes_node_label_failure_domain_beta_kubernetes_io_region] 
        regex: '(.*)' 
        replacement: 'NODE' 
        action: replace 
        target_label: Type 
      - source_labels: [__meta_kubernetes_node_label_failure_domain_beta_kubernetes_io_region] 
        regex: '(.*)' 
        replacement: 'K3S-test' 
        action: replace 
        target_label: Env 
      - action: labelmap 
        regex: __meta_kubernetes_node_label_(.+)

  - job_name: 'kubernetes-pods-monitor' 
    kubernetes_sd_configs: 
    - role: pod 
      api_server: https://192.168.58.133:6443
      tls_config: 
        insecure_skip_verify: true 
      bearer_token_file: /app/prometheus/k8s.token 
    relabel_configs: 
    - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_scrape] 
      action: keep 
      regex: true 
    - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_path] 
      action: replace 
      target_label: __metrics_path__ 
      regex: (.+) 
    - source_labels: [__address__, __meta_kubernetes_pod_annotation_prometheus_io_port] 
      action: replace 
      regex: ([^:]+)(?::\d+)?;(\d+) 
      replacement: $1:$2 
      target_label: __address__ 
    - action: labelmap 
      regex: __meta_kubernetes_pod_label_(.+) 
    - source_labels: [__meta_kubernetes_namespace] 
      action: replace 
      target_label: kubernetes_namespace 
    - source_labels: [__meta_kubernetes_pod_name] 
      action: replace 
      target_label: kubernetes_pod_name 
    - source_labels: [__meta_kubernetes_pod_label_pod_template_hash] 
      regex: '(.*)' 
      replacement: 'K8S-test' 
      action: replace 
      target_label: Env 
```

#### 3.1.12.4：验证数据

![image-20231225185036253](images\image-20231225185036253.png)

## 3.2：static_configs

下面配置以二进制部署的prometheus环境为例

### 3.2.1：prometheus配置文件

```yaml
# A scrape configuration containing exactly one endpoint to scrape: #端点抓取配置
# Here it's Prometheus itself. #prometheus的默认配置
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "prometheus"

    # metrics_path defaults to '/metrics' #默认url
    # scheme defaults to 'http'. #协议

    static_configs:  # 静态服务配置
      - targets: ["localhost:9090"]
  - job_name: "node-exporter"
    static_configs:
       - targets: ["192.168.58.146:9100", "192.168.58.144:9100"]

```

```bash
# systemctl restart prometheus
```

### 3.2.2：验证prometheus web

![image-20231227093009434](images\image-20231227093009434.png)

## 3.3：consul_sd_configs

https://www.consul.io/

```bash
Consul是分布式k/v数据存储集群，目前常用于服务的服务注册和发现。
```

### 3.3.1：部署consul集群

https://releases.hashicorp.com/consul/

```shell
环境：
consul: 1.17.1

consul1: 192.168.58.145
consul2: 192.168.58.146
consul3: 192.168.58.144
```

```shell
consul1:
# wget https://releases.hashicorp.com/consul/1.17.1/consul_1.17.1_linux_amd64.zip
# unzip consul_1.17.1_linux_amd64.zip
# scp consul 192.168.58.146:/usr/local/bin/
# scp consul 192.168.58.144:/usr/local/bin/

consul -h #验证可执行

# 分别创建数据目录
# mkdir -p /data/consul/


启动服务：
consul1:
# consul agent -server -bootstrap -bind=192.168.58.145 -client=192.168.58.145 -data-dir=/data/consul/ -ui -node=192.168.58.145

consul2:
# consul agent  -bind=192.168.58.146 -client=192.168.58.146 -data-dir=/data/consul/  -node=192.168.58.146 -join=192.168.58.145

consul3:
# consul agent  -bind=192.168.58.144 -client=192.168.58.144 -data-dir=/data/consul/  -node=192.168.58.144 -join=192.168.58.145
```

### 3.3.2：验证集群

日志：

![image-20231227101539319](images\image-20231227101539319.png)

web截图：

![image-20231227101724011](images\image-20231227101724011.png)

### 3.3.3：测试写入数据

通过consul的API写入数据

```bash
~# curl -X PUT -d '{"id": "node-exporter146","name": "node-exporter146","address": "192.168.58.146","port":9100,"tags":["node-exporter"],"checks": [{"http":"http://192.168.58.146:9100/","interval":"5s"}]}' http://192.168.58.145:8500/v1/agent/service/register


~# curl -X PUT -d '{"id": "node-exporter144","name": "node-exporter144","address": "192.168.58.144","port":9100,"tags":["node-exporter"],"checks": [{"http":"http://192.168.58.144:9100/","interval":"5s"}]}' http://192.168.58.145:8500/v1/agent/service/register
```

### 3.3.4: consul验证数据

![image-20231227103235795](images\image-20231227103235795.png)

### 3.3.5：配置prometheus到consul发现服务

```shell
consul_sd_configs：指定基于consul服务发现的配置
relabel_configs: 重新标记
services：[]  #表示匹配到consul中所有的service
```

```shell
~# cat /app/prometheus/prometheus.yaml
- job_name: "consul"
    honor_labels: true
    metrics_path: /metrics
    scheme: http
    consul_sd_configs:
      - server: 192.168.58.145:8500
        services: [] #发现目标服务名称，空为所有服务
      - server: 192.168.58.146:8500
        services: []
      - server: 192.168.58.144:8500
        services: []
    relabel_configs: 
    - source_labels: ['__meta_consul_tags'] 
      target_label: 'product'
    - source_labels: ['__meta_consul_dc']
      target_label: 'idc'
    - source_labels: ['__meta_consul_service']
      regex: "consul"
      action: drop  #不匹配consul本身服务
```

![image-20231227104919495](images\image-20231227104919495.png)

### 3.3.6：consul服务删除

```shell
~# curl --request PUT http://192.168.58.145:8500/v1/agent/service/deregister/node-exporter145
```

### 3.3.7：当consul注册新服务，prometheus能否自动发现

#### 3.3.7.1：注册新服务在consul

```shel 
~# curl -X PUT -d '{"id": "node-exporter145","name": "node-exporter145","address": "192.168.58.145","port":9100,"tags":["node-exporter"],"checks": [{"http":"http://192.168.58.145:9100/","interval":"5s"}]}' http://192.168.58.145:8500/v1/agent/service/register
```

![image-20231227105546713](images\image-20231227105546713.png)

#### 3.3.7.2：验证prom能否自动发现

![image-20231227105647893](images\image-20231227105647893.png)

## 3.4：file_sd_configs

### 3.4.1: 编辑sd_configs文件

```bash
~# mkdir /app/prometheus/file_sd
~# vim /app/prometheus/file_sd/my_server.json
[
  {
    "targets": [ "192.168.58.145:9100","192.168.58.144:9100","192.168.58.146:9100"]
  }
]
```

### 3.4.2：prometheus调用sd_configs

```bash
~# vim /app/prometheus/prometheus.yml
- job_name: "fd_my_server"
    file_sd_configs:
    - files:
      - /app/prometheus/file_sd/my_server.json
      refresh_interval: 5s #默认5分钟
      
~# systemctl restart prometheus
```

### 3.4.3：验证数据

![image-20231227111819657](images\image-20231227111819657.png)

## 3.5：DNS服务发现

```bash
基于DNS的服务发现允许配置指定一组DNS域名，这些域名会定期查询以发现目标列表，域名需要可以被配置的DNS服务器解析为IP。

此服务发现的方法仅支持基本的DNS A，AAAA,和SRV记录查询。
A记录：域名解析为IP
SRV: SRV记录了哪台计算机提供了具体哪个服务，格式为：自定义的服务名称.协议的类型.域名（例如：_example-server._tcp.www.mydns.com）
```

```bash
prometheus 会对收集的指标数据进行重新打标，重新标记期间，可以使用以下元标签：
__meta_dns_name： 目标的记录名称
__meta_dns_srv_record_target：SRV记录的目标字段
__meta_dns_srv_record_port: 记录的端口字段
```

### 3.5.1：A记录服务发现

```bash
~$ vim /etc/hosts
192.168.58.145 node01.icloud2native.com
192.168.58.146 node02.icloud2native.com
192.168.58.144 node03.icloud2native.com

~$ vim /app/prometheus/prometheus.yml
- job_name: "dns_fd"
    dns_sd_configs:
    - names: ["node01.icloud2native.com","node02.icloud2native.com","node03.icloud2native.com"]
      type: A
      port: 9100
      refresh_interval: 5s
      
~$ systemctl restart prometheus
```

### 3.5.2：验证服务状态

![image-20231227113738868](images\image-20231227113738868.png)

# 四：PromQL语句简介

https://prometheus.io/docs/prometheus/latest/querying/basics/

Prometheus提供一个函数式的表达式语言PromQL，可以使用户实时地查找和聚合时间序列数据，表达式计算结果可以在图表中展示，也可以在Prometheus表达式浏览器中以表格形式展示，或者作为数据源，以HTTP API的方式提供给外部系统使用。

## 4.1：PromQL数据基础

### 4.1.1：数据分类

```bash
瞬时向量、瞬时数据（instant vector）：是一组时间序列，每个时间序列包含单个数据样本，比如node_memory_MemTotal_bytes查询当前剩余内存就是一个瞬时向量，该表达式的返回值只包含该时间序列中的最新的一个样本值，而这样的表达式称之为是瞬时向量表达式。eg: prometheus_http_requests_total


范围向量、范围数据（range vector）：是指在任何一个时间范围内，抓取的所有度量指标数据，比如最近一天的网卡流量趋势图，eg：prometheus_http_requests_total[5m]



标量、纯量数据（scalar）：是一个浮点类型的数据值，node_load1获取到一个瞬时向量，但使用scalar()将瞬时向量转换为标量，例如：scalar(sum(node_load1))


字符串（string）:字符串类型数据，目前使用较少
```

### 4.1.2：数据类型

![image-20231227144131831](images\image-20231227144131831.png)

#### 4.1.2.1：Counter 只增不减计数器

Counter：计数器，Counter类型代表一个累积2的指标数据，在没有被重置的前提下只增不减，比如磁盘I/O总数、nginx的请求总数、网卡流经的报文总数等。

Counter是一个简单但有强大的工具，例如我们可以在应用程序中记录某些事件发生的次数，通过以时序的形式存储这些数据，我们可以轻松的了解该事件产生速率的变化。 PromQL内置的聚合操作和函数可以让用户对这些数据进行进一步的分析：

例如，通过rate()函数获取HTTP请求量的增长率：

```bash
rate(http_requests_total[5m])
```

查询当前系统中，访问量前10的HTTP地址：

```bash
topk(10, http_requests_total)
```

#### 4.1.2.2：Gauge 可增可减的仪表盘

Gauge：仪表盘，代表一个可以任意变化的指标数据，值可以随时增高或减少，如带宽速率，内存使用率,nginx活动连接数。

![image-20231227145053474](images\image-20231227145053474.png)

#### 4.1.2.3：Histogram 累积直方图

Histogram：累积直方图，Histogram会在一段时间范围内对数据进行采样（通常是请求持续时间或者响应大小），例如每分钟产生一个当前的活跃连接数，那么一天产生1440个数据，查看数据的每间隔绘图跨度为2小时，那么2点的柱状图（bucket）会包含0点到2点两个小时的数据，而4点的柱状图（bucket）会包含0点到4点的数据，而6点的柱状图（bucket）会包含0点到6点的数据.

```bash
# HELP prometheus_http_request_duration_seconds Histogram of latencies for HTTP requests.
# TYPE prometheus_http_request_duration_seconds histogram
prometheus_http_request_duration_seconds_bucket{handler="/-/ready",le="0.1"} 40
prometheus_http_request_duration_seconds_bucket{handler="/-/ready",le="0.2"} 40
prometheus_http_request_duration_seconds_bucket{handler="/-/ready",le="0.4"} 40
prometheus_http_request_duration_seconds_bucket{handler="/-/ready",le="1"} 40
prometheus_http_request_duration_seconds_bucket{handler="/-/ready",le="3"} 40
prometheus_http_request_duration_seconds_bucket{handler="/-/ready",le="8"} 40
prometheus_http_request_duration_seconds_bucket{handler="/-/ready",le="20"} 40
prometheus_http_request_duration_seconds_bucket{handler="/-/ready",le="60"} 40
prometheus_http_request_duration_seconds_bucket{handler="/-/ready",le="120"} 40
prometheus_http_request_duration_seconds_bucket{handler="/-/ready",le="+Inf"} 40
prometheus_http_request_duration_seconds_sum{handler="/-/ready"} 0.00050091
prometheus_http_request_duration_seconds_count{handler="/-/ready"} 40
prometheus_http_request_duration_seconds_bucket{handler="/api/v1/label/:name/values",le="0.1"} 3
prometheus_http_request_duration_seconds_bucket{handler="/api/v1/label/:name/values",le="0.2"} 3
prometheus_http_request_duration_seconds_bucket{handler="/api/v1/label/:name/values",le="0.4"} 3
prometheus_http_request_duration_seconds_bucket{handler="/api/v1/label/:name/values",le="1"} 3
```

![image-20231227150730718](images\image-20231227150730718.png)

#### 4.1.2.4：Summary

```bash
Summary: 摘要，也是一组数据，统计的不是区间的个数而是统计分位数。从0到1，表示的是0%~100%，如下统计的是0、0.25、0.5、0.75、1的数据量分别是多少。eg：go_gc_duration_seconds

# HELP go_gc_duration_seconds A summary of the pause duration of garbage collection cycles.
# TYPE go_gc_duration_seconds summary
go_gc_duration_seconds{quantile="0"} 1.1803e-05
go_gc_duration_seconds{quantile="0.25"} 4.2061e-05
go_gc_duration_seconds{quantile="0.5"} 8.3873e-05
go_gc_duration_seconds{quantile="0.75"} 0.000192238  #百分之75的持续时间
go_gc_duration_seconds{quantile="1"} 0.002703841
go_gc_duration_seconds_sum 0.018500285
go_gc_duration_seconds_count 94
```

![image-20231227151618182](images\image-20231227151618182.png)

## 4.2：PromQL-指标数据

```bash
node_memory_MemTotal_bytes   #查询node节点总内存大小
node_memory_MemFree_bytes    #查询node节点剩余内存大小
node_memory_MemTotal_bytes{instance="192.168.58.144:9100"} #基于标签查询指定节点的总内存
node_memory_MemFree_bytes{instance="192.168.58.144:9100"}  #基于标签查询指定节点的可用内存

node_disk_io_time_seconds_total{device="sda"} # 查询指定磁盘的每秒磁盘io
node_filesystem_free_bytes{fstype="ext4",mountpoint="/"} # 查询指定磁盘剩余空间

# HELP node_load1 1m load average.  # CPU负载
# TYPE node_load1 gauge
node_load1 0
# HELP node_load15 15m load average.
# TYPE node_load15 gauge
node_load15 0
# HELP node_load5 5m load average.
# TYPE node_load5 gauge
node_load5 0.02
```

## 4.3：PromQL-匹配器

```bash
=: 精确匹配
！=：取反
=~：正则匹配
！~：正则取反


# 查询格式<metric name>{<label name>=<label value>,...}
node_load1{instance="192.168.58.144:9100"} #精确匹配
node_load1{instance!="192.168.58.144:9100"} #取反
node_load1{instance=~"192.168.58.14.*:9100$"} # 正则匹配
node_load1{instance!~"192.168.58.144:9100"} # 正则取反
```

## 4.4：PromQL-时间范围

```bash
s: 秒
m：分钟
h：小时
d：天
w：周
y：年


# 瞬时向量表达式，选择当前最新的数据
node_memory_MemTotal_bytes{}

# 区间向量表达式，查询所有节点5分钟内的数据
node_memory_MemTotal_bytes{}[5m]
```

![image-20231227154714263](images\image-20231227154714263.png)

## 4.5：PromQL-运算符

```bash
+ 加法
- 减法
* 乘法
/ 除法
% 模
^ 幂等

node_memory_MemFree_bytes/1024/1024  # 将内存单位从字节转为兆
node_disk_written_bytes_total{device="sda"} + node_disk_read_bytes_total{device="sda"} # 计算磁盘读写数据量
```

![image-20231227155515218](images\image-20231227155515218.png)

## 4.6：PromQL-聚合运算

### 4.6.1：max、min、avg

```bash
max()  #最大值
min()  #最小值
avg()  #平均值

计算每个节点的最大流量值：
max(node_network_receive_bytes_total) by (instance)

计算每个节点最近五分钟每个device的最大流量
max(rate(node_network_receive_bytes_total[5m])) by (device)
```

![image-20231227161310580](images\image-20231227161310580.png)

### 4.6.2：sum、count

```bash
sum()  #求数据值相加的和（总数）
sum(prometheus_http_requests_total)
{}   1131 #最近总共请求数，用于计算返回的总数

count()  #统计返回值的条款
count(node_os_version)
{}   8  #一共两条返回的数据
```

![image-20231227162124327](images\image-20231227162124327.png)

### 4.6.3：abs、absent

```bash
abs()  # 返回指标数据绝对值
abs(sum(prometheus_http_requests_total{handler="/metrics"}))

absent() # 返回布尔值。如果监控项指标有数据返回空，没数据就返回1，可用于对监控项设置告警
absent(sum(prometheus_http_requests_total{handler="/metrics"}))
```

![image-20231227163628345](images\image-20231227163628345.png)

### 4.6.4：stddev、stdvar

```bash
stddev()  #标准差
stddev(prometheus_http_requests_total) #5+5=10，1+9=10. 1+9这一组数据差异大，系统数据波动大，不稳定

stdvar() #求方差
stdvar(prometheus_http_requests_total)
```

### 4.6.5：topk、bottomk

```bash
topk()    #样本值排名最大的N个数据
  # 取从大到小前6个
  topk(6,prometheus_http_requests_total)
  
bottomk()   #样本值排名最小的N个数据
  # 取从小到大前6个
  bottomk(6,prometheus_http_requests_total)
```

![image-20231227165141204](images\image-20231227165141204.png)

### 4.6.6：rate、irate

```yaml
rate() :专门处理counter数据类型，取相邻样本值差，然后取平均数。得到的是这个时间段平均每秒增量平均数。但是精度不够，不能反映峰值。
	rate(prometheus_http_requests_total[5m])
	
irate()：专门处理counter数据类型，区间向量中最后两个样本数据来计算区间向量的增长速率。
	irate(prometheus_http_requests_total[5m])
```

![image-20231227170100265](images\image-20231227170100265.png)

![image-20231227170129774](images\image-20231227170129774.png)

### 4.6.7：by、without

```bash
# by: 在计算结果中，只保留by指定的标签的值。
sum(rate(node_memory_MemFree_bytes[5m])) by (instance)

#without： 从计算结果中移除列举的instabnce标签，保留其他标签
sum(rate(node_memory_MemFree_bytes[5m])) without (instance)
```

![image-20231227170910332](images\image-20231227170910332.png)

### 4.6.8：histogram_quantile()

其中Histogram和Summary都可以用于统计和分析数据的分布情况。区别在于Summary是直接在客户端计算了数据分布的分位数情况。而Histogram的分位数计算需要通过histogram_quantile(φ float, b instant-vector)函数进行计算。其中φ（0<φ<1）表示需要计算的分位数，如果需要计算中位数φ取值为0.5，以此类推即可。

以指标`prometheus_http_request_duration_seconds_bucket`为例：

当计算9分为数时，使用如下表达式：

```bash
histogram_quantile(0.9,prometheus_http_request_duration_seconds_bucket{handler="/metrics"}[1m])


{handler="/metrics", instance="localhost:9090", job="prometheus"}
0.09000000000000001
```

这表示 90% 的样本的最大值为 0.09000000000000001。

# 五：kube-state-metrics组件介绍

https://github.com/kubernetes/kube-state-metrics

```bash
kube-state-metrics通过监听API Servver生成有关资源对象的额状态指标，比如Deployment、Node、Pod。需要注意的是kubee-state-metrics只是简单的提供一个mtrics数据，并不会存储这些指标数据，所以我们呢可以用Prometheus来抓取这些数据然后存储，主要关注的是业务相关的一些元数据，比如Deployment、Pod、副本状态等；调度了多少replicas？现在可用的有几个？多少个pod是runing/stoping/terminated状态？Pod重启了多少次，有多少job运行。

kube-state-metrics (KSM) is a simple service that listens to the Kubernetes API server and generates metrics about the state of the objects.
```

https://xie.infoq.cn/article/9e1fff6306649e65480a96bb1https://xie.infoq.cn/article/9e1fff6306649e65480a96bb1 # 指标

## 5.1：部署kube-state-metrics

```shell
kubernetes 版本： v1.27.1
kube-state-metrics版本： v2.10.0
prometheus (k8s之外二进制)：v2.48.1
```

```bash
~$ cat kube-state-metrics-deploy.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: kube-state-metrics
  namespace: kube-system
spec:
  replicas: 1
  selector:
    matchLabels:
      app: kube-state-metrics
  template:
    metadata:
      labels:
        app: kube-state-metrics
    spec:
      serviceAccountName: kube-state-metrics
      containers:
      - name: kube-state-metrics
        image: registry.k8s.io/kube-state-metrics/kube-state-metrics:v2.10.0
        ports:
        - containerPort: 8080

---
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: kube-state-metrics
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: kube-state-metrics
rules:
- apiGroups: [""]
  resources: ["nodes", "pods", "services", "resourcequotas", "replicationcontrollers", "limitranges", "persistentvolumeclaims", "persistentvolumes", "namespaces", "endpoints"]
  verbs: ["list", "watch"]
- apiGroups: ["extensions"]
  resources: ["daemonsets", "deployments", "replicasets"]
  verbs: ["list", "watch"]
- apiGroups: ["apps"]
  resources: ["statefulsets"]
  verbs: ["list", "watch"]
- apiGroups: ["batch"]
  resources: ["cronjobs", "jobs"]
  verbs: ["list", "watch"]
- apiGroups: ["autoscaling"]
  resources: ["horizontalpodautoscalers"]
  verbs: ["list", "watch"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: kube-state-metrics
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: kube-state-metrics
subjects:
- kind: ServiceAccount
  name: kube-state-metrics
  namespace: kube-system

---
apiVersion: v1
kind: Service
metadata:
  annotations:
    prometheus.io/scrape: 'true'
  name: kube-state-metrics
  namespace: kube-system
  labels:
    app: kube-state-metrics
spec:
  type: NodePort
  ports:
  - name: kube-state-metrics
    port: 8080
    targetPort: 8080
    nodePort: 31666
    protocol: TCP
  selector:
    app: kube-state-metrics
    
    
# kubectl apply -f kube-state-metrics-deploy.yaml
# kubectl get pods -n kube-system | grep kube-state-metrics
kube-state-metrics-7478784f5b-6m7dz        1/1     Running   0            2m1s
```

## 5.2：验证数据

![image-20240103094241377](images\image-20240103094241377.png)

## 5.3：prometheus采集数据

```bash
~$ cat /app/prometheus/prometheus.yml
- job_name: "kube-state-metrics"
    static_configs:
      - targets: ["192.168.58.133:31666"]
```

## 5.4：验证prometheus状态

![image-20240103094750260](images\image-20240103094750260.png)

## 5.5：导入grafana

13824:

![image-20240103095643370](images\image-20240103095643370.png)

# 六：监控基础服务

基于第三方exporter实现对目的服务的监控

## 6.1：监控MySQL

mysqld_exporter监控MySQL服务的运行状态

https://github.com/prometheus/mysqld_exporter

```bash
环境：

prometheus(v2.48.1): 192.168.58.145 
mysqld_exporter(v0.15.1): 192.168.58.146
mariadb(10.3): 192.168.58.146
```

### 6.1.1:安装mysql

```shell
~$ apt install mariadb-server
root@exporter1:~# mysql
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 36
Server version: 10.3.38-MariaDB-0ubuntu0.20.04.1 Ubuntu 20.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> 
```

### 6.1.2: 授权监控账号权限

```sql
MariaDB [(none)]> CREATE USER 'alblue'@'localhost' IDENTIFIED BY '123456';
Query OK, 0 rows affected (0.000 sec)


MariaDB [(none)]> GRANT PROCESS, REPLICATION CLIENT, SELECT ON *.* TO 'alblue'@'localhost';
Query OK, 0 rows affected (0.000 sec)


# 验证权限
root@exporter1:~# mysql -ualblue -p123456 -h localhost
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 37
Server version: 10.3.38-MariaDB-0ubuntu0.20.04.1 Ubuntu 20.04

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]> 
```

### 6.1.3：准备mysqld_exporter环境

```bash
~$ cd /app
~$ wget https://github.com/prometheus/mysqld_exporter/releases/download/v0.15.1/mysqld_exporter-0.15.1.linux-amd64.tar.gz
~$ tar xf mysqld_exporter-0.15.1.linux-amd64.tar.gz
~$ cp mysqld_exporter /usr/local/bin/


# 免密码登录配置
cat /root/.my.cnf
[client]
user = alblue
password = 123456
```

### 6.1.4：启动mysql_exporter

```bash
~$ cat /etc/systemd/system/mysqld_exporter.service
[Unit]
Description=Mysql Exporter
After=network.target

[Service]
ExecStart=/usr/local/bin/mysqld_exporter --config.my-cnf=/root/.my.cnf

[Install]
WantedBy=multi-user.target


~$ systemctl daemon-reload && systemctl restart mysqld_exporter.service && systemctl enable mysqld_exporter.service
```

### 6.1.5：验证metrics

![image-20240103104519933](images\image-20240103104519933.png)

### 6.1.6：prometheus采集数据

```bash
~$ vim prometheus.yml
- job_name: "mysqld exporter"
    static_configs:
      - targets: ["192.168.58.146:9104"]
      
~$ systemctl restart prometheus.service      
```

### 6.1.7：验证指标数据

![image-20240103105010660](images\image-20240103105010660.png)

### 6.1.8：导入模板

11323

![image-20240103105207258](images\image-20240103105207258.png)

## 6.2：监控haproxy

通过haproxy_exporter监控haproxy

https://github.com/prometheus/haproxy_exporter

```bash
环境说明：
haproxy: 192.168.58.146
haproxy_exporter(0.15.0): 192.168.58.146
```

### 6.2.1：部署haproxy

```bash
~$ apt install haproxy 

# 修改socket文件
~$ vim /etc/haproxy/haproxy.cfg
stats socket /run/haproxy/admin.sock mode 660 level admin
~$ systemctl restart haproxy
```

### 6.2.2：部署haproxy_exporter

```bash
~$ cd  /app
~$ wget https://github.com/prometheus/haproxy_exporter/releases/download/v0.15.0/haproxy_exporter-0.15.0.linux-amd64.tar.gz

~$ cp haproxy_exporter /usr/local/bin/

启动方式一：
# haproxy_exporter --haproxy.scrape-uri=unix:/run/haproxy/admin.sock

启动方式二：
开启状态页
~$ vim /etc/haproxy/haproxy.cfg
# Haproxy统计页面
# --------------------------------------------------------------------------------------------
listen haproxy_stats
    bind :9009  #侦听IP:Port
    mode http
    stats enable
    stats refresh 30s
    stats uri /haproxy-stats
    stats realm Haproxy\ Stats\ Page
    stats auth haadmin:123456
    stats auth admin:123456
    # stats hide-version
    
~$ systemctl restart haproxy  
~$ haproxy_exporter  --haproxy.scrape-uri="http://haadmin:123456@192.168.58.146:9009/haproxy-stats;csv"
ts=2024-01-03T03:44:50.103Z caller=haproxy_exporter.go:602 level=info msg="Starting haproxy_exporter" version="(version=0.15.0, branch=HEAD, revision=d4aba878f043fd3ad0bcacd0149e7d75e67c0faa)"
ts=2024-01-03T03:44:50.103Z caller=haproxy_exporter.go:603 level=info msg="Build context" context="(go=go1.19.5, platform=linux/amd64, user=root@d10658e4ead1, date=20230215-11:17:10)"
ts=2024-01-03T03:44:50.103Z caller=tls_config.go:232 level=info msg="Listening on" address=[::]:9101
ts=2024-01-03T03:44:50.103Z caller=tls_config.go:235 level=info msg="TLS is disabled." http2=false address=[::]:9101

```

![image-20240103114347405](images\image-20240103114347405.png)

### 6.2.3：验证metrics数据

```bash
~$ vim /etc/haproxy/haproxy.cfg
frontend web
    bind *:80
    default_backend prom-web
backend prom-web
    mode http
    server prom-1 192.168.58.145:9090 cookie 1 weight 5 check inter 2000 rise 2 fall 3
~$ systemctl restart haproxy
```

![image-20240103120308930](images\image-20240103120308930.png)

### 6.2.4: prometheus添加job

```bash
~$ cat  prometheus.yml
- job_name: "haproxy-monitoring"
    static_configs:
      - targets: ["192.168.58.146:9101"] 
~$ systemctl restart prometheus          
```

![image-20240103120641337](images\image-20240103120641337.png)

### 6.2.5: 导入grafana

367

![image-20240103120846646](images\image-20240103120846646.png)

## 6.3：监控nginx

通过prometheus监控nginx，也是通过nginx status页来监控。

```shell
需要在编译安装nginx的时候添加nginx-module-vts模块

github地址：https://github.com/vozlt/nginx-module-vts
```

### 6.3.1：编译安装nginx

```bash
~$ cd /usr/local/src/
~$ git clone https://github.com/vozlt/nginx-module-vts
~$ wget https://nginx.org/download/nginx-1.24.0.tar.gz
~$ tar xf nginx-1.24.0.tar.gz
~$ cd nginx-1.24.0
~$ ./configure --prefix=/app/nginx --with-http_v2_module --with-http_realip_module --with-http_stub_status_module --without-http_gzip_module --without-http_rewrite_module --with-file-aio --with-stream --with-stream_realip_module --add-module=/usr/local/src/nginx-module-vts
~$ make
~$ make install
```

### 6.3.2：编辑nginx配置文件

```bash
~$ vim /app/nginx/conf/nginx.conf
http {
     .....
     #gzip  on;
    vhost_traffic_status_zone;
    ...
    }
server {
     ...
     #access_log  logs/host.access.log  main;

        location / {
            root   html;
            index  index.html index.htm;
        }
        location /status {
            vhost_traffic_status_display;
            vhost_traffic_status_display_format html;
        }
      ...
}
```

### 6.3.3：启动nginx并验证web状态页

```bash
~$ /app/nginx/sbin/nginx -t
nginx: the configuration file /app/nginx/conf/nginx.conf syntax is ok
nginx: configuration file /app/nginx/conf/nginx.conf test is successful
~$ /app/nginx/sbin/nginx
```

![image-20240103143617728](images\image-20240103143617728.png)

### 6.3.4: 安装nginx exporter

```bash
~$ cd /app && wget  https://github.com/hnlq715/nginx-vts-exporter/releases/download/v0.10.8/nginx-vtx-exporter_0.10.8_linux_amd64.tar.gz
~$ tar xf nginx-vtx-exporter_0.10.8_linux_amd64.tar.gz
~$ ./nginx-vtx-exporter -nginx.scrape_uri=http://192.168.58.146/status/format/json
2024/01/03 06:51:08 Starting nginx_vts_exporter (version=, branch=, revision=)
2024/01/03 06:51:08 Build context (go=go1.20.5, user=, date=)
2024/01/03 06:51:08 Starting Server at : :9913
2024/01/03 06:51:08 Metrics endpoint: /metrics
2024/01/03 06:51:08 Metrics namespace: nginx
2024/01/03 06:51:08 Scraping information from : http://192.168.58.146/status/format/json
```

### 6.3.5: 验证nginx exporter数据

![image-20240103145257144](images\image-20240103145257144.png)

### 6.3.6: 配置prometheus

```bash
~$ vim /app/prometheus/prometheus.yaml
- job_name: "nginx monitoring"
    static_configs:
      - targets: ["192.168.58.146:9913"]
```

![image-20240103145533243](images\image-20240103145533243.png)

### 6.3.7：grafana配置

2949

![image-20240103145807390](images\image-20240103145807390.png)

## 6.4： black_exporter监控URL

https://prometheus.io/download/#blackbox_exporter

blackbox_exporter是prometheus官方提供的一个exporter，可以通过HTTP,HTTPS,DNS,TCP和ICMP对被监控节点进行监控和数据采集。

```bash
HTTP/HTTPS: URL/API可用性探测
TCP：端口监听检测
ICMP：主机存活性探测
DNS：域名解析
```

### 6.4.1：部署black exporter

```bash
~$ wget https://github.com/prometheus/blackbox_exporter/releases/download/v0.24.0/blackbox_exporter-0.24.0.linux-amd64.tar.gz
~$ tar xf blackbox_exporter-0.24.0.linux-amd64.tar.gz
~$ ln -sv blackbox_exporter-0.24.0.linux-amd64 blackbox_exporter
```

### 6.4.2：创建black exporter启动文件

```bash
~$ vim /etc/systemd/system/blackbox-exporter.service
[Unit]
Description=Blackbox Exporter
After=network.target

[Service]
Type:=simple
User=root
Group=root
ExecStart=/app/blackbox_exporter/blackbox_exporter --config.file=/app/blackbox_exporter/blackbox.yml --web.listen-address=:9115
Restart=on-failure

[Install]
WantedBy=multi-user.target

~$ systemctl daemon-reload && systemctl restart blackbox-exporter.service
```

### 6.4.3：验证web界面

![image-20240103152250886](images\image-20240103152250886.png)

### 6.4.4：blackbox exporter实现URL监控

prometheus调用blackbox exporter实现对URL/ICMP的监控。

#### 6.4.4.1：Prometheus URL监控配置

```bash
~$ vim /app/prometheus/prometheus.yml
- job_name: "Http Status"
    metrics_path: /probe
    params:
      module: [http_2xx]
    static_configs:
    - targets:
        - https://prometheus.io   # Target to probe with https.
        - https://www.paypal.cn
        - https://www.xiaomi.com
      labels:
        group: web   # 增加一个label
    relabel_configs:
      - source_labels: [__address__]
        target_label: __param_target
      - source_labels: [__param_target]
        target_label: instance
      - target_label: __address__
        replacement: 192.168.58.146:9115
```

这里针对每一个探针服务（如http_2xx）定义一个采集任务，并且直接将任务的采集目标定义为我们需要探测的站点。在采集样本数据之前通过relabel_configs对采集任务进行动态设置。

- 第1步，根据Target实例的地址，写入`__param_target`标签中。`__param_<name>`形式的标签表示，在采集任务时会在请求目标地址中添加`<name>`参数，等同于params的设置；
- 第2步，获取__param_target的值，并覆写到instance标签中；
- 第3步，覆写Target实例的`__address__`标签值为BlockBox Exporter实例的访问地址。

#### 6.4.4.2：验证prometheus

![image-20240103160218483](images\image-20240103160218483.png)

#### 6.4.4.3: blackbox exporter界面验证数据

![image-20240103160306956](images\image-20240103160306956.png)

### 6.4.5：blackbox exporter实现ICMP监控

#### 6.4.5.1：Prometheus 配置

```bash
~$ vim /app/prometheus/prometheus.yml
- job_name: "Ping Status"
    metrics_path: /probe
    params:
      module: [icmp]
    static_configs:
    - targets:
        - 192.168.58.144
        - 192.168.58.146
      labels:
        group: ping   # 增加一个label
    relabel_configs:
      - source_labels: [__address__]
        target_label: __param_target
      - source_labels: [__param_target]
        target_label: instance
      - target_label: __address__
        replacement: 192.168.58.146:9115   
```

#### 6.4.5.2：blackbox exporter界面验证数据

![image-20240103160959757](images\image-20240103160959757.png)

### 6.4.6：blackbox exporter实现端口监控

#### 6.4.6.1：端口监控配置

```bash
- job_name: "Port Status"
    metrics_path: /probe
    params:
      module: [tcp_connect]
    static_configs:
    - targets:
        - 192.168.58.144:9100
        - 192.168.58.146:9100
      labels:
        group: port   # 增加一个label
    relabel_configs:
      - source_labels: [__address__]
        target_label: __param_target
      - source_labels: [__param_target]
        target_label: instance
      - target_label: __address__
        replacement: 192.168.58.146:9115
```

#### 6.4.6.2：blackbox exporter界面验证数据

![image-20240103161912752](images\image-20240103161912752.png)

### 6.4.7：导入grafana模板

9965

![image-20240103162145617](images\image-20240103162145617.png)

# 七：Alertmanager

prometheus触发一条告警的过程：

```bash
prometheus--->触发阈值---->超出持续时间---->alertmanager---->分组|抑制|静默--->媒体类型--->邮件|钉钉|微信等。
```

![image-20240103164450668](images\image-20240103164450668.png)

```bash
分组(group)：将类似性质的告警合并为单个通知，比如网络通知，主机通知，服务通知。
静默(sliences)：是一种简单的特定时间静音的机制，例如：服务器要升级维护可以先设置这个时间段告警静默。
抑制（inhibition）：当警报发出后，停止发送由此警报引起的其他警报即合并一个故障引起的多个报警事件，可以消除冗余告警。
```

安装alertmanager:

```bash
~$ cd /app
~$ wget https://github.com/prometheus/alertmanager/releases/download/v0.26.0/alertmanager-0.26.0.linux-amd64.tar.gz
~$ tar xf alertmanager-0.26.0.linux-amd64.tar.gz
~$ ln -sv alertmanager-0.26.0.linux-amd64 alertmanager

~$ vim /etc/systemd/system/alertmanager.service
[Unit]
Description=Prometheus Alertmanager
After=network.target

[Service]
Restart=on-failure
ExecStart=/app/alertmanager/alertmanager --config.file=/app/alertmanager/alertmanager.yml

[Install]
WantedBy=multi-user.target

~$ systemctl daemon-reload && systemctl restart alertmanager
```

## 7.1：邮件通知

https://prometheus.io/docs/alerting/latest/configuration/#email_config

### 7.1.1：alertmanager配置文件解析

```bash
~$ vim /app/alertmanager/alertmanager.yml
global:
  # The smarthost and SMTP sender used for mail notifications.
  smtp_smarthost: 'localhost:25'  # 邮箱smtp地址
  smtp_from: 'alertmanager@example.org' #发件人邮箱地址
  smtp_auth_username: 'alertmanager' #发件人的用户名
  smtp_auth_password: 'password' #发件人的登陆密码，有时候是授权码
  smtp_require_tls: #是否需要tls协议。默认true
  
  wechat_api_url:   #企业微信API地址
  wechat_api_secret: #企业微信API secret
  wechat_api_corp_id:  #企业微信corp id信息。
  
  resolve_timeout: 60s #当一个告警在alertmanager持续多长时间未接收新告警标记告警状态reslove
  
  
route:
   group_by: [alertname] #通过alertname的值对告警分类。-alert：物理节点cpu使用率
   group_wait：10s  # 一组告警第一次发送之前等待的延迟时间，即产生告警后延迟10s将组内新产生的消息一起合并发送（一般设置为0秒~几分钟）
   group_interval: 2m #一组已发送过的初始通知的告警接收到新告警后，下次发送通知前等待的时间
   repeat_interval: 5m # 一条成功发送的告警，在最终发送前等待的时间
#简单示例
  
   #group_wait: 10s #第一次产生告警，等待10s，组内有告警一起发出，没有其他告警单独发出
   #group_interval: 2m # 第二次产生告警，先等待2分钟，2分钟后还没恢复就进入repeat_interval
   #repeat_interval: 5m #在最终发送消息前先等待5分钟，5分钟后，还没恢复就发送第二次告警
   receiver: default-receiver #其他的告警发送给default-receiver
   routes: # 将critical的报警发送给myalertmanager
   - receiver: myalertmanager
     group_wait: 10s
     match_re:
         severity: critical
         
receivers: # 定义多接收者
- name: 'default-receiver'
      email_configs:
      - to: <mail to address>
        send_resolved: true   # 通知已恢复的告警
 - name: myalertmanager
       webhook_configs:
       - url: '<address>'
         send_resolved: true   # 通知已恢复的告警   
```

### 7.1.2：配置并启动alertmanager

```bash
global:
  smtp_smarthost: 'smtp.qq.com:465'  
  smtp_from: '353938339@qq.com' 
  smtp_auth_username: '353938339@qq.com'
  smtp_auth_password: 'xrvcmvqfsgqicadh'
  smtp_hello: '@qq.com'
  smtp_require_tls: false
  
  
route:
   group_by: [alertname] 
   group_wait：10s  
   group_interval: 10s
   repeat_interval: 2m 
   receiver: 'email'
   
receivers:
- name: 'email'
  email_configs:
   - to: '353938339@qq.com'
     send_resolved: true    
     
     
inhibit_rules:
  - source_matchers: [severity="critical"]
    target_matchers: [severity="warning"]
    equal: ['alertname', 'dev', 'instance'] 
    
# 源匹配级别，当匹配成功发出通知，但是其他 'alertname', 'dev', 'instance'产生的waring级别的告警将被抑制 
```

```bash
# systemctl restart alertmanager
```

![image-20240103193402541](images\image-20240103193402541.png)

### 7.1.3：配置prometheus报警规则

```bash
root@pro:/app/prometheus# pwd
/app/prometheus
root@pro:/app/prometheus# cat rules/pod_rules.yaml 
groups:
  - name: alertmanager_pod.rules
    rules:
    - alert: Pod_all_cpu_usage
      expr: (sum by(name)(rate(container_cpu_usage_seconds_total{image!=""}[5m]))*100) > 10
      for: 2m
      labels:
        severity: critical
        service: pods
      annotations:
        description: 容器 {{ $labels.name }} CPU 资源利用率大于 10% , (current value is {{ $value }})
        summary: Dev CPU 负载告警

    - alert: Pod_all_memory_usage  
      #expr: sort_desc(avg by(name)(irate(container_memory_usage_bytes{name!=""}[5m]))*100) > 10  #内存大于10%
      expr: sort_desc(avg by(name)(irate(node_memory_MemFree_bytes {name!=""}[5m]))) > 2147483648   #内存大于2G
      for: 2m
      labels:
        severity: critical
      annotations:
        description: 容器 {{ $labels.name }} Memory 资源利用率大于 2G , (current value is {{ $value }})
        summary: Dev Memory 负载告警

    - alert: Pod_all_network_receive_usage
      expr: sum by (name)(irate(container_network_receive_bytes_total{container_name="POD"}[1m])) > 50*1024*1024
      for: 2m
      labels:
        severity: critical
      annotations:
        description: 容器 {{ $labels.name }} network_receive 资源利用率大于 50M , (current value is {{ $value }})

    - alert: node内存可用大小 
      expr: node_memory_MemFree_bytes > 10*1024*1024 #故意写错的
      #expr: node_memory_MemFree_bytes > 1 #故意写错的
      for: 15s
      labels:
        severity: critical
      annotations:
        description: node可用内存小于4G

  - name: alertmanager_node.rules
    rules:
    - alert: 磁盘容量
      expr: 100-(node_filesystem_free_bytes{fstype=~"ext4|xfs"}/node_filesystem_size_bytes {fstype=~"ext4|xfs"}*100) > 80  #磁盘容量利用率大于80%
      for: 2s
      labels:
        severity: critical
      annotations:
        summary: "{{$labels.mountpoint}} 磁盘分区使用率过高！"
        description: "{{$labels.mountpoint }} 磁盘分区使用大于80%(目前使用:{{$value}}%)"

    - alert: 磁盘容量
      expr: 100-(node_filesystem_free_bytes{fstype=~"ext4|xfs"}/node_filesystem_size_bytes {fstype=~"ext4|xfs"}*100) > 60 #磁盘容量利用率大于60%
      for: 2s
      labels:
        severity: warning
      annotations:
        summary: "{{$labels.mountpoint}} 磁盘分区使用率过高！"
        description: "{{$labels.mountpoint }} 磁盘分区使用大于80%(目前使用:{{$value}}%)"
```

### 7.1.4：prometheus加载报警规则

```bash
~$ cat prometheus.yml
global:
  scrape_interval: 15s 
  evaluation_interval: 15s 

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets:
            - 192.168.58.145:9093  # alertmanager地址
rule_files:
  - "rules/*.yaml"  # 指定规则文件
  # - "second_rules.yml"

```

### 7.1.5：规则验证

```bash
root@pro:/app/prometheus# ./promtool check rules rules/pod_rules.yaml 
Checking rules/pod_rules.yaml
  SUCCESS: 6 rules found

```

### 7.1.6: 重启prometheus

```bash
~$ systemctl restart prometheus
```

### 7.1.7: 查看当前告警

在alertmanager服务器，使用amtool查看当前报警事件。

```bash
root@pro:/app/alertmanager# ./amtool alert --alertmanager.url=http://192.168.58.145:9093
Alertname   Starts At                Summary  State   
node内存可用大小  2024-01-03 11:44:59 UTC           active  
node内存可用大小  2024-01-03 11:44:59 UTC           active  
node内存可用大小  2024-01-03 11:44:59 UTC           active  
node内存可用大小  2024-01-03 11:44:59 UTC           active  
node内存可用大小  2024-01-03 11:44:59 UTC           active  
node内存可用大小  2024-01-03 11:44:59 UTC           active  
node内存可用大小  2024-01-03 11:44:59 UTC           active  
node内存可用大小  2024-01-03 11:44:59 UTC           active 
```

### 7.1.8：Prometheus的事件状态

```yaml
prometheus状态：
  inactive：没有异常
  pending：已触发阈值，但未满足告警持续时间（即rule的for事件）
  firing：已触发告警并发送给alertmanager
```

![image-20240103195027175](images\image-20240103195027175.png)

### 7.1.9: 邮箱验证

![image-20240103195148074](images\image-20240103195148074.png)

## 7.2：钉钉通知

### 7.2.1：钉钉群组创建机器人-关键字认证

![image-20240103201605431](images\image-20240103201605431.png)

### 7.2.2：测试发送消息

```bash
~$curl 'https://oapi.dingtalk.com/robot/send?access_token=9e481a9918fb0fe6bd86911f4dfc94bbda5b21d80bb63371c83f79dd1636d484' \
 -H 'Content-Type: application/json' \
 -d '{"msgtype": "text","text": {"content":"我就是我, 是不一样的烟火alertname"}}'
{"errcode":0,"errmsg":"ok"}
```

![image-20240103202320448](images\image-20240103202320448.png)

### 7.2.3: 部署webhook-dingtalk

```bash
root@pro:/app# wget https://github.com/timonwong/prometheus-webhook-dingtalk/releases/download/v2.1.0/prometheus-webhook-dingtalk-2.1.0.linux-amd64.tar.gz
root@pro:/app# tar xf prometheus-webhook-dingtalk-2.1.0.linux-amd64.tar.gz
root@pro:/app/prometheus-webhook-dingtalk-2.1.0.linux-amd64# cat config.yml 
targets:
  webhook1:
    url: https://oapi.dingtalk.com/robot/send?access_token=9e481a9918fb0fe6bd86911f4dfc94bbda5b21d80bb63371c83f79dd1636d484
root@pro:/app/prometheus-webhook-dingtalk-2.1.0.linux-amd64# ./prometheus-webhook-dingtalk --web.listen-address=:8060
ts=2024-01-03T12:36:57.763Z caller=main.go:59 level=info msg="Starting prometheus-webhook-dingtalk" version="(version=2.1.0, branch=HEAD, revision=8580d1395f59490682fb2798136266bdb3005ab4)"
ts=2024-01-03T12:36:57.763Z caller=main.go:60 level=info msg="Build context" (gogo1.18.1,userroot@177bd003ba4d,date20220421-08:19:05)=(MISSING)
ts=2024-01-03T12:36:57.764Z caller=coordinator.go:83 level=info component=configuration file=config.yml msg="Loading configuration file"
ts=2024-01-03T12:36:57.764Z caller=coordinator.go:91 level=info component=configuration file=config.yml msg="Completed loading of configuration file"
ts=2024-01-03T12:36:57.764Z caller=main.go:97 level=info component=configuration msg="Loading templates" templates=
ts=2024-01-03T12:36:57.765Z caller=main.go:113 component=configuration msg="Webhook urls for prometheus alertmanager" urls=http://localhost:8060/dingtalk/webhook1/send
ts=2024-01-03T12:36:57.765Z caller=web.go:208 level=info component=web msg="Start listening for connections" address=:8060
```

### 7.2.4：部署alertmanager

```bash
~$ cat alertmanager.yml
global:
  smtp_smarthost: 'smtp.qq.com:465'  
  smtp_from: '353938339@qq.com' 
  smtp_auth_username: '353938339@qq.com'
  smtp_auth_password: 'xrvcmvqfsgqicadh'
  smtp_hello: '@qq.com'
  smtp_require_tls: false
  
  
route:
   group_by: [alertname] 
   group_wait: 10s  
   group_interval: 10s
   repeat_interval: 2m 
   receiver: 'dingding'
   
receivers:
- name: 'email'
  email_configs:
   - to: '353938339@qq.com'
     send_resolved: true    
- name: 'dingding'
  webhook_configs:
  - url: 'http://192.168.58.145:8060/dingtalk/webhook1/send'  
     
inhibit_rules:
  - source_matchers: [severity="critical"]
    target_matchers: [severity="warning"]
    equal: ['alertname', 'dev', 'instance'] 
```

### 7.2.5: dingtalk验证日志

![image-20240103204730043](images\image-20240103204730043.png)

### 7.2.6：钉钉验证消息

![image-20240103204807209](images\image-20240103204807209.png)

## 7.3：企业微信通知

https://work.weixin.qq.com/

打开企业微信官网注册账号，使用自己手机号注册。

### 7.3.1：注册企业微信账号

![image-20240104090926328](images\image-20240104090926328.png)

### 7.3.2：创建应用

![image-20240104091133402](images\image-20240104091133402.png)

### 7.3.3：填写应用信息

![image-20240104091308052](images\image-20240104091308052.png)

### 7.3.4：注册完成

AgentID和Secret会在发送微信报警信息的时候调用。

![image-20240104092437390](images\image-20240104092437390.png)

### 7.3.5：创建微信账号

用户账号名称必须唯一，在发送微信报警信息的时候调用。

![image-20240104092908970](images\image-20240104092908970.png)

### 7.3.6：验证通讯录

![image-20240104093344250](images\image-20240104093344250.png)

### 7.3.7：查看企业信息

企业ID在发送微信报警信息的时候会被调用。

![image-20240104093501325](images\image-20240104093501325.png)

### 7.3.8：测试发送信息

#### 7.3.8.1：测试发送

![image-20240104093750442](images\image-20240104093750442.png)

#### 7.3.8.2：企业微信验证信息

![image-20240104093854434](images\image-20240104093854434.png)

### 7.3.9：认证信息收集

```bash
AgentId: 1000002
Secret: OZECFCwjyZJwDrAmUOlQoiG-kiqY6t1J9pPHlfot1Bs
企业ID：wwd56ca1b1c186dc87
```

### 7.3.10：prometheus配置

配置与前面配置一样。

```bash
~$ cat prometheus.yml
global:
  scrape_interval: 15s 
  evaluation_interval: 15s 

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets:
            - 192.168.58.145:9093  # alertmanager地址
rule_files:
  - "rules/*.yaml"  # 指定规则文件
  # - "second_rules.yml"
```

### 7.3.11：alertmanager配置

```bash
~$ vim /app/alertmanager/alertmanager.yml
global:
  smtp_smarthost: 'smtp.qq.com:465'  
  smtp_from: '353938339@qq.com' 
  smtp_auth_username: '353938339@qq.com'
  smtp_auth_password: 'xrvcmvqfsgqicadh'
  smtp_hello: '@qq.com'
  smtp_require_tls: false
  
  
route:
   group_by: [alertname] 
   group_wait: 10s  
   group_interval: 10s
   repeat_interval: 2m 
   # receiver: 'dingding'
   receiver: 'wechat'
   
receivers:
- name: 'email'
  email_configs:
   - to: '353938339@qq.com'
     send_resolved: true    
- name: 'dingding'
  webhook_configs:
  - url: 'http://192.168.58.145:8060/dingtalk/webhook1/send'  
- name: 'wechat'
  wechat_configs:
  - corp_id: wwd56ca1b1c186dc87
    to_user: '@all'
    agent_id: 1000002
    api_secret: OZECFCwjyZJwDrAmUOlQoiG-kiqY6t1J9pPHlfot1Bs
    send_resolved: true
     
inhibit_rules:
  - source_matchers: [severity="critical"]
    target_matchers: [severity="warning"]
    equal: ['alertname', 'dev', 'instance'] 
```

### 7.3.12：企业微信验证消息

目前自建的企业微信应用，都要配置可信IP，但是本地开发测试，无法配置，企业微信官方在处理这个bug.

```bash
alertmanager报错：
ts=2024-01-04T02:39:04.861Z caller=dispatch.go:352 level=error component=dispatcher msg="Notify for alerts failed" num_alerts=1 err="wechat/wechat[0]: notify retry canceled due to unrecoverable error after 1 attempts: not allow to access from your ip, hint: [1704335944429391615909812], from ip: 120.244.232.190, more info at https://open.work.weixin.qq.com/devtool/query?e=60020"
```

社区讨论：https://github.com/prometheus/alertmanager/issues/3036

​                    https://developer.work.weixin.qq.com/community/search?keyword=60020&type=question&from=community

### 7.3.13：消息发送给指定组

#### 7.3.13.1：获取部门ID

![image-20240104105335892](images\image-20240104105335892.png)

#### 7.3.13.2：alertmanager配置

```bash
~$ cat alertmanager.yml 
global:
  smtp_smarthost: 'smtp.qq.com:465'  
  smtp_from: '353938339@qq.com' 
  smtp_auth_username: '353938339@qq.com'
  smtp_auth_password: 'xrvcmvqfsgqicadh'
  smtp_hello: '@qq.com'
  smtp_require_tls: false
  
  
route:
   group_by: [alertname] 
   group_wait: 10s  
   group_interval: 10s
   repeat_interval: 2m 
   # receiver: 'dingding'
   receiver: 'wechat'
   
receivers:
- name: 'email'
  email_configs:
   - to: '353938339@qq.com'
     send_resolved: true    
- name: 'dingding'
  webhook_configs:
  - url: 'http://192.168.58.145:8060/dingtalk/webhook1/send'  
- name: 'wechat'
  wechat_configs:
  - corp_id: wwd56ca1b1c186dc87
    # to_user: '@all'
    to_party: 2  # 指定部门ID
    agent_id: 1000002
    api_secret: OZECFCwjyZJwDrAmUOlQoiG-kiqY6t1J9pPHlfot1Bs
    send_resolved: true
     
inhibit_rules:
  - source_matchers: [severity="critical"]
    target_matchers: [severity="warning"]
    equal: ['alertname', 'dev', 'instance']
```

## 7.4：消息分类发送

根据消息中的属性信息设置规则，将消息分类发送，如以下为将severity级别为critical的通知信息发送给dingding，其他的则发送给邮件。

### 7.4.1：alertmanager配置

```bash
~$ cat alertmanager.yml
global:
  smtp_smarthost: 'smtp.qq.com:465'  
  smtp_from: '353938339@qq.com' 
  smtp_auth_username: '353938339@qq.com'
  smtp_auth_password: 'xrvcmvqfsgqicadh'
  smtp_hello: '@qq.com'
  smtp_require_tls: false
  
  
route:
   group_by: [alertname] 
   group_wait: 10s  
   group_interval: 10s
   repeat_interval: 2m 
   receiver: 'email'  # 默认发给邮箱
   # receiver: 'wechat'
   # 添加消息路由
   routes:
   - receiver: 'dingding'  # critical级别的日志发送给dingding
     group_wait: 10s
     match_re:
       severity: critical
   
receivers:
- name: 'email'
  email_configs:
   - to: '353938339@qq.com'
     send_resolved: true    
- name: 'dingding'
  webhook_configs:
  - url: 'http://192.168.58.145:8060/dingtalk/webhook1/send'  
- name: 'wechat'
  wechat_configs:
  - corp_id: wwd56ca1b1c186dc87
    # to_user: '@all'
    to_party: 2
    agent_id: 1000002
    api_secret: OZECFCwjyZJwDrAmUOlQoiG-kiqY6t1J9pPHlfot1Bs
    send_resolved: true
     
inhibit_rules:
  - source_matchers: [severity="critical"]
    target_matchers: [severity="warning"]
    equal: ['alertname', 'dev', 'instance'] 
```

### 7.4.2：验证消息发送

![image-20240104111821082](images\image-20240104111821082.png)

## 7.5：自定义消息模板

默认的消息模板中消息内容需要调整，而且消息是连在一起的。

### 7.5.1：定义模板

#### 7.5.1.1：定义微信模板

```bash
~$ cat /app/alertmanager/templates/wechat_template.tmpl
{{ define "wechat.default.message" }}
{{- if gt (len .Alerts.Firing) 0 -}}
{{- range $index, $alert := .Alerts -}}
{{- if eq $index 0 }}
========= 监控报警 =========
告警状态：{{   .Status }}
告警级别：{{ .Labels.severity }}
告警类型：{{ $alert.Labels.alertname }}
故障主机: {{ $alert.Labels.instance }}
告警主题: {{ $alert.Annotations.summary }}
告警详情: {{ $alert.Annotations.message }}{{ $alert.Annotations.description}};
触发阈值：{{ .Annotations.value }}
故障时间: {{ ($alert.StartsAt.Add 28800e9).Format "2006-01-02 15:04:05" }}
========= = end =  =========
{{- end }}
{{- end }}
{{- end }}

{{- if gt (len .Alerts.Resolved) 0 -}}
{{- range $index, $alert := .Alerts -}}
{{- if eq $index 0 }}
========= 异常恢复 =========
告警类型：{{ .Labels.alertname }}
告警状态：{{   .Status }}
告警主题: {{ $alert.Annotations.summary }}
告警详情: {{ $alert.Annotations.message }}{{ $alert.Annotations.description}};
故障时间: {{ ($alert.StartsAt.Add 28800e9).Format "2006-01-02 15:04:05" }}
恢复时间: {{ ($alert.EndsAt.Add 28800e9).Format "2006-01-02 15:04:05" }}
{{- if gt (len $alert.Labels.instance) 0 }}
实例信息: {{ $alert.Labels.instance }}
{{- end }}
========= = end =  =========
{{- end }}
{{- end }}
{{- end }}
{{- end }}
```

#### 7.5.1.2:  定义邮件模板

```bash
~$ cat   /app/alertmanager/templates/email_template.tmpl
{{ define "email.to.html" }}
{{- if gt (len .Alerts.Firing) 0 -}}
{{ range .Alerts }}
=========start==========<br>
告警程序: prometheus_alert <br>
告警级别: {{ .Labels.severity }} <br>
告警类型: {{ .Labels.alertname }} <br>
告警主机: {{ .Labels.instance }} <br>
告警主题: {{ .Annotations.summary }}  <br>
告警详情: {{ .Annotations.description }} <br>
触发时间: {{ .StartsAt.Format "2006-01-02 15:04:05" }} <br>
=========end==========<br>
{{ end }}{{ end -}}
 
{{- if gt (len .Alerts.Resolved) 0 -}}
{{ range .Alerts }}
=========start==========<br>
告警程序: prometheus_alert <br>
告警级别: {{ .Labels.severity }} <br>
告警类型: {{ .Labels.alertname }} <br>
告警主机: {{ .Labels.instance }} <br>
告警主题: {{ .Annotations.summary }} <br>
告警详情: {{ .Annotations.description }} <br>
触发时间: {{ .StartsAt.Format "2006-01-02 15:04:05" }} <br>
恢复时间: {{ .EndsAt.Format "2006-01-02 15:04:05" }} <br>
=========end==========<br>
{{ end }}{{ end -}}
{{- end }}
```

#### 7.5.1.3：定义钉钉模板

钉钉的模板是配置在`prometheus-webhook-dingtalk`的`config.yml`中。

```bash
# 自定义钉钉模板
~$ cat  /app/alertmanager/templates/dingtalk_template.tmpl
{{ define "email.to.message" }}

{{- if gt (len .Alerts.Firing) 0 -}}
{{- range $index, $alert := .Alerts -}}

=========  **监控告警** =========  

**告警程序:**     Alertmanager   
**告警类型:**    {{ $alert.Labels.alertname }}   
**告警级别:**    {{ $alert.Labels.severity }} 级   
**告警状态:**    {{ .Status }}   
**故障主机:**    {{ $alert.Labels.instance }} {{ $alert.Labels.device }}   
**告警主题:**    {{ .Annotations.summary }}   
**告警详情:**    {{ $alert.Annotations.message }}{{ $alert.Annotations.description}}   
**主机标签:**    {{ range .Labels.SortedPairs  }}  </br> [{{ .Name }}: {{ .Value | markdown | html }} ] 
{{- end }} </br>

**故障时间:**    {{ ($alert.StartsAt.Add 28800e9).Format "2006-01-02 15:04:05" }}  
========= = end =  =========  
{{- end }}
{{- end }}

{{- if gt (len .Alerts.Resolved) 0 -}}
{{- range $index, $alert := .Alerts -}}

========= 告警恢复 =========  
**告警程序:**     Alertmanager   
**告警主题:**    {{ $alert.Annotations.summary }}  
**告警主机:**    {{ .Labels.instance }}   
**告警类型:**    {{ .Labels.alertname }}  
**告警级别:**    {{ $alert.Labels.severity }} 级   
**告警状态:**    {{   .Status }}  
**告警详情:**    {{ $alert.Annotations.message }}{{ $alert.Annotations.description}}  
**故障时间:**    {{ ($alert.StartsAt.Add 28800e9).Format "2006-01-02 15:04:05" }}  
**恢复时间:**    {{ ($alert.EndsAt.Add 28800e9).Format "2006-01-02 15:04:05" }}  

========= = **end** =  =========
{{- end }}
{{- end }}
{{- end }}
```

##### 7.5.1.3.1：配置config.yaml

```bash
# 1、引用自定义模板
~$ cat config.yml
## Request timeout
# timeout: 5s

## Uncomment following line in order to write template from scratch (be careful!)
#no_builtin_template: true

## Customizable templates path
templates:
  - /app/alertmanager/templates/dingtalk_template.tmpl

## You can also override default template using `default_message`
## The following example to use the 'legacy' template from v0.3.0
#default_message:
#  title: '{{ template "legacy.title" . }}'
#  text: '{{ template "dingtalk.default.message" . }}'

## Targets, previously was known as "profiles"
targets:
  webhook1:
    url: https://oapi.dingtalk.com/robot/send?access_token=9e481a9918fb0fe6bd86911f4dfc94bbda5b21d80bb63371c83f79dd1636d484
    message:
      text: '{{ template "email.to.message" . }}'
```

```bash
# 2、 使用默认模板
~$ cat config.yml
templates:
  - contrib/templates/legacy/template.tmpl

## You can also override default template using `default_message`
## The following example to use the 'legacy' template from v0.3.0
default_message:
  title: '{{ template "legacy.title" . }}'
  text: '{{ template "legacy.content" . }}'

## Targets, previously was known as "profiles"
targets:
  webhook1:
    url: https://oapi.dingtalk.com/robot/send?access_token=9e481a9918fb0fe6bd86911f4dfc94bbda5b21d80bb63371c83f79dd1636d484
```

### 7.5.2: alertmanager引用模板

```bash
~$ cat alertmanger.yml
global:
  smtp_smarthost: 'smtp.qq.com:465'  
  smtp_from: '353938339@qq.com' 
  smtp_auth_username: '353938339@qq.com'
  smtp_auth_password: 'xrvcmvqfsgqicadh'
  smtp_hello: '@qq.com'
  smtp_require_tls: false
  
  
route:
   group_by: [alertname] 
   group_wait: 10s  
   group_interval: 10s
   repeat_interval: 2m 
   receiver: 'email'  # 默认发给邮箱
   # receiver: 'wechat'
   # 添加消息路由
   routes:
   - receiver: 'dingding'  # critical级别的日志发送给dingding
     group_wait: 10s
     match_re:
       severity: critical

templates:
  - '/app/alertmanager/templates/email_template.tmpl'
  - '/app/alertmanager/templates/wechat_template.tmpl'
   
receivers:
- name: 'email'
  email_configs:
   - to: '353938339@qq.com'
     html: '{{ template "email.to.html" . }}' # 邮件引用模板
     send_resolved: true    
- name: 'dingding'  # dignding的模板在dingtalk的config.yml配置
  webhook_configs:
  - url: 'http://192.168.58.145:8060/dingtalk/webhook1/send'  
- name: 'wechat'
  wechat_configs:
  - corp_id: wwd56ca1b1c186dc87
    # to_user: '@all'
    to_party: 2
    agent_id: 1000002
    api_secret: OZECFCwjyZJwDrAmUOlQoiG-kiqY6t1J9pPHlfot1Bs
    send_resolved: true
    message: '{{ template "wechat.default.message" . }}'  # 微信引用自定义模板
     
inhibit_rules:
  - source_matchers: [severity="critical"]
    target_matchers: [severity="warning"]
    equal: ['alertname', 'dev', 'instance'] 
```

### 7.5.3: 验证消息内容

#### 7.5.3.1：邮件自定义模板验证

![image-20240104154153356](images\image-20240104154153356.png)

#### 7.5.3.2： 钉钉自定义模板验证

![image-20240104154352884](images\image-20240104154352884.png)

## 7.6：告警抑制与静默

### 7.6.1：告警抑制

基于告警规则，超过80%就不再发60%的告警，即由60%的表达式触发的告警被抑制了。

```bash
groups:
  - name: alertmanager_node.rules
    rules:
    - alert: 磁盘容量
      expr: 100-(node_filesystem_free_bytes{fstype=~"ext4|xfs"}/node_filesystem_size_bytes {fstype=~"ext4|xfs"}*100) > 80  #磁盘容量利用率大于80%
      for: 2s
      labels:
        severity: critical
      annotations:
        summary: "{{$labels.mountpoint}} 磁盘分区使用率过高！"
        description: "{{$labels.mountpoint }} 磁盘分区使用大于80%(目前使用:{{$value}}%)"

    - alert: 磁盘容量
      expr: 100-(node_filesystem_free_bytes{fstype=~"ext4|xfs"}/node_filesystem_size_bytes {fstype=~"ext4|xfs"}*100) > 60 #磁盘容量利用率大于60%
      for: 2s
      labels:
        severity: warning
      annotations:
        summary: "{{$labels.mountpoint}} 磁盘分区使用率过高！"
        description: "{{$labels.mountpoint }} 磁盘分区使用大于80%(目前使用:{{$value}}%)"
```

### 7.6.2:  手动静默

先找到要静默的告警事件，然后手动静默指定的事件：

![image-20240104161453025](images\image-20240104161453025.png)

点击slience，填写信息并创建：

![image-20240104161541490](images\image-20240104161541490.png)

验证告警是否被静默：

![image-20240104161639449](images\image-20240104161639449.png)

## 7.7：alertmanager高可用

https://yunlzheng.gitbook.io/prometheus-book/part-ii-prometheus-jin-jie/readmd/alertmanager-high-availability

```bash
Alertmanager 引入了Gossip机制。Gossip机制为多个Alertmanager之间提供了信息传递机制。确保即使在多个Alertmanger分别接收到相同告警信息的情况下，并且只有一个告警通知被发送给receiver。

集群环境搭建：
为了能够让Alertmanager节点之间进行通讯，需要在Alertmanager启动时设置相应的参数。其中主要参数包括：

-cluster.listen-address string: 当前实例集群服务监听地址
--cluster.peer value: 初始化时关联的其它实例的集群服务地址
```

![image-20240104163301836](images\image-20240104163301836.png)

### 7.7.1：高可用集群搭建

定义Alertmanager实例a1，其中Alertmanager的服务运行在9093端口，集群服务地址运行在8001端口。

```bash
~$ alertmanager  --web.listen-address=":9093" --cluster.listen-address="127.0.0.1:8001" --config.file=/etc/prometheus/alertmanager.yml  --storage.path=/data/alertmanager/
```

定义Alertmanager实例a2，其中主服务运行在9094端口，集群服务运行在8002端口。为了将a1，a2组成集群。 a2启动时需要定义--cluster.peer参数并且指向a1实例的集群服务地址:8001。

```bash
alertmanager  --web.listen-address=":9094" --cluster.listen-address="127.0.0.1:8002" --cluster.peer=127.0.0.1:8001 --config.file=/etc/prometheus/alertmanager.yml  --storage.path=/data/alertmanager2/
```

定义Alertmanager实例a3，其中主服务运行在9095端口，集群服务运行在8003端口。为了将a1，a2, a3组成集群。 a3启动时需要定义--cluster.peer参数并且指向a1实例的集群服务地址:8001。

```bash
alertmanager  --web.listen-address=":9095" --cluster.listen-address="127.0.0.1:8003" --cluster.peer=127.0.0.1:8001 --config.file=/etc/prometheus/alertmanager-ha.yml  --storage.path=/data/alertmanager2/ 
```

## 7.8: PrometheusAlert

```bash
PrometheusAlert是开源的运维告警中心消息转发系统，支持主流的监控系统Prometheus、Zabbix，日志系统Graylog2，Graylog3、数据可视化系统Grafana、SonarQube。阿里云-云监控，以及所有支持WebHook接口的系统发出的预警消息，支持将收到的这些消息发送到钉钉，微信，email，飞书，腾讯短信，腾讯电话，阿里云短信，阿里云电话，华为短信，百度云短信，容联云电话，七陌短信，七陌语音，TeleGram，百度Hi(如流)等。
```

https://github.com/feiyu563/PrometheusAlert

# 八：Prometheus联邦

Prometheus Server 环境：

```bash
192.168.58.145 #主节点

192.168.58.147 #联邦节点1
192.168.58.148  #联邦节点2

192.168.58.146 # node1，联邦节点1的目标采集服务器
192.168.58.144 # node2，联邦节点2的目标采集服务器
```

## 8.1：部署prometheus server

Prometheus 主server和prometheus联邦server分别部署prometheus。

```bash
# cd /app
# wget https://mirror.ghproxy.com/https://github.com/prometheus/prometheus/releases/download/v2.48.1/prometheus-2.48.1.linux-amd64.tar.gz
# tar xf prometheus-2.48.1.linux-amd64.tar.gz
# ln -sv prometheus-2.48.1.linux-amd64 prometheus
# cd /app/prometheus
# ls -ltr
total 238524
-rwxr-xr-x 1 1001 127 125066649 Dec  8 23:35 prometheus #prometheus服务可执行文件
-rwxr-xr-x 1 1001 127 119151581 Dec  8 23:36 promtool #测试工具，用于检测prometheus配置文件，检测metrics数据等
-rw-r--r-- 1 1001 127       934 Dec  9 00:03 prometheus.yml # prometheus配置文件
-rw-r--r-- 1 1001 127      3773 Dec  9 00:03 NOTICE
-rw-r--r-- 1 1001 127     11357 Dec  9 00:03 LICENSE
drwxr-xr-x 2 1001 127      4096 Dec  9 00:03 consoles
drwxr-xr-x 2 1001 127      4096 Dec  9 00:03 console_libraries


# ./promtool check config prometheus.yml
Checking prometheus.yml
 SUCCESS: prometheus.yml is valid prometheus config file syntax
 
# vim /etc/systemd/system/prometheus.service
[Unit]
Description=Prometheus Server
Documentation=https://prometheus.io/docs/introduction/overview/
After=network.target

[Service]
Restart=on-failure
WorkingDirectory=/app/prometheus/
ExecStart=/app/prometheus/prometheus --config.file=/app/prometheus/prometheus.yml

[Install]
WantedBy=multi-user.target

# systemctl daemon-reload && systemctl restart prometheus && systemctl enable prometheus
```

## 8.2：部署node_exporter

Node节点分别部署node_exporter(exporter)。

```bash
# cd /app
# wget https://github.com/prometheus/node_exporter/releases/download/v1.7.0/node_exporter-1.7.0.linux-amd64.tar.gz
# tar xf node_exporter-1.7.0.linux-amd64.tar.gz
# ln -sv node_exporter-1.7.0.linux-amd64 node_exporter

# vim /etc/systemd/system/node-exporter.service
[Unit]
Description=Prometheus Node Exporter
After=network.target

[Service]
ExecStart=/app/node_exporter/node_exporter

[Install]
WantedBy=multi-user.target

# systemctl daemon-reload && systemctl restart node-exporter && systemctl enable node-exporter
```

## 8.3：配置联邦server 监控 node_exporter

分别在联邦节点1监控node1，在联邦节点2监控node2。

```bash
Prometheus 联邦节点1：
~$ vim /app/prometheus/prometheus.yml
- job_name: "prometheus-node1"
    static_configs:
      - targets: ["192.168.58.146:9100"]
~$ systemctl restart prometheus           
```

验证数据：

![image-20240105112232172](images\image-20240105112232172.png)

```bash
prometheus 联邦节点2：
~$ vim /app/prometheus/prometheus.yml

- job_name: "prometheus-node2"
  static_configs:
    - targets: ["192.168.58.144:9100"]
~$ systemctl restart prometheus     
```

验证数据：

![image-20240105112523909](images\image-20240105112523909.png)

## 8.4：prometheus server采集联邦server

```bash
~$ vim /app/prometheus/prometheus.yml
- job_name: 'federate'
    scrape_interval: 15s

    honor_labels: true
    metrics_path: '/federate'

    params:
      'match[]':
        - '{job="prometheus"}'
        - '{__name__=~"job:.*"}'
        - '{__name__=~"node.*"}'

    static_configs:
      - targets:
        - '192.168.58.147:9090'  # 联邦节点1
        - '192.168.58.148:9090' # 联邦节点2
```

## 8.5：验证prometheus server

### 8.5.1: 验证数据收集状态

![image-20240105113219204](images\image-20240105113219204.png)

### 8.5.2：验证指标数据

![image-20240105113304465](images\image-20240105113304465.png)

# 九：prometheus存储系统

Prometheus有着非常高效的时间序列数据存储方法，每个采样数据仅仅占用3.5byte左右空间，上百万条时间序列，30秒间隔，保留60天，大概200多G空间（引用官方PPT）。

## 9.1：prometheus本地存储简介

![image-20240105113901173](images\image-20240105113901173.png)

```bash
默认情况下，prometheus将采集到的数据存储到本地的TSDB数据库，路径默认为prometheus安装目录的data目录，数据写入过程为先把数据写入wal日志并放在内存里面，然后2小时后将内存数据保存至一个block块，同时再把新采集的数据写入内存并在2小时后在保存一个新的block块，以此类推。
```

![image-20240105114912641](images\image-20240105114912641.png)

### 9.1.1：block简介

每个block为一个data目录中以01开头的存储目录，如下：

```bash
root@pro:/app/prometheus# ls -l /app/prometheus/data/
total 56
drwxr-xr-x 3 root root  4096 Dec 27 12:28 01HJNKYNY5TE0E1D1WVWA0R670  #block
drwxr-xr-x 3 root root  4096 Jan  3 05:58 01HK6YDC4N9C98FTMWVETH75R2  #block
drwxr-xr-x 3 root root  4096 Jan  4 06:44 01HK9KE4BK3WGZ4CXV3Y89XQFF  #block
drwxr-xr-x 3 root root  4096 Jan  4 09:00 01HK9V777PDJF7J2KXPZD2E7F3  #block
drwxr-xr-x 3 root root  4096 Jan  4 11:00 01HKA22VF3TKNQ5VGPYRB5S6D5  #block
drwxr-xr-x 3 root root  4096 Jan  4 11:00 01HKA22VKT96JR5C3S3VK1MZQA  #block
drwxr-xr-x 3 root root  4096 Jan  5 01:44 01HKBMPY9GXFCXM9NCGJQX1NM6  #block
```

![image-20240105115300708](images\image-20240105115300708.png)

### 9.1.2：block特性

```bash
block会压缩、合并历史数据块，以及删除过期的块，随着压缩合并，block数量会减少，在压缩过程中会发生三件事：定期执行压缩，合并小的block到大的block，清理过期的块。
```

每个块有4部分组成：

```bash
root@pro:~# tree /app/prometheus/data/01HJNKYNY5TE0E1D1WVWA0R670
/app/prometheus/data/01HJNKYNY5TE0E1D1WVWA0R670
├── chunks
│   └── 000001  #数据目录，每个大小为512MB,超过会被切分多个
├── index       # 索引文件，记录存储的数据索引信息，通过文件内的几个表来查询时序数据
├── meta.json   #block元数据信息，包含了样本数，采集数据的起始时间，压缩历史
└── tombstones  # 逻辑数据，主要记载删除记录和标记要删除的内容，删除标记，可在查询块时排除样本

```

### 9.1.3：本地存储配置参数

```bash
--config.file="prometheus.yml"  #指定配置文件
--web.listen-address="0.0.0.0:9090"  #指定监听地址
--storage.tsdb.path="data/"  #指定存储目录

--storage.tsdb.retention.size= B, KB, MB, GB, TB, PB, EB #指定chunk大小，默认512MB
--storage.tsdb.retention.time= #数据保存时长，默认15天

--query.timeout=2m #最大查询超时时间
--query.max-concurrency=20  #最大查询并发数

--web.read-timeout=5m  #最大空闲超时时间
--web.max-connections=512 # 最大并发连接数
--web.enable-lifecycle  #启用API动态加载
```

## 9.2：远端存储--victoriametrics

https://github.com/VictoriaMetrics/VictoriaMetrics/tree/v1.96.0

https://docs.victoriametrics.com/Single-server-VictoriaMetrics.html

![image-20240105143400366](images\image-20240105143400366.png)

### 9.2.1: 单机版部署

```bash
victoriametrics: v1.96.0
victoriametrics: 192.168.58.147
```

#### 9.2.1.1：部署单机版

```bash
~$ cd /app
~$ wget https://github.com/VictoriaMetrics/VictoriaMetrics/releases/download/v1.96.0/victoria-metrics-linux-amd64-v1.96.0.tar.gz
~$ tar xf victoria-metrics-linux-amd64-v1.96.0.tar.gz

参数：
-httpListenAddr=0.0.0.0:8428 #监听的地址及端口，默认8428
-storageDataPath # victoriaMetrics 将所有数据存储在此目录中，默认为执行启动victoria的当前目录下的victoria-metrics-data目录中。
-retentionPeriod # 数据的保留时长，旧的数据会自动删除，默认保留1个月。默认单位m(月),支持的单位有h(hour),d(day),w(week),y(year).


~$ mv /app/victoria-metrics-prod /usr/local/bin/

# service启动文件
~$ cat /etc/systemd/system/victoria-metrics-prod.service
[Unit]
Description=victoria-metrics-prod
After=network.target

[Service]
Restart=on-failure
ExecStart=/usr/local/bin/victoria-metrics-prod -httpListenAddr=0.0.0.0:8428 -storageDataPath=/data/victoria -retentionPeriod=3

[Install]
WantedBy=multi-user.target

~$ systemctl daemon-reload && systemctl restart victoria-metrics-prod.service && systemctl enable victoria-metrics-prod.service
```

验证web页面：

![image-20240105150314464](images\image-20240105150314464.png)

#### 9.2.1.2：prometheus设置

```bash
~$ vim /app/prometheus/prometheus.yml
remote_write:
  - url: http://192.168.58.147:8428/api/v1/write
```

#### 9.2.1.3：验证VictoriaMetrics数据

http://192.168.58.147:8428/vmui/

![image-20240105151306517](images\image-20240105151306517.png)

#### 9.2.1.4：grafana设置

添加数据源：类型为prometheus，地址及端口为VictoriaMetrics：

![image-20240105151644478](images\image-20240105151644478.png)

导入指定模板：8919

![image-20240105151805807](images\image-20240105151805807.png)

#### 9.2.1.5 ：验证数据

![image-20240105152254494](images\image-20240105152254494.png)

### 9.2.2： k8s集群版部署victorametrics

参考下面：

https://www.qikqiak.com/post/victoriametrics-usage/

### 9.2.3：二进制集群版部署（分片）

![image-20240106153014022](images\image-20240106153014022.png)

#### 9.2.3.1：组件介绍

```bash
vminsert #写入组件，vminsert负责接收数据写入并根据对度量名称及其所有标签的一致性hash结果，将数据分散写入不同的后端vmstorage，vminsert默认端口8480.

vmstorage #存储原始数据，默认端口8482
vmselect  # 查询组件（读），连接vmstroage，默认端口8481
```

![image-20240106144925144](images\image-20240106144925144.png)

#### 9.2.3.2：环境准备

```bash
环境信息：
vm1: 192.168.58.149
vm2: 192.168.58.150
vm3: 192.168.58.151
victorametrics版本： v1.96.0

192.168.58.145 #主节点

192.168.58.147 #联邦节点1
192.168.58.148  #联邦节点2

192.168.58.146 # node1，联邦节点1的目标采集服务器
192.168.58.144 # node2，联邦节点2的目标采集服务器
```

分别在各个victorametrics节点进行安装配置：

```bash
# wget https://mirror.ghproxy.com/https://github.com/VictoriaMetrics/VictoriaMetrics/releases/download/v1.96.0/victoria-metrics-linux-amd64-v1.96.0-cluster.tar.gz
# tar xf victoria-metrics-linux-amd64-v1.96.0-cluster.tar.gz
# mv vminsert-prod vmselect-prod vmstorage-prod /usr/local/bin/

```

#### 9.2.3.3：部署vmatorage-prod组件（所有节点）

负责数据的持久化:

`vmstorage`监听端口：`8482`, 

`vmstorage`对`vminsert`提供服务的监听端口：`8400`，

`vmstorage`对`vmselect`提供服务的监听端口：`8401`

```bash
~$ vim /etc/systemd/system/vmstorage.service
[Unit]
Description=Vmstorage Server
After=network.target

[Service]
Restart=on-failure
ExecStart=/usr/local/bin/vmstorage-prod -loggerTimezone=Asia/Shanghai -storageDataPath=/data/vmstorage -httpListenAddr=":8482" -vminsertAddr=":8400" -vmselectAddr=":8401" 

[Install]
WantedBy=multi-user.target

~$ systemctl daemon-reload && systemctl restart vmstorage.service && systemctl enable vmstorage.service
```

#### 9.2.3.4：部署vminsert-prod组件（所有节点）

接收外部的写请求，默认端口8480。

```bash
~$ vim /etc/systemd/system/vminsert.service
[Unit]
Description=Vminsert Server
After=network.target

[Service]
Restart=on-failure
ExecStart=/usr/local/bin/vminsert-prod -httpListenAddr=":8480" -storageNode=192.168.58.149:8400,192.168.58.150:8400,192.168.58.151:8400

[Install]
WantedBy=multi-user.target


~$ systemctl daemon-reload && systemctl restart vminsert.service && systemctl enable vminsert.service
```

#### 9.2.3.5：部署vmselect-prod组件（所有节点）

负责接收外面的读请求，默认端口8481.

```bash
~$ vim  /etc/systemd/system/vmselect.service
[Unit]
Description=Vmselect Server
After=network.target

[Service]
Restart=on-failure
ExecStart=/usr/local/bin/vmselect-prod -httpListenAddr=":8481" -storageNode=192.168.58.149:8401,192.168.58.150:8401,192.168.58.151:8401

[Install]
WantedBy=multi-user.target


~$ systemctl daemon-reload && systemctl restart vmselect.service && systemctl enable vmselect.service
```

#### 9.2.3.6：验证服务端口

```bash
192.168.58.149:
# curl http://192.168.58.149:8480/metrics
# curl http://192.168.58.149:8481/metrics
# curl http://192.168.58.149:8482/metrics

192.168.58.150:
# curl http://192.168.58.150:8480/metrics
# curl http://192.168.58.150:8481/metrics
# curl http://192.168.58.150:8482/metrics

192.168.58.151:
# curl http://192.168.58.151:8480/metrics
# curl http://192.168.58.151:8481/metrics
# curl http://192.168.58.151:8482/metrics
```

#### 9.2.3.7:  Prometheus主节点配置远程写入

```bash
~$ vim prometheus.yml
# 单机写入
#remote_write:
#  - url: http://192.168.58.147:8428/api/v1/write

#集群写入
remote_write:
  - url: http://192.168.58.149:8480/insert/0/prometheus
  - url: http://192.168.58.150:8480/insert/0/prometheus
  - url: http://192.168.58.151:8480/insert/0/prometheus
```

#### 9.2.3.8：grafana配置数据源及导入模板

配置数据源：

http://192.168.58.150:8481/select/0/prometheus

![image-20240106162907038](images\image-20240106162907038.png)

导入指定模板：13824

![image-20240106181944509](images\image-20240106181944509.png)

### 9.2.4：二进制集群部署（副本）

默认情况下，VictoriaMetrics 的数据复制依赖 `-storageDataPath` 指向的底层存储来完成。

但是我们也可以手动通过将 `-replicationFactor=N` 命令参数传递给 `vminsert` 来启用复制，这保证了如果多达 `N-1` 个 `vmstorage` 节点不可用，所有数据仍可用于查询。集群必须至少包含 `2*N-1` 个 `vmstorage` 节点，其中 `N` 是复制因子，以便在 `N-1` 个存储节点丢失时为新摄取的数据维持指定的复制因子。

例如，当 `-replicationFactor=3` 传递给 `vminsert` 时，它将所有摄取的数据复制到 3 个不同的 `vmstorage` 节点，因此最多可以丢失 2 个 `vmstorage` 节点而不会丢失数据。`vmstorage` 节点的最小数量应该等于 `2*3-1 = 5`，因此当 2 个 `vmstorage` 节点丢失时，剩余的 3 个 `vmstorage` 节点可以为新摄取的数据提供服务。

启用复制后，必须将 `-dedup.minScrapeInterval=1ms` 命令行标志传递给 `vmselect` 节点，当多达 `N-1` 个 `vmstorage` 节点响应缓慢和/或暂时不可用时，可以将可选的 `-replicationFactor=N` 参数传递给 `vmselect` 以提高查询性能，因为 `vmselect` 不等待来自多达 `N-1` 个 `vmstorage` 节点的响应。有时，`vmselect` 节点上的 `-replicationFactor` 可能会导致部分响应。`-dedup.minScrapeInterval=1ms` 在查询期间对复制的数据进行重复数据删除，如果重复数据从配置相同的 `vmagent` 实例或 Prometheus 实例推送到 VictoriaMetrics，则必须根据重复数据删除文档将 `-dedup.minScrapeInterval` 设置为更大的值。

请注意，复制不会从灾难中保存，因此建议执行定期备份。另外复制会增加资源使用率 - CPU、内存、磁盘空间、网络带宽这些最多 `-replicationFactor` 倍。所以可以将复制转移 `-storageDataPath` 指向的底层存储来做保证，例如 Google Compute Engine 永久磁盘，该磁盘可以防止数据丢失和数据损坏，它还提供始终如一的高性能，并且可以在不停机的情况下调整大小。对于大多数用例来说，基于 HDD 的永久性磁盘应该足够了。

#### 9.2.4.1：vmstorage部署

```bash
~$ vim /etc/systemd/system/vmstorage.service
[Unit]
Description=Vmstorage Server
After=network.target

[Service]
Restart=on-failure
ExecStart=/usr/local/bin/vmstorage-prod -loggerTimezone=Asia/Shanghai -storageDataPath=/data/vmstorage -httpListenAddr=":8482" -vminsertAddr=":8400" -vmselectAddr=":8401" -dedup.minScrapeInterval=30s
# dedup.minScrapeInterval和vmselect保持一致
[Install]
WantedBy=multi-user.target

~$ systemctl daemon-reload && systemctl restart vmstorage.service && systemctl enable vmstorage.service
```

#### 9.2.4.2：部署vminsert

```bash
~$ vim /etc/systemd/system/vminsert.service
[Unit]
Description=Vminsert Server
After=network.target

[Service]
Restart=on-failure
ExecStart=/usr/local/bin/vminsert-prod -httpListenAddr=":8480" -storageNode=192.168.58.149:8400,192.168.58.150:8400,192.168.58.151:8400 -replicationFactor=2

[Install]
WantedBy=multi-user.target


~$ systemctl daemon-reload && systemctl restart vminsert.service && systemctl enable vminsert.service
```

#### 9.2.4.3：部署vmselect

```bash
~$ vim  /etc/systemd/system/vmselect.service
[Unit]
Description=Vmselect Server
After=network.target

[Service]
Restart=on-failure
ExecStart=/usr/local/bin/vmselect-prod -httpListenAddr=":8481" -storageNode=192.168.58.149:8401,192.168.58.150:8401,192.168.58.151:8401 -dedup.minScrapeInterval=30s -replicationFactor=3

[Install]
WantedBy=multi-user.target


~$ systemctl daemon-reload && systemctl restart vmselect.service && systemctl enable vmselect.service
```





































































































































































































































































