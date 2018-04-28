---
title: terminator美化
date: 2018-04-28 17:40:28
tags: linux
---

首先安装terminator
```
sudo apt-get install terminator
```
因为初始化界面不太美观，可以设置配置文件，方法如下：

```
vim ~/.config/terminator/config
```
如果报错，`Unable to open ~/.config/terminator/config`，解决方法：
打开`terminator`终端，然后右击终端的黑色背景，选择`preference->layouts->add`，关闭该窗口即可找到`config`文件。

我当前使用的配置
```
[global_config]
[keybindings]
[profiles]
  [[default]]
    use_system_font = False # 是否启用系统字体
    login_shell = True
    background_darkness = 0.92 # 背景颜色
    background_type = transparent
    background_image = None
    cursor_color = "#3036ec" # 光标颜色
    foreground_color = "#00ff00"
    show_titlebar = False # 不显示标题栏，也就是 terminator 中那个默认的红色的标题栏
    custom_command = tmux
    font = Ubuntu Mono 15  # 字体设置，后面的数字表示字体大小
[layouts]
  [[default]]
    [[[child1]]]
      type = Terminal
      parent = window0
    [[[window0]]]
      type = Window
      parent = ""
[plugins]
```
