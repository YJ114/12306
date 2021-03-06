##  第一章 urllib 和 urllib2 介绍

### 1. urllib

#### 1.1urlencode 方法

```python
import urllib,urllib2
a = {
    'username': 'yunjun',
    'password': '123456'
}
print urllib.urlencode(a)  # 把一个字典变成查询字符串
# 执行结果如下
username=yunjun&password=123456
```

### 2. urllib2

#### 2.1 urlopen 方法

post请求方式可以接受的参数的类型

1. 字符串
2. 二进制代码

```python
# data参数决定请求方式，当data不为空时，采用post请求
# timeout 设定请求超时时间
response = urllib2.urlopen('http://www.baidu.com',
                data='a=1',
                timeout=5)
# 使用 read 方法得到请求的html源代码
html = response.read()
print html
```

#### 2.2 添加request请求 header 的两种方式

```python
req = urllib2.Request('http://baidu.com',
                      headers={'a':1})
```

```python
req = urllib2.Request('http://baidu.com')
req.add_header('a', 1)
```

#### 2.3 geturl 方法

在实际的请求过程中，会存在重定位的过程，geturl 方法用来获取最终定位到的 url

#### 2.4 getcode 方法

此方法用来获取返回的HTTP状态代码

#### 2.5 HTTPCookieProcessor

很多网站的资源需要用户登录之后才能获取。

我们一旦登录后再访问其他被保护的资源的时候,就不再需要再次输入账号、密码。那么网站是怎么办到的呢?

一般来说，用户在登录之后，服务器端会为该用户创建一个 Session, Session相当于该用户的档案，该档案就代表看该用户。

那么某一次访问请求是属于该用户呢?登录的时候服务競要求浏览器储存了一个Session1D 的 Cookie 值。每一个访问都带上了该 Cookie ，服务器将 Cookie 中的Session ID 与服务器中的 Session ID 比对就知道该请求来自哪个用户了。

#### 2.6 opener

我们在调用 urlib2.urlopen(url) 的时候,其实 urlib2 在 open 函数内部创建了一个默认的 opener 对象。

然后调用 opener.open() 函数。但是默认的opener并不支持cookie。那么我们先新建一个支持cookie的opener。

urlib2中供我们使用的是HTTPCookieProcessor。



## 第二章 手动登录

登录是一种post请求，需要如下内容

+ 请求的 url （str）
+ 请求的方式（str）
+ 参数 （str， bytes）

###  2.1 验证码校验

+ https://kyfw.12306.cn/passport/captcha/captcha-check
+ post
+ answer: 22,118


