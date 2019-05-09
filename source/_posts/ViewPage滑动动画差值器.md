---
title: ViewPage滑动动画差值器
date: 2019-04-18 17:32:22
categories: AndroidUI
tags: [android, ui, viewpage, ViewPageIndicator]
hide: true
top: 99

---

很久以前看到一个这样的效果，很多文章都是只重点选择器，`ViewPager` 的差值器动画效果都没有考虑，这里我努力做到最像，完成这个设计

<img src="https://user-gold-cdn.xitu.io/2018/2/6/16169f802550c42e?imageslim" style="zoom:40%">

## 本文知识点

- `ViewPager`  滑动解析
- 自定义 `Scroller` 
- 反射

------

<!--more-->