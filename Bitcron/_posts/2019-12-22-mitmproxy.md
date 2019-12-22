---
title: 使用 mitmproxy 进行 iphone 抓包
layout: post
---

### 安装

Mac上直接用 homebrew 装就好了

```
brew install mitmproxy
```

Linux 和 Windows(WSL) 直接[下载](https://mitmproxy.org/downloads/)使用

### 使用

iphone 和 运行的机器需要在同一局域网下

机器上直接启动`mitmproxy`，默认端口为`8080`

iphone上根据机器ip和端口设置代理即可

### https

上述步骤完成就可以抓包了，但是访问https会有证书问题，需要安装mitmproxy的证书

手机上用`safari`访问`mitm.it`

会出现下面的网页
![](https://docs.mitmproxy.org/stable/certinstall-webapp.png)

点击 Apple 进行安装

在设置->通用->关于里找到`mitmproxy`的证书安装

然后还要打开证书的信任，具体在哪忘记了，找一找就能找到

完成之后就可以抓到`https`的包了