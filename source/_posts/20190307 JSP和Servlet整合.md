---
title: 'JSP 和 Servlet 整合'
date: 2019-3-7
categories: ['后端']
---

# 1 登录模块套用

## 1.1 添加插件

> 添加前端书写插件，把插件放在 MyEclipse 的安装目录中 drops 文件中，然后重启
>
> MyElipse，即可使用前端书写快捷键 `Ctrl+E`



## 1.2 套用登录模块

> 先创建一个 JSP 页面，然后剪切 `<base href="<%=basePath%>">`
>
> 复制 模块.html 中的代码到 JSP界面。



# 2 项目系统分析

项目名称：

​	后台管理系统

项目需求：

​	实现用户登录

​	实现用户退出

​	实现用户注册

功能分析

​	用户登录

​	用户退出

​	用户注册

数据库设计

​	用户表

​		字段

```sql
create database project;
create table t_user(
	uid int not null auto_increment,
    pwd String varchar(50) not null,
    name varchar(20) not null,
    age int(3) not null,
    sex varchar(10) not null,
    birthday date not null
)engine=INoDB,charset=utf8
```

SQL 语句设计

​	用户登录  

​	用户注册

----



代码实现：

​	参照源码

---------------------------------------------------------------------------------------

问题1：

​	现在我们一个请求或者一个独立的业务逻辑都单独进行一个Servlet的创建进行请求处理。

但是一个网站的功能是非常的多，如果每个都创建单独的Servlet进行处理，这样造成

Servlet 过多。造成资源浪费。

解决：

​	服务器在接受到浏览器发送的请求后，会调用对应的Servlet进行请求

​	然后调用 Servlet 中 Service 方法进行处理

​	我们将不同功能的处理封装成对应的方法。

​	在service方法中 调用其对应的功能处理方法进行请求处理

​	这样Servlet 我们只需要一个

新的问题：

​	如何在 Service 方法中实现根据请求动态的调用器功能处理方法呢？

解决：

​	使用反射动态的获取 Servlet 中的方法

注意：**请求中要附带方法的名称**

----



问题2： 现在使用反射我们事先了在service 方法中动态的根据请求调用对应的方法

进行请求处理，但是真实开发过程中，不对每个功能都创建一个servlet ，但是

也不会只使用一个 Servlet ，我们的 Servlet 不只是一个。

一般是一个独立的功能模块一个servlet 。我们需要在这些 servlet 中的  service 中

都要将 反射的代码声明一个遍。



# 3  登录 Servlet 创建和MVC思想

> 用户登录：
>
> ​	用户点击登录发送请求到 UserServet
>
> ​	tomcat 服务器接受到
>
> MVC 分层开发；
>
> ​	M：model  service层、dao层和 实体类
>
> ​	V： view     视图层   JSP 页面
>
> ​	C：controller   控制层 Servlet



注意： 定义birthday 属性可以使用 String 类型。



service层： getUserInfoService(String name,String pwd)

dao 层： getUserInfoDao(String uname,String pwd)   查询用户信息





# 4 用户登录失败和成功处理

> 在用户登录失败的页面上，打印用户登录失败的提示，使用 JSP 和 session。
>
> 在用户成功登录后，在合适的位置打印当前用户登录名。
>
> 在 JSP 界面寻找合适的位置的方法：
>
> 方法可以先使用行内样式`border: solid 3px red `,确定边框的大小和位置
>
> 然后通过添加 span 标签或其他标签内，声明 java 代码.



# 5 用户退出

> 点击 退出按钮，使用 JS 确认框，询问用户是否退出。
>
> 若退出，选择是，否则不执行退出操作

## 5.1  LoginOutServlet.java

```java
package cn.szxy.web;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

/**
 * 
 * 用户退出
 * 
 * 销毁session 
 */
public class LoginOutServlet extends HttpServlet {

		@Override
		protected void service(HttpServletRequest req, HttpServletResponse resp)
				throws ServletException, IOException {
			  	//设置请求编码格式
				req.setCharacterEncoding("utf-8");
				//设置响应编码格式
				resp.setContentType("text/html;charset=utf-8");
				//响应处理结果
					//获取session 对象
					HttpSession session = req.getSession();
					//销毁 session 对象
					session.invalidate();
					//重定向
					resp.sendRedirect("/projectsxt/login.jsp");
		}
}
```

## 5.2  JS 事件绑定

```js
<script>
    /* 	function loginOut(){
    			
    		return window.confirm("您确定要退出嘛？");
    			
    	}  */
    	
    	$(function(){
    		/* 
    			ID 选择器 ，注意前面加 井号# 
            	事件绑定函数
            */	
    		$("#out").click(
    			
    			function(){
    				/*
    					确定框，如果点 "是" ,则返回 true，这样就触发 a 标签的 href 属性
    					反之，则什么也不做，不会触发 a 标签的 href 属性。
    				*/
    				return window.confirm("您确定要退出嘛？");
    		});
    		
    	});
    </script>
```

```html
 <div class="head-l" style="position: relative; left: 850px; color:white; font-size: 15px;"> 	  当前用户:<%=(String)session.getAttribute("uname") %>
     &nbsp;&nbsp;
     <a id="out" class="button button-little bg-red" href="user/out" onclick="loginOut()">			<span class="icon-power-off"></span>退出登录
     </a> 
</div>
```



# 6 用户注册

## 6.1 用户注册界面

> 找用户注册界面相似的模块进行修改
>
> MySQL 会将字符类型的数据，按照隐形转换成数字和日期类型
>
> regUserInfoDao 方法
>
> regUserInfoService 方法

```html
<!-- 选择出生日期  -->
<div class="form-group">
    <div class="label">
        <label for="sitename">出生日期：</label>
    </div>
    <div class="field">
        <!-- 设置 type 的属性为 date ，选择日期 -->
        <input type="date" class="input w50" id="mpass" name="mpass"
               size="50"  />
    </div>
</div>
```

```js

<script type="text/javascript">
	
		$(function(){
			
				/**    设置性别选择                   ****/
				$("#male").click(function(){
					
					$("#span_male").addClass("icon-check");
					$("#span_female").removeClass("icon-check");
					
				});
			
				$("#female").click(function(){
					
					$("#span_female").addClass("icon-check");
					$("#span_male").removeClass("icon-check");
					
				});
		});
</script>
```

# 7 项目改良

> 用一个 Servlet 解决，使用反射的方法，获取方法名，然后执行相应的方法。
>
> 方法：请求附带方法名的方式
>
> 一、使用隐藏标签发送附带请求信息
>
> 二、使用超链接附带请求信息

```html
<!-- 隐藏标签 请求的方法名-->
<input type="hidden" name="method"  value="方法名">
<!-- 超链接 -->
<a href="data?method="某某方法名"></a>
<!-- 使用 js -->
window.location.href="data?method="某某方法名"
```

## 7.1 DataServlet

> 用户模块 
>
> ​	用户登录
>
> ​	用户注销
>
> ​	用户注册
>
> 将原来的三个 Servlet 变为一个 Servlet ，使用反射动态获取请求方法。
>
> 好处：减少 servlet 的数量，从服务器角度来说，serlvet 从第一次启动就会一直运行，直到服务器结束运行，这样对服务器的压力比较大，尤其是当前业务比较多的时候。减少多余代码的书写，将原来每个细小的模块都放在一个大的模块中作为一个 servlet。
>
> 注意：请求方法在请求中附带，可使用 `input` 隐藏标签

```java
package cn.szxy.web;

import java.io.IOException;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

import cn.szxy.pojo.User;
import cn.szxy.service.UserService;
import cn.szxy.service.impl.UserServiceImpl;

/**
 * 
 * 使用一个 servlet 动态分发一个模块的请求方法
 * 
 */
public class DataServlet extends HttpServlet {
	@Override
	protected void service(HttpServletRequest req, HttpServletResponse resp)
			throws ServletException, IOException {

		// 设置请求编码格式
		req.setCharacterEncoding("utf-8");
		// 设置响应编码格式
		resp.setContentType("text/html;utf-8");
		// 获取请求的方法名
		String methodName = req.getParameter("method");
		// 根据方法名的不同动态选择方法对应处理请求
		// 获取该类的类对象
		Class clazz = this.getClass();
		try {
			// 获取该类的方法
			Method method = clazz.getMethod(methodName,
					HttpServletRequest.class, HttpServletResponse.class);
			// 执行对应的请求方法
			method.invoke(this, req, resp);

		} catch (Exception e) {
			e.printStackTrace();
		}

	}

	// 用户登录
	public void userLogin(HttpServletRequest req, HttpServletResponse resp)
			throws IOException {
		System.out.println("DataServlet.userLogin() 处理请求...");
		// 获取请求数据
		String uname = req.getParameter("uname");
		String pwd = req.getParameter("pwd");

		// 处理请求数据
		// 获取 业务逻辑层对象
		UserService service = new UserServiceImpl();
		User u = service.getUserInfoService(uname, pwd);
		System.out.println(u);
		// 获取或创建 session 对象
		HttpSession session = req.getSession();
		// 检查用户名和密码
		if (u != null) {

			// 处理响应结果
			session.setAttribute("uname", uname);
			session.setAttribute("pwd", pwd);
			// 重定向
			resp.sendRedirect("/projectsxt2/index.jsp");

		} else {

			// 处理响应结果
			session.setAttribute("flag", "LoginFailure");
			// 重定向
			resp.sendRedirect("/projectsxt2/login.jsp");
		}

	}

	// 用户退出
	public void userLoginOut(HttpServletRequest req, HttpServletResponse resp)
			throws IOException {
		System.out.println("DataServlet.userLoginOut() 处理请求");
		// 响应处理结果
		// 获取session 对象
		HttpSession session = req.getSession();
		// 销毁 session 对象
		session.invalidate();
		// 重定向
		resp.sendRedirect("/projectsxt2/login.jsp");
	}

	// 用户注册
	public void userRegister(HttpServletRequest req, HttpServletResponse resp)
			throws IOException {
		System.out.println("DataServlet.userRegister() 处理请求");
		// 获取请求数据
		String uname = req.getParameter("uname");
		String pwd = req.getParameter("pwd");
		String sex = req.getParameter("sex");
		int age = Integer.valueOf(req.getParameter("age"));
		String birthday = req.getParameter("birthday");
		// System.out.println(uname+" "+pwd+" "+sex+" "+age+" "+birthday);
		// 处理请求数据
		// 获取业务层对象
		UserService service = new UserServiceImpl();
		int flag = service.regUserInfoService(uname, pwd, sex, age, birthday);
		// 创建 session 对象
		HttpSession session = req.getSession();

		if (flag != -1) {
			session.setAttribute("flag", "RegisterSuccess");
			// 重定向
			resp.sendRedirect("/projectsxt2/login.jsp");

		} else {

			session.setAttribute("flag", "RegisterFailure");
			// 重定向
			resp.sendRedirect("/projectsxt2/login.jsp");

		}

	}
}

```



# 8  BaseServlet

> 向上抽取成父类，解决多个模块书写相同代码的问题
>
> 注意：
>
> 一： BaseServlet 不能被访问 ，在 web.xml 不配置 BaseServlet
>
> 二： BaseServlet 不能被实例化，改为 abstract 类
>
> 使用：
>
> 一： 创建 Servlet 继承 BaseServlet 即可。
>
> 二：在自己的 Servlet 中 不要声明  service 方法
>
> 三：正常访问我们自己的servlet
>
> 注意：**请求必须附带要被执行的方法名**

```java
package cn.szxy.web;

import java.io.IOException;
import java.lang.reflect.Method;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

import cn.szxy.pojo.User;
import cn.szxy.service.UserService;
import cn.szxy.service.impl.UserServiceImpl;

/**
 * 
 * Servlet 工具类
 * 
 * 不配置 web.xml 访问路径
 * 抽象类不能被实例化
 * 父类的 this 指针指向 子类对象
 * 
 * 使用：
 * 	  只要继承该类就可以了，不可以重写 HttpServlt父类的方法
 * 	 在自己的  servlet 中只写 请求方法
 *  
 *
 */
public abstract  class BaseServlet extends HttpServlet {
	
	@Override
	protected void service(HttpServletRequest req, HttpServletResponse resp)
			throws ServletException, IOException {

		// 设置请求编码格式
		req.setCharacterEncoding("utf-8");
		// 设置响应编码格式
		resp.setContentType("text/html;utf-8");
		// 获取请求的方法名
		String methodName = req.getParameter("method");
		// 根据方法名的不同动态选择方法对应处理请求
		// 获取该类的类对象
		Class clazz = this.getClass();
		try {
			// 获取该类的方法
			Method method = clazz.getMethod(methodName,
					HttpServletRequest.class, HttpServletResponse.class);
			// 执行对应的请求方法
			method.invoke(this, req, resp);

		} catch (Exception e) {
			e.printStackTrace();
		}

	}
	
}

```



# 9 总结

1. 套用模板进行页面快速构建

   在自己的项目中常见 jsp 文件，然后将模板中的前端相关代码赋值到

   自己的jsp 文件中，将静态资源赋值到 webRoot 下

2. MVC的开发流程

   M： model      service dao pojo 

   v：view         Jsp js  css html

   c：controller   Servlet 控制

3. Servlet+jsp+jdbc 的功能开发流程

   浏览器发起页面请求直接给 jsp 

   浏览器发起功能请求给 servlet ，servlet 调用service， service 进行业务逻辑处理

   service  调用dao，dao 进行数据库操作( jdbc)，dao 层将处理结果返回给 servcie 

   servcie 再将结果返回给 servlet ，请求转发或重定向给 jsp ，jsp 做出页面响应

4. request 和session 作用有的使用

   request： 请求转发的数据流转的载体

   session： 重定向类型的数据流转的载体(但是 session 可以解决 同一个用户不同请求的数据共享)

5. 浏览器发起请求到服务器请求发起的方式(重点记忆)

   1. 非 ajxk

   form 表单提交： action 数据提交地址，method：数据提交方法

   超链接标签（相当于 get 请求） href:为数据提交地址，可以直接使用？拼接请求数据

   js中的window.location.herf ：为数据提交地址，可以直接使用？拼接请求数据

   注意：

   ​	使用以上请求发起的请求，浏览器在接收到响应内容后，会原有内容覆盖，显示响应效果

   6. ajax 技术

      在整个页面中局部的页面刷新操作

7. BaeSrrvlet 的抽去和使用

   1. 反射

   2. 抽象类

8. 项目缺陷

   1. 在jsp中获取从Servlet 流转过来的数据特别麻烦   

    解决:使用 EL 表达式

         1. 在 jsp 页面中使用 java 代码块进行逻辑处理书写和阅读极不方便

    解决：使用 JSTL 标签库

         1. 使用 session 进行数据流转是很方便的，但是 session 失效了，所有 依赖 session 都会失效。

         2. 响应结果都是覆盖原有内容显示给用户

      解决：使用 ajax 技术

9. 删除用户信息

   delUserInfo 下一章节

   问题： 在删除成功后，响应内容会将请求页面的所有的内容覆盖

   ​	显示新的内容，但是我们希望在保留当前请求页信息的基础上显示新的内容

   明确：

   (没有指明资源显示位置)指的不一定是浏览器中一个标签页，一般 frameset 标签中都的划分区域，

   都是单独的。如果某个区域发起了请求，则该区域可以称为当前请求页

   也就是说浏览器在当前页向服务器发出请求，服务器接受请求，处理请求数据，在未指明资源显示位置，a 标签 默认将响应结果发送给浏览器当前页上，会覆盖之前的响应内容，显示新的响应内容。

   	解决：使用 ajax 技术

 9. 显示当前在线人数:

     统计当前系统的 session 的个数，一个 session就是一个用户在线。

     在 session 被创建的使用计数器+1，session 数据被销毁时计数器 -1

     问题：

     ​	我怎么能在 session 创建的时触发计数器执行 +1

 ​		