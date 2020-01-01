---
title: 基于AutoHotKey整合自己的常用软件
date: 2019-06-08
---

>[AutoHotkey_L](https://github.com/Lexikos/AutoHotkey_L/releases)

### 常用的Ahk函数：
```ahk
;获取文件浏览器中被选中的文件路径
/*
	Library for getting info from a specific explorer window (if window handle not specified, the currently active
	window will be used).  Requires AHK_L or similar.  Works with the desktop.  Does not currently work with save
	dialogs and such.
	
	
	Explorer_GetSelected(hwnd="")   - paths of target window's selected items
	Explorer_GetAll(hwnd="")        - paths of all items in the target window's folder
	Explorer_GetPath(hwnd="")       - path of target window's folder
	
	example:
		F1::
			path := Explorer_GetPath()
			all := Explorer_GetAll()
			sel := Explorer_GetSelected()
			MsgBox % path
			MsgBox % all
			MsgBox % sel
		return
	
	Joshua A. Kinnison
	2011-04-27, 16:12
*/
Explorer_GetPath(hwnd="")
{
    if !(window := Explorer_GetWindow(hwnd))
        return ErrorLevel := "ERROR"
    if (window="desktop")
        return A_Desktop
    path := window.LocationURL
    path := RegExReplace(path, "ftp://.*@","ftp://")
    StringReplace, path, path, file:///
    StringReplace, path, path, /, \, All 
    
    ; thanks to polyethene
    Loop
        If RegExMatch(path, "i)(?<=%)[\da-f]{1,2}", hex)
            StringReplace, path, path, `%%hex%, % Chr("0x" . hex), All
        Else Break
    return path
}
Explorer_GetAll(hwnd="")
{
    return Explorer_Get(hwnd)
}
Explorer_GetSelected(hwnd="")
{
    return Explorer_Get(hwnd,true)
}
Explorer_GetWindow(hwnd="")
{
    ; thanks to jethrow for some pointers here
    WinGet, process, processName, % "ahk_id" hwnd := hwnd? hwnd:WinExist("A")
    WinGetClass class, ahk_id %hwnd%
    
    if (process!="explorer.exe")
        return
    if (class ~= "(Cabinet|Explore)WClass")
    {
        for window in ComObjCreate("Shell.Application").Windows
            if (window.hwnd==hwnd)
                return window
    }
    else if (class ~= "Progman|WorkerW") 
        return "desktop" ; desktop found
}
Explorer_Get(hwnd="",selection=false)
{
    if !(window := Explorer_GetWindow(hwnd))
        return ErrorLevel := "ERROR"
    if (window="desktop")
    {
        ControlGet, hwWindow, HWND,, SysListView321, ahk_class Progman
        if !hwWindow ; #D mode
            ControlGet, hwWindow, HWND,, SysListView321, A
        ControlGet, files, List, % ( selection ? "Selected":"") "Col1",,ahk_id %hwWindow%
        base := SubStr(A_Desktop,0,1)=="\" ? SubStr(A_Desktop,1,-1) : A_Desktop
        Loop, Parse, files, `n, `r
        {
            path := base "\" A_LoopField
            IfExist %path% ; ignore special icons like Computer (at least for now)
                ret .= path "`n"
        }
    }
    else
    {
        if selection
            collection := window.document.SelectedItems
        else
            collection := window.document.Folder.Items
        for item in collection
            ret .= item.path "`n"
    }
    return Trim(ret,"`n")
}
```

```ahk
; 设置窗口置顶

;激活并置顶当前窗体，直至，esc退出。
#t::
WinGetActiveTitle, OutputVar
WinSet, AlwaysOnTop, On,%OutputVar%
Return

$#+t::
WinSet, AlwaysOnTop, Off,%OutputVar%
Return
```

```ahk
; 修改窗口透明度
;左侧shift+鼠标滚轮调整窗口透明度（设置30-255的透明度，低于30基本上就看不见了，如需要可自行修改）2016.09.20.by M.（2017.01.11__1635 edit again.M）
;
;使用说明：
;   ◆左侧shift+滚轮下滑：减少透明度，一次10
;   ◆左侧shift+滚轮上滑：增加透明度，一次20
;   ◆左侧shift+中键按下：恢复透明度至255(完全不透明).
;
~LShift & WheelUp::
; 透明度调整，增加。
WinGet, Transparent, Transparent,A
If (Transparent="")
    Transparent=255
    ;Transparent_New:=Transparent+10
    Transparent_New:=Transparent+20    ;◆透明度增加速度。
    If (Transparent_New > 254)
                    Transparent_New =255
    WinSet,Transparent,%Transparent_New%,A
 
    tooltip now: ▲%Transparent_New%`nmae: __%Transparent%  ;查看当前透明度（操作之后的）。
    ;sleep 1500
    SetTimer, RemoveToolTip_transparent_Lwin__2016.09.20, 1500  ;设置统一的这个格式，label在最后。
return
```

```ahk
; 用键盘控制鼠标方向移动
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
```

```ahk
; 鼠标点击

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

---

### 文档转换类
**pdf -> html**
>采用pdf2html来实现将pdf文档转换为html，好处是可以直接利用Chrome的翻译插件来辅助查看pdf文档内容，并且在分屏的时候可以少开一个pdf阅读器，直接新开一个浏览器页签就行了
```ahk
; 为pdf2htmlex添加全局快捷键执行
#p::
    sel := Explorer_GetSelected()
    #支持外部输入页面缩放比例
    InputBox, zoom, 输入缩放倍数，如1.3
    Run "xxx\pdf2htmlEx\pdf2html.bat" "%sel%" %zoom%
return
```

```sh
# pdf2html.bat
@echo off
if [%2] == [] (set zoom_param=1.3) else (set zoom_param=%2)

set source_path=%1
call :get_out_dir %source_path%
cd /d %~dp0
pdf2htmlEX --zoom %zoom_param% --dest-dir %out_dir% %source_path%
REM  echo pdf2htmlEX --zoom %zoom_param% --dest-dir %out_dir% %source_path%

pause
goto end

:get_out_dir
set out_dir=%~dp1
set out_dir=%out_dir:~,-1% 
goto end

:end
```

**markdown -> word/pdf/html**
>采用[pandoc](https://pandoc.org/installing.html)来实现，目前官方支持多种markdown的导出格式，如：`word`、`pdf`、`html`等

```sh
# pandoc.bat
@echo off

set source_path=%1
call :get_out_dir %source_path%
cd /d %~dp0
pandoc -s -o "%out_dir%.html" %source_path%

pause
goto end

:get_out_dir
set out_dir=%~dpn1
goto end

:end
```

### FAQ
 - 如何查看ahk的内置变量
   - ![查看ahk的内置变量](/assets/2019-10-02/1570005377287.png)
     >比如，`%A_WorkingDir%`为ahk.exe的工作目录