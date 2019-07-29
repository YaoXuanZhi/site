---
title: 不同操作系统的使用习惯备忘录
date: 2019-07-24
---

  - ✔ Office 套件
    - Windows：Exe、Zip、7z(官方下载地址：Windows应用商店和各种软件的官网)
      >msys2下可以使用`pacman -S xxx`
    - Mac：Dmg、Pkg(官方软件包：App Store)
    - Linux(Ubuntu)：`apt-get install xxx`
    - Linux(CentOS)：`yum install -g xxx`

  - ✔ Office 套件
    - Windows：Wps Office
    - Mac：Wps Office
    - Linux(Ubuntu)：Wps Office

  - ✔ App Package
    - Windows：Exe、Zip、7z(官方下载地址：Windows应用商店和各种软件的官网)
    - Mac：Dmg、Pkg(官方软件包：App Store)，和homebrew
    - Linux(Ubuntu)：apt-get install xxx
    - Linux(CentOS)：yum install -g xxx

  - ✔ 浏览器
    - Windows：CentBrowser、Chrome
    - Mac：Chrome
    - Ubuntu：Chrome
    >注意，还需要搭配`Vimium`插件

  - ❑ Gif录制工具：
    - Windows：Licecap
    - Mac：Licecap
      >不能全屏录制啥的，还有不能将应用程序的顶部菜单栏进行绘制

  - ❑ 截图／贴图工具
    - Windows：Snipaste
    - Mac：Snipaste

  - ✔ 高级编辑器：VSCode、Vim

  - ✔ 开发工具：IdeaU(包含了Java、Python、Php、Lua、Erlang、Golang、Rust等多种语言) CLion(C++)
    >注意，还需要搭配`ideaVim`插件

  - ✔ 热键辅助工具：
    - Windows：AutoHotKey
    - Mac：AppleScript

  - ✔ 进入终端操作
    - Mac：**【Mac+Shift+ `】**
    - Windows：**【Win+R】**，然后输入`cmd`
    - Linux(Utuntu)：**【Ctrl+Alt+T】**

  - ✔ 强制关闭某个进程(ps：注意，这个要用Gif来进行演示哦)
    - Windows:**【Shift+Ctl+Esc】**打开任务管理器，然后找到对应的进程关闭
    - Mac: 鼠标点击左上角的 `苹果图标`，然后左击打开菜单，找到 `强制退出` 菜单项进行退出

  - ✔ 在终端打开文件夹所在窗口
    - Windows：`explorer .`
    - Mac：`open .`

  - ❑ 安装随身WiFI驱动
    >包括但不限于360随身WIFI
    - Windows：
      - [360随身WIFI官网](http://wifi.360.cn/easy/pc/)
    - Ubuntu：
      ```sh
      sudo add-apt-repository ppa:thopiekar/mt7601
      sudo apt-get update
      sudo apt-get install mt7601-sta-dkms
      ```
    - 参考资料
      - [双系统win+ubuntu14.04使用360随身wifi 3代](https://blog.csdn.net/mdjxy63/article/details/78304708/)
      - [360/小米/百度 随身wifi Ubuntu下作为无线网卡使用](https://www.cnblogs.com/platero/p/4417458.html)