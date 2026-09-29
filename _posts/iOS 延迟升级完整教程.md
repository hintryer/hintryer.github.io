---
title: iOS 延迟升级完整教程
description: >-
  这份完整概述带你了解 Chirpy 的基础。
  你将学习如何安装、配置、搭建第一个基于 Chirpy 的网站，并部署到 Web 服务器。
author: cotes
date: 2025-08-09 20:55:00 +0800
categories: [iOS, 教程]
tags: [教程]
media_subpath: '/posts/20180809'
---

# iOS 延迟升级｜Win｜Mac｜免电脑｜免越狱｜多方法升级验证已关闭的 iOS/iPadOS 系统 DelayOTA 完整教程

作者: TAIS3  发布时间: 2022-08-07 01:01

教程分为 未越狱设备（Windows 或 Mac）和 越狱设备（免电脑）两个版本，以升级 iOS 15.4.1 为例，操作前**请先关闭「查找我的** **iPhone」以及备份 iPhone/iPad 数据，如果之前安装了屏蔽更新的描述文件，也需要先删除。**

此方法只能用于升级，不能用于降级，原理是苹果的「监督模式（用于企业、教育机构等）」有 90 天内的 OTA 在线升级延迟期，通过开启该模式，再升级已关闭验证通道但还未超过 90 天的 iOS/iPadOS 系统版本，升级后再关闭「监督模式」就和正常升级的系统一样使用（包括之后的越狱）。如果你现在还在 iOS 11/12 老旧的系统版本，由于很多 App 和插件已经不支持这些旧版本系统，想要升级到有希望越狱的版本但之前又错过了，那么该教程比较适合，毕竟 iOS 14.0-15.4.1 可以实现永久版越狱工具。

## 未越狱设备延迟升级

> [!NOTE]
>
> 注意⚠️操作前请先关闭「查找我的 iPhone」以及备份 iPhone/iPad 数据，如果之前安装了屏蔽更新的描述文件，也需要先删除。
>

### Windows 版教程

- 下载「iBackupBot」工具以及「开启监督模式」与「关闭监督模式」文件。

  下载地址｜[https://wwd.lanzout.com/b03j781yd](https://wwd.lanzout.com/b03j781yd)  密码: 2o6c

  ![507bb](./assets/iOS 延迟升级完整教程/507bb80b0b221b314c4e2c705a78b6fb.png)

- 安装「ibackupbot_setup.exe」，桌面会生成 iBackupBot 工具快捷图标。将需要延迟升级的 iPhone/iPad 连接 Windows 电脑，打开 iTunes 确定连接成功。解压下载的「开启监督模式」文件，将解压出来的「SUPERVISEDBACKUP」文件夹放在桌面。双击打开电脑桌面的 iBackupBot 工具，点击右上角文件夹图标，选中刚才解压出来放在桌面的「SUPERVISEDBACKUP」文件夹，再点【选择文件夹】按钮。

  ![d1200](./assets/iOS 延迟升级完整教程/d12002ab2ab297a3727e71daca1fbb78.jpeg)

- 在左侧文件列表中选择「Add Supervision」-「System Files」，右侧搜索框搜索「ConfigurationProfiles」，右击「ConfigurationProfiles」文件夹，再点击「Restore selected item(s) to device」

  ![d350e](./assets/iOS 延迟升级完整教程/d350e4dc775d9147da07fa84ec8601d4.jpeg)

- 再次确认设备已经关闭「查找我的 iPhone」以及备份了 iPhone/iPad 数据，如果之前安装了屏蔽更新的描述文件，也需要先删除。如果未关闭**「查找我的 iPhone」那么接下来的操作会遇到「**Restore Error**」报错。**

- **输入 Password 密码「1111」点击 OK，iPhone/iPad 即开始进入恢复模式（如果出现其他报错情况，多半是 iTunes 问题，可使用爱思助手工具箱里的「iTunes及驱动」功能「修复驱动」）**

  ![809ca](./assets/iOS 延迟升级完整教程/809cacd7f848fcd8fb1d7b2e4457e0e6.jpeg)

- **等待开机后按步骤激活设备（建议先将其设置为新 iPhone，选择不传输App与数据，不登录 Apple ID）打开系统设置就会发现设备已经处于「监督模式」。如果未成功开启监督模式，可再重复操作一遍。**

  ![d7a65](./assets/iOS 延迟升级完整教程/d7a6569a9592e54fb549100d88f548bd.jpeg)

- iPhone/iPad 处于「监督模式」后，用自带 Safari 浏览器打开[https://dhinakg.github.io/delayed-otas.html](https://dhinakg.github.io/delayed-otas.html) iPhone 12/13 设备就选 iOS (iPhone 12 series/13 series only) 这一栏里的「Download profile」，如果是旧机型就选「iOS (all other non-legacy devices)」里的「Download profile」，iPadOS 同理。点击对应的「Download profile」安装描述文件，「允许」（这里以 iPhone 6s 为例）：

  ![cc915](./assets/iOS 延迟升级完整教程/cc915df94ddd2e581a5f4a9cd013cb48.jpeg)

- 再打开「设置」，点击「已下载描述文件」安装「OTA Delay – 90 Days」描述文件，重启设备后再打开「设置」-「通用」-「软件更新」安装延迟升级的 iOS/iPadOS 新系统。

  ![34c7f](./assets/iOS 延迟升级完整教程/34c7fe4ad7a3920c1597c4d1930417be.jpeg)

- 升级完成后接下来我们要关闭「监督模式」

  第一种方法是直接在「设置」-「通用」-「传输或还原 iPhone」-「抹掉所有内容和设置」即可关闭「监督模式」（抹除后可以通过之前备份还原设备用户资料）。

  第二种方法就是和上述步开启监督模式步骤类似，只是这次要选择「关闭监督模式」文件。

  确认设备已经关闭「查找我的 iPhone」，iPhone/iPad 连接 Windows 电脑，打开 iTunes 确定连接成功。解压下载的「关闭监督模式」文件，将解压出来的「NOSUPERVISEDBACKUP」文件夹放在桌面。双击打开电脑桌面的 iBackupBot 工具，点击右上角文件夹图标，选中刚才解压出来放在桌面的「NOSUPERVISEDBACKUP」文件夹，再点【选择文件夹】按钮。

  ![29d7f](./assets/iOS 延迟升级完整教程/29d7fc24f269064a6de56da0c65e28db.jpeg)

- 在左侧文件列表中选择「Remove Supervision」-「System Files」，右侧搜索框搜索「ConfigurationProfiles」，右击「ConfigurationProfiles」文件夹，再点击「Restore selected item(s) to device」，**输入 Password 密码「1111」点击 OK，iPhone/iPad 即开始进入恢复模式。等待开机后按步骤激活设备，再打开系统设置就会发现设备已经关闭「监督模式」**

  ![150f7](./assets/iOS 延迟升级完整教程/150f7f4f72f2b546699ab015945e2751.jpeg)

### Mac 版教程

- iPhone/iPad 连接 Mac 电脑，打开 Mac 的 App Store，搜索苹果自家的「 Apple Configurator」应用，安装后打开，点击「开始使用」：

  ![0e29d](./assets/iOS 延迟升级完整教程/0e29d1f56b7f99ea9bd15b7dd3eab725.png)

  ![2ac7b](./assets/iOS 延迟升级完整教程/2ac7b0a85bfc94ea85efb52294c6a169.png)

- 点击已连接的设备，再点击「准备」：

  ![c5e5e](./assets/iOS 延迟升级完整教程/c5e5e70518edc9daf1ba312da2f54f19.jpeg)

- 选择「手动配置」，再勾选「监督设备」，再点击「下一步」：

  ![86e35](./assets/iOS 延迟升级完整教程/86e359fdacdfe8f5afb250ea4ca7347d.jpeg)

- 选择「不注册 MDM」，再点击「下一步」：

  ![60d11](./assets/iOS 延迟升级完整教程/60d1189014c54922a94d95a9ebcf0670.jpeg)

- 不用输入 Apple ID，直接点击「跳过」：

  ![fbd1a](./assets/iOS 延迟升级完整教程/fbd1ae5d21500d9eb2e2a92ab409f411.jpeg)

- 自定义一个名称，其他空着不用填，再点击「下一步」：

  ![6f3b6](./assets/iOS 延迟升级完整教程/6f3b6af01933fb9511d174feae7458ed.jpeg)

- 勾选「生成新的监督身份」，再点击「下一步」：

  ![2d7e0](./assets/iOS 延迟升级完整教程/2d7e0d36da0e9bd1ae6c22049263124f.jpeg)

- 点击「准备」，输入 Mac 用户密码「更新设置」：

  ![17369](./assets/iOS 延迟升级完整教程/173697a409fa980329fff5bb2bf773e8.jpeg)

- 接下来需要点击「抹掉」，确保在此之前你已经备份了设备资料：

  ![069c6](./assets/iOS 延迟升级完整教程/069c6069761a10d1f287c0e8010fedf1.jpeg)

- 抹除完成前不可断开设备与 Mac 的连接，等待抹除完成后，按正常步骤激活设备：

  ![4e0b0](./assets/iOS 延迟升级完整教程/4e0b040b213643e46a9a0ae4f7e19d08.jpeg)

- 激活设备后打开「设置」即可发现已经处于「监督模式」，然后用自带 Safari 浏览器打开<<https://dhinakg.github.io/delayed-otas.html>，如果你是iPhone 12/13 设备就选 iOS (iPhone 12 series/13 series only) 这一栏里的「Download profile」，如果是旧机型就选「iOS (all other non-legacy devices)」里的「Download profile」，iPadOS 同理。点击对应的「Download profile」安装描述文件，「允许」（这里以 iPhone 6s 为例）：

  ![35d2e](./assets/iOS 延迟升级完整教程/35d2ea22972c773a48fb7dd2367bd15b.jpeg)

- 再打开「设置」，点击「已下载描述文件」安装「OTA Delay – 90 Days」描述文件，重启设备后再打开「设置」-「通用」-「软件更新」安装延迟升级的 iOS/iPadOS 新系统，升级完成后接下来我们要关闭「监督模式」，直接在「设置」-「通用」-「传输或还原 iPhone」-「抹掉所有内容和设置」即可关闭「监督模式」（抹除后可以通过之前备份还原设备用户资料）：

  ![34c7f](./assets/iOS 延迟升级完整教程/34c7fe4ad7a3920c1597c4d1930417be.jpeg)

## 已越狱设备延迟升级教程

- Cydia/Sileo 添加以下三个源地址：

  [https://cydia.ichitaso.com/](https://cydia.ichitaso.com/)

  [https://dhinakg.github.io/repo/](https://dhinakg.github.io/repo/)

  [https://repo.cadoth.net/](https://repo.cadoth.net/)

- 安装「SupervisedEnabler」和「Dallas」这两个插件：

  ![7a6da](./assets/iOS 延迟升级完整教程/7a6da50e774954f80421231b67cfd1f8.jpeg)

- 安装完这两个插件后设备会重启，重启后打开越狱工具激活越狱环境，然后用自带 Safari 浏览器打开<<https://dhinakg.github.io/delayed-otas.html>，如果你是iPhone 12/13 设备就选 iOS (iPhone 12 series/13 series only) 这一栏里的「Download profile」，如果是旧机型就选「iOS (all other non-legacy devices)」里的「Download profile」，iPadOS 同理。点击对应的「Download profile」安装描述文件，「允许」（这里以 iPhone 6s 为例）：

  ![8fab7](./assets/iOS 延迟升级完整教程/8fab712beb7f26f8b11d2a69b34a5f7d.jpeg)

- 再打开「设置」，此时设备已经处于「监督模式」，点击「已下载描述文件」安装「OTA Delay – 90 Days」描述文件，然后重启设备，重启设备后打开越狱工具（这里以 unc0ver 为例），点击工具右上角设置，将「Disable Auto Updates（不允许自动升级）」关闭再激活越狱环境：

  ![455f1](./assets/iOS 延迟升级完整教程/455f18b17e554947abb70f473c3675fa.jpeg)

- 激活越狱后再打开「设置」-「通用」-「软件更新」检查是否收到想要的 iOS 版本系统更新推送（有时需要向下滑动才能看到），收到升级包之后不要直接升级，越狱设备需要先清理越狱环境后才能正常升级【[点击查看保留资料一键清理越狱教程](http://mp.weixin.qq.com/s?__biz=MzUzOTU4NDM3OA==&mid=2247496038&idx=1&sn=01290ed849dc1682a59a0e93461d0105&chksm=fac48373cdb30a65176f1c30ace0d1731d1cf095832e022d0f5dec6f1bb556fb760f809416e8&scene=21#wechat_redirect)】，重启设备，打开越狱工具清理完越狱环境后（可重复操作清理几次）再打开「设置」-「通用」-「软件更新」安装更新，安装完延迟升级的 iOS/iPadOS 新系统之后，接下来我们要关闭「监督模式」，方法很简单，直接在「设置」-「通用」-「传输或还原 iPhone」-「抹掉所有内容和设置」即可关闭「监督模式」（所以之前要求先备份设备资料，这样抹除后可以通过备份还原设备用户资料）：

  ![df925](./assets/iOS 延迟升级完整教程/df925d782f275f3d333048dda9293a18.jpeg)

