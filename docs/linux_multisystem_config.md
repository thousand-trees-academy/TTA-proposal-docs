# Linux + Windows 双系统配置

>在本章节，你可以学习到的内容：
>
>* 配置你的第一个双系统主机
>* 搭建基本的 Linux 开发环境（基于 Ubuntu 18.04）

## 什么是 Linux？

>**Linux**（[![聆听](https://images.weserv.nl/?url=upload.wikimedia.org/wikipedia/commons/thumb/3/3b/Speakerlink-new.svg/11px-Speakerlink-new.svg.png)](https://images.weserv.nl/?url=upload.wikimedia.org/wikipedia/commons/0/03/Linus-linux.ogg)**[i](https://wiwiki.kfd.me/wiki/File:Linus-linux.ogg)**[/ˈlɪnəks/](https://wiwiki.kfd.me/wiki/Help:英語國際音標) [*LIN-əks*](https://wiwiki.kfd.me/wiki/Wikipedia:發音重拼)）是一种[自由和开放源码](https://wiwiki.kfd.me/wiki/自由及开放源代码软件)的[类UNIX](https://wiwiki.kfd.me/wiki/类Unix系统)[操作系统](https://wiwiki.kfd.me/wiki/作業系統)。该操作系统的[内核](https://wiwiki.kfd.me/wiki/内核)由[林纳斯·托瓦兹](https://wiwiki.kfd.me/wiki/林纳斯·托瓦兹)在1991年10月5日首次发布[[5\]](https://wiwiki.kfd.me/wiki/Linux#cite_note-5)[[6\]](https://wiwiki.kfd.me/wiki/Linux#cite_note-6)，在加上[用户空间](https://wiwiki.kfd.me/wiki/使用者空間)的[应用程序](https://wiwiki.kfd.me/wiki/應用程式)之后，成为Linux操作系统。Linux也是[自由软件](https://wiwiki.kfd.me/wiki/自由软件)和[开放源代码软件](https://wiwiki.kfd.me/wiki/开放源代码软件)发展中最著名的例子。只要遵循[GNU 通用公共许可证](https://wiwiki.kfd.me/wiki/GNU通用公共许可证)（GPL），任何个人和机构都可以自由地使用Linux的所有底层[源代码](https://wiwiki.kfd.me/wiki/源代码)，也可以自由地修改和再发布。大多数Linux系统还包括像提供[GUI](https://wiwiki.kfd.me/wiki/GUI)的[X Window](https://wiwiki.kfd.me/wiki/X_Window)之类的程序。除了一部分专家之外，大多数人都是直接使用[Linux 发行版](https://wiwiki.kfd.me/wiki/Linux發行版)，而不是自己选择每一样组件或自行设置。（from 维基百科）

目前你可以简单地把它理解为与你电脑上的 Windows 系统类似的另一种操作系统，不过它是完全开源的。

## 你为什么需要 Linux？

对于学习计算机相关专业的同学来说，学会操作 Linux 是一项几乎必备的技能。在本科阶段接下来的学习中，有相当大一部分专业课程需要你学习操作 Linux，因为它的内核代码完全开源，意味着你可以对照其源码来研究操作系统中很多操作的具体实现，并由此对所学知识有更深刻的认识。

## 为什么是双系统，而不是虚拟机或其他的解决方案？

你可能在某些教程/听说过其他相对更加简单，快速地搭建 Linux 系统环境的方式（如安装虚拟机）。但在某些情况下虚拟机可能不会满足你的需求。

如果你即将配置的项目需要用到 GPU 计算资源（需要用到显卡），这通常意味着你需要配置 CUDA + Linux 的环境，而虚拟机由于无法安装 NVIDIA 显卡驱动，就无法满足你的要求。另外，相对虚拟机有可能对速度有所影响的情况，实机 Linux 更能充分利用电脑上的系统资源。所以某些时候需要同学们去实机配置自己的 Linux 环境。

这样就涉及到在本机原系统是 Windows 下来安装配置你的**实机** Linux 环境，如果不想将 Linux 作为主要的操作系统（替代Windows），主要的解决方法是单/双硬盘上的 Windows + Linux。

* 单硬盘双系统的优点是可以在笔记本不支持硬盘拓展的情况下配置环境，缺点是 Linux 与 Windows 系统隔离性不好，如果在 Linux 下误操作可能会影响到原有系统的数据安全。

* 双硬盘的优点是隔离性较好，缺点是需要一定的动手能力，笔记本需要支持硬盘扩展以及相应的硬件成本。

为了搭建实机环境，你可以选择其中一种方式来操作。我的个人建议是利用双硬盘来搭建整个环境，这样隔离性更好，可以将你在日常系统中的数据和 Linux 中的系统数据隔离开。

> **注意：当你开始以下操作之前，请备份好你的全部重要数据，以防数据丢失。**

## 配置双系统的前置准备工作

### 确定你的电脑是否支持双硬盘

首先如果你的电脑是台式机，一般来说都会支持多块硬盘的安装，也即你可以选择双硬盘安装系统的方式。

如果你的电脑是笔记本电脑，请向你的经销商确认电脑是否有两个硬盘位，如果有，请继续确认硬盘位对应的接口类型，防止购买错误。

### 固态硬盘的选购

请参照教程 [计算机配件介绍]() 一节。

### 安装固态硬盘

> 自行拆解电脑可能影响你的电脑保修，同时某些电脑品牌可能不会接受自行购买电脑配件的安装，购买电脑、固态硬盘前请务必咨询清楚。

建议携带你的硬盘与电脑到正规电脑维修中心寻求专业人员的帮助。

### 制作你的第一个系统启动盘

> **注意：当你开始以下操作之前，请备份好你的全部重要数据，以防数据丢失。**

#### 前置准备

* 一块 U 盘（最低容量 4 GB）本步骤会清除你手中 U 盘的所有数据，所以尽量选择不常用的U盘，**并做好数据备份**。
* 在 Windows 系统上安装 [UltraISO](https://cn.ultraiso.net/xiazai.html) 软件（用于烧录镜像，你可以使用试用版）

#### 镜像选择

> **Linux 发行版**（英语：Linux distribution，也被叫做**GNU/Linux 发行版**），为一般用户预先集成好的[Linux](https://wiwiki.kfd.me/wiki/Linux)[操作系统](https://wiwiki.kfd.me/wiki/作業系統)及各种应用软件。一般用户不需要重新[编译](https://wiwiki.kfd.me/wiki/编译)，在直接安装之后，只需要小幅度更改设置就可以使用，通常以[软件包管理系统](https://wiwiki.kfd.me/wiki/软件包管理系统)来进行应用软件的管理。Linux发行版通常包含了包括[桌面环境](https://wiwiki.kfd.me/wiki/桌面环境)、[办公包](https://wiwiki.kfd.me/wiki/办公套件)、[媒体播放器](https://wiwiki.kfd.me/wiki/媒体播放器)、[数据库](https://wiwiki.kfd.me/wiki/数据库)等应用软件。这些[操作系统](https://wiwiki.kfd.me/wiki/操作系统)通常由Linux内核、以及来自GNU计划的大量的[函数库](https://wiwiki.kfd.me/wiki/函式庫)，和基于[X Window](https://wiwiki.kfd.me/wiki/X_Window)的图形界面。有些发行版考虑到容量大小而没有预装 X Window，而使用更加轻量级的软件，如：[BusyBox](https://wiwiki.kfd.me/wiki/BusyBox)、[musl](https://wiwiki.kfd.me/wiki/Musl)或[uClibc-ng](https://wiwiki.kfd.me/wiki/UClibc)。现在有超过300个Linux发行版（[Linux发行版列表](https://wiwiki.kfd.me/wiki/Linux发行版列表)）。大部分都正处于活跃的开发中，不断地改进。
>
> 由于大多数软件包是[自由软件](https://wiwiki.kfd.me/wiki/自由软件)和[开源软件](https://wiwiki.kfd.me/wiki/开源软件)，所以Linux发行版的形式多种多样——从功能齐全的桌面系统以及服务器系统到小型系统（通常在[嵌入式](https://wiwiki.kfd.me/wiki/嵌入式)设备，或者启动[软盘](https://wiwiki.kfd.me/wiki/软盘)）。除了一些定制软件（如安装和配置工具），发行版通常只是将特定的应用软件安装在一堆[函数库](https://wiwiki.kfd.me/wiki/函式庫)和内核上，以满足特定用户的需求。
>
> 这些发行版可以分为商业发行版，比如[Ubuntu](https://wiwiki.kfd.me/wiki/Ubuntu)（[Canonical公司](https://wiwiki.kfd.me/wiki/Canonical公司)）、[Red Hat Enterprise Linux](https://wiwiki.kfd.me/wiki/Red_Hat_Enterprise_Linux)、[openSUSE](https://wiwiki.kfd.me/wiki/OpenSUSE)（[Novell](https://wiwiki.kfd.me/wiki/Novell)）；和社区发行版，它们由自由软件社区提供支持，如[Debian](https://wiwiki.kfd.me/wiki/Debian)、[Fedora](https://wiwiki.kfd.me/wiki/Fedora)、[Arch](https://wiwiki.kfd.me/wiki/Arch_Linux)和[Gentoo](https://wiwiki.kfd.me/wiki/Gentoo_Linux)。（from 维基百科）

实际上我们日常所说的 Linux 系统一般指 Linux 发行版。Linux 本身并不包括图形界面。没有图形界面的 Linux 系统，只能通过命令行来管理。

对于新手来说，一个易于使用的 Linux 发行版镜像可以帮助你快速上手，忽略各种繁杂的问题。在这里推荐 Ubuntu 发行版，本章节接下来的部分将以 Ubuntu 18.04 LTS 为例。

> **Ubuntu**（[国际音标](https://wiwiki.kfd.me/wiki/國際音標)：[/ʊˈbʊntuː/](https://wiwiki.kfd.me/wiki/Help:英語國際音標)，[*uu-BUUN-too*](https://wiwiki.kfd.me/wiki/Wikipedia:發音重拼)）[[7\]](https://wiwiki.kfd.me/wiki/Ubuntu#cite_note-7)[[8\]](https://wiwiki.kfd.me/wiki/Ubuntu#cite_note-about_ubuntu-8)是基于Debian，以桌面应用为主的[Linux发行版](https://wiwiki.kfd.me/wiki/Linux發行版)。Ubuntu有三个正式版本，包括桌面版、[服务器](https://wiwiki.kfd.me/wiki/服务器)版及用于[物联网](https://wiwiki.kfd.me/wiki/物联网)设备和[机器人](https://wiwiki.kfd.me/wiki/机器人)的Core版。从17.10版本开始，Ubuntu以[GNOME](https://wiwiki.kfd.me/wiki/GNOME)为默认[桌面环境](https://wiwiki.kfd.me/wiki/桌面环境)。[[9\]](https://wiwiki.kfd.me/wiki/Ubuntu#cite_note-9)
>
> Ubuntu是著名的Linux发行版之一，也是目前最多用户的[Linux](https://wiwiki.kfd.me/wiki/Linux)版本。Ubuntu每六个月（即每年的四月与十月）发布一个新版本，长期支持（LTS）版本每两年发布一次。普通版本一般只支持9个月，但LTS版本一般能提供5年的支持。

在 [中国科大开源软件镜像站](https://mirrors.ustc.edu.cn/) 你可以在 获取安装镜像 处获得 Ubuntu /其他发行版各个版本的发行版镜像（iso文件）。

#### 镜像烧录

你可以参考这篇 [百度经验](https://jingyan.baidu.com/article/154b46311befea28ca8f41ae.html)，需要注意的是：

* 第二步你需要找到并打开你下载的 **Ubuntu** 镜像文件，而不是教程中的**Windows** 安装镜像。
* **特别注意：**第四步你需要确保**硬盘驱动器**项你选择的是你拿来做启动盘的U盘而不是其他盘。

当烧录完成之后你就有了你的第一块系统安装盘啦！让我们进入下一步。

### 安装 Ubuntu 18.04 系统

在你的电脑上插入之前安装好的启动盘，开机同时进行一些操作进入 BIOS 模式

> 啥是一些操作！！！
>
> 因为不同电脑对应进入 BIOS 的方法不同，请到网上搜索“ XXX 电脑如何进入 BIOS 模式”。
>
> 常见进入 BIOS 模式的方法可以参见 [百度经验](https://jingyan.baidu.com/article/d45ad14875f56c69542b8060.html)。

在 BIOS 模式中选择用 U 盘启动或设置启动顺序，将你的U盘设置为第一位，保存退出重启，此时你应该可以看到 Ubuntu 安装程序已经启动了。

你可以选择 Try Ubuntu without installing，在进入之后在桌面选择 Install Ubuntu。

双硬盘分区可以参考[这篇博客](https://www.pianshen.com/article/5493316203/)。如果你感觉根目录不够多就多分一点，或者不单独挂载/usr分区也是可以的。

正常安装后重启就可以看到 GRUB 的引导界面，选择 Ubuntu 之后就可以进入系统啦！

## 在 Linux 中的第一个 `Hello world`
你可以很方便地在系统中用 `ctrl + T` 打开终端（Terminal）。
试试输入这行命令，并回车执行它吧：

```bash
echo "Hello,World!"
```
它的意思是在终端输出一个字符串 `Hello, World!`，你可以得到以下输出：

```bash
Hello,World!
```

## Linux 基本操作

对于 Linux 的基本操作以及进阶内容，中国科大 Linux User Group （USTC LUG） 撰写了一份相当详细的讲义 [Linux 101](https://101.ustclug.org/)。在这里你可以继续探索 Linux 的更多用法。 Enjoy！
