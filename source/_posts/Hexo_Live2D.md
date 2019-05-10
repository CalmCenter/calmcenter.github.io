---
title: Live2D 看板娘
date: 2019-05-9 14:32:22
categories: live2D
tags: [live2D]
hide: true


---

目录请看  [Hexo 搭建博客大全](https://calmcenter.club/2019/Complete_works_of_hexo.html)

## 本文主要记载

- 使用 `hexo-helper-live2d` 完成看板娘
- 自定义看板娘(右下角那个~)
  - 运行、接入 `Demo`
  - 更换、修改模型

------

<!--more-->

## 使用 `hexo-helper-live2d` 完成看板娘

我的 `Live2D` 版本是 `3.1.1`

首先安装配置 hexo-helper-live2d，在 `hexo` 根目录下执行

```
npm install hexo-helper-live2d --save
```

插件就安装完成了，你可一下选一个 [模型](https://huaji8.top/post/live2d-plugin-2.0/) 这个给出了展示效果，但是不全， [更多模型](https://github.com/xiazeyu/live2d-widget-models) 这个没有展示效果，比之前的全一点，可以自己试试效果 ~

在模型中记住自己选择模型的名字 `live2d-widget-model-你选中的模型名字` ，然后进行安装

```
npm install live2d-widget-model-wanko --save
```

然后再 `Hexo 配置文件` 中，添加如下代码，**代码格式很重要！！！** 有时候复制进去没有缩进，效果是出不来的。

```
live2d:
  enable: true
  scriptFrom: local
  pluginRootPath: live2dw/
  pluginJsPath: lib/
  pluginModelPath: assets/
  tagMode: false
  debug: false
  model:
    use: live2d-widget-model-wanko
  display:
    position: left
    width: 150
    height: 300
  mobile:
    show: true
  react:
    opacity: 0.7
```

这样一只可爱的小白狗就出现了。

如果要加载自定义模型，需要在根目录新建文件夹 `live2d_models` 下，再新建一个文件夹 `kesshouban （此处自定义）` 然后将资源文件放入 `kesshouban ` 内 。然后修改 `Hexo 配置文件` ，将 `model.use` 写成 `kesshouban` 。

## 自定义看板娘

首先感谢 [大佬](https://haokan.baidu.com/v?pd=wisenatural&vid=11405187949707723550) 提供的视屏教程，清晰易懂。

感谢 [galnetwen](https://github.com/galnetwen) 提供的代码。

### 1. 运行 `Demo`

首先你需要将 [代码](https://github.com/galnetwen/Live2D) 下载下来

解压代码并将 `Live2D-master` 里的内容 `live2d` 和 `demo.html` ，解压到 `hexo` 根目录的 `public` 的文件夹下。并运行且进入本地访问

```
hexo s
```

```
http://localhost:4000/demo.html
```

如果出现 [药水制作师](https://play.google.com/store/apps/details?id=com.sinsiroad.potionmaker&hl=zh_CN) 里的模型，就可以啦，如果出不来，证明你路径有问题，请检查路径， `live2d` 和 `demo.html` 文件在 `public` 文件夹下。

### 2. 接入 `Demo` 

将 `live2d` 文件夹剪切到 `hexo/themes/next/source` , 文件夹内应该有三个文件夹 `css js model` 和一个文件 `message.json` 。

然后将 `demo.html` 中的代码整理出来

```
 <link rel="stylesheet" href="/live2d/css/live2d.css" />
      <div id="landlord">
          <div class="message" style="opacity:0"></div>
          <canvas id="live2d" width="280" height="250" class="live2d"></canvas>
          <div class="hide-button">隐藏</div>
      </div>
      <script type="text/javascript" src="https://cdn.bootcss.com/jquery/2.2.4/jquery.min.js"></script>
      <script type="text/javascript">
          var message_Path = '/live2d/'
          var home_Path = 'https://calmcenter.club/'
      </script>
      <script type="text/javascript" src="/live2d/js/live2d.js"></script>
      <script type="text/javascript" src="/live2d/js/message.js"></script>
      <script type="text/javascript">
          loadlive2d("live2d", "/live2d/model/tia/model.json");
      </script>
```

粘贴到 `/theme/next/layout/layout.swig` 的 `<footer>` 标签下

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/pictures/20190509151030.png" style="zoom:50%">

执行

```
hexo clean && hexo g && hexo s
```

看板娘就到我们的博客上来啦~

### 3. 更换模型

感谢 [猫与向日葵](https://imjad.cn/) 提供血小板模型 [下载地址](https://cdn.imjad.cn/usr/uploads/kesshouban_v2.7z)

在 `hexo/next/source/live2d/model` 中新建一个文件夹，将压缩包里面的内容，也就是模型放到里面，然后修改 `model.json` 

```
{
	"type": "Live2D Model Setting",
	"name": "model",
	"model": "model.moc",
	"textures": [
		"model.2048/texture_00.png"
	],
	"layout":{
        "center_x":0.0,
        "center_y":-0.1,
        "width":2
    },
    "hit_areas_custom":{
        "head_x":[-0.35, 0.6],
        "head_y":[0.19, -0.2],
        "body_x":[-0.3, -0.25],
        "body_y":[0.3, -0.9]
    },
	"motions":{
		"idle":[
			{"file":"motions/Idle.mtn"}
		],
        "sleepy":[
            {"file":"motions/Nemui.mtn"}
        ],
		"flick_head":[
			{"file":"motions/Anone_Synced.mtn"}
		],
		"tap_body":[
			{"file":"motions/Dance.mtn"}
		],
	}
}
```

最终成这样，一个标点都不能错 ！主要是 `layout(用于)` 和 `hit_areas_custom` 

然后将  `/theme/next/layout/layout.swig` 的 `<footer>` 添加的那句话

```
 <script type="text/javascript">
          loadlive2d("live2d", "/live2d/model/xxb/model.json");
      </script>
```

将 `xxb` 改成你新建的文件夹名字，编译运行

```
hexo g && hexo s
```

### 4. 修改模型

