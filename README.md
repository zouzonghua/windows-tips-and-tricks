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




