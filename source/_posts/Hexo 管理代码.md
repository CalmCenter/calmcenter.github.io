---
title: Hexo 管理代码
date: 2019-04-18 17:32:22
categories: Hexo
tags: [Hexo, git, github]

---

目录请看 [Hexo 搭建博客大全](https://calmcenter.github.io/2019/04/18/Hexo%20%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2%E5%A4%A7%E5%85%A8/)

## 本文主要记载

- `git` 拉取代码
- `git` 创建分支
- `git` 提交分支代码
- 其他终端如何使用 `Hexo` 源码

------

<!--more-->

##  一、管理代码

当我们需要在不同的终端去写博客的时候，发现 `github` 库中只有编译后的代码，所以我们需要将我们的 `hexo` 源码页放入 `github` 的分支中

首先我们需要拉取所有代码，选择一个空文件夹例如 `D:\blog\github_hexo` 

### 1.1 拉取主分支代码

#### 1.1.1 初始化 `git`

```
git init
```

#### 1.1.2 clone 远程代码，复制刚才的 `SSH` 路径 或者 `HTTPS` 路径

```
git clone <SSH/HTTPS>
```

#### 1.1.3 和远程仓库建立关联

```
git remote add origin <SSH/HTTPS>
```

如果 `falal：remote origin already exists.` ，执行下面命令

```
git remote rm origin
```

然后再次建立关联 `git remote add origin <SSH/HTTPS>` 

### 1.2 创建分支

#### 1.2.1 查看分支情况

进入拉取下来的目录 `cd <文件名>`

查看分支，查看本地分支包括远程分支

```
git branch -a
```

#### 1.2.2 创建本地分支

创建本地分支并切换到新分支

```
git checkout -b test
```

等价于 `git branch test` 和 `git checkout test` 

<img src="https://raw.githubusercontent.com/CalmCenter/picGo/master/picturesgit_branch1.png" style="zoom:100%">

这里会告诉你本地当前所处的分支，切换分支可以用，**当你切换分支时，如果本地没有但是远程有这个分支，它会自动给你拉取远程分支，并切换**

```
git checkout test 
```

#### 1.2.3 更新远程分支

上图你可以看到本地分支比远程分支多一个 `test` 下一步就是将新分支推送至远程GitHub

```
git push origin test
```

完成后，执行查看分支命令 `git branch -a` 会发现远程 多了 `test` 分支。

**如果想删掉分支**，删除本地分支

```
git branch -d <分支名称>
```

提交删除到远程

```
git push origin --delete <分支名称>
```

### 1.3 提交源码到远程分支

#### 1.3.1 本地操作代码

在确保是 `test` 分支下，然后将 `.git` 以外的所有文件删掉，将 `hexo` 源码复制到  `D:\blog\github_hexo` 下，查看文件状态

```
git status
```

**注意:如果你之前是 `git` 直接 `clone` 的 `NexT` ，在 `them/next` 会自带 `.git` 和 `.github` 文件，需要删掉 `.git` 和 `.github` 文件，如果不删会出现 `them/next` 里的文件提交不上去的问题**

### 设置语言、标题等

#### 1.3.2 添加到暂存区

**(最后是一个 . 或者 -A 表示所有)**

```
git add .
```

#### 1.3.3 提交本地代码库

```
git commit -m "描述"
```

#### 1.3.4 提交到远程分支

```
git push
```

如果提示没有关联，则用下面指令

```
git push --set-upstream origin <分支名>
```

### 1.5 其他终端操作

#### 1.5.1 `hexo` 环境搭建

首先创建一个空目录，初始化 `git`

```
git init
```

安装 `hexo-cli` 执行下面命令，如果该终端执行过可跳过，再次执行会报错，需要删除掉 `C:\Users\<电脑名字>\AppData\Roaming` 目录下 `npm-cache` 和 `npm` 文件，重新执行这个命令就好。`(个人多次实践出来的，不行就删。。。)` 

如果 `hexo` 命令执行过程中报 `bash: hexo: command not found` 就是没有安装 `hexo` ，需要执行下面的命令

```
npm install hexo-cli -g
```

#### 1.5.2 拉取远程分支代码

然后执行 5.1 的操作 `git clone <SSH/HTTPS>`、`git remote add origin <SSH/HTTPS>` ，将远程所有代码拉下来。当前状态你只有主分支代码，你还需要拉取你 `test` 分支的代码，进入拉取下来的目录 `cd <文件名>` 。

`git branch -a` 查看分支情况。然后切换并拉取 `test` 分支。

```
git checkout test
```

#### 1.5.3 安装环境

首先在文件目录下，安装 `hexo` 和 `deployer`

```
npm install hexo --save
```

```
npm install hexo-deployer-git --save
```

然后编译并运行

```
hexo g && hexo s
```

这样本地就好了，发布 `github` 需要配置 `SSH` 和之前 4.3 操作是一样的。