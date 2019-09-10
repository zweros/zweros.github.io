---
title: 20190520 ZooKeeper
date: 2019-05-20
categories: ['后端']
tags: ['Zookeeper']
---

### ZooKeeper 简介

zookeeper 就是动物管理员，它是管理hadoop（大象）、Hive（蜜蜂）、ping（猪）

主要功能： 配置管理、名字服务、分布式锁、集群管理。

#### 配置管理

将之前分散的配置文件做集中式管理，Zookeeper 使用 Zab 这种一致性协议来提供一致性。

#### 名字服务

为服务提供统一的入口，方便管理记忆，类似于用DNS服务器管理IP地址与域名之间的映射关系。

#### 分布式锁

协调多个分布式进程之间的活动。注意：这里的锁与进程中的锁有区别，更加严谨

#### 集群管理

管理集群中节点的增加、删除、更新以及分配节点。

### Zookeeper 存储结构

#### ZNode

底层数据结构是树形结构

#### Znode 的节点类型

![](https://zookeeper.apache.org/doc/current/images/zknamespace.jpg)



### Zookeeper 安装

#### 单机版

##### 解压到  /usr 目录下

```shell
tar -zxf zookeeper.tar.gz
```

##### 修改 conf/zoo_samiple.cfg

复制 zoo_sample.cfg 并重命名为zoo.cfg

```shell
#dataDir=/tmp/zookeeper
dataDir=/usr/zookeeper/data
```

##### 启动  Zookeeper

```shell
#默认加载 conf 目录下的 zoo.cfg 配置文件
./zkServer.sh start
#指定加载 conf 目录下的 **.cfg 配置文件
./zkServer.sh start **.cfg
```

#### 集群版

##### 集群角色

leader  

fellower

![](https://zookeeper.apache.org/doc/current/images/zkservice.jpg)

##### 集群安装

创建标识符文件 myid

```shell
#将标识符写入 myid 文件中，若 myid 文件不存在则创建该文件
[root@localhost zookeeperCluster]# echo 1 >> zookeeper01/data/myid
```

配置 zoo.cfg 

```shell
#2881、2882、2883 是投票端口
#3881、3882、3883 是选举端口
server.1=192.168.170.4:2881:3881
server.2=192.168.170.4:2882:3882
server.3=192.168.170.4:2883:3883
```

开启集群脚本 startall.sh

```shell
./zookeeper01/bin/zkServer.sh start
./zookeeper02/bin/zkServer.sh start
./zookeeper03/bin/zkServer.sh start
```

开启集群

```shell
[root@localhost zookeeperCluster]# ./startall.sh 
JMX enabled by default
Using config: /usr/zookeeperCluster/zookeeper01/bin/../conf/zoo.cfg
Starting zookeeper ... STARTED
JMX enabled by default
Using config: /usr/zookeeperCluster/zookeeper02/bin/../conf/zoo.cfg
Starting zookeeper ... STARTED
JMX enabled by default
Using config: /usr/zookeeperCluster/zookeeper03/bin/../conf/zoo.cfg
Starting zookeeper ... STARTED
```

开启集群成功的状态信息

```shell
[root@localhost zookeeperCluster]# ./statusAll.sh 
JMX enabled by default
Using config: /usr/zookeeperCluster/zookeeper01/bin/../conf/zoo.cfg
Mode: follower
JMX enabled by default
Using config: /usr/zookeeperCluster/zookeeper02/bin/../conf/zoo.cfg
Mode: leader
JMX enabled by default
Using config: /usr/zookeeperCluster/zookeeper03/bin/../conf/zoo.cfg
Mode: follower
```

### ZooKeeper 常用命令

#### 客户端常用命令工具使用 

```shell
./zkCli.sh            #启动 zookeeper  客户端概念股将
create /path          #持久节点
create -e /path data  #临时节点 
create -s /path  data #顺序持久及数据
```

##### simple API

- *create* : creates a node at a location in the tree
- *delete* : deletes a node
- *exists* : tests if a node exists at a location
- *get data* : reads the data from a node
- *set data* : writes data to a node
- *get children* : retrieves a list of children of a node
- *sync* : waits for data to be propagated

```shell
ls /      
get path  #查看节点信息
set  path data[version] 
delete  path   #删除节点
rmr path  #删除节点即子节点
quit  

```

