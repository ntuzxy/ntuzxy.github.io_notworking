# 博客写作要求和规范：
详细内容见_posts/2019-08-08-write-a-new-post.md。


## 1. 文件名和路径
在_post/下创建文件。
文件名必须以日期开头，且格式为YYYY-MM-DD-TITLE.EXTENSION。例如：2021-11-11-testing_for_a-b-c.md。

## 2. 文件头
按一下格式填写文件头
---
title: TITLE
date: YYYY-MM-DD HH:MM:SS +/-TTTT
categories: [TOP_CATEGORIE, SUB_CATEGORIE]
tags: [TAG]     # TAG names should always be lowercase
---

其中，title是真正的博客标题，data是发布时间，categories是分类（方便归档，最多只能有两项），tags是标签（方便搜索查找，标签数无限制）。
默认情况，目录（TOC）会显示在博文右侧。

此外，还可以在文件头配置其它内容（注：以下配置为非默认值）：
### 2.1 目录（TOC）
---
toc: false
---
### 2.2 评论（Comments）
---
comments: false
---
### 2.3 数学公式（Mathematics）
---
math: true
---
### 2.4 绘图（Mermaid）
---
mermaid: true
---
### 2.5 图片（Images)
---
image:
  src: /path/to/image/file
  alt: image alternative text
---

### 2.6 置顶博文
---
pin: true
---




## 3. 全局配置 (慎改)
源配置文件`_config.yml`



