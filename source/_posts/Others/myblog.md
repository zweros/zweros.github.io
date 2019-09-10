---
title: My hexo blog
date: 2018-08-19 17:25:20
tags: [myblog]
---


[参考资料-hexo的搭建](http://qjzhixing.com/2015/08/26/)

**下载git和node.js**
[git下载地址](https://git-scm.com/)
[Node.js下载地址](https://nodejs.org/en/)


**安装Hexo**

```
npm install  -g hexo
```

然后到在任意盘符下，新建一个文件夹hexo，C:/hexo
到该文件夹下，点击鼠标右击打开git bash，输入
```
hexo init
```

**安装依赖库**

```
npm install 
```

**本地预览hexo博客网页**

```
hexo g
hexo s
```


**配置github账户**
新建repository
形式：yourname/yourname.github.io
把https://yourname.github.io.git加入到hexo的配置文件_config.yml中

出现的问题：

```
hexo d
ERROR  Deployer not found：github
```
把配置文件中的type类型从github修改为git

Hexo常用命令


```
hexo generate ==  hexo g    生成
hexo server ==  hexo s      本地测试
hexo deploy   ==   hexo d    发布

hexo clean
hexo d -g 

```

更换本地预览端口
```
hexo server -p 5000 #更改端口
```



[参考资料-hexo的搭建](http://qjzhixing.com/2015/08/26/)

**下载git和node.js**
[git下载地址](https://git-scm.com/)
[Node.js下载地址](https://nodejs.org/en/)


**安装Hexo**

```
npm install  -g hexo
```

然后到在任意盘符下，新建一个文件夹hexo，C:/hexo
到该文件夹下，点击鼠标右击打开git bash，输入
```
hexo init
```

**安装依赖库**

```
npm install 
```

**本地预览hexo博客网页**

```
hexo g
hexo s
```


**配置github账户**
新建repository
形式：yourname/yourname.github.io
把https://yourname.github.io.git加入到hexo的配置文件_config.yml中

**出现的问题**：

```
hexo d
ERROR  Deployer not found：github
```
把配置文件中的type类型从github修改为git

Hexo常用命令


```
hexo generate ==  hexo g    生成
hexo server ==  hexo s      本地测试
hexo deploy   ==   hexo d    发布

hexo clean
hexo d -g 

```

更换本地预览端口
```
hexo server -p 5000 #更改端口
```

**其他问题**

标签：tags的使用

在E:\hexo的目录下的_config.yml文件下添加新的标签tags
然后再.md文件就可以使用自己新定义的标签了。

    tags: [tag1，tag2，tag3]