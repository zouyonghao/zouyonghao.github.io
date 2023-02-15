---
title: Install BaoTa(宝塔) on Termux
layout: post
---

1. Install Termux
    
    Just install from any Android store

2. Install proot-distro

    ```sh
    pkg install proot-distro
    ```

3. Install ArchLinux

    ```sh
    proot-distro install archlinux
    ```

4. Run the install script

    ```sh
    if [ -f /usr/bin/curl ];then curl -sSO https://download.bt.cn/install/install_panel.sh;else wget -O install_panel.sh https://download.bt.cn/install/install_panel.sh;fi;bash install_panel.sh
    ```

5. Change the ownership of directory

    ```sh
    chown -R 777 /www
    ```

6. Reload the panel

    ```sh
    bt 4
    ```
