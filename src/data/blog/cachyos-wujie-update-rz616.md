---
author: halunhaku
pubDatetime: 2026-03-12T22:15:00+08:00
title: 机械革命无界14Xpro CachyOS 记录（更新）：更换 RZ616 解决无线网卡问题
featured: false
draft: false
tags:
  - linux
  - CachyOS
description: 机械革命无界14Xpro CachyOS 记录更新，更换 RZ616 无线网卡，完全解决没法使用 Wi-Fi 的问题。
---

在上一篇关于机械革命无界 14X Pro 安装 CachyOS 的记录中，我提到了自带的 AX210 无线网卡在 CachyOS 下无法开启 Wi-Fi（处于 Hard blocked 状态，只能使用蓝牙）。

目前，我已经更换了 RZ616 网卡，无线网卡的问题已经完全解决了！

## 更换 RZ616 后的体验

拆机并更换为 RZ616 之后，重新开机进入系统，Wi-Fi 终于可以正常开启并连接了。同时，蓝牙功能也一切正常。对系统来说几乎是即插即用的体验，非常省心。

我们可以通过 `rfkill list` 命令来查看当前网络设备的软硬件阻塞状态。之前使用自带的 AX210 时，Wireless LAN 总是处于被硬件屏蔽（Hard blocked）的状态。而换上 RZ616 之后，可以看到此时软硬件屏蔽均已解除，一切正常：

```shell
❯ rfkill list
0: hci0: Bluetooth
        Soft blocked: no
        Hard blocked: no
1: phy0: Wireless LAN
        Soft blocked: no
        Hard blocked: no
```

目前系统运行十分稳定，再也不用插着网线或者忍受没有 Wi-Fi 的情况了。如果你也遇到了鸡哥这款本子自带网卡在 Linux 下的 Hard block 问题，并且查遍全网通过软件层面也无法解决，那么强烈建议直接换一张 RZ616 网卡。


## 关于指纹模块的折腾

至于指纹模块，我查阅了一下资料，确认目前在 Linux 下应该是无法驱动的。
我的指纹识别模块设备信息为：

```shell
Bus 003 Device 002: ID 2f0a:8020 PXAT PT2887-SS Module
```

经过查询得知，这个 PXAT（通常是部分国产方案或特定供应商的定制芯片）指纹模块，目前在 Linux 生态中没有任何驱动支持。这意味着如果想要在 Linux 下使用指纹解锁，目前可以说是无解的，只能期待后续是否有开源社区的驱动跟进。

目前的进度先更新到这里，后续如果其他配置有新的进展，我还会继续通过博客记录更新。
