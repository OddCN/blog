---
english_title: project-remind-sleep-demo
title: Android：提醒睡觉Demo
date: 2017-06-25 10:46:16
---

弹出提示来提醒：快别玩手机了，该睡觉了！

<!-- more -->

---

躺在床上玩手机，玩着玩着看了下时间——“？？？，这么晚了！！”

那么咱需要这个。

# 截图

![p1][1]

上图：假设5点钟起床，那么从21点开始，每隔10分钟弹出一个Toast提醒睡觉。

![p2][2]

![p3][3]

# 细节

## 功耗与稳定性

该Demo的这种周期性的任务，选择JobSchedule妥妥的，功耗又低又不会被杀，缺点就是不那么准时。

通常以Alarm或服务形式执行的周期性任务，逃脱不过国内高度优化过的rom的绞杀，当然也逃不过最新的Android 8.0！



[1]: http://oqmaz8z4y.bkt.clouddn.com/notimemo/screenshot1.jpg?imageView2/2/w/300
[2]: http://oqmaz8z4y.bkt.clouddn.com/notimemo/screenshot2.jpg?imageView2/2/w/300
[3]: http://oqmaz8z4y.bkt.clouddn.com/notimemo/screenshot3s.jpg?imageView2/2/w/300

