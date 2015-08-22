---
layout: post
title: Full Stack Foundation Using Python 2
---

Python 全栈基础
===

现在我们有了数据库的支持，现在让我们来创建一个 Web 服务。

### CLient Server 客户端服务器模式

* Client 发送请求
* Server 等待请求

### TCP IP HTTP 协议

* TCP

  把信息切成许多小包发送给服务器，如果有包丢失，服务器返回丢失的包信息，客户端重新发送

* IP

  跟你的地址相似，IP 是你在网络上的地址。 客户端根据URL从 DNS 获取服务端IP

* PORTS

  使用 ports 区分同一个 IP 的不同服务，Web 访问一般使用 80，8080 端口

* localhost

  代表了你自己，同时对应了特殊的 IP 127.0.0.1，localhost 会使客户端自动访问本机服务

* HTTP

  使用 HTTP Method 来描述客户端需要获取什么信息的一种协议。

  通常使用 Get 和 Post 两种协议

  Get 用来表示我需要得到某些信息

  Post 表示我需要添加/修改/删除某些信息

  服务器返回 Status Code 表示操作结果

  - 200 - Get 成功
  - 301 - Post 成功
  - 404 - 文件未找到
  - 同时返回 Html CSS JavaScript 等

## 使用 BaseHTTPServer 创建 Http 服务

代码如下

```python
#webserver.py
from BaseHTTPServer import BaseHTTPRequestHandler, HTTPServer

class webserverHandler(BaseHTTPRequestHandler):
    def do_GET(self):
        try:
            if self.path.endswith("/hello"):
                self.send_response(200)
                self.send_header('Content-type', 'text/html')
                self.end_headers()

                output = ""
                output += "<html><body>Hello!</body></html>"
                self.wfile.write(output)
                print output
                return
        except IOError:
            self.send_error(404, "File Not Found %s" % self.path)

def main():
    try:
        port = 8080
        server = HTTPServer(('', port), webserverHandler)
        print "Web server running on port %s" % port
        server.serve_forever()

    except KeyboardInterrupt:
        print "^C entered, stopping web server..."
        server.socket.close()

if __name__ == '__main__':
    main()

```

1. 定义 main 函数，except KeyboardInterrupt 可以获取到用户输入 Ctrl C 时的异常

2. if __name__ = '__main__' 表示当此由用户执行时，运行下面的语句，此处为 main 函数

3. 使用 BaseHTTPServer 提供 HTTP 服务。 函数为 HTTPServer, webserverHandler 为处理 webserverHandler 的类

4. 定义 do_GET 方法，获取 Get 信息。使用 self.path.endswith 获取 URL.

5. 捕获 IOError ，定义 404 事件

6. 使用 send_response 定义返回状态。 wfile.write 写入返回信息。

运行 webserver.py, 访问 localhost:8080 即可。

定义多个 Get 请求

```python
if self.path.endswith("/hola"):
    self.send_response(200)
    self.send_header('Content-type', 'text/html')
    self.end_headers()

    output = ""
    output += "<html><body>&#161Hola <a href='/hello' >Back to Hello</a></body></html>"
    self.wfile.write(output)
    self.end_headers()
```

定义 Post 请求

```python
def do_POST(self):
        try:
            self.send_response(301)
            self.end_headers()

            ctype, pdict = cgi.parse_header(self.headers.getheader('content-type'))
            if ctype == 'multipart/form-data':
                fields = cgi.parse_multipart(self.rfile, pdict)
                messagecontent = fields.get('message')

            output = ""
            output += "<html><body>"
            output += " <h2> Okay, how about this: </h2>"
            output += "<h1> %s </h1>" % messagecontent[0]

            output += "<form method='POST' enctype='multipart/form-data' action='/hello'><h2>What would you like me to say?</h2><input name='message' type='text' ><input type='submit' value='Submit'></form>"

            output += "</body></html>"

            self.wfile.write(output)
            self.end_headers()
        except:
            pass

```

在 do_GET 中添加表单：

```python

output += "<form method='POST' enctype='multipart/form-data' action='/hello'><h2>What would you like me to say?</h2><input name='message' type='text' ><input type='submit' value='Submit'></form>"
output += "</body></html>"

```

## 添加 CRUD
```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker
from database_setup import Base, Restaurant, MenuItem

engine = create_engine('sqlite:///restaurantmenu.db')
Base.metadata.bind = engine
DBSession = sessionmaker(bind = engine)
session = DBSession()
```

## 列出所有 Restaurant
```python
if self.path.endswith("/restaurant"):
    self.send_response(200)
    self.send_header('Content-type', 'text/html')
    self.end_headers()

    restaurants = session.query(Restaurant).all()

    output = ""
    output += "<html><body>"

    for restruant in restaurants:
        output += restruant.name
        output += "<br>"

    output += "</body></html>"
    self.wfile.write(output)
    print output
    return
```

## 添加 Restaurant
do_GET 中添加以下代码
```python
if self.path.endswith("/restaurant/new"):
    self.send_response(200)
    self.send_header('Content-type', 'text/html')
    self.end_headers()

    output = ""
    output += "<html><body>"
    output += "<h2>Add restaurant</h2>"
    output += "<form method='POST' enctype='multipart/form-data' action='/restaurant/new'>"
    output += "<input type='text' name='name' />"
    output += "<input type='submit' value='Submit' />"
    output += "</form>"
    output += "</body></html>"
    self.wfile.write(output)
    print output
    return
```

do_POST 中添加以下代码
```python
if self.path.endswith("/restaurant/new"):

    ctype, pdict = cgi.parse_header(self.headers.getheader('content-type'))
    if ctype == 'multipart/form-data':
        fields = cgi.parse_multipart(self.rfile, pdict)
        print fields
        restaurant_name = fields.get('name')[0]

    new_restaurant = Restaurant(name = restaurant_name)
    session.add(new_restaurant)
    session.commit()

    self.send_response(301)
    self.send_header('Content-type', 'text/html')
    self.send_header('Location', '/restaurants')
    self.end_headers()

    return
```

## 修改名称

do_GET 添加以下代码

```python
if self.path.endswith("/edit"):

    self.send_response(200)
    self.send_header('Content-type', 'text/html')
    self.end_headers()

    restaurant_id = self.path.split("/")[2]

    output = ""
    output += "<html><body>"
    output += "<h2>edit restaurant</h2>"
    output += "<form method='POST' enctype='multipart/form-data' action='/restaurant/%s/edit'>" % restaurant_id
    output += "<input type='text' name='name' />"
    output += "<input type='submit' value='Submit' />"
    output += "</form>"
    output += "</body></html>"
    self.wfile.write(output)
    print output
    return

```

do_POST 添加以下代码
```python
if self.path.endswith("/edit"):
    restaurant_id = self.path.split("/")[2]

    ctype, pdict = cgi.parse_header(self.headers.getheader('content-type'))
    if ctype == 'multipart/form-data':
        fields = cgi.parse_multipart(self.rfile, pdict)
        print fields
        restaurant_name = fields.get('name')[0]

    edit_restaurant = session.query(Restaurant).filter(Restaurant.id == restaurant_id).one()
    edit_restaurant.name = restaurant_name
    session.add(edit_restaurant)
    session.commit()

    self.send_response(301)
    self.send_header('Content-type', 'text/html')
    self.send_header('Location', '/restaurants')
    self.end_headers()

    return
```

## 删除 Restaurant

do_GET 添加以下代码
```python
if self.path.endswith("/delete"):
    self.send_response(200)
    self.send_header('Content-type', 'text/html')
    self.send_header('Location', '/restaurants')
    self.end_headers()

    restaurant_id = self.path.split("/")[2]

    output = ""
    output += "<h2>Are you sure delete this Restaurant?</h2>"
    output += "<form method='POST' enctype='multipart/form-data' action='/restaurant/%s/delete'>" % restaurant_id
    output += "<input type='submit' value='Yes' />"
    output += "</form>"

    self.wfile.write(output)
    print output
    return
```

do_POST 添加以下代码
```python
if self.path.endswith("/delete"):
    restaurant_id = self.path.split("/")[2]

    restaurant = session.query(Restaurant).filter(Restaurant.id == restaurant_id).one()
    session.delete(restaurant)
    session.commit()

    self.send_response(301)
    self.send_header('Content-type', 'text/html')
    self.send_header('Location', '/restaurants')
    self.end_headers()

    return
```

以上，一个简单的服务，包括增删改查就搭建完成了。
