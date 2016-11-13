---
layout: post
title: Download Coursera materials and videos with coursera-dl
---

最近在追 [依据基本原理构建现代计算机：从与非门到俄罗斯方块](https://www.coursera.org/learn/build-a-computer) 这门课，不过梯子比较慢，看着很不爽，希望下下来看。

之前用 coursera-dl 下 http://class.coursera.org 上的课程，自从 coursera 更新后，不能用了一段时间，今天发现又可以使用了。

安装：

```
pip install coursera-dl
```

使用：

比如这门课网址为
https://www.coursera.org/learn/build-a-computer

那么下命令即为

```
coursera-dl -u 用户名 -p 密码 build-a-computer
```

下载过程

![下载过程图](/images/coursera-dl-downloading.PNG) 

下载完成后，默认在用户文件夹下，会按照 Unit 分目录

![下载完成图](/images/coursera-dl-downloaded.PNG)