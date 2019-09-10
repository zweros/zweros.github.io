# tomcat基本配置

- 一个workspace只能对应tomcat
- tomcat的应用目录把wetwebapps改为webapp

- &nbsp;&nbsp;当用户访问Web应用时，如果没有指定具体要访问的页面资源 <br/>
Tomcat 会按照 <welcome-file-list> 元素指定默认页面的顺序 <br/>
停止查找后面的默认页面，若没有找到，则返回访问资源不存在的错误提示页面。


