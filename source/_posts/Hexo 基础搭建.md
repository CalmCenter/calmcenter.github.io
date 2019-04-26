---
title: Hexo 基础搭建
date: 2019-04-18 17:32:22
categories: Hexo
tags: [Hexo, github, git]

---

目录请看 [Hexo 搭建博客大全](https://calmcenter.github.io/2019/04/18/Hexo%20%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2%E5%A4%A7%E5%85%A8/)

## 本文主要记载

- 搭建本地博客
- 部署到 `Github Pages`

```
本文环境是 win10 或 win 7。mac 再执行 npm 时需要在前面添加 sudo
本文整理于各大佬文章，文中会给出相应链接，如有侵权，请联系我修改或删除。
```

---

<!--more-->

## 一、搭建本地博客

### 1.1 首先安装 `Node.js`

首先去 [官方页面](https://nodejs.org/en/download/) 下载安装文件，无脑安装就好 （~。~）

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/picturesnode.png" style="zoom:20%">

图中绿色选择部分，安装完成后输入 `npm -v` , 会告诉你版本号，就证明你安装成功了

3.2 安装 `Git`

去 [git官网](https://git-scm.com/download/win) 下载电脑对应版本，进行安装，安装完成后，输入 `git version` ，会告诉你版本号，就证明你安装成功了。安装成功后，鼠标右键菜单里会多出 `Git GUI Here` 和 `Git Bash Here` 两个按钮。

**[Git安装教程](https://www.cnblogs.com/wj-1314/p/7993819.html)  这个是百度的，如果不会查看本链接或重新百度就好~**

**我管理代码都是在 [Sourcetree](https://www.sourcetreeapp.com/) 上进行，后续会说，当然也是要 Git 的支持，这个还是很方便的，无脑操作~6**

### 1.2 安装 `Hexo`

**注意执行命令期间 `WARN` 不管 只看 `ERR` **

在文件夹内如 `D:\blog` ，鼠标右键点击 `Git Bash Here` 一气呵成，来到了命令行界面。

首先安装 `hexo` 

```
npm install hexo-cli -g
```

#### 1.2.1 镜像相关（如果 npm 可以正常使用这里跳过！）

 上面正常情况是没有问题的，但是由于国内访问官方 NPM 源速度较慢，为了一劳永逸，此处可以将 NPM 源更换为了淘宝 NPM 镜像源。
**请注意!!，如果你觉得你的 NPM 源速度够快，更换镜像源这部分可选择性使用**

在 `Git Bash Here` 中输入指令，将官方 npm 源更换为淘宝 npm 镜像源

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

可以输入 

```
cnpm config list
```

 查看是否更换成功

**请注意，如需使用上方安装的淘宝源，需要在使用 npm 命令时将其改为 cnpm **，但是如果用了 cnpm 再使用 npm 的话，好像有点问题，npm 一直报 err 。所以这里给出卸载镜像的命令

```
npm uninstall cnpm -g
```

但是 npm 命令还是报错，还需要删除掉 `C:\Users\<电脑名字>\AppData\Roaming` 目录下  `npm-cache` 和 `npm` 文件，重新执行上面两个安装命令即可

### 1.3 Hexo初始化

安装完成后，输入 `hexo -v` 会输出 hexo 版本号，证明安装成功。

然后在当前目录新建一个文件夹，比如 `D:\blog\hexos` ，在此目录下鼠标右键点击 `Git Bash Here` 执行，这条命令需要一个空文件夹所以新建一个。

```
hexo init
```

完成后，文件目录如下

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/pictureshexo_file.png" style="zoom:100%">

这样就证明初始化完成了，然后我们继续要生成静态页面，用到的命令是

```
hexo g
```

其中，`g` 的全称是 `generate`，当然也可以用 `hexo generate` 这条命令。

然后就是运行了

```
hexo s
```

其中， `s` 的全称是 `server`，当然也可以用 `hexo server` 这条命令

然后，打开你的浏览器，输入`http://localhost:4000/` 即可看到本地静态博客

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/pictureshexo_page.png" style="zoom:20%">

本地静态博客完成 ~ 

------

## 二、部署到 Github Pages

### 2.1 注册Github账户

进入 [github首页](https://github.com/) ，点击右上角 [sign up](https://github.com/join?source=header-home) 进行注册。

### 2.2 创建项目

登录后，创建一个自己的 `GitHub Pages `。 点击头像中的 [New repository](https://github.com/new) 。

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/picturesnew_repository.png" style="zoom:50%">

**敲黑板！！ 这里重点就是项目名称必须是 `自己名称.github.io`  **

### 2.3 配置SSH密钥

#### 2.3.1 查看是否存在SSH密钥

首先通过输入命令

```
cd ~/. ssh 
```

如果存在则会进入此目录,可以略过 4.3.2，否则会提示你不存在，那么继续 4.3.2

#### 2.3.2 创建新的SSH密钥

```
ssh-keygen -t rsa -C "your_email@example.com"
```

这将按照你提供的邮箱地址，创建一对密钥，然后让你输入 密码

```
Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]
```

如果你放心，可以不用密码，直接回车，这样每次提交的时候比较方便。

#### 2.3.3 在  [GitHub](https://github.com/) 添加你的公钥

1. 首先拷贝公钥内容（ mac 可能用不了，需要手动找到这个文件复制内容）

```
clip < ~/.ssh/id_rsa.pub
```

2. 然后登陆 [GitHub](https://github.com/) ，点击头像

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/picturessetting.png" style="zoom:50%">

3. 进入设置页，选择SSH

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/picturessetting_list.png" style="zoom:50%">



4. 粘贴密钥，添加即可

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/picturesssh_content.png" style="zoom:50%">

5. 测试

```
ssh -T git@github.com
```

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/picturestest_ssh.png" style="zoom:100%">

6. 设置用户信息

`Git` 会根据用户的名字和邮箱来记录提交。

```
git config --global user.name "name"
```

```
git config --global user.email "email"
```

这样就配置好了SSH

### 2.4 将本地 `Hexo` 文件编译并上传 `GitHub` 的库中

1. 打开 [github首页](https://github.com/) 登录，找到左上角自己的项目

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/picturesgithub_list.png" style="zoom:70%">

2. 点击 clone 点击 Use SSH 并复制 `SSH` 路径

   <img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/picturesgithub_ssh_path.png" style="zoom:70%">

3. 打开 `hexo` 目录，找到 `_config` 文件

   <img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/pictureshexo_catalog_config.png" style="zoom:70%">

4. 打开并找到 `deploy` 关键字

```
deploy:
  type: git
  repository: git@github.com:CalmCenter/calmcenter.github.io.git
  branch: master
```

**注意: 引号 后有一个空格，repository 填写 ssh 地址，branch 如果没有特殊要求，写master**

5. 编译并提交

部署前需要先装 `deployer` ，`deployer` 用于将 `hexo` 部署到  `git page` 

```
npm install hexo-deployer-git --save
```

提交前，有时候提交了不生效，需要清理一下缓存

```
hexo clean
```

编译并提交

```
hexo g -d
```

 和 `hexo g` 、 `hexo d` 一样

**提交后线上会有延迟才会展现最新效果，特别是配置样式之后**

提交过程中会让你输入一次密码，完成后就可以在外网访问博客了。[https://calmcenter.github.io/](https://calmcenter.github.io/) `https://用户名.github.io`

假如这时候，报错 `ERROR Deployer not found: git`，那么就是你的 `deployer` 没有安装成功，你需要执行如下命令再安装一次：

```
npm install hexo-deployer-git --save
```

这样，你再执行 `hexo g -d` ，你的博客就部署到 `Github` 上了。