title: 一个伪Vim党的习惯养成
date: 2019-05-10
tag:
 - ahk
 - autohotkey
 - vim
---

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

---

### 常用的Vim命令：
 - 切换到常态：`Esc`或`Ctrl+O`
 - 显示行号：`:set nu`
 - 取消行号：`:set nonu`
 - 往下查找：`/word` 配合n或N来索引下一个匹配项
 - 往上查找：`?word` 配合n或N来索引下一个匹配项
 - 创建文件：`:new filename` - 打开文件：`:vim filepath`
 - 重新加载文件`:e!`
 - 保存文件并退出：`:wq!`
 - 不保存文件直接退出：`:q!`
 - 打开函数列表：`tb`
 - 切换窗口：`Ctrl+W` [j k l n]
 - 在文件夹文件夹下查找文库本：`:Ag word`
 - 不采用插件直接自动补全：`Ctr+N` `Ctrl+P`
 - 快速输入文件名：在插入模式下，按下`Ctrl+X` `Ctrl+F`
 - 设置搜索时忽略字母的大小写差异：`:set ic`
 - 设置搜索使用字母的大小写匹配；`:set noic`
 - 搜索当前文件夹的文件：`;p`(常态下)
 - 回到刚才编辑的文件：`:e#`(常态下)
 - 进入块模式编辑：`Ctrl+v`
  - 在块的前面插入字符：`Shift+i`
  - 在块的后面插入字符：`Shift+a`
 - 假设安装了 **NERD Commenter** 插件，那么可以使用下列方式来进行代码注释：
   - 设置光标所在行的注释：`;cc`
   - 取消光标所在行的注释：`;cu`
   - 切换光标所在行的注释/非注释状态；`;c<space>`
 - 切换tab
   - 关闭当前的tab：`:tabc`
   - 关闭所有其他的tab：`:tabo`
   - 查看所有打开的tab：`:tabs`
   - 前一个：`:tabp`
   - 后一个：`:tabn`
 - 设置Vim的快捷键，直接在_VIMRC上插入这些语句即可：`map <F10> <Esc>:!explorer %:p:h<CR>`
 - 在资源管理器上显示(仅Windows)：`map <F10> <Esc>:!explorer /select, %:p<CR>`
 - 代码折叠
   - 打开关闭折叠：`zi`
   - 查看此行：`zv`
   - 关闭折叠：`zm`
   - 关闭所有：`zM`
   - 打开：`zr`
   - 打开所有：`zR`
   - 折叠当前行：`zc`
   - 打开当前折叠：`zo`
   - 删除折叠：`zd`
   - 删除所有折叠：`zD`
 - 命令集
   - 替换文本所有字符串：`:%s/oldstr/newstr/g`
   - 搜索文件夹的字符串：`:lv /正则表达式/gj *`，注意需要配合`:lw`来查看搜索结果
 - 分割窗口调整
   - 纵向调整
     - 纵向扩大(行数增加)：`:ctrl+w +`
     - 纵向缩小(行数减少)：`:ctrl+w -` 
     - 显示行数调整为num行：`:res(ize) num`
     - 把当前窗口高度增加num行：`:res(ize)+num` 
     - 把当前窗口高度减少num行：`:res(ize)-num` 
   - 横向调整
     - 指定当前窗口为num列：`:vertical res(ize) num`
     - 把当前窗口增加num列：`:vertical res(ize)+num` 
     - 把当前窗口减少num列：`:vertical res(ize)-num` 
   - 文件浏览
     - 在侧边栏中打开目录树：`:NERDTREE`
     - 显示当前文件所在侧边栏：`:NERDTreeFind`
     - 打开当前文件所在目录树(窗口不分割)：`:Ex(plore)`
     - 打开当前文件所在目录树(水平分割窗口)：`:Se(xplore)`
     - 打开当前文件所在目录树(垂直分割窗口)：`:Ve(xplore)`

### Chrome浏览器下的Vim模式
>在Chrome浏览器的应用商店里安装**Vimium**插件即可，不过，由于众所周知的原因，如果不自建梯子是访问不了的，此时可以到[Crx4Chrome](https://www.crx4chrome.com/crx)上下载并安装此插件。以下罗列一些常用的快捷键操作：

 - 标签页间操作
   - 跳到左侧标签页(Vimium)：`J(Shift+h)`
   - 跳到右侧标签页(Vimium)：`K(Shift+j)`
   - 跳到最左端标签页(Vimium)：`g0`
   - 跳到最右端标签页(Vimium)：`g$`
   - 查找已打开的标签页：`T(Shift+t)`
   - 关闭标签页(Vimium)：`x`
   - 跳到左侧标签页(内置)：`Ctrl+Shift+Tab`
   - 跳到右侧标签页(内置)：`Ctrl+Tab`
   - 关闭标签页(内置)：`Ctrl+w`

 - 页内移动
   - 往下移动：`j`
   - 往上移动：`k`
   - 往左移动：`h`
   - 往右移动：`h`
   - 移动到顶端：`gg`
   - 移动到底端：`G(Shift+g)`

 - 页内操作
   - 选择文本：`v`
   - 输入文本：`i`
   - 复制被选中文本：`y`
   - 找到当前页面的首个文本框输入：`gi`
   - 复制当前标签页链接：`yy`
   - 在本标签页内打开剪贴板上的链接：`p`
   - 新开标签页来打开剪贴板上的链接：`P(Shift+p)`
   - 打开可挑选的跳转面板：`f`
   - 在本标签页内往前跳转：`H(Shift+h)`
   - 在本标签页内往后跳转：`L(Shift+l)`
   - 在本标签页内刷新(Vimium)：`r`
   - 在本标签页内刷新(内置)：`F5`

 - 页内查找
   - 查找文本(Vimium)：`/`
   - 往下查找匹配项(Vimium)：`n`
   - 往上查找匹配项(Vimium)：`N(Shift+n)`
   - 查找文本(内置)：`Ctrl+F`

 - 书签/历史
   - 在本标签页来打开书签/历史的链接：`o`
   - 新开标签页来打开书签/历史的链接：`O(Shift+o)`
   - 在本标签页来打开书签的链接：`b`
   - 新开标签页来打开书签的链接：`B(Shift+b)`

---

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
---

### FAQ
 - 在shell vim上粘贴文本出现缩进错乱的问题
   >这个需要设置终端Vim的粘贴模式为粘贴保留格式：`:set paste`
 - 如何进行Vim 插件开发
   >学习[Vimscript 文档](https://www.w3cschool.cn/vim/gsenvozt.html)
 - 如何查看ahk的内置变量
   - ![查看ahk的内置变量](/assets/2019-10-02/1570005377287.png)
     >比如，`%A_WorkingDir%`为ahk.exe的工作目录