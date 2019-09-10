---
title: 20190610 HttpClient
date: 2019-06-10
categories: ['前端']
tags: ['HttpClient']
---

# 1 HttpClient 简介

支持 HttpClient 客户端工具的使用

# 2 使用 HttpClient 

新建 Maven 的 jar 工程，修改 pom.xml 文件

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.szxy</groupId>
	<artifactId>HttpClientDemo</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<dependencies>
		<dependency>
			<groupId>org.apache.httpcomponents</groupId>
			<artifactId>httpclient</artifactId>
			<version>4.3.5</version>
		</dependency>
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>4.10</version>
			<scope>test</scope>
		</dependency>
	</dependencies>
</project>
```

## 2.1 Get 请求不带参

```java
@Test
public void doGet() throws Exception{
    //创建  HttpClient 连接对象
    CloseableHttpClient client = HttpClients.createDefault();
    //创建 Get 请求
    HttpGet get = new HttpGet("http://www.baidu.com");
    //发送 请求，获取响应
    CloseableHttpResponse resp = client.execute(get);
    //获取响应行的中状态码 
    int statusCode = resp.getStatusLine().getStatusCode();
    System.out.println(resp.getStatusLine());
    System.out.println(statusCode);
    System.out.println(resp.getStatusLine().getProtocolVersion());
    System.out.println(resp.getStatusLine().getReasonPhrase());
    //获取响应实体
    HttpEntity entity = resp.getEntity();
    //解析响应实体
    String str = EntityUtils.toString(entity, "utf-8");
    System.out.println(str);
    //关闭连接
    client.close();
}
```

## 2.2 Get 请求带参

```java
/**
	 * 请求带参数
	 * @throws Exception 
	 */
	@Test
	public void doGETWithParam() throws Exception{
		CloseableHttpClient client = HttpClients.createDefault();
		//创建 URIBuider 对象
		URIBuilder builder = new URIBuilder("https://www.sogou.com/web");
		//添加参数
		builder.addParameter("query", "1");
		//创建 Get 请求
		HttpGet get = new HttpGet(builder.build());
		//设置请求头
		get.setHeader("User-Agent",
"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/74.0.3729.169 Safari/537.36");
		//发送请求并响应返回结果
		CloseableHttpResponse resp = client.execute(get);
		//获取状态行
		System.out.println(resp.getStatusLine());
		//获取响应实体
		HttpEntity entity = resp.getEntity();
		String html = EntityUtils.toString(entity,"utf-8");
		System.out.println(html);	
	}
```

## 2.3  Post 请求不带参

```java
/**
	 *   post 请求不参数
	 * @throws Exception 
	 * @throws ClientProtocolException 
	 */
@Test
public void doPost() throws ClientProtocolException, Exception{
    //创建 HttpClient 对象连接
    CloseableHttpClient client = HttpClients.createDefault();
    //创建 POST 请求对象
    HttpPost post = new HttpPost("http://localhost:8080/test/post");
    //设置请求头
    //post.setHeader("accept", "*/*");
    //发送 post 请求并返回执行结果
    CloseableHttpResponse resp = client.execute(post);
    //获取响应行信息
    System.out.println(resp.getStatusLine());
    //获取响应实体
    HttpEntity entity = resp.getEntity();
    //以 utf-8 编码解析响应实体
    String str = EntityUtils.toString(entity, "utf-8");
    System.out.println(str);
}
```

## 2.4 Post 请求带参

```java
/**
	 *   post 请求带参数
	 * @throws Exception 
	 * @throws ClientProtocolException 
	 */
@Test
public void doPostWithParm() throws ClientProtocolException, Exception{
    //创建 HttpClient 对象连接
    CloseableHttpClient client = HttpClients.createDefault();
    //创建 POST 请求对象
    HttpPost post = new HttpPost("http://localhost:8080/test/post/param");
    //携带post 请求参数
    List<BasicNameValuePair> list = new ArrayList<>();
    list.add(new BasicNameValuePair("name", "笑笑"));
    list.add(new BasicNameValuePair("pwd", "123"));
    //封装 post 请求参数
    StringEntity encodedFormEntity = new UrlEncodedFormEntity(list,"utf-8");
    //添加 post 请求实体
    post.setEntity(encodedFormEntity);
    //发送 post 请求并返回执行结果
    CloseableHttpResponse resp = client.execute(post);
    //获取响应行信息
    System.out.println(resp.getStatusLine());
    //获取响应实体
    HttpEntity entity = resp.getEntity();
    //以 utf-8 编码解析响应实体
    String str = EntityUtils.toString(entity, "utf-8");
    System.out.println(str);
}

```

## 2.5  Post 请求使用 Json格式

```java
/**
	 *   post 请求带参数
	 * @throws Exception 
	 * @throws ClientProtocolException 
	 */
	@Test
	public void doPostWithParm() throws ClientProtocolException, Exception{
		//创建 HttpClient 对象连接
		CloseableHttpClient client = HttpClients.createDefault();
		//创建 POST 请求对象
		HttpPost post = new HttpPost("http://localhost:8080/test/post/param");
		//携带post 请求参数
		List<BasicNameValuePair> list = new ArrayList<>();
		list.add(new BasicNameValuePair("name", "笑笑"));
		list.add(new BasicNameValuePair("pwd", "123"));
		//封装 post 请求参数
		StringEntity encodedFormEntity = new UrlEncodedFormEntity(list,"utf-8");
		//添加 post 请求实体
		post.setEntity(encodedFormEntity);
		//发送 post 请求并返回执行结果
		CloseableHttpResponse resp = client.execute(post);
		//获取响应行信息
		System.out.println(resp.getStatusLine());
		//获取响应实体
		HttpEntity entity = resp.getEntity();
		//以 utf-8 编码解析响应实体
		String str = EntityUtils.toString(entity, "utf-8");
		System.out.println(str);
	}
	
```



## 3 HttpClientUtils 工具类

```java
package com.szxy.commons;

import java.io.IOException;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Map.Entry;
import java.util.Set;

import org.apache.http.HttpEntity;
import org.apache.http.client.entity.UrlEncodedFormEntity;
import org.apache.http.client.methods.CloseableHttpResponse;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.client.methods.HttpPost;
import org.apache.http.client.utils.URIBuilder;
import org.apache.http.entity.ContentType;
import org.apache.http.entity.StringEntity;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClients;
import org.apache.http.message.BasicNameValuePair;
import org.apache.http.util.EntityUtils;
import org.junit.Test;

/**
 * 
 * HttpClient 工具类
 * 提供 Get、Post 请求方法及发送 json 格式的请求
 *  
 */
public class HttpClientUtil {

	public static String doGet(String url,Map<String,String> params){
		//创建 HttpClient 的客户端对象
		CloseableHttpClient client = HttpClients.createDefault();
		HttpGet get = null;
		String resultEntity = "";
		CloseableHttpResponse resp = null;
		try {
			if(params != null){
				URIBuilder builder = new URIBuilder(url);
				Set<Entry<String, String>> set = params.entrySet();
				for (Entry<String, String> entry : set) {
					builder.addParameter(entry.getKey(), entry.getValue());
				}
				get= new HttpGet(builder.build());
			}else{
				get = new HttpGet(url);
			}
			//设置请求参数
			get.setHeader("User-Agent",
					"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/74.0.3729.169 Safari/537.36");
			resp = client.execute(get);
			HttpEntity entity = resp.getEntity();
			resultEntity = EntityUtils.toString(entity, "utf-8");
		} catch (Exception e) {
			e.printStackTrace();
		}finally{
			if(client !=null){
				try {
					client.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
		}
		return resultEntity;
	}
	
	public static String doGet(String url){
		return doGet(url,null);
	}
	
	public static String doPost(String url,Map<String,String> params){
		CloseableHttpClient client = HttpClients.createDefault();
		HttpPost post = null;
		UrlEncodedFormEntity formEntity = null;
		CloseableHttpResponse resp = null;
		String resultEntity = "";
		try {
			post = new HttpPost(url);
			if(params != null){
				List<BasicNameValuePair> list = new ArrayList<>();
				Set<Entry<String, String>> set = params.entrySet();
				for (Entry<String, String> entry : set) {
					list.add(new BasicNameValuePair(entry.getKey(),entry.getValue()));
				}
				formEntity = new UrlEncodedFormEntity(list);
				//放入 post 请求主体中
				post.setEntity(formEntity);
			}
			resp = client.execute(post);
			HttpEntity entity = resp.getEntity();
			resultEntity = EntityUtils.toString(entity, "utf-8");
		} catch (Exception e) {
			e.printStackTrace();
		}finally{
			if(client != null){
				try {
					client.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
		}
		return resultEntity;
	}
	
	public static String doPost(String url){
		return doPost(url,null);
	}
	
	public static String doPostJson(String url,String json){
		CloseableHttpClient client = HttpClients.createDefault();
		HttpPost post = null;
		CloseableHttpResponse resp = null;
		String resultEntity = "";
		try {
			post = new HttpPost(url);
			//指定请求实体的类型
			StringEntity stringEntity = new StringEntity(json,ContentType.APPLICATION_JSON);
			post.setEntity(stringEntity);
			resp = client.execute(post);
			HttpEntity entity = resp.getEntity();
			resultEntity = EntityUtils.toString(entity, "utf-8");
		} catch (Exception e) {
			e.printStackTrace();
		}finally{
			if(client != null){
				try {
					client.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
		}
		return resultEntity;
	}
	
	
	//--------------------------------------------------------
    //		 测试工具类 											 *
	//--------------------------------------------------------
	@Test
	public void doGetDemo(){
		String url = "https://www.sogou.com/web";
		Map<String,String> params = new HashMap<>();
		params.put("query", "HH");
		String str = HttpClientUtil.doGet(url, params);
		System.out.println(str);
	}
	
	@Test
	public void doGetDemo2(){
		String url = "http://www.baidu.com";
		String str = HttpClientUtil.doGet(url);
		System.out.println(str);
	}
	
	@Test 
	public void doPostDemo(){
		String url = "http://localhost:8080/test/post/param/";
		Map<String,String> params = new HashMap<>();
		params.put("name", "HttpClientUtils");
		params.put("pwd", "123");
		String str = HttpClientUtil.doPost(url, params);
		System.out.println(str);
	}
	
	@Test 
	public void doPostJsonDemo(){
		String url = "http://localhost:8080/user/addUser";
		String json = "{\"userid\":6,\"username\":\"admin\",\"userage\":\"123\"}";
		String user = HttpClientUtil.doPostJson(url, json);
		System.out.println(user);
		
	}
}

```

# 3 HTTPClient 的 API

| 方法名                                                       | 功能                      |
| ------------------------------------------------------------ | ------------------------- |
| HttpClients.createDefault()                                  | 创建默认的 ttpClient 对象 |
| public HttpGet(final String uri)                             | 创建 HttpGet 请求         |
| public HttpPost(final String uri)                            |                           |
| public StringEntity(final String string, final ContentType contentType) |                           |
| public URIBuilder(final String string)                       |                           |
| public UrlEncodedFormEntity (final List <? extends NameValuePair> parameters) |                           |
|                                                              |                           |

# 4 HttpClient 实战

## 4.1  需求

创建 client 和  server

实现添加用户和查询用户的操作

![](http://img.zwer.xyz/blog/20190612150903.png)

## 4.2 实施

### Server 端

#### pom.xml 

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>com.szxy</groupId>
		<artifactId>parent</artifactId>
		<version>0.0.1-SNAPSHOT</version>
	</parent>
	<groupId>com.szxy</groupId>
	<artifactId>Service</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>war</packaging>
	<dependencies>
		<dependency>
			<groupId>com.szxy</groupId>
			<artifactId>commons</artifactId>
			<version>0.0.1-SNAPSHOT</version>
		</dependency>
		<!-- 单元测试 -->
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
		</dependency>
		<!-- 日志处理 -->
		<dependency>
			<groupId>org.slf4j</groupId>
			<artifactId>slf4j-log4j12</artifactId>
		</dependency>
		<!-- Mybatis -->
		<dependency>
			<groupId>org.mybatis</groupId>
			<artifactId>mybatis</artifactId>
		</dependency>
		<dependency>
			<groupId>org.mybatis</groupId>
			<artifactId>mybatis-spring</artifactId>
		</dependency>
		<!-- MySql -->
		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
		</dependency>
		<!-- 连接池 -->
		<dependency>
			<groupId>com.alibaba</groupId>
			<artifactId>druid</artifactId>
		</dependency>
		<!-- Spring -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-context</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-beans</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-webmvc</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-jdbc</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-aspects</artifactId>
		</dependency>
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>servlet-api</artifactId>
			<scope>provided</scope>
		</dependency>
	</dependencies>
	<build>
		<resources>
			<resource>
				<directory>src/main/java</directory>
				<includes>
					<include>**/*.xml</include>
				</includes>
			</resource>
			<resource>
				<directory>src/main/resources</directory>
				<includes>
					<include>**/*.xml</include>
					<include>**/*.properties</include>
				</includes>
			</resource>
		</resources>
		<!-- tomcat插件，由于子项目不一定每个都是web项目，所以该插件只是声明，并未开启 -->
			<plugins>
				<!-- 配置Tomcat插件 -->
				<plugin>
					<groupId>org.apache.tomcat.maven</groupId>
					<artifactId>tomcat7-maven-plugin</artifactId>
					<configuration>
						<port>8080</port>
						<path>/</path>
					</configuration>
				</plugin>
			</plugins>
	</build>
</project>
```

#### UserController.java

```java
package com.szxy.web.controller;

import java.util.HashMap;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.ResponseBody;

import com.szxy.pojo.Users;
import com.szxy.service.UserService;

@Controller
@RequestMapping("/user")
public class UserController {

	@Autowired
	private UserService userService;
	
	@RequestMapping(value="/addUser",method=RequestMethod.POST)
	@ResponseBody
	public Object addUser(@RequestBody Users user){//@RequestBody 将 json格式数据，封装成 User 对象
		//System.out.println(user);
		HashMap<String,Integer> map = new HashMap<>();
		try {
			this.userService.addUser(user);
			map.put("code", 200);
		} catch (Exception e) {
			e.printStackTrace();
			map.put("code", 500);
		}
		return map;
	}
	
	@RequestMapping("/findAllUser")
	@ResponseBody
	public Object findAllUser(){
		List<Users> users = this.userService.findAllUser();
		return users;
	}	
}
```

#### UserService.java

```java
package com.szxy.service;

import java.util.List;

import com.szxy.pojo.Users;

public interface UserService {
	
	public void addUser(Users user);
	
	public List<Users> findAllUser();
	
}

```

#### UserServiceImpl.java

```java
package com.szxy.service.impl;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.szxy.mapper.UserMapper;
import com.szxy.pojo.Users;
import com.szxy.service.UserService;

@Service
public class UserServiceImpl implements UserService {

	@Autowired
	private UserMapper userMapper;
	
	@Override
	public void addUser(Users user) {
		this.userMapper.insertUser(user);
	}

	@Override
	public List<Users> findAllUser() {
		return this.userMapper.selectAllUsers();
	}

}
```

### Client 端

#### pom.xml

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>com.szxy</groupId>
		<artifactId>parent</artifactId>
		<version>0.0.1-SNAPSHOT</version>
	</parent>
	<artifactId>Client</artifactId>
	<packaging>war</packaging>
	<dependencies>
		<dependency>
			<groupId>com.szxy</groupId>
			<artifactId>commons</artifactId>
			<version>0.0.1-SNAPSHOT</version>
		</dependency>
		<!-- 单元测试 -->
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
		</dependency>
		<!-- 日志处理 -->
		<dependency>
			<groupId>org.slf4j</groupId>
			<artifactId>slf4j-log4j12</artifactId>
		</dependency>
		<!-- Spring -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-context</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-beans</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-webmvc</artifactId>
		</dependency>
		<dependency>
			<groupId>jstl</groupId>
			<artifactId>jstl</artifactId>
		</dependency>
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>servlet-api</artifactId>
			<scope>provided</scope>
		</dependency>
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>jsp-api</artifactId>
			<scope>provided</scope>
		</dependency>
	</dependencies>
	<build>
		<!-- tomcat插件，由于子项目不一定每个都是web项目，所以该插件只是声明，并未开启 -->
		<plugins>
			<!-- 配置Tomcat插件 -->
			<plugin>
				<groupId>org.apache.tomcat.maven</groupId>
				<artifactId>tomcat7-maven-plugin</artifactId>
				<configuration>
					<port>8081</port>
					<path>/</path>
				</configuration>
			</plugin>
		</plugins>
	</build>
</project>
```

#### UserController.java

```java
package com.szxy.web.controller;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

import com.szxy.pojo.Users;
import com.szxy.service.UserService;

@Controller
@RequestMapping("/user")
public class UserController {
	
	@Autowired
	private UserService userService;
	
	@RequestMapping("/addUser")
	public String addUser(Users user){
		//System.out.println("user:"+user);
		this.userService.addUser(user);
		return "ok";
	}
	
	@RequestMapping("/showUser")
	public String showUser(Model model){
		List<Users> users = this.userService.findAllUser();
		model.addAttribute("users", users);
		return "showUser";
	}
}

```

#### UserService.java

```java
package com.szxy.service;

import java.util.List;

import com.szxy.pojo.Users;

public interface UserService {
		
	public void addUser(Users user);

	public List<Users> findAllUser();
	
}
```

#### UserServiceImpl.java

```java
package com.szxy.service.impl;

import java.util.List;
import java.util.Map;

import org.springframework.stereotype.Service;

import com.szxy.commons.HttpClientUtil;
import com.szxy.commons.JsonUtils;
import com.szxy.pojo.Users;
import com.szxy.service.UserService;

@Service
public class UserServiceImpl implements UserService {

	@Override
	public void addUser(Users user) {
		String url = "http://localhost:8080/user/addUser";
		String json = JsonUtils.objectToJson(user);
	    String resultJson = HttpClientUtil.doPostJson(url, json);
	    Map<String,Integer> map = JsonUtils.jsonToPojo(resultJson, Map.class);
	    Integer code = map.get("code");
	    if(code == 200){
	    	System.out.println("添加成功");
	    }else if(code == 500){
	    	System.out.println("添加失败");
	    }
	}

	@Override
	public List<Users> findAllUser() {
		String url = "http://localhost:8080/user/findAllUser";
		String str = HttpClientUtil.doPost(url);
		List<Users> users = JsonUtils.jsonToList(str, Users.class);
		return users;
	}
}

```

### 注意

在 springmvc 中使用 @RequestBody 注解用于将 json 格式数据转化为可以接受到的请求数据的格式