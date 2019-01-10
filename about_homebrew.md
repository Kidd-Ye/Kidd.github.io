# Homebrew
Homebrew是一款macOS 缺失的软件包的管理器，拥有安装、卸载、更新、查看、搜索等很多实用的功能。


## Homebrew安装
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

```

homebrew在安装软件时可能会碰到/usr/local目录不可写的权限问题。可以使用下面的命令修复：

重新打开一个终端，输入

```
sudo chown -R username:staff /usr/local

```

## Homebrew 安装 Node.js
```
brew install node

```
设置国内镜像：[参考链接](https://npm.taobao.org/)

```
npm config set registry https://registry.npm.taobao.org 
```

## Homebrew 查看安装的包列表
```
brew list
```


