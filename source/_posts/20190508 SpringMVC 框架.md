---
title: 20190508 SpringMVC 框架
date: 2019-05-08
categories: ['后端']
tags: ['SpringMVC']
---

# 1 Spring MVC 概念

> SpringMVC 是 Spring 框架中一部分（子框架），是实现对 Servlet 技术进行封装。

## 1.1 MVC 介绍

MVC 全名是 Model View Controller  ，是模型 视图 控制的缩写，是一种软件设计典范，是一种软件架构设计分层模式

Model 模型 是应用程序中用于**处理数据**逻辑部分‘

View 视图 是应用程序**处理数据**显示的部分’

Controller 控制器 是应用程序处理**用户交互**的部分‘



例子： JSP + Servlet + Bean   分层开发



## 1.2 SpringMVC 运行原理

Dispatherservlet  中央控制器



## 1.3 第一个SpringMVC 项目

1. 新建JavaWeb 工程 ，导入 jar包 

   com.springsource.com.mchange.v2.c3p0-0.9.1.2.jar
   com.springsource.org.aopalliance-1.0.0.jar
   com.springsource.org.apache.commons.logging-1.1.1.jar
   com.springsource.org.apache.log4j-1.2.15.jar
   com.springsource.org.aspectj.weaver-1.6.8.RELEASE.jar
   junit-4.9.jar
   mysql-connector-java-5.1.30.jar
   spring-aop-4.1.6.RELEASE.jar
   spring-aspects-4.1.6.RELEASE.jar
   spring-beans-4.1.6.RELEASE.jar
   spring-context-4.1.6.RELEASE.jar
   spring-context-support-4.1.6.RELEASE.jar
   spring-core-4.1.6.RELEASE.jar
   spring-expression-4.1.6.RELEASE.jar
   spring-jdbc-4.1.6.RELEASE.jar
   spring-tx-4.1.6.RELEASE.jar
   spring-web-4.1.6.RELEASE.jar
   spring-webmvc-4.1.6.RELEASE.jar

   

2. 编写 web.xml ，配置中央调度器

   注意：配置中央调度器中 springmvc.xml 文件的配置

```java
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd" id="WebApp_ID" version="3.0">

	  <!-- 配置 SpringMVC 中央控制器 -->
	  <servlet>
	  		<servlet-name>SpringMVC</servlet-name>
	  	 	<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
	  	 	<!-- 配置SpringMVC.xml 的位置及名称 -->
	  	 	<init-param>
	  	 		<param-name>contextConfigLocation</param-name>
	  	 		<param-value>classpath:SpringMVC.xml</param-value>
	  	 	</init-param>
	  </servlet>
	  <servlet-mapping>
	  		<servlet-name>SpringMVC</servlet-name>
	  		<url-pattern>/</url-pattern>
	  </servlet-mapping>
	  
</web-app>
```

3. 编写 后台控制器

```java
package com.szxy.controller;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.web.servlet.ModelAndView;
import org.springframework.web.servlet.mvc.Controller;



public class MyController implements Controller{

	@Override
	public ModelAndView handleRequest(HttpServletRequest req,
			HttpServletResponse resp) throws Exception {
			//创建 ModelAndView 对象
			ModelAndView mv = new ModelAndView();
			//添加响应信息
			mv.addObject("msg", "HelloWorld");
			//设置逻辑视图
			mv.setViewName("/jsp/index.jsp");
			
			return mv;
	}
}
```

4. 编写  springmvc.xml 中注册 bean

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xmlns:tx="http://www.springframework.org/schema/tx"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
         http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/tx
        http://www.springframework.org/schema/tx/spring-tx.xsd
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop.xsd">
    
    <!-- 注册 MyController -->
    <bean id="/*.do" class="com.szxy.controller.MyController"></bean>

</beans>

```

5. 编写 jsp 

```html
<%@ page language="java" import="java.util.*" pageEncoding="UTF-8"%>
<%
String path = request.getContextPath();
String basePath = request.getScheme()+"://"+request.getServerName()+":"+request.getServerPort()+path+"/";
%>

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html>
  <head>
    <base href="<%=basePath%>">
    
    <title>My JSP 'index.jsp' starting page</title>
    
	<meta http-equiv="pragma" content="no-cache">
	<meta http-equiv="cache-control" content="no-cache">
	<meta http-equiv="expires" content="0">    
	<meta http-equiv="keywords" content="keyword1,keyword2,keyword3">
	<meta http-equiv="description" content="This is my page">
	<!--
	<link rel="stylesheet" type="text/css" href="styles.css">
	-->

  </head>
  
  <body>
    	${msg}  
  </body>
</html>

```

## 1.4  web.xml 中urlpathern 问题

- 配置 / 与 配置 /* 的区别

  / 拦截某个路径下的所有资源

  /* 拦截所有资源包括静态资源

- 静态资源无法访问的问题

1. 第一种解决方案

```xml
<?xml version="1.0" encoding="UTF-8"?>
	<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
	xmlns="http://java.sun.com/xml/ns/javaee" 
	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd" 
	id="WebApp_ID" version="3.0">
		
	  <!-- 第一种解决方案 -->
	  <servlet-mapping>
	  		<servlet-name>default</servlet-name>
	  		<url-pattern>*.png</url-pattern>
	  </servlet-mapping>		
	  <servlet-mapping>
	  		<servlet-name>default</servlet-name>
	  		<url-pattern>*.js</url-pattern>
	  </servlet-mapping>		
	  <servlet-mapping>
	  		<servlet-name>default</servlet-name>
	  		<url-pattern>*.css</url-pattern>
	  </servlet-mapping>		
		
	  <!-- 配置 SpringMVC 中央控制器 -->
	  <servlet>
	  		<servlet-name>SpringMVC</servlet-name>
	  	 	<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
	  	 	<!-- 配置SpringMVC.xml 的位置及名称 -->
	  	 	<init-param>
	  	 		<param-name>contextConfigLocation</param-name>
	  	 		<param-value>classpath:SpringMVC.xml</param-value>
	  	 	</init-param>
	  </servlet>
	  <servlet-mapping>
	  		<servlet-name>SpringMVC</servlet-name>
	  		<url-pattern>/</url-pattern>
	  </servlet-mapping>
	  
</web-app>
```

2. 第二种解决方案

```xml
<!-- 
	第二种 解决方案 
	在 springmvc.xml 文件中添加下面的标签 	
-->
<mvc:default-servlet-handler/>
```

3. 第三种解决方案

```xml
<!-- 第三种 解决方案 
	 在springmvc.xml 文件指定静态的位置及映射
-->
<mvc:resources location="/images/" mapping="/images/**"></mvc:resources>    
```

# 2  SpringMVC 注解开发

## 2.1 搭建环境

后台控制器不需要实现 Ctroller 接口，添加相应的注解

```java
package com.szxy.controller;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.servlet.ModelAndView;


//访问路径  http://localhost:8080/mvc/springmvc/hander

/**
 * 
 *  使用注解后台控制器
 *	不需要实现 Contrller 接口
 */
@Controller  	//将该后台控制器交给 spring 容器管理
@RequestMapping("/springmvc")   //指定命令空间
public class MyController{
	
	@RequestMapping("/hander")
	public ModelAndView handleRequest(HttpServletRequest req,
			HttpServletResponse resp) throws Exception {
			//创建 ModelAndView 对象
			ModelAndView mv = new ModelAndView();
			//添加响应信息
			mv.addObject("msg", "HelloWorld");
			//设置逻辑视图
			mv.setViewName("/jsp/index.jsp");
			
			return mv;
	}	
}

```



2. 在 配置 springmvc.xml 文档

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xmlns:tx="http://www.springframework.org/schema/tx"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
         http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/tx
        http://www.springframework.org/schema/tx/spring-tx.xsd
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop.xsd">
    
    <!-- 开启组件扫描器 -->
    <context:component-scan base-package="com.szxy.controller"></context:component-scan>
    
    <!-- 开启注解驱动 -->
    <mvc:annotation-driven />
    
	<mvc:default-servlet-handler/> 

</beans>

```

## 2.2   视图解析器

- springmvc.xml 配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xmlns:tx="http://www.springframework.org/schema/tx"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
         http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/tx
        http://www.springframework.org/schema/tx/spring-tx.xsd
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop.xsd">
    
    <!-- 开启组件扫描器 -->
    <context:component-scan base-package="com.szxy.controller"></context:component-scan>
    
    <!-- 开启注解驱动 
    	 自动注册 适配器、处理器
    -->
    <mvc:annotation-driven />  
    
    <!-- 注册视图解析器
    	 由 springmvc 调用，故不需要 设置 id 属性
     -->
    <bean 	class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    	<property name="prefix" value="/jsp/"></property>
    	<property name="suffix" value=".jsp"></property>
    </bean>
    
	<mvc:default-servlet-handler/> 

</beans>

```

- 后台控制器

```java
package com.szxy.controller;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.servlet.ModelAndView;



/**
 * 
 *  使用注解后台控制器
 *	不需要实现 Contrller 接口
 */
@Controller  	//将该后台控制器交给 spring 容器管理
@RequestMapping("/springmvc")   //指定命令空间
public class MyController{
	
	@RequestMapping("/hander")
	public String hello(){
		return "index";
	}

}

```

##  2.3 处理器方法常用的方法参数

- HttpServletRequest
- HttpServletResponse
- HttpSession
- 用于承载数据的Model 、Map、ModelMap
- 请求中携带的参数



## 2.4 接受请求参数

- #### 逐个接受请求参数

  @RequestParam  在方法名前使用

  应用场景：表示当表单属性名与方法参数名不一致的和接受集合方式的数据

- #### 使用对象整体接受 

  注意：对象属性名与表单属性名一致。

- #### 以域属性接受（也就是属性对象） 

  注意：表单中域属性的属性名填写方式 对象名.属性名 pattern.name

- #### 数组或集合的接受 @PathVaiable

  注意：以集合形式接受数据 (@RequestParam List<String>  arr)

- #### restful 风格传参  @PathVaiable

  (地址栏路径上带有参数 /hello/zhangsan/3）

  RequestMapping("/hello/{name}/{age}")

  注意: 在控制器方法名参数名前加上 @PathVaiable

- #### 接受 json 格式字符串 @RequestBody

  pathContext.request.contextPath

  contentType: application/json

  JSON.stringify()   //将 json对象转为 json字符串

  注意：要导入 json jar 包

  jackson-annotations-2.5.0.jar
  jackson-core-2.5.0.jar
  jackson-databind-2.5.0.jar

- #### 获取请求头的参数 @RequestHeader 

  

  - 测试类-控制器


  ```java
  package com.szxy.controller;
  
  import java.util.List;
  
  import org.springframework.stereotype.Controller;
  import org.springframework.web.bind.annotation.PathVariable;
  import org.springframework.web.bind.annotation.RequestBody;
  import org.springframework.web.bind.annotation.RequestHeader;
  import org.springframework.web.bind.annotation.RequestMapping;
  import org.springframework.web.bind.annotation.RequestParam;
  import org.springframework.web.servlet.ModelAndView;
  
  import com.szxy.pojo.Star;
  
  /**
   * 
   *	接受请求数据
   *
   *
   */
  @Controller
  @RequestMapping("/mvc")
  public class ReceviceDataFormRequest {
  	
  	//逐个接受请求参数
  	@RequestMapping("/formdata0")
  	public ModelAndView getFormData0(String uname,int age){
  		//创建 ModelAndView 对象
  		ModelAndView mv = new ModelAndView();
  		//添加响应信息
  		mv.addObject("uname", uname);
  		mv.addObject("age",age);
  		mv.setViewName("showData");
  		return mv;		
  	}
  	
  	//逐个接受请求参数2
  	@RequestMapping("/formdata1")    //更正接受参数名称
  	public ModelAndView getFormData1(@RequestParam("uname")String username,int age){
  		//创建 ModelAndView 对象
  		ModelAndView mv = new ModelAndView();
  		//添加响应信息
  		mv.addObject("uname", username);
  		mv.addObject("age",age);
  		mv.setViewName("showData");
  		return mv;		
  	}
  	
  	//通过对象整体接受
  	@RequestMapping("/formdata2")
  	public ModelAndView getFormData2(Star star){
  		//创建 ModelAndView 对象
  		ModelAndView mv = new ModelAndView();
  		//添加响应信息
  		mv.addObject("uname", star.getUname());
  		mv.addObject("age",star.getAge());
  		mv.setViewName("showData");
  		return mv;		
  	}
  	
  	//接受域属性数据
  	@RequestMapping("/formdata3")
  	public ModelAndView getFormData3(Star star){
  		//创建 ModelAndView 对象
  		ModelAndView mv = new ModelAndView();
  		//添加响应信息
  		mv.addObject("uname", star.getUname());
  		mv.addObject("age",star.getAge());
  		mv.addObject("pattern",star.getPattern().getName());
  		mv.setViewName("showData");
  		return mv;		
  	}
  	
  	//接受数组数据
  	@RequestMapping("/formdata4")
  	public void getFormData4(String[] hobbys){
  		for (String str : hobbys) {
  			System.out.println(str);
  		}
  	}
  	
  	//以集合方式接受多条数据
  	//注意：使用集合
  	@RequestMapping("/formdata5")
  	public void getFormData5(@RequestParam List<String> hobbys){
  		
  		for (String str : hobbys) {
  			System.out.println(str);
  		}
  	}
  	
  	//接受 restful 风格的数据  
  	// /getFormData6/zhangsan/12
  	@RequestMapping("/formdata6/{uname}/{age}")
  	public void getFormData6(@PathVariable String uname,@PathVariable int age){
  		
  		System.out.println(uname+"\t"+age);
  	}
  	
  	//接受 json 格式字符串数据
  	//注意：要导入 json jar包，不然包 415 服务器不能处理该类型的请求
  	@RequestMapping("/formdata7")
  	public void getFormData7(@RequestBody Star star){
  		
  		System.out.println(star.getUname()+"\t"+star.getAge());
  	}
  	
  	// 获取请求头信息
  	@RequestMapping("/formdata8")
  	public void getFormData8(@RequestHeader String host,@RequestHeader  String cookie){
  		
  		System.out.println(host+"\t"+cookie);
  	}
  
  }
  
  ```

  - 发送 ajax 请求

  ```html
  <script type="text/javascript" src="js/jquery-1.7.2.min.js"></script>
  	<script type="text/javascript">
  		$(function(){
  			$("#btn").click(function(){
  				// json 对象
  				var varJson = {
  						uname:"zhangsan",
  						age:31
  				};
  				
  				$.ajax({
  					url:"mvc/formdata7",
  					type:"POST",
  					contentType:"application/json", //以 json格式发送请求
  					data:JSON.stringify(varJson)  //将 json 对象转为 json格式的字符串
  				});
  			});
  		});
  	</script>
  ```

  

## 2.5 处理器方法返回值

- ModelAndView  承载数据和跳转视图资源
- String 返回值类型  
- void 无返回值类型
- Object  Object 返回值类型



#### String 类型返回值

- 使用 Model 、 Map 、ModelMap 承载数据
- 直接返回 json 字符串，添加注解@ReponseBody



#### Obejct 类型返回值

- 注解@ResponseBody
- 注册 springmvc 驱动 
- 导入 jackson 包



#### 解决中文乱码问题

​	在 @RequestMapping 注解中添加 produces = “text/html;charset=utf-8”

​	同时在方法前添加注解@ResponseBody



#### @ResponseBody 注解作用

- 将当前方法的返回值放到响应体中，并转成 json 格式

- 接受 json 格式的字符串，将该注解放在方法名参数前



```java
package com.szxy.controller;

import java.io.IOException;
import java.util.Map;
import javax.servlet.http.HttpServletResponse;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.ui.ModelMap;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
@RequestMapping("/return")
public class ReturningToView {
	
	//使用 Model 、 Map 、 ModelMap 承载数据
	@RequestMapping(value="/sendData1")
	public String  sendData(String username,int age,Model model,Map<String,Integer> map,ModelMap modelMap){
		
			//承载数据 
			model.addAttribute("username", username);
			map.put("age", age);
			modelMap.addAttribute("age1", age);
			
			return "showData";  //只写视图即可，前缀和后缀由视图解析器完成
	}
	
	//返回 json格式字符串
	@RequestMapping(value="/sendData2",produces="text/html;charset=utf-8") //解决响应中文乱码问题
	@ResponseBody      //作用：将当前方法的返回值放到响应体中，并转成 json 格式
	public String  sendData2(){
		
		return "{china:中国}"; 
	}
	
	// void 返回类型    
	@RequestMapping(value="/sendData3")
	public void sendData3(HttpServletResponse resp) throws IOException{
		resp.setContentType("text/html;charset=utf-8");
		String json = "{\"name\":\"张三\",\"age\":32}";
		resp.getWriter().print(json);
	}
	
	@RequestMapping(value="/sendData4")
	@ResponseBody   //作用：将当前方法的返回值放到响应体中，并转成 json 格式
	public Object sendData4(){
		return "aaa";
	}
	
}

```



## 2.6 请求转发与重定向

#### 请求转发（服务内部跳转）

springmvc 默认使用请求转发

- 请求转发到视图

``` java
setViewName("逻辑视图名")
```

- 请求转发给处理器

```java
return "forward:***.do";
```



#### 重定向（服务器外部跳转）

- 重定向到视图

springmvc 使用重定向，会将默认会将数据通过地址栏的方式传递物理视图

```java
setViewName("redirct:逻辑视图名")
//http://localhost:8080/mvc/jsp/showData.jsp?username=张三&age=123
//获取地址栏中的数据  
//${param.username}---${param.age}
```

- 重定向到处理器

注意：**前面不需要加斜杠**

```java
setViewName("redirct:处理器方法请求路径")
```

- 测试

```java
package com.szxy.controller;

import java.util.Map;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.servlet.ModelAndView;

@Controller
@RequestMapping("/redirect")
public class RedirctController {
	
	//请求转发到视图页面中
	@RequestMapping(value="/helloWord",produces="text/html;charset=utf-8")
	public ModelAndView testDispather(String username,int age){
		ModelAndView mv = new ModelAndView();
		//承载数据
		mv.addObject("username", username);
		mv.addObject("age",age);
		//采用默认的请求转发
		mv.setViewName("showData");
		return mv;
	}
	
	@RequestMapping(value="/helloWord4")
	public String testDispather2(String username,int age,Map<String,Object> map){
		map.put("username", username);
		map.put("age", age);
		System.out.println(map);
		return "forward:helloWorld5.do";
	}
	
	@RequestMapping(value="/helloWord5.do",produces="text/html;charset=utf-8")
	public void testDispather3(String username,int age){
			
			System.out.println(username+"\t"+age);
			
	}
	
	
	//重定向到视图页面
	@RequestMapping(value="/helloWord2",produces="text/html;charset=utf-8")
	public ModelAndView testRedirect(String username,int age){
		ModelAndView mv = new ModelAndView();
		//承载数据
		mv.addObject("username", username);
		mv.addObject("age",age);
		//采用重定向
		mv.setViewName("redirect:/jsp/showData.jsp");
		return mv;
	}
	
	// 重定向另一个处理器
	@RequestMapping(value="/helloWord3",produces="text/html;charset=utf-8")
	public ModelAndView testRedirect2(String username,int age){
		ModelAndView mv = new ModelAndView();
		//承载数据
		mv.addObject("username", username);
		mv.addObject("age",age);
		//采用重定向，到另一个处理器中
		mv.setViewName("redirect:helloWord");
		return mv;
	}
}

```

## 2.7 文件上传

要求：

- 注册 mvc 注解驱动

- **文件上传解析器**-   

  CommonsoMultipartRes

- 导入相关 jar 包

  com.springsource.org.apache.commons.fileupload-1.2.0.jar
  com.springsource.org.apache.commons.io-1.4.0.jar

#### form 表单修改上传类型

```html
<form action="file/fileUpload" method="post"  enctype="multipart/form-data" >
    图片<input type="file"  name="img"/><br />
    <input type="submit"  value="提交"/>
</form>
```

#### 后台控制器 ---上传文件

```java
package com.szxy.controller;

import java.io.File;
import java.util.HashMap;
import java.util.Map;

import javax.servlet.http.HttpSession;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.multipart.MultipartFile;

@Controller
@RequestMapping("/file")
public class FileUploadController {
		
		//单文件上传
		@RequestMapping(value="/fileUpload",method= RequestMethod.POST)
		public String fileUploadOne(MultipartFile img,Model model){
			//指定文件上传路径
			String path = "E:/";  //这里是服务器目录下
			//获取文件上传名,中文处理在 springmvc.xml 的文件上传解析器修改默认编码
			String fileName = img.getOriginalFilename();
			//上传文件
			File file = new File(path,fileName);
			//上传文件到服务器中 
			try {
				img.transferTo(file);
				model.addAttribute("fileName", fileName);
				model.addAttribute("flag", "上传成功");
			} catch (Exception e) {
				e.printStackTrace();
				model.addAttribute("flag", "上传失败");
			} 
			//返回视图界面
			return "showData";
		}
		
		//多文件上传
		//多文件上传，需采用 @RequestParam 自动修正参数
		@RequestMapping(value="/fileUpload2",method= RequestMethod.POST)
		public String fileUploadMany(@RequestParam MultipartFile imgs[],Model model,HttpSession session){
			//获取服务器上下文，找到 images 目录
			String path = session.getServletContext().getRealPath("/images");
			System.out.println("path="+path);
			//存储数据
			Map<String,String>  map = new HashMap<String,String>(); 
			//遍历文件
			for (MultipartFile img : imgs) {
				//获取文件上传名,中文处理在 springmvc.xml 的文件上传解析器修改默认编码
				String fileName = img.getOriginalFilename();
				//上传文件
				File file = new File(path,fileName);
				//上传文件到服务器中 
				try {
					img.transferTo(file);
					map.put("flag", "成功");
				} catch (Exception e) {
					e.printStackTrace();
					map.put("flag", "失败");
				} 
			}
			//Map 添加到 model 中
			model.addAllAttributes(map);
			//返回视图界面
			return "showData";
		}
	
}

```

#### 注册文件上传解析器

​	注意：文件上传解析器的 id 属性是由 DispatherServlet 中获取的。

​	因为文件上传解析器是由中央调度器 DispatherServlet 控制的  

​	记住：文件上传解析器的类名  CommonsMultipartResolver

```java
 <!-- 注册文件上传解析器 -->
  <bean id="multipartResolver"  
     class=" org.springframework.web.multipart.commons.CommonsMultipartResolver" >
```

#### 解决上传文件中文名乱码

​	在 springmvc.xml 中的文件上传解析器中，添加属性 defaultEncoding 为 utf-8

```xml
<!-- 注册文件上传解析器 -->
<bean id="multipartResolver"  
      class=" org.springframework.web.multipart.commons.CommonsMultipartResolver" >
    <!-- 处理中文乱码问题 -->	 
    <property name="defaultEncoding" value="utf-8"></property>
</bean>
```

#### 上传文件路径问题

```java
//获取服务器上下文，找到 images 目录
String path = session.getServletContext().getRealPath("/images");
```

#### 多文件上传参数问题

```http
HTTP Status 500 - Request processing failed; nested exception is org.springframework.beans.BeanInstantiationException: Failed to instantiate [[Lorg.springframework.web.multipart.MultipartFile;]: No default constructor found; nested exception is java.lang.NoSuchMethodException: [Lorg.springframework.web.multipart.MultipartFile;.<init>()
```

解决：

​	添加方法参数类型前添加注解 @RequestParam ，自动修正参数

​	`public String fileUploadMany(@RequestParam MultipartFile imgs[]; `



## 2.8  文件下载

- 使用返回值类型 ReponseEntity<byte[]>

```java
package com.szxy.controller;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.InputStream;

import javax.servlet.http.HttpSession;

import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.client.HttpStatusCodeException;

@Controller
@RequestMapping("/fileDownload")
public class FileDownLoadController {
	
	@RequestMapping("/download")
	public ResponseEntity<byte[]> downloadFile(HttpSession session) throws IOException{
		//要下载文件路径
		String path = session.getServletContext().getRealPath("/images");
		/*	String path = "d:/ab小情歌.jpg";*/
		//要下载文件对象
		File file = new File(path,"ab.png");
		//获取文件输入流对象
		InputStream is = new FileInputStream(file);
		//创建字节数组，数组大小根据  is 对象可用字节数指定
		byte[] body = new byte[is.available()];
		//将文件读字节数组
		is.read(body);
		//添加响应信息
		HttpHeaders headers = new HttpHeaders();
		//解决文件名文件乱码问题
		String fileName = file.getName();
		String fileDownloadName = new String(fileName.getBytes("utf-8"),"iso-8859-1");
		//以附件的形式发送给浏览器，并指定下载名称
		headers.add("Content-Disposition", "attatchment;filename="+fileDownloadName);
		//设置响应状态码
		HttpStatus statusCode = HttpStatus.OK;  //200  浏览器正常访问
		
		ResponseEntity<byte[]> responseEntity = 
				new ResponseEntity<byte[]>(body, headers, statusCode);
				
		return responseEntity;  
	}
}

```



## 2.9 自定义拦截器

要求：

-  实现 HandleInterceptor 接口 
- 注册拦截器  `<mvc:interceptores>`

拦截情况

- 拦截所有请求
- 拦截特定请求路径
- 放行请求路径
- 使用多个拦截器拦截的顺序

#### 后台拦截器

```java
package com.szxy.intercetor;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;

public class FirstInterceptor implements  HandlerInterceptor {

	//在服务器响应给浏览器数据之前拦截
	@Override
	public void afterCompletion(HttpServletRequest arg0,
			HttpServletResponse arg1, Object arg2, Exception arg3)
			throws Exception {
		// TODO Auto-generated method stub
			System.out.println("FirstInterceptor.afterCompletion() 执行！");
	}
	
	//在处理器方法执行之后拦截
	@Override
	public void postHandle(HttpServletRequest arg0, HttpServletResponse arg1,
			Object arg2, ModelAndView arg3) throws Exception {
		// TODO Auto-generated method stub
			System.out.println("FirstInterceptor.postHandle() 执行！");
	}

	//在处理器方法执行之前拦截
	@Override
	public boolean preHandle(HttpServletRequest arg0, HttpServletResponse arg1,
			Object arg2) throws Exception {
		System.out.println("FirstInterceptor.preHandle() 执行！");
		return true; // false 表示拦截对应请求，不交给对应 处理器处理   
					 //true 表示放行
	}
}
```



#### 注册拦截器 

```xml
<!-- 注册自定义拦截器 -->
<mvc:interceptors>
    <mvc:interceptor>
        <!-- 执行拦截器中拦截路径 -->
        <!-- <mvc:mapping path="/**"/> --><!-- 拦截所有 -->
        <!-- 方式1 ：执行指定路径的处理器方法  -->
        <!-- <mvc:mapping path="/mvc/formdata0" /> -->
        <!-- 方式2 ：执行指定路径的处理器方法  -->
        <mvc:mapping path="/**"/><!-- 拦截所有 -->
        <!-- 排除在拦截器之外，直接放行 -->
        <mvc:exclude-mapping path="/mvc/formdata1"/>
        <!-- 注册拦截器 -->
        <bean class="com.szxy.intercetor.HelloInterceptor"></bean>
    </mvc:interceptor>
    <mvc:interceptor>
        <mvc:mapping path="/**"/>
        <bean class="com.szxy.intercetor.FirstInterceptor"/>
    </mvc:interceptor>
    <mvc:interceptor>
        <mvc:mapping path="/**"/>
        <bean class="com.szxy.intercetor.SecondInterceptora"/>
    </mvc:interceptor>
</mvc:interceptors>

```

#### 使用多个拦截器拦截的顺序

- 在处理器执行之前，拦截器的顺序由springmvc.xml 声明自定义拦截器的顺序执行
- 在处理执行完成后。拦截器的顺序是从后往前执行
- 在服务器响应数据给客户端之前，拦截器的顺序是从后往前执行（一般情况）



## 2.10  Spring 与 SpringMVC  父子容器关系

- 在Spring 整体框架中，容器是核心思想，是用来管理 bean 的生命周期的。

- Spring 是父容器，SpringMVC 是子容器。

- SpringMVC 可以访问父容器中 注册的bean 对象，但是父容器不能访问子容器注册的 bean 对象。

  例如：SpringMVC  容器可以访问 Spring 容器中 dao 层、 service 层 中 bean 对象。



​	