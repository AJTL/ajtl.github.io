---
author: "AJTL"
title: 解决brew cask软件更新
linktitle: "解决brew cask软件更新"
weight: 10
date: 2019-06-25T10:13:41+08:00
draft: true
tags: [Homebrew,cask,upgrade]
topics: [Homebrew]
description: ""
---

## 关于Homebrew/Homebrew Cask

`Homebrew`是现如今在Mac平台下较为流行的包管理工具，用以简化 macOS 上的软件安装过程。

> 项目主页：<https://brew.sh> 
> GitHub地址：<https://github.com/Homebrew>

`Homebrew Cask`是 `Homebrew`的扩展，借助它可以方便地在 macOS 上安装图形界面程序，即我们常用的各类应用。

但是在实际使用过程中发现cask 更新命令很难达到更新的效果。

```sh
brew cask upgrade
```

最后发现有这样一个方法`buo/cask-upgrade`

## brew cu

`buo/cask-upgrade`这个项目是用来更新通过`brew cask`安装的每一个过时的APP。 它替代了原生的`upgrade`命令，提供了更为人性化的细节展示。

> GitHub地址：<https://github.com/buo/homebrew-cask-upgrade>

## 使用brew cu

### 安装

```sh
brew tap buo/cask-upgrade
```

### 使用

更新所有过时APP:

```sh
brew cu
```

更新指定的APP:

```sh
brew cu [CASK]
```

带参更新指定的APP:

```sh
brew cu [CASK] [options]
```

当运行`brew cu`命令又不带任何参数时，该命令会自动运行`brew update`获取软件的最新版本。

### brew cu 参数

 输入

 ```sh
brew help cu
 ```

 可以获得命令行的文档帮助

 ```sh
Usage: brew cu [CASK] [options]
    -a, --all             Include apps that auto-update in the upgrade.
        --cleanup         Cleans up cached downloads and tracker symlinks after
                          updating.
    -f  --force           Include apps that are marked as latest
                          (i.e. force-reinstall them).
        --no-brew-update  Prevent auto-update of Homebrew, taps, and formulae
                          before checking outdated apps.
    -y, --yes             Update all outdated apps; answer yes to updating packages.
    -q, --quiet           Do not show information about installed apps or current options.
        --no-quarantine   Pass --no-quarantine option to `brew cask install`.
        --pinned          Print all pinned apps
        --pin CASK        Pin the current app version
        --unpin CASK      Unpin the current app version
    -i, --interactive     Running update in interactive mode
 ```


我一般使用

```sh 
brew cu -facy
```

去更新所有CASK,问题是有时遇上网络的问题会更新失败。

<img src="/post/Screen Shot 2019-06-25 at 12.53.14.png" width="90%" height="70%" />
