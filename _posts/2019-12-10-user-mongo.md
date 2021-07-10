---
title: 非管理员用户安装 mongodb
layout: post
---

0. 背景

    需求是在服务器上安装mongodb，但是没有sudo权限，只能在自己的用户目录下安装，碰到了很多坑，记录一下。

1. 下载

    直接在官网选择tar包下载后解压，此时如果直接运行，报错为找不到相关 .so 包，如

    ```
    ./mongodb-linux-x86_64-ubuntu1804-4.2.2/bin/mongos: error while loading shared libraries: libcurl.so.4: cannot open shared object file: No such file or directory
    ```

2. 安装相关依赖

    此时服务器上缺少相关依赖，如果是`sudo`用户，可以直接用 `apt-get` 安装 `libxxx` 即可，但现在没有`sudo`权限，怎么办呢？

    - 使用 `homebrew`

        `homebrew` 是 `mac` 上的包管理工具，但是现在在`linux`上也能使用，好处是不需要`sudo`权限，在用户目录下安装相关库

        安装方式见[官网](https://docs.brew.sh/Homebrew-on-Linux)

        有几个库可以直接用 `linuxbrew` 装，但有些库还是不行，怎么办呢？
    
    - 直接从其他机器拷贝

        可以在本机上先安装相关库，然后直接拷贝到服务器上，不过本机发行版和服务器最好一致

    - 如何使用？

        修改`LD_LIBRARY_PATH`，将`linuxbrew`安装的库和拷贝的库放在系统库之前，如：

        ```bash
        export LD_LIBRARY_PATH='/home/xxx/.linuxbrew/lib:/home/xxx/uploadlib:/lib/x86_64-linux-gnu/:/usr/lib/x86_64-linux-gnu'
        ```

3. glibc

    所有东西都装完了，这时候运行发现如下问题
    
    ```
    ./mongodb-linux-x86_64-ubuntu1804-4.2.2/bin/mongos: /lib/x86_64-linux-gnu/libc.so.6: version `GLIBC_2.25' not found (required by /home/xxx/libcrypto.so.1.1)
    ```

    机器上的`GLIBC`版本太老，只能重新下载编译一个
    在`https://ftp.gnu.org/gnu/glibc/`下载新版本，编译安装之后，把新的`libc.so.6`所在目录加入`LD_LIBRARY_PATH`中，又发现新的问题，此时不管运行哪个程序，都会有如下错误

    ```bash
    $ ls
    Segmentation fault (core dumped)
    ```

    别慌，先把`LD_LIBRARY_PATH`路径改回之前路径，让普通程序恢复正常

4. 修改程序使用的 `ld-linux`

    程序使用的`li-linux.so`在编译是路径被写死，与新编译的`glibc`不匹配，如何修改呢？我们可以使用`patchelf`，安装[在此](https://github.com/NixOS/patchelf) 使用方法[在此](https://nixos.org/patchelf.html)

    那么我们直接修改`mongodb`的二进制文件

    ```bash
    ./patchelf-0.10/src/patchelf --set-interpreter lib/ld-linux-x86-64.so.2 ./mongodb-linux-x86_64-ubuntu1804-4.2.2/bin/mongod
    ```

    修改后，再把`LD_LIBRARY_PATH`的值改为加入新的`glibc`的路径，发现终于可以正常运行

    但我们其他程序没法运行了怎么办呢？

    先把`LD_LIBRARY_PATH`改为空，新写一个`mongo`的启动脚本，内容为：

    ```bash
    LD_LIBRARY_PATH='/home/xxx/.linuxbrew/lib:/home/xxx/uploadlib:/home/xxx/glibc/lib:/lib/x86_64-linux-gnu/:/usr/lib/x86_64-linux-gnu' ./mongodb-linux-x86_64-ubuntu1804-4.2.2/bin/mongod --dbpath=xxx
    ```

    此时，运行该脚本，程序正常启动