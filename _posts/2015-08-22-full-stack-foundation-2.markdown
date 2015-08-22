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
