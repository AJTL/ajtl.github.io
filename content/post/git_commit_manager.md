---
author: "AJTL"
title: Git Commit Message 规范设置
linktitle: "Git Commit Message 规范设置"
weight: 10
date: 2021-03-17T16:13:50+08:00
draft: true
tags: [Git]
topics: [Git]
description: ""
---

## Chapter 1 简介

规范的进行 Git 提交有助于团队的开发管理。

符合规范的提交内容也能通过自动化脚本自动生成 changlog。

## Chapter 2 准备工作

1. 安装 [Git](https://git-scm.com/)
2. 安装 [Node.Js](https://nodejs.org/)[^1]

[^1]: 在安装 `Node.Js` 的过程中，需确保勾选了安装 `npm` 包管理器。

## Chapter 3 提交格式

每一个提交都由**header**(标题)、**body**(内容)和**footer**(页脚)组成。其中**header**还包括了 _type_ 、_scope_ 和 _subject_，如下图所示：

```markdown
<type>(<scope>): <subject>
<BLANK-LINE>

<body>
<BLANK-LINE>
<footer>
```

### 标题部分: _type_、_scope_、_subject_

#### _type_ 必需

type 表示提交类别，比如是修复一个 bug 还是增加一个新的 feature。
| | |
|--|--|
|feat|添加新特性|
|fix|修复漏洞|
|docs |仅仅修改了文档，比如 README, CHANGELOG, CONTRIBUTE 等等|
|style |仅仅修改了空格、格式缩进、逗号等等，不改变代码逻辑 |
|refactor | 代码重构，没有加新功能或者修复漏洞|
|perf | 优化相关，比如提升性能、体验|
|test | 增加测试用例，包括单元测试、集成测试等|
| chore| 改变构建流程、或者增加依赖库、工具等|
| revert|回滚到之前某一版本 |

#### _scope_ 可选

scope 表示修改范围，建议填写影响的功能模块。

#### _subject_ 必需

subject 表示标题内容，是对提交的简短描述，不超过 50 个字符。
最好遵循

- 以动词开头，使用第一人称现在时，比如 `change`，而不是 `changed` 或 `changes`
- 首字母不要大写
- 结尾不用句号

### 内容部分: _body_ 可选

body 表示主体描述内容，是对 subject 里内容的展开，在此做更加详尽的描述，内容里应该包含修改动机和修改前后的对比，可以多行。

### 页脚部分: _footer_ 可选

footer 表示页脚，主要放置`BREAKING CHANGE`和 `Issue` 关闭的信息.

1. BREAKING CHANGE

   > 格式：以 BREAKING CHANGE 开头，后面是对变动的描述、以及变动理由和迁移方法。

   ```markdown
   BREAKING CHANGE: xxxxxx

   Before:
   xxx

   After:
   xxx
   ```

2. Close Issue

   ```markdown
   Closes <issue-number>
   ```

### 特殊情况

#### revert

当撤销上次提交时，必须使用`revert`，后面跟着被撤销提交的标题部分。
内容部分是固定的，必须写成`This reverts commit <hash>`。其中`<hash>`是被撤销的提交 sha 标识符。
示例：

```markdown
revert: fix: fix a bug

This reverts commit 1234567812345678.
```

更多关于提交格式的资料都可以在[🌐 这里](https://www.conventionalcommits.org/)找到。

## Chapter 4 配置

### commitizen

[commitizen](https://github.com/commitizen)是 是一款标准化 `git commit` 信息的工具。
`commitizen` 被设计用于更好的阅读和强制性的进行规范化的提交。除此之外，规范化的提交有助于利用过往的提交进行一些其他的分析和操作，比如可以自动化的生成 `chenglog`。

```bash
npm install -g commitizen
```

安装完成后，提交时使用 `git cz` 或者`cz` 就可以替代 `git commit`。还可以使用 `git-cz`，他是`cz`的别称。

#### 适配器

`commitizen` 支持不同适配器的扩展 。这里使用 `cz-conventional-changelog` 。

```bash
npm install -g cz-conventional-changelog
```

#### package.json

```bash
npm init -y
```

打开生成的`package.json`，补全配置：

```json
"config": {
    "commitizen": {
      "path": "cz-conventional-changelog"
    }
  }
```

在 bash 中输入 `git cz` /`cz` / `git-cz`:

```bash
$ cz
cz-cli@4.2.3, cz-conventional-changelog@3.2.0

? Select the type of change that you're committing: (Use arrow keys)
> feat:     A new feature
  fix:      A bug fix
  docs:     Documentation only changes
  style:    Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
  refactor: A code change that neither fixes a bug nor adds a feature
  perf:     A code change that improves performance
  test:     Adding missing tests or correcting existing tests
(Move up and down to reveal more choices)
```
