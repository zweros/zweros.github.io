---
title: python学习之路
date: 2018-08-19 17:45:31
tags: [python学习]
---

## python学习 ##

**缩进是python的灵魂**

具有相同缩进量==代码块


```
age = 20
if age >= 18:
    print 'your age is', age
    print 'adult'
print 'END'
```
注:这是在python2.7版版本的环境中


**注意1:**
 Python代码的缩进规则。具有相同缩进的代码被视为代码块，上面的3，4行 print 语句就构成一个代码块（但不包括第5行的print）。如果 if 语句判断为 True，就会执行这个代码块。
缩进请严格按照Python的习惯写法：4个空格，不要使用Tab，更不要混合Tab和空格，否则很容易造成因为缩进引起的语法错误。
**注意2:**
 if 语句后接表达式，然后用:表示代码块开始。如果你在Python交互环境下敲代码，还要特别留意缩进，并且退出缩进需要多敲一行回车：
**注意3**
ifesle语句后面加冒号:而不是用小括号()

变量 = print()
变量 = 数据类型()
BIF == Built-in functions   内置函数
dir(_bultins_)                    查找函数
help(函数名)                  查看函数的用法

转义字符
\\            →       \
\'             →      '

若需要多个转义字符，用print r''' '''
 eg：打印Let's go!
```python
1."Let's go！"
2.'Let\'s go!'
```