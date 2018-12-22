---
english_title: draco-guide-2
title: draco教程（二）：3D模型obj压缩
date: 2017-07-12 10:46:16
---

3D模型文件obj、ply的压缩，以及参数配置

<!-- more -->

---

索引：

[draco教程（一）：准备工作](http://oddcn.cn/2017/07/11/draco-guide-1/)
draco教程（二）：3D模型obj压缩
[draco教程（三）：draco与Three.js相遇](http://oddcn.cn/2017/07/26/draco-guide-3/)

---

# 测试

继上一篇，现在我们已经得到了draco_encoder、draco_decoder，并且该项目也为我们准备了一些测试数据，就在testdata文件夹中。

![testdata](http://oqmaz8z4y.bkt.clouddn.com/draco/testdata.png)

draco_encoder可以将.obj或.ply编码压缩成.drc，我们就先拿测试数据中的bun_zipper.ply开刀。

依然在draco_encoder的外层文件夹draco，右键后选择“在终端打开”，执行命令`./draco_encoder -i testdata/bun_zipper.ply -o bunny.drc`

![encoder_saved](http://oqmaz8z4y.bkt.clouddn.com/draco/encoder_saved.png)

见到saved就说明压缩成功了，draco文件夹下已经可以找到bunny.drc，大小为82KB，而压缩前为3MB。

# 参数配置

压缩参数有两个：
1. **压缩率**：用cl表示，10为最大化压缩，1为最低档压缩。
2. **quantization bits**（量化位？）：用qp表示，数值越小输出文件越小，模型效果越差。推荐使用默认配置。

可以看到在上一步压缩测试对象的时候，draco默认使用了参数 cl：7、qp：14。

现在我们自己动手：
- 当参数为 cl：10 时：
  执行`./draco_encoder -i testdata/bun_zipper.ply -o bunny_cl10.drc -cl 10`
- 当参数为 cl：10、qp：12 时：
  执行`./draco_encoder -i testdata/bun_zipper.ply -o bunny_qp12_cl10.drc -qp 12 -cl 10`

测试不同数值的cl、qp参数，输出文件的大小如下表：

| bunny.drc | cl = 1 |  cl = 7 | cl = 10 |
| :-------: | -----: | ------: | ------: |
|  qp = 12  |   95KB |    57KB |    53KB |
|  qp = 14  |  121KB | 默认 82KB | 推荐 76KB |

cl参数的值越高，压缩率越高，压缩后文件体积越小，但在解码时更为耗时，因此需要对cl参数的取值做一个权衡。

降低qp参数的值虽然能够缩小输出文件，但降多了会对复杂模型的效果有较大影响，因此推荐尝试性地使用。

# 压缩obj

我准备了一个obj文件，名为tttttt.obj，大小为256MB，放在draco文件夹中，执行`./draco_encoder -i tttttt.obj -o tttttt_cl10.drc -cl 10`
压缩后的drc大小为5.7MB。