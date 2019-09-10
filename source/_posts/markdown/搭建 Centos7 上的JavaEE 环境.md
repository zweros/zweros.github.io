---
title: 在 Centos 7 上搭建JavaEE 环境
---

# Mysql 安装

> CentOS7 上有带有 MariaDB ，而不是 mysql

解决方案：

```shell
#如果必须要安装MySQL，首先必须添加mysql社区repo通过输入命令：
sudo rpm -Uvh http://dev.mysql.com/get/mysql-community-release-el7-5.noarch.rpm
#最后使用像安装MySQL的常规方法一样安装mysql：
yum install mysql mysql-server mysql-libs mysql-server
```

### 在线安装

```shell
　yum -y install mysql-server
```

### 设置权限

```shell
mysql>grant all privileges on *.* to 'root'@'%' identified by 'admin';
mysql>grant all privileges on *.* to 'root'@'localhost' identified by 'admin';  
#刷新权限
mysql> flush privileges;  
```

### 删除 Mysql 

```shell
#删除mysql(安装出错时再执行)
yum remove mysql mysql-server mysql-libs compat-mysql51  
rm -rf /var/lib/mysql  
rm /etc/my.cnf

#查看是否存在mysql(安装出错时再执行)
rpm -qa|grep mysql  //有的话继续删除  
rpm -ql mysql       //查看文件位置
```

# JDK 下载与安装

### 下载

从官网上下载，tar.gz 格式的 JDK 文件，然后通过 ftp 软件发给 远程终端

### 解压

```shell
tar -zxf  jdk的位置
```

### 配置 JDK 环境变量

```shell
[root@localhost java]# vi ~/.bashrc
export JAVA_HOME=/opt/java/jdk1.7.0_71
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
export PATH=${JAVA_HOME}/bin:$PATH
```

### 使环境变量生效

```shell
source ~/.bashrc
```

# Tomcat 服务器的下载与使用 

> 注意 ：web.xml 和 server.xml的 配置，以及设置环境变量

## 1 Tomcat 下载与安装

上传 tomcat 压缩包到 linxu 上

解压 tomcat 压缩包，并移动到  /usr/local 目录下

## 2 配置 Tomcat 环境变量

```shell
vim ~/.bashrc
#添加下面语句 
#指定 tomcat 的位置
export CATALINA_HOME=/opt/tomcat
#使环境变量生效
source ~/.bashrc
```

## 3 Tomcat 使用

1. 开启服务器

```shell
./startup.sh

或者

./catalina.sh run   //这种启动可以看到详细的启动信息
```

2. 关闭服务器

```shell
./shutdown.sh
```

# tomcat 服务器启动非常慢问题

- 找到 jdk 安装目录下   `jdk1.8.0_171/jre/lib/security/java.security` 文件

```shell
//修改前
securerandom.source=file:/dev/random
//修改后
securerandom.source=file:/dev/./urandom
```

- 保存文件，去除 tomcat 进程，重启 tomcat 服务器



# 项目中文乱码问题

> 注意：mysql 中 服务器的编码格式。在mysql 中默认的编码格式是 latin

## 1 Tomcat中的配置

- 修改Tomcat 下  web.xml 文件

```xml
<filter>
    <filter-name>setCharacterEncodingFilter</filter-name>
    <filter-class>
        	org.apache.catalina.filters.SetCharacterEncodingFilter
    </filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </init-param>
    <async-supported>true</async-supported>
</filter>
```

## 2 Mysql 中 my.cnf 文件的配置

```shell
vi /etc/my.cnf   
```

在 [mysqld] 后面加上下面的语句

```shell
character-set-server = utf8
```

# 参考博客

[Linux 下搭建 JavaEE 环境]: https://www.cnblogs.com/qlqwjy/p/7465279.html#undefined

