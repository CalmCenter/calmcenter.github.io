---
title: Hexo 功能样式配置
date: 2019-04-18 17:32:22
categories: Hexo
tags: [Hexo, git, github]


---

目录请看 [Hexo 搭建博客大全](https://calmcenter.github.io/2019/04/18/Hexo%20%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2%E5%A4%A7%E5%85%A8/)

## 本文主要记载

- `NexT` 主题设置
- 基础样式设置
- 添加 `Live2D` 
- 图片相关
- 打赏、评论、复制功能
- 细节美化

```
本文环境是 win10 或 win 7。mac 再执行 npm 时需要在前面添加 sudo
本文整理于各大佬文章，文中会给出相应链接，如有侵权，请联系我修改或删除。
```

------

<!--more-->

## 功能样式配置

### `NexT` 主题设置

**重点标注：`hexo` 根目录配置文件 `hexo/_config.yml`  下文用 `Hexo 配置文件` 表示，`NexT` 样式配置文件 `hexo/theme/next/_config.yml` 下文用 `NexT 配置文件` 表示一定要分清，它们都叫 `_cpmfig.yml` **

[这里有很多主题](https://hexo.io/themes/) 这里主要说 [NexT](https://github.com/theme-next/hexo-theme-next) 

进入 `hexo` 文件目录 ，执行

```
git clone https://github.com/theme-next/hexo-theme-next themes/next
```

成功后，在 `Hexo 配置文件` 找到 `theme` 字段

```
theme: next
```

这样 `next` 样式就设置好了，快打开看看吧  [http://localhost:4000/](http://localhost:4000/)

### 设置语言、标题等

在  `Hexo 配置文件` 找到 `Site` 字段 

| 字段        | 作用                           |
| :---------- | :----------------------------- |
| title       | 网站标题                       |
| subtitle    | 副标题                         |
| description | 描述                           |
| author      | 作者(您的名字)                 |
| language    | 语言 (zh-CN，en等)             |
| timezone    | 网站时区，默认使用您电脑的时区 |

### [Live2D  GitHub](https://github.com/EYHN/hexo-helper-live2d)

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

如果要加载自定义模型，需要将模型放到 `\themes\next\source` 目录下。然后修改 `Hexo 配置文件` ，将 `model.use` 写成 `/live2d_models/kesshouban/kesshouban.model.json` ，我再 `source` 下有个文件夹 `live2d_models` 这里需要指向 `.model.json` 文件。

### `NexT` 样式

在 `Hexo 配置文件` 找到 `Schemes` 字段，这里有四种样式

```
# Schemes
#scheme: Muse
#scheme: Mist
#scheme: Pisces
scheme: Gemini
```

### 图片上传 `PicGo` + `GitHub` 图床

参考自作者 [EnjoyToShare 《PicGo+GitHub图床，让Markdown飞起》](https://blog.enjoytoshare.club/article/hexo-do-optimization-picture.html)  

1. 首先下载工具

下载地址 : [PicGo v2.1.2](https://github.com/Molunerfinn/PicGo/releases/tag/v2.1.2) 

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/picturespicgo_down.png" style="zoom:50%">

2. 登录 `GitHub` 

创建 `Repository` 之前都讲过怎么创建，名字可以取成 `PicGo` 类似的名字，主要用于存放图片。

3. 生成 Token  

点击头像 `Settings -> Developer settings -> Personal access tokens` 点击  `Generate new token`  

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/picturesnew_token.png" style="zoom:80%">

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/picturesaccess_tokens.png" style="zoom:30%">

点击最下面的  `Generate token` ，会出现 `token` ，这个 `token` 只出现一次，所以要保存一下

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/picturesaccess_token.png" style="zoom:50%">

4. 配置 `PicGo` 客户端

打开 `PicGo` ，输入相关信息

- 仓库名 即你的仓库名
- 分支名 默认 master
- Token 就是刚刚复制的那一串字符
- 存储路径 这个可以填也可以不填，填了的话图片就上传到这个文件夹，比如 `picture/` 图中少一个 `/`
- 自定义域名 这个要改一下 格式： `https://raw.githubusercontent.com/[仓库名]/master` 

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/picturespic_go_token.png" style="zoom:50%">

然后点确定就OK了，不妨试试。

还有一个方便的操作就是 修改上传快捷键 ，快捷键直接上传，跳过拖入上传区

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/pictures/20190426111300.png" style="zoom:50%">



### 图片全屏查看

首先进入 `hexo\themes\next\source\lib` 目录，下载插件

```
git clone https://github.com/theme-next/theme-next-fancybox3 fancybox
```

然后更改 `NexT 配置文件`  

```
fancybox: true
```

完成 ~ 

### 打赏功能

参考自作者 [EnjoyToShare 《Hexo的NexT主题打赏功能》](https://blog.enjoytoshare.club/article/hexo-do-donate.html)  

准备好收款二维码，放入 `hexo\themes\next\source\images` ，打开 `NexT 配置文件` 

```
reward_settings:
  enable: true
  animation: false
  comment: 分享不易，可否赏杯咖啡钱
reward:
  wechatpay: /images/wechatpay.png
  alipay: /images/alipay.png
  #bitcoin: /images/bitcoin.png
```

### 评论功能

参考自作者 [EnjoyToShare 《Hexo NexT 加入评论功能gitalk》](https://blog.enjoytoshare.club/article/hexo-do-gitalk.html)  

`Gitalk` :

- 一个基于 `Github Issue` 和 `Preact` 开发的评论插件
- 详情 `Demo` 可见:  [https://gitalk.github.io/](https://gitalk.github.io/)

增加评论区

- 注册 `OAuth Application`
- 在 `GitHub` 上注册新应用, 链接:  [https://github.com/settings/applications/new](https://github.com/settings/applications/new) 

| 参数                       | 说明                        |
| :------------------------- | :-------------------------- |
| Application name           | 应用名称, 可以任意填入      |
| Homepage URL               | 网站URL, 注意用https://开头 |
| Application description    | 应用描述, 可以任意填入      |
| Authorization callback URL | 网站URL, 注意用https://开头 |

注册后记录 `Client ID` 和 `Client Secret` , 后续要使用到。

打开 `NexT 配置文件` ， **根据自己信息** 进行一下修改，

```
gitalk:
  enable: true
  github_id: CalmCenter
  repo: calmcenter.github.io
  client_id: ****
  client_secret: ****
  admin_user: CalmCenter  
  distraction_free_mode: true 
  language:
```

 集成过程中出现的错误 [Junzhou Liu](https://liujunzhou.top/2018/8/10/gitalk-error/#%E5%AE%89%E8%A3%85%E6%95%99%E7%A8%8B) 这里给出了很多，但是在我集成是发现有的 `NexT` 已经修正，所以这里说几点需要注意的地方。

- 你的评论仓库或者 `GitHub Page` 仓库必须是 `public` ， `NexT 配置文件` 的 `reop` 指定的仓库名称也必须是 `public` ，否者可能出现 `404` 的错误
- `NexT` 中的字段配置 和 `Gitalk` 有两个不一样，需要用 `NexT` 指定的，否者会出现 `Erroe Not Found` 

如果错误修改后没反应，试一下

```
hexo clean
```

重新编译运行。

成功后会提示你未找到相关 `issues`  ，需要你登录

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/pictures/20190426155441.png" style="zoom:100%">



### 代码块复制功能

在 `NexT 配置文件` 中

```
codeblock:
  border_radius:
  copy_button:
    enable: true
    show_result: true
    style:
```

`NexT` 随着版本的升级，省去了很多操作，基本都省开关设置了

### `DaoVoice` 实现在线联系

1. 注册登录 注册登录 `DaoVoice`

[DaoVoice](http://www.daovoice.io/) 点击

### 细节美化

#### 头像

在`NexT 配置文件` 中，找到 `avatar` 字段

| 字段    | 作用                                                         |
| ------- | ------------------------------------------------------------ |
| url     | 图片相对位置(/image/xxx.png)图片保存在  \hexo\themes\next\source\images 文件下 |
| rounded | 是否启用圆角                                                 |
| opacity | 透明度                                                       |
| rotated | 旋转动画                                                     |

#### 回到顶部

打开 `NexT 配置文件` 搜索 `back2top`  

```
back2top:
  enable: true
  # 回到侧边栏顶部.
  sidebar: true
  # 滚动%标签.
  scrollpercent: true
```

#### 页面底部优化

- 跳动的心

参考自作者 [十一種情緒的堆棧](https://11.tt/posts/2018/set-up-hexo-with-coding-and-github/) 在这篇文章 1/2 处左右

效果就在本页面底部 ~ ，首先先去 [The Icons](https://fontawesome.com/v4.7.0/icons/) 选择一张图片，例如搜索 `heartbeat` ，点击进去将图片代码 `fa-heartbeat` 复制下来，打开`NexT 配置文件` ，搜索 `footer` 关键字

```
footer:
  icon:
    name: fas fa-heartbeat
    animated: true
    color: "#ff0000"
```

需要将复制的图片代码粘贴到 `name` 字段，并且前面加上 fas ，如果需要动画的话，将 `animated` 设置为 `true` ，并将 `color` 修改为 `#ff0000` 。就和我底部效果一样了啦。

- 访问统计

还是在 `NexT 配置文件` ，搜索 `busuanzi_count` 字段。

```
busuanzi_count:
  enable: true
  total_visitors: true
  total_visitors_icon: user
  total_views: true
  total_views_icon: eye
  post_views: true
  post_views_icon: eye
```

将 `enable` 设置为 `true` 就有和我底部一样的 访问统计 功能了

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/picturesvisit.png" style="zoom:100%">



统计这块还可以添加一个字数和阅读时长统计，在`hexo` 根目录配置文件 `hexo/_config.yml` 搜索 `symbols_count_time` 如果没有则添加

```
symbols_count_time:
 symbols: true 
 time: true 
 total_symbols: true 
 total_time: true
```

在 `NexT 配置文件` 搜索 `symbols_count_time` 

```
symbols_count_time:
  separated_meta: true
  item_text_post: true
  item_text_total: false
  awl: 4
  wpm: 275
```

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/picturesnumber.png" style="zoom:100%">

**注: 格式很重要** 

#### 圆角布局

参考自作者 [EnjoyToShare](https://blog.enjoytoshare.club/article/hexo-do-optimization.html) 在这篇文章 3.12，这篇里边还有好多好看的样式 ~

在 `\themes\next\source\css\_variables` 中的 `Gemini.styl` 文件添加

```
// 修改主题页面布局为圆角
$border-radius-inner            = 15px 15px 15px 15px;
$border-radius                  = 15px;
```

#### 文章标签、分类

我们在用 `hexo new post` 创建文件时

```
hexo new post "name"
```

`hexo` 自动为我们的文章头部生成了如下的内容

```
title: 标题
date: 2019-04-18 17:32:22
```

- 首先添加分类

在 `data` 下方添加 `categories` 

```
title: 标题
date: 2019-04-18 17:32:22
```

```
categories: Hexo
```

**注意：英文冒号，还有一个空格**

这样分类就添加上了，还需要给分类一个跳转页，创建一个 `categories.md` 用于跳转

```
hexo new page categories
```

会提示我们输入目录 `\source\categories\index.md`  ，打开这个 `index.md` ，加入 `type` 这个页面用于做什么的，`comment` 是否开启评论，前提是你有评论功能的话。

```
title: categories
date: 2019-04-25 14:53:31
```

```
type: categories
comments: false
```

这样分类就设置好了，检查一下 `Hexo 配置文件` ，搜索  `category_dir` 字段 `category_dir: categories` 这里已经设置了分类夹的名称，如果之前创建的文件夹完成和这个不一样，需要统一才行。

- 添加标签

同样在 `Hexo 配置文件` 搜索，`tag_dir` 可以知道 `tag` 设置好的文件夹名称，`tag_dir: tags`  ，我们可以在 `categories` 下添加 `tags` 来添加标签。

```
tags: [Hexo, NexT, 博客]
```

然后添加跳转页面

```
hexo new page tags
```

创建完成后，为 `tags\index.md` 添加内容 

```
title: categories
date: 2019-04-25 15:34:07
```

```
type: tags
comments: false
```

标签比分类多一步，我们需要安装一个插件

```
npm install hexo-generator-tag --save
```

这样 `hexo g && hexo s` 编译并运行，本地就可以看到了，标签在文章底部，发现它是 `# xxx` 很难看，修改的 `#` 需要找到 `/themes/next/layout/_macro/post.swig` ，搜索 

```
rel="tag">#
```

将 `#` 换成

```
<i class="fa fa-tag"></i>
```

这里的 `fa-tag` 也是在 [The Icons](https://fontawesome.com/v4.7.0/icons/) 中的图片。

- 将标签、分类添加至做出菜单栏

打开 `NexT 配置文件`   搜索 `menu` 

```
menu:
  home: / || home
  #about: /about/ || user
  tags: /tags/ || tags
  categories: /categories/ || th
  archives: /archives/ || archive
  #schedule: /schedule/ || calendar
  #sitemap: /sitemap.xml || sitemap
  #commonweal: /404/ || heartbeat
```

将 `tags` 和 `categories` 打开，完成 ~ 

#### 强调颜色

参考自作者 [Moorez](https://www.jianshu.com/p/f054333ac9e6) 

- ‘’ 内容样式的修改

打开 `\themes\next\source\css\_custom\custom.styl` ，在里面加入

```
// Custom styles.
code {
    color: #ff7600;
    background: #fbf7f8;
    margin: 2px;
}
// 大代码块的自定义样式
.highlight, pre {
    margin: 5px 0;
    padding: 5px;
    border-radius: 3px;
}
.highlight, code, pre {
    border: 1px solid #d6d6d6;
}
```

- 链接样式修改

修改文件 `themes\next\source\css\_common\components\post\post.styl`，在末尾添加如下css样式

```
// 文章内链接文本样式
.post-body p a{
  color: #0593d3;
  border-bottom: none;
  border-bottom: 1px solid #0593d3;
  &:hover {
    color: #fc6423;
    border-bottom: none;
    border-bottom: 1px solid #fc6423;
  }
}
```

设置网站图标

#### 设置网站图标

参考自作者 [Moorez](https://www.jianshu.com/p/f054333ac9e6) 

首先找一张喜欢的图片，可以在 [EasyIcon](http://www.easyicon.net/) 中或其他任意地方，分别下载 `32px` 和 `16px` 两张，然后放到 `/themes/next/source/images` 里，然后修改 `NexT 配置文件`  

```
favicon:
  small: /images/c_16.png
  medium: /images/c_32.png
  apple_touch_icon: /images/apple-touch-icon-next.png
  safari_pinned_tab: /images/logo.svg
```

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/picturesblog_title.png" style="zoom:100%">



------

