---
layout:     post                    # 使用的布局（不需要改）
title:      屏蔽CapsLock 键               # 标题 
subtitle:   CapsLock 键与Esc 键互换 #副标题
date:       2020-02-14              # 时间
author:     Shang                      # 作者
header-img: img/post-bg-2015.jpg    #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    -  小常识
---
当在使用Vim 的时候，Esc键是一个使用频率很高的键，但是它的键位在键盘区域的左上角，摁着很不方便。而CapsLock 键，是大写锁定键，一般情况下用处不是很大。偶尔输入大写字母时，可以连着Shift 一起按来输入。这里我们可以把CapsLock 键映射为Esc 键，实际操作上可以是两个键的互换。

综合起来，如下。
# Windows 系统中将CapsLock 大写锁定键映射为Esc 键
将下面的代码保存为 capslock2esc.reg：
```
Windows Registry Editor Version 5.00
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout]
"Scancode Map"=hex:00,00,00,00,00,00,00,00,02,00,00,00,01,00,3a,00,00,00,00,00
```  
注：上面不是互换，如果需要互换，则使用以下代码。
```
Windows Registry Editor Version 5.00
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout]
"Scancode Map"=hex:00,00,00,00,00,00,00,00,03,00,00,00,3a,00,01,00,01,00,3a,00,00,00,00,00
```
具体方法：打开记事本，把这段代码粘贴进去，保存为后缀为reg 的文件。双击运行即可。

贴一大小写锁定键转Ctrl键的解释图。
![](../img/2020-02-14/1.png)
![](../img/2020-02-14/2.png)

这里的原理基本是一致的。
也可以查看注册表编辑器是否修改成功。

1. Windows键 + R，打开运行对话框，输入regedit。
2. 一次打开 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout 

![](../img/2020-02-14/3.png)

完成之后，重启即可生效。

## Linux 系统中将CapsLock键映射为Esc键

Linux 系统中的转换是非常简单的，只要在 .profile文件中加入

```
xmodmap -e ``'clear Lock'` `-e ``'keycode 0x42 = Escape'
```

当你不需要的时候，将这条语句删除，重启即可。

如果要连续输入大写字母的内容，可以先以小写输入，然后选中该内容，按U即可（在Vim中）。或者通过下面的命令设置，以实现将光标之前的连续字母转为小写。

```
inoremap <C-u> <esc>gUiwea
```