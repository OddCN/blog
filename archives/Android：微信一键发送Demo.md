---
english_title: project-fast-wechat-demo
title: Android：微信一键发送Demo
date: 2017-06-24 10:46:16
---

将特定短句一键发送给微信好友

<!-- more -->

需求来源于生活中需要经常性地向某个人发送特定的内容，如若身处车来人往不方便打字，或是时间紧迫，来不及输入，就会有些捉急。

# 截图

![p1][1]

![p2][2]

# 细节

## 发送

在单击一项短语后，跳转至微信的分享页面，通过AccessibilityService寻找目标好友：

- 若分享页面找到了该好友，自动点击完成分享操作。

![gif1][3]

- 若分享页面未找到该好友，将好友名称粘贴到搜索框，等待用户操作。

![gif2][4]

以上的自动操作都通过AccessibilityService完成。

## 优化

1. 增加对误操作的补救措施：在发送前静待几秒。
2. 应对夜间出行的弱光环境，增加夜间模式。

![gif3][5]

3. 删除操作以及撤回

![gif4][6]

# 总结

此Demo依赖于Android的无障碍服务，通过这次尝试，初步接触了AccessibilityService。

由于自动点击等操作需要获知微信内相关View的id，而微信每次更新都会更换这些View的id，所以该Demo还需要一个在线的id管理库，根据用户的微信版本动态下发对应的id。

个人认为具有此类需求的人较少，所以仅做练习。

[1]: http://oqmaz8z4y.bkt.clouddn.com/fastwechat/screenshot1.jpg?imageView2/2/w/300
[2]: http://oqmaz8z4y.bkt.clouddn.com/fastwechat/screenshot2.jpg?imageView2/2/w/300
[3]: http://oqmaz8z4y.bkt.clouddn.com/fastwechat/fastwechat1s.gif
[4]: http://oqmaz8z4y.bkt.clouddn.com/fastwechat/fastwechat2.gif
[5]: http://oqmaz8z4y.bkt.clouddn.com/fastwechat/fastwechat3.gif
[6]: http://oqmaz8z4y.bkt.clouddn.com/fastwechat/fastwechat4.gif

