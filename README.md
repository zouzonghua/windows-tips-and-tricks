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

# 交换 CapsLock 键和 Ctrl 键
$hexified = "00,00,00,00,00,00,00,00,03,00,00,00,1d,00,3a,00,3a,00,1d,00,00,00,00,00".Split(',') | % { "0x$_"};
$kbLayout = 'HKLM:\System\CurrentControlSet\Control\Keyboard Layout';
New-ItemProperty -Path $kbLayout -Name "Scancode Map" -PropertyType Binary -Value ([byte[]]$hexified);

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
