---
title: git使用
date: 2025-03-27 14:35:26
tags:
---

不管是写代码项目，还是实验报告，我们总是要遇到这样的情况：为了写出最完美的版本，我们要更改多次，但是含怕更改后出现问题且无法恢复，就必须复制出一个副本,于是就有了这样的情况：

- "test_1"
- "test_2"
- "test_3"
- ...最终版
- ...究极版
- ......

于是写着写着,自己都忘记了每个版本都干了什么了，只能再一个一个去看,找了个看着还凑合的就提交上去了......

不过，那些程序员大佬可没这个闲工夫看来看去。有了这样的需求，**版本控制器**应运而生，通过版本控制器，我们可以随时管理回溯到一个文件的各个版本，也方便多个人共同作业。

当下最主流的一款版本控制器叫**Git**，当然我们也听说过大名鼎鼎的**Github**就是一个由git发展而来的远程管理的网站，方便一些开源以及团队协同办公。 

## Git安装



## Git基本操作



### 配置Git

安装完Git后的第一个任务就是配置你的用户名称和邮箱地址（在团队协作中，我们需要知道是做了更改，并且可以通过什么方式联系到他）。配置方法：

```bash
git config [--global] user.name "Your Name" 
git config [--global] user.email "email@example.com"
#  Your Name 为你的昵称 
#  email@example.com 为你的邮箱 
```

配置完可以使用下面命令查看配置的信息：

```bash
git config -l
```

也可以使用下面命令删除配置信息：

```bash
git config [--global] --unset user.name
git config [--global] --unset user.email
```

上方**[--global]**是一个可选项，使用这个选项表明我们以后管理所有的文件都使用这个名字，如果想要在不同的仓库中使用不同的名字，可以去掉这个选项，然后在某个仓库内部执行命令。

### 创建本地仓库

现实中我们可以使用仓库来对物品进行管理（贴标签，做记录等），同理我们想要对文件进行管理，也要建立一个仓库，在这里我们的仓库实际上就是文件夹，不同的项目可以对应创建不同的仓库（即文件夹），Git通过追踪仓库内文件的变化实现版本控制。以下是两种创建本地仓库的方法：

-----

第一种：直接创建并初始化仓库

在终端内直接执行：

```bash
git init my-repo   #my-repo为你的仓库名，可以自己取名
```

- 作用：在当前目录下自动创建名为 `my-repo` 的文件夹，并初始化Git仓库。
- 注意：  
  - 仓库名称建议使用英文、数字或连字符（如 `my-project`），避免空格或特殊字符。
  - 执行后会在 `my-repo` 目录下生成隐藏的 `.git` 子目录，存放Git的版本控制数据。

------

第二种：手动创建文件夹后初始化

1. 先创建一个目录：

```bash
mkdir my-repo	# 创建文件夹
cd my-repo		# 进入该目录
```

2. 初始化仓库：

```bash
git init
```

注意：  

- 此方法适用于已有项目目录的初始化。
- 初始化后需确保当前目录下生成 `.git` 文件夹，可通过 `ls -a`（Linux/macOS）或显示隐藏文件（Windows）查看。

-----

注意：仓库目录中包含 `.git` 隐藏文件夹，该目录由Git自动管理，不要手动修改内部文件，否则可能导致版本信息损坏。进入`.git`文件夹下，可以看到里面的文件（看看就行[dog]）

```bash
.git
├── branches
├── config
├── description
├── HEAD
├── hooks
│   ├── applypatch-msg.sample
│   ├── commit-msg.sample
│   ├── fsmonitor-watchman.sample
│   ├── post-update.sample
│   ├── pre-applypatch.sample
│   ├── pre-commit.sample
│   ├── pre-merge-commit.sample
│   ├── prepare-commit-msg.sample
│   ├── pre-push.sample
│   ├── pre-rebase.sample
│   ├── pre-receive.sample
│   ├── push-to-checkout.sample
│   └── update.sample
├── info
│   └── exclude
├── objects
│   ├── info
│   └── pack
└── refs
    ├── heads
    └── tags
```



---

### 工作区、暂存区和版本库的概念

1. **工作区**：就是我们刚刚创建的仓库目录，也是我们以后要放代码或其他文件的目录。
2. **暂存区**：
