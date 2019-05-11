title: 一个伪Vim党的习惯养成
date: 2019-05-10
tag:
 - ahk
 - autohotkey
---
>作为一个伪Vim党，看个视频还要碰下鼠标太不舒服啦.jpg

### 常用工具的Vim化
 - 浏览器
   - Windows：CentBrowser + Vimium extension(Crx4Chrome)
   - Osx：Chrome + Vimium extension(Crx4Chrome)
 - IDE
   - Idea + IdeaVim
   - VS + VsVim
 - Editor
   - VSCode + Vim
   - Sublime修改配置即可
     >在`Preferences -> Settings`里如下设置：
     ```json
     {
         "ignored_packages": []
     }
     ```

### 键盘控制鼠标
>目前常用的工具安装了Vim插件后，并不能控制应用里的所有东西，比如在Chrome浏览器上查看视频时，Vimium插件是无法控制视频的播放/暂停的，因此有必要提供一个键盘控制鼠标的功能，让双手停留在键盘上
 - 键盘控制鼠标移动、点击
   - Windows：采用AutoHotKey可以实现，ahk如下：
      ```sh
      ; 鼠标往下移动
      !^down::
      mousemove,0,+8,0,R
      return

      ; 鼠标往上移动
      !^up::
      mousemove,0,-8,0,R
      return

      ; 鼠标往左移动
      !^left::
      mousemove,-8,0,0,R
      return

      ; 鼠标往右移动
      !^right::
      mousemove,+8,0,0,R
      return

      ; --------------鼠标点击

      ; 鼠标左击
      !^h::
      ; MouseClick, left,,, 1, 0, D  ; Hold down the left mouse button.
      MouseGetPos, x, y
      MouseClick, left, %x%, %y%
      return

      ; 鼠标右击
      !^l::
      MouseGetPos, x, y
      ; MouseClick, right, %x%, %y%
      ; ButtonRight
      ; MouseClick, right,,, 1, 0, D  ; Hold down the right mouse button.
      MouseClick, right, %x%, %y%
      return
      ```

   - Osx：采用ApplyScript+MouseTools可以实现： 
     - [MouseTools](http://www.hamsoftengineering.com/codeSharing/MouseTools/MouseTools.html)
      ```applescript
      -- 后续再补充了
      ```