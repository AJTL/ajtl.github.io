---
author: "AJTL"
title: Docker 从入门到实践
linktitle: "Docker 从入门到实践"
weight: 10
date: 2019-05-24T14:28:54+08:00
draft: true
tags: [docker]
topics: [docker]
description: ""
---

update on 20:31  28/5/2019

- [source site](https://yeasy.gitbooks.io/docker_practice)
- [Docker 从入门到实践.mindnote](https://github.com/AJTL/Mind-Map/tree/master/Docker-%E4%BB%8E%E5%85%A5%E9%97%A8%E5%88%B0%E5%AE%9E%E8%B7%B5.mindnode)

<img src="/post/Docker-从入门到实践.png" width="100%" height="100%" />

## Docker 简介

### 什么是 Docker

- 使用Go进行开发实现
- 基于Linux内核,对进程进行封装隔离
- 操作系统层面的虚拟化技术
  
### Docker 优势

- 更高效的利用系统
- 更快速的启动时间
- 一致的运行环境
- 持续交付和部署
- 更轻松的迁移
- 更轻松的维护和扩展
  
## 基本概念

### 镜像 Image

- 一个类root 文件系统
- 提供运行所需文件及配置参数
- 不包含任何动态数据
- 在构建后不会被改变
- 分层存储，使得镜像的复用、定制更容易
  
### 容器 Container

- 镜像运行的实体
- 基于镜像 创建存储层
  
### 仓库 Repository

- 存储镜像
- 一个dock registry 包含多个仓库
- 一个仓库包含多个镜像
- 通过<仓库名>:<标签>指定镜像
  
## 安装Docker

### CE 社区版

- Stable 6months
- Test
- Nightly
  
### EE 企业版

### 配置镜像加速器

## 使用镜像

### 获取镜像

`docker pull`

### 查看镜像、容器、数据卷所占用的空间

`docker system df`

### 列出镜像(只列出顶层)

- `docker images`
- `docker image ls`
  - 部分镜像
    - `docker image ls 仓库：标签`
  - 虚悬镜像
    - `docker image ls -f dangling=true`
    - 由于新旧镜像同名，旧镜像名称被取消，从而出现仓库名、标签均为 `<none>`的镜像
  - 中间层镜像
    - `docker image ls -a`
    - 其它镜像所依赖的镜像

### 删除镜像

- `docker image rm`/`docker rmi`

### 制作镜像

- 基于image运行的容器在修改其内容后 可`commit`为新的镜像
  - `docker commit`
  - 黑箱镜像
  - 越来越臃肿
  - 难以维护
- 使用Dockerfile制作镜像
  - FROM baseImage
    - 一个 Dockerfile 中 FROM 是必备的指令，并且必须是第一条指令
    - 特殊镜像:scratch
      - 表示空白镜像
      - 表示不以任何镜像为基础
  - RUN newImage
    - 每一个RUN  命令都会建立新的一层镜像
  - 为避免不必要的冗余 在撰写 Dockerfile 的时候，要经常提醒自己，这并不是在写 Shell 脚本，而是在定义每一层该如何构建
  - 镜像构建时，一定要确保每一层只添加真正需要添加的东西，任何无关的东西都应该清理掉
  - 镜像构建命令
    - docker build [选项] <上下文路径/URL/->
    - 镜像构建上下文（Context）
    - 直接用 Git repo 进行构建
    - 用给定的 tar 压缩包构建
    - 从标准输入中读取 Dockerfile 进行构建
    - 从标准输入中读取上下文压缩包进行构建
- Dockerfile 指令详解
  - COPY 复制文件
  - ADD 更高级的复制文件
  - CMD 容器启动命令
  - ENTRYPOINT 入口点
  - ENV 设置环境变量
  - ARG 构建参数
  - VOLUME 定义匿名卷
  - EXPOSE 声明端口
  - WORKDIR 指定工作目录
  - USER 指定当前用户
  - HEALTHCHECK 健康检查
  - ONBUILD 为他人做嫁衣裳
- Dockerfile 多阶段构建
  - Before
    - 全部放入一个Dockerfile
    - 分散到多个Dockerfile
  - After
    - 只构建某一阶段的镜像
    - 构建时从其他镜像复制文件

## 容器

### 启动

- 基于镜像新建容器并启动
- 将终止的容器重新启动
- docker run
