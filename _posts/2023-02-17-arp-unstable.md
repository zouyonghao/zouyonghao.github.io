---
title: Solve network issue caused by unstable arp
layout: post
---

## Question

Network is unstable.

```sh
PS C:\Users\zyh> ping -t 114.114.114.114

正在 Ping 114.114.114.114 具有 32 字节的数据:
来自 114.114.114.114 的回复: 字节=32 时间=28ms TTL=67
请求超时。
来自 114.114.114.114 的回复: 字节=32 时间=28ms TTL=88
请求超时。
来自 114.114.114.114 的回复: 字节=32 时间=28ms TTL=83
请求超时。
来自 114.114.114.114 的回复: 字节=32 时间=30ms TTL=66
请求超时。
来自 114.114.114.114 的回复: 字节=32 时间=28ms TTL=68
来自 114.114.114.114 的回复: 字节=32 时间=28ms TTL=75
请求超时。
请求超时。
```

## Reason

arp entry is not stable.

```sh
root@OpenWrt:~# arp
IP address       HW type     Flags       HW address            Mask     Device
192.168.32.128   0x1         0x2         44:af:28:57:66:a6     *        br-lan
192.168.32.214   0x1         0x2         00:ec:0a:1b:87:40     *        br-lan
192.168.3.1      0x1         0x6         d4:61:fe:ce:c4:c8     *        wan     <--
root@OpenWrt:~# arp
IP address       HW type     Flags       HW address            Mask     Device
192.168.32.128   0x1         0x2         44:af:28:57:66:a6     *        br-lan
192.168.32.214   0x1         0x2         00:ec:0a:1b:87:40     *        br-lan
192.168.3.1      0x1         0x6         34:96:72:a9:4e:d9     *        wan     <-- changed!
```

## Solution

Set static arp entry.

```sh
ip neighbor replace 192.168.3.1 lladdr d4:61:fe:ce:c4:c8 nud permanent dev wan
```

**Then we can get stable network.**

```sh
PS C:\Users\zyh> ping -t 114.114.114.114

来自 114.114.114.114 的回复: 字节=32 时间=32ms TTL=84
来自 114.114.114.114 的回复: 字节=32 时间=29ms TTL=68
来自 114.114.114.114 的回复: 字节=32 时间=28ms TTL=65
来自 114.114.114.114 的回复: 字节=32 时间=28ms TTL=91
来自 114.114.114.114 的回复: 字节=32 时间=28ms TTL=88
来自 114.114.114.114 的回复: 字节=32 时间=28ms TTL=64
来自 114.114.114.114 的回复: 字节=32 时间=28ms TTL=72
来自 114.114.114.114 的回复: 字节=32 时间=30ms TTL=84
来自 114.114.114.114 的回复: 字节=32 时间=28ms TTL=77
来自 114.114.114.114 的回复: 字节=32 时间=28ms TTL=72
```

## Reference

[superuser](https://superuser.com/questions/928247/how-to-set-up-a-static-persistent-arp-entry-with-openwrt-14-07-barrier-breaker)
