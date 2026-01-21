# Windows 工作环境配置

> 尽量使用开源软件 尽量少装不必要软件 尽量使用自带软件

## 系统设置

- 修改鼠标光标样式：设置 - 个性化 - 主题 - 鼠标光标 - 指针 - 方案 - Windows 黑色（系统方案）
- 桌面显示此电脑：设置 - 个性化 - 主题 - 桌面图标设置 - 计算机（勾选）
- 关闭活动历史记录: 设置 - 隐私 - 活动历史记录 - 在此设备上存储我的活动历史记录（取消勾选）、向 Microsoft 发送我的活动历史记录（取消勾选）
- 开启 WSL 支持: 设置 - 应用 - 程序和功能 - 启用或关闭 Windows 功能 - 适用于 Linux 的 Windows 子系统（勾选）

## 常见问题

- 关闭安装软件提示：更改这些通知的出现时间 - 用户账户控制设置 - 从不通知
- 关闭系统更新: 任务管理器 - 服务 - 打开服务 - 找到 `WindowsUpdate` - 常规 - 启动类型（禁用）、恢复 - 第一次失败（无操作）

## 工具安装

```shell
# 【必装】安装 scoop - Windows 包管理器(命令行轻松装软件)
iwr -useb get.scoop.sh | iex

# 【必装】Git - Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.
scoop install git

# 添加额外软件源
scoop bucket add extras
scoop bucket add java
scoop bucket add versions
scoop bucket add dorado https://github.com/chawyehsu/dorado # autodarkmode

# 【必装】Windows Terminal - The new Windows Terminal and the original Windows console host, all in the same place!
scoop install windows-terminal

# 【必装】OpenJDK - 是一个由OpenJDK构建，并以免费软件的形式提供社区版的 OpenJDK 二进制包。 它至少提供 4 年的免费长期支持(LTS)。 CentOS7.5和EulerOS2.8操作系统在鲲鹏生态中可以完整运行AdoptOpenJDK的全部功能。
scoop install adopt8-upstream

# 【必装】MySQL - MySQL 是最流行的关系型数据库管理系统，在 WEB 应用方面 MySQL 是最好的 RDBMS(Relational Database Management System：关系数据库管理系统)应用软件之一。
scoop install mysql57

# 【必装】Nvm - 是一个 NodeJS 版本控制。
scoop install nvm
nvm node_mirror https://npm.taobao.org/mirrors/node/
nvm npm_mirror https://npm.taobao.org/mirrors/npm/
nvm install 12.19.0
nvm use 12.19.0 64

# 【必装】 Yarn - 快速、可靠、安全的依赖管理工具。
npm i -g yarn

# 【必装】Heidisql - 数据库工具。
scoop install heidisql

# 【必装】Visual Studio Code - Javascript 编辑器。
scoop install vscode

# 【必装】IntelliJ IDEA - Java 编辑器。
scoop install idea

# 【必装】Typora - Markdown 编辑器。
scoop install typora

# 【必装】Google Chrome - 是由Google开发的免费网页浏览器。
scoop install googlechrome

# 【必装】V2rayn - 科学上网工具。
scoop install v2rayn

# 【必装】Openvpn - vpn 代理工具。
scoop install openvpn

# 【必装】Geek uninstaller - 卸载工具。
scoop install geekuninstaller

# 【必装】Rufus - 刻录工具。
scoop install rufus

# 【必装】Listary - 快速启动工具。
scoop install Listary

# 【必装】Mpc-be - 视频播放器。
scoop install mpc-be

# 【必装】Auto Dark Mode - 自动切换主题工具。
scoop install autodarkmode

# 【必装】微信 - 一款跨平台的通讯工具。支持单人、多人参与。通过手机网络发送语音、图片、视频和文字。
scoop install wechat

# 【必装】微信开发者工具 - 一款集成了公众号网页调试和小程序调试两种开发模式。
https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html

# 【必装】网易云音乐 - 是一款专注于发现与分享的音乐产品，依托专业音乐人、DJ、好友推荐及社交功能，为用户打造全新的音乐生活。
https://music.163.com/#/download

```

## 开发相关

```shell

# 交换 CapsLock, Ctrl 键
$hexified = "00,00,00,00,00,00,00,00,03,00,00,00,1d,00,3a,00,3a,00,1d,00,00,00,00,00".Split(',') | % { "0x$_"};
$kbLayout = 'HKLM:\System\CurrentControlSet\Control\Keyboard Layout';
New-ItemProperty -Path $kbLayout -Name "Scancode Map" -PropertyType Binary -Value ([byte[]]$hexified);

# 还原 CapsLock, Ctrl 键盘
- 打开注册表编辑器。你可以按下 Win + R 组合键，输入 regedit，然后按 Enter 打开注册表编辑器。
- 导航到以下路径：
- ```HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout```
- 找到名为 "Scancode Map" 的键，右键点击它，然后选择 "删除" 来删除这个键。或者，你也可以双击这个键，然后在弹出的窗口中将其值清空，然后点击 "确定"。
- 重新启动计算机以使更改生效。


# 配置 Git
git config --global core.autocrlf false
git config --global user.name "zouzonghua"
git config --global user.email "zouzonghua.cn@gmail.com"
ssh-keygen -t rsa -C "zouzonghua.cn@gmail.com"
cat C:/Users/zouzonghua/.ssh/id_rsa.pub
ssh git@github.com

# 配置 ssh 免密登陆服务器
ssh-copy-id -i /mnt/c/Users/zouzonghua/.ssh/id_rsa.pub -p 22 root@www.zouzonghua.cn
```

```
#Requires AutoHotkey v2.0
; Bringing the Unix/Emacs soul to the Windows body.
 
; --- 排除列表：避免在真正的 Emacs 或某些终端中产生双重触发 ---
GroupAdd "ExclusionList", "ahk_exe emacs.exe"
GroupAdd "ExclusionList", "ahk_exe WindowsTerminal.exe"
 
#HotIf !WinActive("ahk_group ExclusionList")
 
; =================================================================
; --- 1. Emacs 风格光标移动/编辑 (Ctrl-P/N/B/F/A/E) ---
; =================================================================
 
; --- 字符/行移动 (基本 Emacs) ---
^p::Send "{Up}"            ; Ctrl + P -> 上一行 (Previous)
^n::Send "{Down}"          ; Ctrl + N -> 下一行 (Next)
^b::Send "{Left}"          ; Ctrl + B -> 左一个字符 (Backward)
^f::Send "{Right}"         ; Ctrl + F -> 右一个字符 (Forward)
^a::Send "{Home}"          ; Ctrl + A -> 行首 (Start of Line)
^e::Send "{End}"           ; Ctrl + E -> 行尾 (End of Line)
^g::Send "{Esc}"           ; Ctrl + G -> Esc 键盘退出 (Keyboard Quit)
 
; --- 字符/单词删除 (Delete) ---
^d::Send "{Delete}"        ; Ctrl + D -> 删除光标后一字符
^h::Send "{Backspace}"     ; Ctrl + H -> 删除光标前一字符
 
; --- 单词/页面跳转 (Alt/Win 替代 Ctrl) ---
#f::Send "^{Right}"        ; Win + F -> 向前跳一个单词 (Ctrl + Right)
#b::Send "^{Left}"         ; Win + B -> 向后跳一个单词 (Ctrl + Left)
#d::Send "^{Delete}"       ; Win + D -> 删除光标后一个单词 (Kill Word)
 
; =================================================================
; --- 2. 增强的 Emacs/Mac 风格选择与剪切 (Selection & Kill) ---
; =================================================================
 
; --- 行首尾选择 (Emacs 风格) ---
^+e::Send "+{End}"         ; Ctrl + Shift + E -> 选中到行尾
^+a::Send "+{Home}"        ; Ctrl + Shift + A -> 选中到行首
 
; --- 字符选择 (Emacs 风格) ---
^+f::Send "+{Right}"       ; Ctrl + Shift + F -> 向前选中一个字符
^+b::Send "+{Left}"        ; Ctrl + Shift + B -> 向后选中一个字符
 
; --- 单词选择 (Option + Shift + F/B -> Alt + Shift + F/B) ---
; 模拟 Option+Shift+F/B (Mac/Hack 风格)
#+f::Send "^+{Right}"      ; Win + Shift + F -> 向前选中一个单词
#+b::Send "^+{Left}"       ; Win + Shift + B -> 向后选中一个单词
 
; --- 行选择 (Ctrl + Shift + P/N -> Emacs 风格) ---
; 模拟 Ctrl+Shift+P/N (Hack 风格)
^+p::Send "+{Up}"          ; Ctrl + Shift + P -> 向上选中一行
^+n::Send "+{Down}"        ; Ctrl + Shift + N -> 向下选中一行
 
; --- Emacs Kill/Yank (剪切/粘贴行) ---
^k::Send "+{End}^x"        ; Ctrl + K -> 选中到行尾并剪切 (Kill Line)
^y::Send "^v"              ; Ctrl + Y -> 粘贴 (Yank)
 
; --- 单词删除 (Kill Word Backward) ---
^w::Send "^h"              ; Ctrl + W -> 删除光标前一个单词 (Kill Word Backward)
 
; =================================================================
; --- 3. 翻页功能 ---
; =================================================================
^v::Send "{PgDn}"          ; Ctrl + V -> 向下翻页 (Page Down)
#v::Send "{PgUp}"          ; Win + V  -> 向上翻页 (Page Up)
 
; =================================================================
; --- 4. 基于 Alt 的常用快捷键 (Mac 体验/替换 Ctrl 键) ---
; =================================================================
!Space::Send "#s"      ; Alt + Space -> 弹出 Windows 搜索框 (Win + S)
!s::Send "^s"              ; Alt + S -> 保存 (Save)
!a::Send "^a"              ; Alt + A -> 全选 (Select All)
!c::Send "^c"              ; Alt + C -> 复制 (Copy)
!v::Send "^v"              ; Alt + V -> 粘贴 (Paste)
!x::Send "^x"              ; Alt + X -> 剪切 (Cut)
!z::Send "^z"              ; Alt + Z -> 撤销 (Undo)
!+z::Send "^y"           ; Alt + Shift + Z -> 反撤销 (Redo)
!w::Send "^w"           ; Alt + W -> 关闭当前标签/分页
!q::Send "!{F4}"          ; Alt + Q -> 关闭整个应用程序 (Alt + F4)
!f::Send "^f"              ; Alt + F -> 搜索
!r::Send "^r"              ; Alt + R -> Ctrl + R
!t::Send "^t"              ; Alt + T -> Ctrl + T
!/::Send "^/"              ; Alt + / -> Ctrl + /
 
#HotIf
```

## 常用快捷键

- Win + Shift + S
  	+ 屏幕截图

- Win + Tab
	+ 打开任务视图
- Win + Ctrl + D
	+ 添加虚拟桌面
- Win + Right
	+ 在你于右侧创建的虚拟桌面之间切换
- Win + Left
	+ 在你于左侧创建的虚拟桌面之间切换
- Win + F4
	+ 关闭你正在使用的虚拟桌面

- Win + `
	+ 打开终端
- Win + l
	+ 锁屏
- Win + s
	+ 打开搜索
- Win + v
	+ 打开剪贴板
- Win + i
	+ 打开设置
- Win + a
	+ 打开通知中心
- Win + k
	+ 打开蓝牙和其他设备
- Win + m
	+ 隐藏应用
- Win + p
	+ 切换屏幕投影
- Win + e
	+ 打开文件管理器
- Win + d
	+ 回到桌面

- Win + 1~9
	+ 切换虚拟桌面

## Hyper-V

###  配置网络

#### 1. 配置虚拟交换机
打开 Hyper-V 管理器，`虚拟交换机管理器` -> `新建虚拟网络交换机` -> `内部`

#### 2. 主机网络配置
打开 控制面板，`网络和 Internet` -> `更改适配器设备` -> `vEthernet (Debian240507)` 双击 -> `属性` -> 固定 IPv4 地址
```
IP 地址    192.168.137.1
子网掩码   255.255.255.0
```
找到 物理主机网络 双击 -> `属性` -> `共享` -> 选择 `vEthernet (Debian240507)`

#### 3. 虚拟网络配置

虚拟机固定 IP （Debian12）

sudo vim /etc/network/interfaces
```
auto eth0
iface eth0 inet static
   address 192.168.137.200
   netmask 255.255.255.0
   gateway 192.168.137.1
```

sudo vim /etc/resolv.conf
```
nameserver 192.168.137.1
```

#### 4. 代理主机网络

```
export https_proxy=http://192.168.137.1:7890 http_proxy=http://192.168.137.1:7890 all_proxy=socks5://192.168.137.1:7890
```

## emacs

[解决 Ctrl + @ 快捷键问题](https://github.com/microsoft/terminal/issues/2865#issuecomment-1340977061)

```
scoop install openssh
C:\Users\zonghua\scoop\shims\ssh.exe zonghua@debian240507
```




