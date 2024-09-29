# 1 堡垒机和 JumpServer

## 1.1 跳板机和堡垒机

**跳板机**

跳板机是一种用于单点登陆的主机应用系统。跳板机通常是由一台服务器能过特定的软件实现，维护人 员在维护过程中，首先要统一登录到这台服务器上，然后从这台服务器再登录到目标设备进行维护。但 跳板机没有实现对运维人员操作行为的控制和审计，此外，跳板机存在严重的安全风险，一旦跳板机系 统被攻入，则将后端资源风险完全暴露无遗。对于一些服务（如:telnet）可以通过跳板机来完成一定的 控制访问，但是对于更多的服务（SSH、RDP等）来讲，就显得力不从心了。

**堡垒机**

由于跳板机的不足，更多的组织需要更先进、更好的安全技术,来实现运维操作管理和安全。堡垒机开始 以独立的产品形态被广泛部署，有效降低了运维操作风险，使得运维操作管理变得更简单、更安全。堡 垒机能满足角色管理与授权审批、信息资源访问控制、操作记录和审计、系统变更和维护控制要求，并 生成一些统计报表配合管理规范，从而不断提升IT内控的合规性。

![image-20240929094940235](images\image-20240929094940235.png)

## 1.2 JumpServer 简介

JumpServer 是全球首款完全开源的堡垒机, 使用 GNU GPL v2.0 开源协议, 是符合 4A 的专业运维审计系 统。为互联网企业提供了认证，授权，审计，自动化运维等功能。

JumpServer 使用 Python / Django 进行开发, 遵循 Web 2.0 规范, 配备了业界领先的 Web Terminal 解 决方案, 交互界面美观、用户体验好。

JumpServer 采纳分布式架构, 支持多机房跨区域部署, 中心节点提供 API, 各机房部署登录节点, 可横向扩 展、无并发访问限制。

JumpServer 现已支持管理 SSH、 Telnet、 RDP、 VNC 协议资产。

![image-20240929095146779](images\image-20240929095146779.png)

**JumpServer 历史**

![image-20240929095226759](images\image-20240929095226759.png)

官方地址： http://www.jumpserver.org/ 

github项目: https://github.com/jumpserver

## 1.3 JumpServer 生产应用场景

![image-20240929095505721](images\image-20240929095505721.png)

## 1.4 JumpServer的优势和功能

### 1 . 4 . 1  特 色 优 势

- 开 源:  零 门 槛 ， 线 上 快 速 获 取 和 安 装 
- 分 布 式:  轻 松 支 持 大 规 模 并 发 访 问 ； 
- 无 插 件:  仅 需 浏 览 器 ， 极 致 的  W e b  T e r min al  使 用 体 验 
- 多 云 支 持:  一 套 系 统 ， 同 时 管 理 不 同 云 上 面 的 资 产 
- 云 端 存 储:  审 计 录 像 云 端 存 储 ， 永 不 丢 失 
- 多 租 户:  一 套 系 统 ， 多 个 子 公 司 和 部 门 同 时 使 用

### 1.4.2 功能列表

堡 垒 机 四 个 核 心 能 力:  运 维 安 全 审 计 的 4 A 规 范

![image-20240929095755067](images\image-20240929095755067.png)



## 1.5 JumpServer 组成

![image-20240929095908305](images\image-20240929095908305.png)

![image-20240929095928895](images\image-20240929095928895.png)



- **Lina**

  前端 UI 项目，实现web页面展示，主要使用 Vue，Element UI 完成

- **Core**

  现指 Jumpserver 管理后台，是核心组件（Core）, 使用 Django Class Based View 风格开发，支 持 Restful API。

- **Coco/Koko**

  实现了 SSH Server 和 Web Terminal Server 的组件，提供 SSH 和 WebSocket 接口, 使用  Paramiko 和 Flask 开发。

  Koko 是 Go 版本的 coco，重构了 coco 的 SSH/SFTP 服务和 Web Terminal 服务。

- **Luna**

  现在是 Web Terminal 前端，计划前端页面都由该项目提供，Jumpserver 只提供 API，不再负责 后台渲染html等。主要使用Angular CLI 完成

- **Lion**

  Lion 使用了 Apache 软件基金会的开源项目 Guacamole，JumpServer 使用 Golang 和 Vue 重构 了 Guacamole 实现 RDP/VNC 协议跳板机功能。

# 2 JumpServer 安装

官方说明

```http
https://docs.jumpserver.org/zh/master/install/setup_by_fast/
```

## 2.1 安装要求

JumpServer 环境要求:

- 硬件配置: 2个CPU核心, 4G 内存, 50G 硬盘（最低）
- 操作系统: Linux 发行版 x86_64
- Python = 3.6.x
- MySQL Server ≥ 5.6 或者 Mariadb Server ≥ 5.5.56 数据库编码要求 uft8,新版要求5.7以上
- Redis: 新版要求6.0以上

## 2.2 安装方法介绍

官方提供了多种安装方法

- 手动部署: 按组件逐个实现
- 极速部署: 资产数量不多，或者测试体验的用户请使用本脚本快速部署
- 容器部署: 基于 docker 实现
- 分布式部署: 适用大型环境
- Kubernetes部署：基于Helm部署

## 2.3 基于容器部署

官方文档：

```http
https://github.com/jumpserver/Dockerfile/tree/master/allinone
```

### 2.3.1 环境说明

```http
https://github.com/jumpserver/Dockerfile/tree/master/allinone
```

使用外置MYSQL数据库和Redis

```http
- 外置数据库要求 MySQL 版本大于等于 5.7
- 外置 Redis 要求 Redis 版本大于等于 6.0
# 自行部署 MySQL 可以参考 
(https://docs.jumpserver.org/zh/master/install/setup_by_lb/#mysql)
# mysql 创建用户并赋予权限, 请自行替换 nu4x599Wq7u0Bn8EABh3J91G 为自己的密码
mysql -u root -p
create database jumpserver default charset 'utf8';
create user 'jumpserver'@'%' identified by 'nu4x599Wq7u0Bn8EABh3J91G';
grant all on jumpserver.* to 'jumpserver'@'%';
flush privileges;
# 自行部署 Redis 可以参考 
(https://docs.jumpserver.org/zh/master/install/setup_by_lb/#redis)
```

**基于容器,安装完毕后可以通过以下方式访问**

- 浏览器访问: http://<容器所在服务器IP> 
- 默认管理员账户 admin 密码 ChangeMe
- SSH 访问: ssh -p 2222 <容器所在服务器IP>
- XShell 等工具请添加 connection 连接, 默认 ssh 端口 2222

### 2.3.2 安装docker环境

```bash
root@ubutun2204-1:~# apt update && apt list docker.io
Listing... Done
docker.io/jammy-updates 24.0.7-0ubuntu2~22.04.1 amd64
N: There are 2 additional versions. Please use the '-a' switch to see them.

root@ubutun2204-1:~# apt-cache madison docker.io
 docker.io | 24.0.7-0ubuntu2~22.04.1 | http://cn.archive.ubuntu.com/ubuntu jammy-updates/universe amd64 Packages
 docker.io | 20.10.21-0ubuntu1~22.04.3 | http://security.ubuntu.com/ubuntu jammy-security/universe amd64 Packages
 docker.io | 20.10.12-0ubuntu4 | http://cn.archive.ubuntu.com/ubuntu jammy/universe amd64 Packages
 
root@ubutun2204-1:~# apt -y install docker.io
root@ubutun2204-1:~# docker version
Client:
 Version:           24.0.7
 API version:       1.43
 Go version:        go1.21.1
 Git commit:        24.0.7-0ubuntu2~22.04.1
 Built:             Wed Mar 13 20:23:54 2024
 OS/Arch:           linux/amd64
 Context:           default

Server:
 Engine:
  Version:          24.0.7  # docker版本为24.0.7
  API version:      1.43 (minimum version 1.12)
  Go version:       go1.21.1
  Git commit:       24.0.7-0ubuntu2~22.04.1
  Built:            Wed Mar 13 20:23:54 2024
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.7.12
  GitCommit:        
 runc:
  Version:          1.1.12-0ubuntu2~22.04.1
  GitCommit:        
 docker-init:
  Version:          0.19.0
  GitCommit:        

```

### 2.3.3 安装MYSQL服务

官方说明：

```bash
# 自行部署 MySQL 可以参考 (https://docs.jumpserver.org/zh/master/install/setup_by_lb/#mysql)
# mysql 创建用户并赋予权限, 请自行替换 nu4x599Wq7u0Bn8EABh3J91G 为自己的密码
mysql -u root -p
```

MYSQL要求

```sql
create database jumpserver default charset 'utf8';
create user 'jumpserver'@'%' identified by 'nu4x599Wq7u0Bn8EABh3J91G';
grant all on jumpserver.* to 'jumpserver'@'%';
flush privileges;
```

注意：JumpServer-v2.28.7之前版本默认不支持MySQL8.0，选择MySQL5.7

#### 2.3.3.1 下载MySQL镜像查看默认配置

下载MySQL镜像并运行, 查看当前默认配置不符合JumpServer安装要求

```bash
#下载MySQL镜像并启动
root@ubutun2204-1:~# docker run --rm --name mysql -e MYSQL_ROOT_PASSWORD=123456 -e MYSQL_DATABASE=jumpserver -e MYSQL_USER=jumpserver -e MYSQL_PASSWORD=123456 -d -p 3306:3306 mysql:5.7.30

# 查看默认的MySQL容器配置不符合jumpserver要求
root@ubutun2204-1:~# docker exec -it mysql bash
root@456911a729c0:/# mysql -uroot -p123456
mysql: [Warning] Using a password on the command line interface can be insecure.
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2
Server version: 5.7.30 MySQL Community Server (GPL)

Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| jumpserver         |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.01 sec)

mysql> select user,host from mysql.user;
+---------------+-----------+
| user          | host      |
+---------------+-----------+
| jumpserver    | %         |
| root          | %         |
| mysql.session | localhost |
| mysql.sys     | localhost |
| root          | localhost |
+---------------+-----------+
5 rows in set (0.00 sec)

mysql> exit
Bye

#查看配置文件路径
root@456911a729c0:/# cat /etc/mysql/mysql.cnf
!includedir /etc/mysql/conf.d/
!includedir /etc/mysql/mysql.conf.d/

#默认配置文件
root@456911a729c0:/# grep '^[^#]' /etc/mysql/mysql.conf.d/mysqld.cnf
[mysqld]
pid-file	= /var/run/mysqld/mysqld.pid
socket		= /var/run/mysqld/mysqld.sock
datadir		= /var/lib/mysql
symbolic-links=0

root@ubutun2204-1:~# docker stop mysql
```

#### 2.3.3.2 在宿主机准备MySQL配置文件

```bash
#准备相关目录
root@ubutun2204-1:~# mkdir -p /etc/mysql/mysql.conf.d/
root@ubutun2204-1:~# mkdir -p /etc/mysql/conf.d/

#生成服务器配置文件,指定字符集
root@ubutun2204-1:~# tee /etc/mysql/mysql.conf.d/mysqld.cnf <<EOF
[mysqld]
pid-file= /var/run/mysqld/mysqld.pid
socket= /var/run/mysqld/mysqld.sock
datadir= /var/lib/mysql
symbolic-links=0
character-set-server=utf8   #添加此行,指定字符集
EOF

#生成客户端配置文件,指定字符集
tee /etc/mysql/conf.d/mysql.cnf <<EOF
[mysql]
default-character-set=utf8  #添加此行,指定字符集
EOF

root@ubutun2204-1:~# tee /etc/mysql/conf.d/mysql.cnf <<EOF
[mysql]
default-character-set=utf8
EOF
```

#### 2.3.3.3 启动 MySQL 容器

将上面宿主机的设置好的配置文件挂载至MySQL容器

```bash
root@ubutun2204-1:~# docker run -d -p 3306:3306 --name mysql --restart always -e MYSQL_ROOT_PASSWORD=123456 -e MYSQL_DATABASE=jumpserver -e MYSQL_USER=jumpserver -e MYSQL_PASSWORD=123456  -v /data/mysql:/var/lib/mysql -v /etc/mysql/mysql.conf.d/mysqld.cnf:/etc/mysql/mysql.conf.d/mysqld.cnf -v /etc/mysql/conf.d/mysql.cnf:/etc/mysql/conf.d/mysql.cnf mysql:5.7.30
```

#### 2.3.3.4 验证MySQL

```bash
root@ubutun2204-1:~# docker exec -it mysql sh
# mysql -p123456 -e 'show variables like "character%"'
mysql: [Warning] Using a password on the command line interface can be insecure.
+--------------------------+----------------------------+
| Variable_name            | Value                      |
+--------------------------+----------------------------+
| character_set_client     | utf8                       |
| character_set_connection | utf8                       |
| character_set_database   | utf8                       |
| character_set_filesystem | binary                     |
| character_set_results    | utf8                       |
| character_set_server     | utf8                       |
| character_set_system     | utf8                       |
| character_sets_dir       | /usr/share/mysql/charsets/ |
+--------------------------+----------------------------+
# mysql -p123456 -e 'show variables like "collation%"' 
mysql: [Warning] Using a password on the command line interface can be insecure.
+----------------------+-----------------+
| Variable_name        | Value           |
+----------------------+-----------------+
| collation_connection | utf8_general_ci |
| collation_database   | utf8_general_ci |
| collation_server     | utf8_general_ci |
+----------------------+-----------------+
#  mysql -p123456 -e 'select user,host from mysql.user'
mysql: [Warning] Using a password on the command line interface can be insecure.
+---------------+-----------+
| user          | host      |
+---------------+-----------+
| jumpserver    | %         |
| root          | %         |
| mysql.session | localhost |
| mysql.sys     | localhost |
| root          | localhost |
+---------------+-----------+
```

### 2.3.4: 安装Redis服务

官方说明：

```http
# 自行部署 Redis 可以参考 (https://docs.jumpserver.org/zh/master/install/setup_by_lb/#redis)
```

新版要求：

```http
外置 Redis 要求 Redis 版本大于等于 6.0
```

#### 2.3.4.1 启动 Redis

```bash
root@ubutun2204-1:~# docker run -d -p 6379:6379 --name redis --restart always redis:6.2.7
```

### 2.3.5 部署 JumpServer

#### 2.3.5.1 生成 key 和 token

官方说明：

```bash
https://github.com/jumpserver/Dockerfile/tree/master/allinone
https://docs.jumpserver.org/zh/master/install/docker_install/
```

**需要先生成key和token**

![image-20240929122429361](images\image-20240929122429361.png)

```bash
root@ubutun2204-1:~# cat key.sh 
#!/bin/bash
if [ ! "$SECRET_KEY" ]; then
  SECRET_KEY=`cat /dev/urandom | tr -dc A-Za-z0-9 | head -c 50`;
  echo "SECRET_KEY=$SECRET_KEY" >> ~/.bashrc;
  echo SECRET_KEY=$SECRET_KEY;
else
  echo SECRET_KEY=$SECRET_KEY;
fi  
if [ ! "$BOOTSTRAP_TOKEN" ]; then
  BOOTSTRAP_TOKEN=`cat /dev/urandom | tr -dc A-Za-z0-9 | head -c 16`;
  echo "BOOTSTRAP_TOKEN=$BOOTSTRAP_TOKEN" >> ~/.bashrc;
  echo BOOTSTRAP_TOKEN=$BOOTSTRAP_TOKEN;
else
  echo BOOTSTRAP_TOKEN=$BOOTSTRAP_TOKEN;
fi
root@ubutun2204-1:~# bash key.sh 
SECRET_KEY=b4saJ5a1ORyZ73ghMemXqrK9HRp1HaBJb5vryBW8f3nERu5pQM
BOOTSTRAP_TOKEN=AbNyEdE5MpLnHnN6
```

#### 2.3.5.1 运行容器

范例：JumpServer v4.0.2版

```bash
root@ubutun2204-1:~# docker run --name jms_all -d \
  -v /opt/jumpserver/core/data:/opt/jumpserver/data \
  -v /opt/jumpserver/koko/data:/opt/koko/data \
  -v /opt/jumpserver/lion/data:/opt/lion/data \
  -p 80:80 \
  -p 2222:2222 \
  -e SECRET_KEY=b4saJ5a1ORyZ73ghMemXqrK9HRp1HaBJb5vryBW8f3nERu5pQM \
  -e BOOTSTRAP_TOKEN=Q6POdPQZ2ktV7ZEa \
  -e LOG_LEVEL=ERROR \
  -e DB_HOST=192.168.159.103 \ #不支持127.0.0.1
  -e DB_PORT=3306 \
  -e DB_USER=jumpserver \
  -e DB_PASSWORD=123456 \
  -e DB_NAME=jumpserver \
  -e REDIS_HOST=192.168.159.103 \ #不支持127.0.0.1
  -e REDIS_PORT=6379 \
  -e REDIS_PASSWORD='' \
  --privileged=true \
  jumpserver/jms_all:v4.0.2
```

#### 2.3.5.3 验证是否成功

##### 2.3.5.3.1 查看日志

范例：查看jumpserver 4.0.2日志确认成功

```bash
root@ubutun2204-1:~# docker logs -f jms_all
Time: 2024-09-29 12:48:40
The Installation is Complete.
    --------------------------------------------------
    | Documentation:    https://docs.jumpserver.org/ |
    | Official Website: https://www.jumpserver.org/  |
    --------------------------------------------------

       ██╗██╗   ██╗███╗   ███╗██████╗ ███████╗███████╗██████╗ ██╗   ██╗███████╗██████╗
       ██║██║   ██║████╗ ████║██╔══██╗██╔════╝██╔════╝██╔══██╗██║   ██║██╔════╝██╔══██╗
       ██║██║   ██║██╔████╔██║██████╔╝███████╗█████╗  ██████╔╝██║   ██║█████╗  ██████╔╝
  ██   ██║██║   ██║██║╚██╔╝██║██╔═══╝ ╚════██║██╔══╝  ██╔══██╗╚██╗ ██╔╝██╔══╝  ██╔══██╗
  ╚█████╔╝╚██████╔╝██║ ╚═╝ ██║██║     ███████║███████╗██║  ██║ ╚████╔╝ ███████╗██║  ██║
   ╚════╝  ╚═════╝ ╚═╝     ╚═╝╚═╝     ╚══════╝╚══════╝╚═╝  ╚═╝  ╚═══╝  ╚══════╝╚═╝  ╚═╝

                                                                   VERSION: v4.0.2
```

##### 2.3.5.3.2 查看 MySQL 中生成相关表

```bash
mysql> show tables;
+----------------------------------------------------------+
| Tables_in_jumpserver                                     |
+----------------------------------------------------------+
| accounts_account                                         |
| accounts_accountbackupautomation                         |
| accounts_accountbackupautomation_obj_recipients_part_one |
| accounts_accountbackupautomation_obj_recipients_part_two |
| accounts_accountbackupautomation_recipients_part_one     |
| accounts_accountbackupautomation_recipients_part_two     |
| accounts_accountbackupexecution                          |
| accounts_accounttemplate                                 |
| accounts_accounttemplate_platforms                       |
| accounts_changesecretautomation                          |
| accounts_changesecretautomation_recipients               |
| accounts_changesecretrecord                              |
| accounts_gatheraccountsautomation                        |
| accounts_gatheraccountsautomation_recipients             |
| accounts_gatheredaccount                                 |
| accounts_historicalaccount                               |
| accounts_pushaccountautomation                           |
| accounts_verifyaccountautomation                         |
| accounts_virtualaccount                                  |
| acls_commandfilteracl                                    |
| acls_commandfilteracl_command_groups                     |
| acls_commandfilteracl_reviewers                          |
| acls_commandgroup                                        |
| acls_connectmethodacl                                    |
| acls_connectmethodacl_reviewers                          |
| acls_loginacl                                            |
| acls_loginacl_reviewers                                  |
| acls_loginassetacl                                       |
| acls_loginassetacl_reviewers                             |
| assets_asset                                             |
| assets_asset_nodes                                       |
| assets_automationexecution                               |
| assets_baseautomation                                    |
| assets_baseautomation_assets                             |
| assets_baseautomation_nodes                              |
| assets_cloud                                             |
| assets_custom                                            |
| assets_database                                          |
| assets_device                                            |
| assets_domain                                            |
| assets_favoriteasset                                     |
| assets_gatherfactsautomation                             |
| assets_gpt                                               |
| assets_host                                              |
| assets_label                                             |
| assets_node                                              |
| assets_pingautomation                                    |
| assets_platform                                          |
| assets_platformautomation                                |
| assets_platformprotocol                                  |
| assets_protocol                                          |
| assets_web                                               |
| audits_activitylog                                       |
| audits_ftplog                                            |
| audits_operatelog                                        |
| audits_passwordchangelog                                 |
| audits_userloginlog                                      |
| audits_usersession                                       |
| auth_group                                               |
| auth_group_permissions                                   |
| auth_permission                                          |
| authentication_accesskey                                 |
| authentication_connectiontoken                           |
| authentication_passkey                                   |
| authentication_privatetoken                              |
| authentication_ssotoken                                  |
| authentication_temptoken                                 |
| captcha_captchastore                                     |
| django_admin_log                                         |
| django_cas_ng_proxygrantingticket                        |
| django_cas_ng_sessionticket                              |
| django_celery_beat_clockedschedule                       |
| django_celery_beat_crontabschedule                       |
| django_celery_beat_intervalschedule                      |
| django_celery_beat_periodictask                          |
| django_celery_beat_periodictasks                         |
| django_celery_beat_solarschedule                         |
| django_content_type                                      |
| django_migrations                                        |
| django_session                                           |
| labels_label                                             |
| labels_labeledresource                                   |
| notifications_messagecontent                             |
| notifications_messagecontent_groups                      |
| notifications_sitemessage                                |
| notifications_systemmsgsubscription                      |
| notifications_systemmsgsubscription_groups               |
| notifications_systemmsgsubscription_users                |
| notifications_usermsgsubscription                        |
| ops_adhoc                                                |
| ops_celerytask                                           |
| ops_celerytaskexecution                                  |
| ops_historicaljob                                        |
| ops_job                                                  |
| ops_job_assets                                           |
| ops_jobexecution                                         |
| ops_playbook                                             |
| orgs_organization                                        |
| perms_assetpermission                                    |
| perms_assetpermission_assets                             |
| perms_assetpermission_nodes                              |
| perms_assetpermission_user_groups                        |
| perms_assetpermission_users                              |
| perms_userassetgrantedtreenoderelation                   |
| rbac_menupermission                                      |
| rbac_role                                                |
| rbac_role_permissions                                    |
| rbac_rolebinding                                         |
| settings_chatprompt                                      |
| settings_setting                                         |
| terminal                                                 |
| terminal_applet                                          |
| terminal_applethost                                      |
| terminal_applethostdeployment                            |
| terminal_appletpublication                               |
| terminal_appprovider                                     |
| terminal_command                                         |
| terminal_commandstorage                                  |
| terminal_endpoint                                        |
| terminal_endpointrule                                    |
| terminal_replaystorage                                   |
| terminal_session                                         |
| terminal_sessionjoinrecord                               |
| terminal_sessionreplay                                   |
| terminal_sessionsharing                                  |
| terminal_status                                          |
| terminal_task                                            |
| terminal_virtualapp                                      |
| terminal_virtualapppublication                           |
| tickets_applyassetticket                                 |
| tickets_applyassetticket_apply_assets                    |
| tickets_applyassetticket_apply_nodes                     |
| tickets_applycommandticket                               |
| tickets_applyloginassetticket                            |
| tickets_applyloginticket                                 |
| tickets_approvalrule                                     |
| tickets_approvalrule_assignees                           |
| tickets_comment                                          |
| tickets_ticket                                           |
| tickets_ticketassignee                                   |
| tickets_ticketflow                                       |
| tickets_ticketflow_rules                                 |
| tickets_ticketsession                                    |
| tickets_ticketstep                                       |
| users_preference                                         |
| users_user                                               |
| users_user_groups                                        |
| users_user_user_permissions                              |
| users_usergroup                                          |
| users_userpasswordhistory                                |
+----------------------------------------------------------+
150 rows in set (0.01 sec)

```

##### 2.3.5.3.3 查看端口

```bash
root@ubutun2204-1:~# ss -ntl
State                         Recv-Q                        Send-Q                                               Local Address:Port                                                  Peer Address:Port                        Process                        
LISTEN                        0                             4096                                                     127.0.0.1:33781                                                      0.0.0.0:*                                                          
LISTEN                        0                             4096                                                 127.0.0.53%lo:53                                                         0.0.0.0:*                                                          
LISTEN                        0                             4096                                                       0.0.0.0:6379                                                       0.0.0.0:*                                                          
LISTEN                        0                             4096                                                       0.0.0.0:2222                                                       0.0.0.0:*                                                          
LISTEN                        0                             128                                                      127.0.0.1:6010                                                       0.0.0.0:*                                                          
LISTEN                        0                             4096                                                       0.0.0.0:3306                                                       0.0.0.0:*                                                          
LISTEN                        0                             4096                                                       0.0.0.0:80                                                         0.0.0.0:*                                                          
LISTEN                        0                             128                                                        0.0.0.0:22                                                         0.0.0.0:*                                                          
LISTEN                        0                             4096                                                          [::]:6379                                                          [::]:*                                                          
LISTEN                        0                             4096                                                          [::]:2222                                                          [::]:*                                                          
LISTEN                        0                             128                                                          [::1]:6010                                                          [::]:*                                                          
LISTEN                        0                             4096                                                          [::]:3306                                                          [::]:*                                                          
LISTEN                        0                             4096                                                          [::]:80                                                            [::]:*                                                          
LISTEN                        0                             128                                                           [::]:22               
```

##### 2.3.5.3.4 验证登录

![image-20240929130952921](images\image-20240929130952921.png)

## 2.4 一键脚本安装

```bash
https://docs.jumpserver.org/zh/v4/installation/setup_linux_standalone/online_install/
```

## 2.5 Kubernetes Helm 模式部署

```http
https://docs.jumpserver.org/zh/v4/installation/setup_kubernetes/helm_online_install/
```

# 3 JumpServer 常见功能

官方文档：

```http
https://docs.jumpserver.org/zh/master/
```

## 3.1 登录并初始化配置

### 3.1.1 首次登录

#### 3.1.1.1 浏览器访问

```http
http:<JumpServerIP>
```

登录 JumpServer 默认用户: admin 密码: ChangeMe

![image-20240929140548725](images\image-20240929140548725.png)

第一次登录要求重置密码

![image-20240929140634381](images\image-20240929140634381.png)

新版：v4.0.2

![image-20240929140819368](images\image-20240929140819368.png)

#### 3.1.1.2 ssh 登录

可以用admin用户和修改过的新密码, 连接jumpserver的ssh端口2222/tcp进行连接访问

注意:新版需要实现资产授权后才能连接登录

![image-20240929141335983](images\image-20240929141335983.png)

### 3.1.2 修改 admin 用户的密码

![image-20240929141601388](images\image-20240929141601388.png)

### 3.1.3 配置邮件

![image-20240929143337660](images\image-20240929143337660.png)

测试连接,可以收到邮件

![image-20240929143411783](images\image-20240929143411783.png)

## 3.2 创建JumpServer用户和组

JumpServer 支持三种登录用户

- 系统管理员
- 普通用户
- 系统审计员

### 3.2.1 创建用户

填写用户信息,注意: 邮箱地址不能重复

![image-20240929145021168](images\image-20240929145021168.png)

**相同方法再创建leilei用户**

![image-20240929145235673](images\image-20240929145235673.png)

![image-20240929145315837](images\image-20240929145315837.png)

### 3.2.2 创建组并将用户加入组中

创建development组,并将前面创建的用户加入组中

![image-20240929145427889](images\image-20240929145427889.png)

创建test组,将入用户

![image-20240929145513021](images\image-20240929145513021.png)

### 3.2.3 使用新用户登录

![image-20240929145704897](images\image-20240929145704897.png)

### 3.2.4 禁用和启用用户

**禁用用户**

![image-20240929145910942](images\image-20240929145910942.png)

![image-20240929145935215](images\image-20240929145935215.png)

**启用用户**

![image-20240929150023934](images\image-20240929150023934.png)

### 3.2.5 启用用户多因子认证功能

多因子认证Multi-Factor Authentication (MFA) 是一种简单有效的最佳安全实践方法，用户要通过两种 以上的认证机制之后，才能得到授权，使用计算机资源

JumpServer 启用 MFA 后，用户登录网站时，系统将要求输入用户名和密码（第一安全要素），然后要 求输入来自其 MFA 设备的动态验证码（第二安全要素），双因素的安全认证将为您的账户提供更高的安 全保护

#### 3.2.5.1 开启MFA

在用户列表中,对指定用户更新配置

![image-20240929150228523](images\image-20240929150228523.png)

![image-20240929150307469](images\image-20240929150307469.png)

#### 3.2.5.2 绑定手机APP

![image-20240929150356486](images\image-20240929150356486.png)

![image-20240929150429719](images\image-20240929150429719.png)

![image-20240929150701067](images\image-20240929150701067.png)

#### 3.2.5.3 重新登录验证

![image-20240929150741526](images\image-20240929150741526.png)

![image-20240929150823127](images\image-20240929150823127.png)

### 3.2.6 创建系统审计员

系统审计员即审计操作权限

![image-20240929151036989](images\image-20240929151036989.png)

## 3.3 管理资产

JumpServer 可以管理各种类型的资产

![image-20240929151419474](images\image-20240929151419474.png)

**JumpServer中的三种用户**

- 登录用户: 

  分配给用户用于登录JumpServer时使用

- 系统用户中的特权用户(管理用户): 

  对后端服务器具有管理权限的系统帐号 root或administrator 及sudo ALL权限的用户,用于管理后 端服务器

  新版中已取消此名称,改名为**系统用户中特权用户**

- 系统用户中的普通用户(系统用户): 

  给登录用户使用ssh连接后端服务器时对应的系统用户 ,一般是后端服务器的普通的系统用户帐号 

  新版中改名为**系统用户中普通用户**

### 3.3.1 创建管理用户(系统用户中特权用户)

管理用户是jumpServer用来管理后端服务器或其它资产的管理员用户,此用户必须对后端服务器有管理 权限

管理用户特点:

- 通常是后端服务器的root或者是具备root权限的超级用户
- 用于推送或者是创建系统用户
- 用于获取被管理的硬件资产信息

![image-20240929152213694](images\image-20240929152213694.png)

### 3.3.2 创建资产

创建可以被jumpServer用户访问的后端服务器和其它资产,比如:路由器,交换机等

#### 3.3.2.1 创建资产

![image-20240929152750596](images\image-20240929152750596.png)



![image-20240929153749089](images\image-20240929153749089.png)

#### 3 . 3 . 2 . 2  创 建 节 点 实 现 资 产 分 类

创 建 节 点 将 资 产 分 类

![image-20240929153903775](images\image-20240929153903775.png)

![image-20240929153959693](images\image-20240929153959693.png)

![image-20240929154215277](D:\云原生\JumpServer\images\image-20240929154215277.png)

## 3.4 授权管理

![image-20240929154624927](images\image-20240929154624927.png)

### 3.4.1 创建系统用户(系统用户中普通用户)

系统用户是分配给JumpServer用户,用来让JumpServer用户在连接后端服务器和其它资产,一般不会给管 理权限

生产环境中,一般都会利用自动化运维工具提前在后端服务器创建好系统用户,在所有后端服务器统一用户 ID信息,而非在jumpserver中创建

![image-20240929155051761](images\image-20240929155051761.png)

### 3.4.2 关联使用系统用户的资产

将前面创建的系统用户推送到后端服务器并自动创建

在系统用户中添加使用此用户的资产

![image-20240929155352294](images\image-20240929155352294.png)

测试可连接性

注意:连接性是利用系统用户进行连接的,所以之前必须先推送系统用户后才能测试连接

![image-20240929160220263](images\image-20240929160220263.png)



![image-20240929160340943](images\image-20240929160340943.png)

![image-20240929160517204](images\image-20240929160517204.png)



### 3.4.3 创建授权规则

通过授权规则, 为JumpServer用户分配可以访问的资产及使用的系统用户

![image-20240929161754978](images\image-20240929161754978.png)

### 3.4.4 测试登录访问后端服务器

然后用`development`用户组里面的wanglei用户登录，可以看到资产，并且可以登录上去

![image-20240929162236299](images\image-20240929162236299.png)

![image-20240929162319148](images\image-20240929162319148.png)

点右上角的web终端,可以打开终端界面

![image-20240929162350504](images\image-20240929162350504.png)

### 3.4.5 测试上传和下载文件

可以通过web方式或者通过filezilla等工具直接连接jumpserver的2222端口都可以实现文件的上传下载

**上传**

![image-20240929162846205](images\image-20240929162846205.png)

![image-20240929163017894](images\image-20240929163017894.png)

### 3.4.6 ssh连接JumpServer

JumpServer 还支持用户通过ssh连接其2222/tcp端口进行访问

连接方式：

```http
ssh -p 2222 user@jumpserver 
```

![image-20240929163904793](images\image-20240929163904793.png)

## 3.5 数据库授权

### 3.5.1 在后端服务器安装MySQL并创建数据库和用户

范例：Ubutun 2404

```bash
root@ubutun2204-1:~# apt -y install mysql-server

root@ubutun2204-1:~# sed -i '/127.0.0.1/s/^/#/' /etc/mysql/mysql.conf.d/mysqld.cnf

root@ubutun2204-1:~# systemctl restart mysql

root@ubutun2204-1:~# mysql
mysql> create database wordpress;
mysql> create user wordpress@'192.168.159.%' identified by '123456';
mysql> grant all on wordpress.* to wordpress@'192.168.159.%';
mysql> exit
Bye
```

### 3.5.2 创建数据库应用

![image-20240929164837179](images\image-20240929164837179.png)

![image-20240929165044757](images\image-20240929165044757.png)

### 3.5.3 创建数据库的系统用户

创建针对数据库的专用系统用户

**注意: 协议选择mysql**

![image-20240929165427080](images\image-20240929165427080.png)

### 3 . 5 . 4  创 建 数 据 库 授 权 规 则

授权管理-->资产授权

![image-20240929165721295](images\image-20240929165721295.png)

### 3.5.5 测试数据库连接

#### 3.5.5.1 web 方式连接MySQL资产

![image-20240929165825085](images\image-20240929165825085.png)

![image-20240929165900117](images\image-20240929165900117.png)

![image-20240929171238593](images\image-20240929171238593.png)

#### 3.5.5.2 用ssh连接MySQL资产

![image-20240929171436667](images\image-20240929171436667.png)

## 3.6 会话管理

会话管理可以实现查看当前在线的会话命令记录、历史会话过去的执行过的命令,也可以强制将用户踢出.z

只有具有审计员权限的才能进行会话管理

![image-20240929172126771](images\image-20240929172126771.png)

### 3.6.1 查看在线会话

![image-20240929172433597](images\image-20240929172433597.png)

### 3.6.2 查看历史会话

#### 3.6.2.1 在线回放

![image-20240929172533527](images\image-20240929172533527.png)

![image-20240929172605689](images\image-20240929172605689.png)

#### 3.6.2.2 离线查看录像

可以将历史会话过程下载再播放,但需要下载相关的播放器

```http
https://github.com/jumpserver/VideoPlayer/releases
```

![image-20240929172745436](images\image-20240929172745436.png)

![image-20240929172802767](images\image-20240929172802767.png)

### 3.6.3 查看命令历史

![image-20240929172856403](images\image-20240929172856403.png)

### 3.6.4 终端管理

可以在线监控用户正在进行的操作过程,甚至可以强制中断用户的连接,将其踢出会话

![image-20240929173151909](images\image-20240929173151909.png)

## 3.7 命令过滤器

使用命令过滤器可以禁止用户执行特定的危险命令,防止误操作或恶意行为

系统用户可以绑定一些命令过滤器，一个过滤器可以定义一些规则 当用户使用这个系统用户登录资产， 然后执行一个命令.这个命令需要被绑定过滤器的所有规则匹配，高优先级先被匹配， 当一个规则匹配到 了，如果规则的动作是允许，这个命令会被放行， 如果规则的动作是禁止，命令将会被禁止执行， 否则 就匹配下一个规则，如果最后没有匹配到规则，则允许执行

![image-20240929173232996](D:\云原生\JumpServer\images\image-20240929173232996.png)

### 3.7.1 创建命令过滤器

![image-20240929173427391](images\image-20240929173427391.png)

创建命令组

![image-20240929173524747](images\image-20240929173524747.png)

## 3.8 资产的批量导出和导入

当需要管理的后端服务器很多时,每台主机手动导入效率很低,可以利用资产的导出导入功能实现批量导 入,提高效率

### 3.8.1 资产的批量导出

![image-20240929173827438](images\image-20240929173827438.png)

![image-20240929173920698](images\image-20240929173920698.png)

### 3.8.2 批量导入资产

参考上面导出的文件格式,生成导入的文件,再批量导入资产

注意: 删除id列,修改主机名和IP字段,再导入

![image-20240929173920698](images\image-20240929173920698.png)

还需要将系统帐号推送到新添加的服务器

![image-20240929174049917](images\image-20240929174049917.png)



























