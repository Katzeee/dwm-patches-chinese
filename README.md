# dwm-patches-chinese
The Chinese translation of DWM patches / DWM补丁的中文翻译

最近入坑Arch，了解到Window Manager的概念，从此展开了对dwm的探索。

为了探索各补丁的功能，我一一翻看dwm的各补丁，仅从标题能得到的信息太少，点入详情页也有很多解释不清楚的补丁，因此在此给出各补丁功能的中文翻译以及部分自己的理解与使用效果，以便各位找到适合自己的补丁，也欢迎各位分享自己的使用体验，推荐功能强大的补丁。

并不是每一个patch我都使用过，我的解释大多来源于对代码的理解，因此可能有错误的地方，欢迎各位指正。

在此先给出常用词汇的解释：
- monitor：显示器，针对多显示器用户，外接显示器用户。
- tag：最初页面上出现的1-9个界面每一个都是一个tag。
- bar：显示tag和状态栏的最上面的条。
- client：每一个tag上的一个任务界面是一个client，比如在tag1打开两个st，则每一个st的界面被称为一个client。
- focus：目前可以进行操作的client就是被focus的，也就是聚焦。
- vaccant：空闲的，一个没有client的tag就是一个vaccant tag。
- tary：系统托盘，最小化的图标显示的位置。
- master：新创建的client会被放在左边也就使master的位置。