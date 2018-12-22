---
english_title: draco-guide-1
title: draco教程（一）：准备工作
date: 2017-07-11 10:46:16
---

如何生成draco_encoder、draco_decoder文件?

<!-- more -->

---

索引：

draco教程（一）：准备工作
[draco教程（二）：3D模型obj压缩](http://oddcn.cn/2017/07/12/draco-guide-2/)
[draco教程（三）：draco与Three.js相遇](http://oddcn.cn/2017/07/26/draco-guide-3/)

---

# draco是什么？

Google大法好，这是该开源项目的地址：https://github.com/google/draco

官方描述：
> Draco是用于压缩和解压缩3D几何网格和点云的库，旨在改善3D图形的存储和传输。

通俗地讲：
draco帮我们把3D模型中的.obj文件，编码压缩成draco的.drc文件，在之后的使用过程中，我们再用draco提供的API将.drc解码。

经测试，256MB的.obj在默认参数压缩的情况下，可压缩至6MB；而如果像我们平时用到的普通3D模型，几MB大小的.obj，压缩后就是几十几百KB的.drc。

# 准备

由于Windows对于开发者不友好，笔者强烈推荐Windows用户安装虚拟机，使用Ubuntu进行下面的cmake和make等操作。

Mac用户和Linux用户请略过。

1. VirtualBox下载：https://www.virtualbox.org/wiki/Downloads
2. Ubuntu下载：http://cn.ubuntu.com/download/
3. VirtualBox设置共享文件夹：[参考](http://blog.csdn.net/longerzone/article/details/32119457)、[疑难解决](http://blog.csdn.net/longerzone/article/details/32119457)

# 下载源码

## 安装git

打开终端，安装git。

![install_git](http://oqmaz8z4y.bkt.clouddn.com/draco/install_git.png)

## clone

git安装完成后，使用命令`git clone https://github.com/google/draco.git`下载源码。

![git_clone](http://oqmaz8z4y.bkt.clouddn.com/draco/git_clone.png)

# 编译

为了获得编码所使用的draco_encoder文件、和解码所使用的draco_decoder文件，需要cmake和make这两个步骤。

## cmake

进入刚才新建的文件夹，这时我们可以看到名为draco的文件夹了，这就是这个开源项目的源码，右键该文件夹，然后选择“在终端打开”。

执行`cmake`后发现，就像上面的git一样，Ubuntu还没有安装cmake，按照提示安装即可。

执行`cmake ./`

![cmake](http://oqmaz8z4y.bkt.clouddn.com/draco/cmake.png)

> 你或许听过好几种 Make 工具，例如 GNU Make ，QT 的 qmake ，微软的 MS nmake，BSD Make（pmake），Makepp，等等。这些 Make 工具遵循着不同的规范和标准，所执行的 Makefile 格式也千差万别。这样就带来了一个严峻的问题：如果软件想跨平台，必须要保证能够在不同平台编译。而如果使用上面的 Make 工具，就得为每一种标准写一次 Makefile ，这将是一件让人抓狂的工作。
> CMake就是针对上面问题所设计的工具：它首先允许开发者编写一种平台无关的 CMakeList.txt 文件来定制整个编译流程，然后再根据目标用户的平台进一步生成所需的本地化 Makefile 和工程文件，如 Unix 的 Makefile 或 Windows 的 Visual Studio 工程。从而做到“Write once, run everywhere”。

上面我们可以直接cmake是因为draco文件夹中已经内置了CMakeLists.txt。

## make

这里很简单，直接执行`make`，然后等待它完成。

![make](http://oqmaz8z4y.bkt.clouddn.com/draco/make.png)

此时进入draco文件夹，可以看到我们已经生成draco_encoder、draco_decoder文件了。

![en_de](http://oqmaz8z4y.bkt.clouddn.com/draco/encoder_decoder.png)