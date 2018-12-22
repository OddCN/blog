---
english_title: project-noti-memo
title: Android：通知栏备忘
date: 2017-06-24 16:46:16
---

在通知栏记录待办事项

<!-- more -->

市面上类似应用已经有很多了，但没有找到满足我个人需求的。于是我就动手做一个，希望同时具有功能多、简单这两个特征。

应用介绍：
```
使用本应用，可将每天待要处理、却又容易忘记的各种事项，以通知的形式展示在通知栏。 
与其他同类应用相比，本应用：实用小功能可提高操作效率；已通知的事项意外丢失后可以快速恢复；在界面设计、手势操作上对用户更加友好。
```
更新日志：
```
- 通知快捷操作：增加通知的编辑和完成功能。 
- 定制通知风格：个性化设置通知的样式和行为。 
- 通知栏快捷入口：在通知栏添加新建事项的入口。 
- 文字分享：选中文字分享至本应用即可新建一条事项。 
- 事项管理：可对所有事项进行管理和统一操作。 
- 即时保存：可快速恢复意外丢失的通知事项。 
- 优化手势操作：增加应用中各类滑动操作的成功率。
```

# 概览

![p1][1]

![p2][2]

![p3][3]

![p4][4]

![p5][5]

# 细节

## 优化手势操作

重写触摸事件的分发，增加滑动操作的成功率。

![gif][6]

## 快速恢复

快速恢复意外丢失的通知事项。（例如重启导致）

![gif][7]

## 定制通知风格

设置通知的样式。

![gif][8]

## 应对不同系统

设置操作通知的执行力度。

![gif][9]

## 较强的稳健性

应对花式操作可能带来的状况。

![gif][10]






[1]:  http://oqmaz8z4y.bkt.clouddn.com/notimemo/%E5%B9%BB%E7%81%AF%E7%89%871.JPG?imageView2/2/w/300
[2]:  http://oqmaz8z4y.bkt.clouddn.com/notimemo/%E5%B9%BB%E7%81%AF%E7%89%872.JPG?imageView2/2/w/300
[3]: http://oqmaz8z4y.bkt.clouddn.com/notimemo/%E5%B9%BB%E7%81%AF%E7%89%873.JPG?imageView2/2/w/300
[4]: http://oqmaz8z4y.bkt.clouddn.com/notimemo/%E5%B9%BB%E7%81%AF%E7%89%874.JPG?imageView2/2/w/300
[5]: http://oqmaz8z4y.bkt.clouddn.com/notimemo/%E5%B9%BB%E7%81%AF%E7%89%875.JPG?imageView2/2/w/300
[6]: http://oqmaz8z4y.bkt.clouddn.com/notimemo/notimemo1.gif
[7]: http://oqmaz8z4y.bkt.clouddn.com/notimemo/notimemo2.gif
[8]: http://oqmaz8z4y.bkt.clouddn.com/notimemo/notimemo3.gif
[9]: http://oqmaz8z4y.bkt.clouddn.com/notimemo/notimemo4.gif
[10]: http://oqmaz8z4y.bkt.clouddn.com/notimemo/notimemo5.gif
