---
title: opencv和matplotlib的一些小问题
mathjax: true
date: 2018-04-06 18:49:03
categories:
- 工程
tags:
- python3
- opencv3
- matplotlib
---
[问题参考](https://stackoverflow.com/questions/15072736/extracting-a-region-from-an-image-using-slicing-in-python-opencv/15074748#15074748)
- opencv
当调用opencv的imread函数读取图像时，若读取彩色图像，返回的彩色图像以BGR顺序保存，而不是
我们常见的RGB形式保存。
- matplotlib
当调用pylot的imshow函数显示彩色图像时，默认是以RGB形式显示的，所以用opencv打开的图像需要做进一步处理方可正常显示。
- 解决方法 **BGR ----> RGB**
    -  b, g, r = cv2.split(img)
        img = cv2.merge(\[r, g, b\]) 从代码来看，就是更换顺序再合并
    -  img = img\[:, :, ::-1\] or img = img\[..., ::-1\] 这种方式利用了numpy的切片操作， 代码就是反转第三维数列，（img数据类型要注意，为np.ndarray）
    -  img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB) 调用官方API
