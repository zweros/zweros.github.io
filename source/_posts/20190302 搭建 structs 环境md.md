---
title: 搭建 structs 环境
date: 2019-3-2
---



# 前言

> 环境:  window 10 ,JDK 1.8  ,Tomcat 7 ,MyEclipse 2014 pro

# 搭建 SSH 环境的步骤

1. 创建 JavaWeb 项目

2. 导入 structs2 的jar包，只需导入13个基础 jar 包即可，后续 jar 包根据需要导入。

   asm-3.3.jar
   asm-commons-3.3.jar
   asm-tree-3.3.jar
   commons-fileupload-1.3.1.jar
   commons-io-2.2.jar
   commons-lang3-3.2.jar
   freemarker-2.3.22.jar
   javassist-3.11.0.GA.jar
   log4j-api-2.2.jar
   log4j-core-2.2.jar
   ognl-3.0.6.jar
   struts2-core-2.3.24.jar
   xwork-core-2.3.24.jar

3. web.xml 配置  structs2 核心过滤器（很重要）。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
            xmlns="http://java.sun.com/xml/ns/javaee" 
            xmlns:web="http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" 
            xsi:schemaLocation="http://java.sun.com/xml/ns/javaee 
                                http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd" 
            version="3.0">
     <filter>
       <filter-name>struts2</filter-name>
       <filter-class>org.apache.struts2.dispatcher.ng.filter.StrutsPrepareAndExecuteFilter</filter-class>
     </filter>
     <filter-mapping>
       <filter-name>struts2</filter-name>
       <url-pattern>/*</url-pattern>
     </filter-mapping>
     <welcome-file-list>
       <welcome-file>index.jsp</welcome-file>
     </welcome-file-list>
   </web-app>
   ```

   

4. 定义处理用户请求的 Action 类

```java
package cn.itcast.action;
import com.opensymphony.xwork2.ActionSupport;
public class HelloWorldAction extends ActionSupport{	
	public String execute() throws Exception {
		return SUCCESS;
	}
}
```

在项目目录 src 下，新建一个 structs.xml，书写下面的代码。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- 指定Struts2配置文件的DTD信息 -->
<!DOCTYPE struts PUBLIC
	"-//Apache Software Foundation//DTD Struts Configuration 2.3//EN"
	"http://struts.apache.org/dtds/struts-2.3.dtd">
<!-- Struts2配置文件的根元素 -->
<struts>
  <!-- Struts2的Action必须放在指定的包空间下定义 -->
  <package name="hello" extends="struts-default" namespace="/*">
    <!-- 定义 action，该action对应的类为cn.itcast.action.HelloWorldAction类 
    -->
    <action name="helloWorld" class="cn.itcast.action.HelloWorldAction">
      <!-- 定义处理结果和视图资源之间的映射关系 -->
      <result name="success">/success.jsp</result>
    </action>
  </package>
</struts>
```



5. 创建访问视图 

   1. index.jsp

   ```jsp
   <%@ page language="java" contentType="text/html; charset=UTF-8"
      pageEncoding="UTF-8"%>
   <html>
   	<head>
   		<title>首页</title>
   </head>
   	<body>
   		<h1>Welcome To Struts 2!</h1>
   		<a href="${pageContext.request.contextPath }/helloWorld.action">
      		Hello World
   		</a>
   	</body>
   </html>
   
   ```

   2. success.jsp

   ```jsp
   <%@ page language="java" import="java.util.*" pageEncoding="UTF-8"%>
   <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
   <html>
   	<head>
   		<title>成功页面</title>
   	</head>
   	<body>
   		欢迎学习第一个Struts2程序！
   	</body>
   </html>
   
   ```

   

6. 效果图

![](https://img2018.cnblogs.com/blog/1569987/201903/1569987-20190302183446846-1844507426.gif)

# 总结

> 注意别忘记在 web.xml 里配置 structs2 核心过滤器。
>
> HelloAction 类继承 ActionSupport 要覆写父类的 execute 方法。
>
> execute 方法中返回值 `SUCCESS` 是常量。