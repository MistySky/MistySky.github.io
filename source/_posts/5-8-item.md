---
title: iterm2+zsh+oh my zsh 打造专属程序员的酷炫mac终端
date: 2017-05-08 22:39:56
tags: [iterm2,zsh,oh my zsh]
categories: mac
---

Mac一直都是被人称道的，但是自带的终端却并不是那么好看和强大。所以现在一般都使用iterm2+zsh+ohmyzsh来DIY，分享一下我配置的过程和方案：

---
## 下载iTerm2
前往[iTerm2官网](http://www.iterm2.com/) 下载安装。

---
## 下载oh my zsh
打开iTerm2，输入下列命令下载:
```
curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh
```

---
## 安装Powerline和字体库
使用pip安装Powerline：
```bash
$ sudo easy_install pip
$ pip install powerline-status
```
使用下列命令下载字体库：
```bash
$ git clone https://github.com/powerline/fonts.git
```
找到install.sh，执行此指令。出现如下提示则安装字体成功:
```
All Powerline fonts installed to /Users/superdanny/Library/Fonts
```
然后把iTerm 2的设置里的Profile中的Text 选项卡中里的Regular Font和Non-ASCII Font的字体都设置成 Powerline的字体。

---
## 配色方案
我使用的是solarized，使用下列命令下载:
```bash
$ git clone https://github.com/altercation/solarized.git
```
然后在iTerm 2的设置里的Profile中的Color 选项卡里import，使用solarized。

---
## 主题安装
1. 下载[agnoster主题](https://github.com/fcamblor/oh-my-zsh-agnoster-fcamblor)
运行install文件,主题将安装到~/.oh-my-zsh/themes目录下。
2. 进入`~/.zshrc`打开`.zshrc`文件，然后将`ZSH_THEME`后面的字段改为`agnoster。ZSH_THEME="agnoster"`。

---
## 语法高亮
使用如下命令下载zsh-syntax-highlighting到当前目录:
```bash
$ git clone git://github.com/zsh-users/zsh-syntax-highlighting.git
```
打开`.zshrc`，添加如下内容并保存:
```
source XXX/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```
使用如下命令，进入plugins：
```bash
$ cd ~/.oh-my-zsh/custom/plugins
```
打开`.zshrc`，添加如下内容并保存:
```
bashplugins=(zsh-syntax-highlighting)
```
酷炫的“iterm2+zsh+ohmyzsh”DIY Mac终端就完成了！！！
