# 项目中的Git工作流程


一些规范
--------------------------
1. 项目中有两个固定分支master和development
2. 开发本地只克隆development分支, 只有需要relase或者hotfix时候才会在本地克隆master代码来进行合并
3. 所有开发时新添加的feature或者新修复的bug都只能直接合并到development分支上


实际开发流程
--------------------------
###  1. 克隆远端的development分支

```bash
git clone -b development <remote-repository-name>
```

###  2. 创建新的分支
开始实现一个feature或者解决一个bug之前，首先切换到development分支上

```bash
git checkout development
```

创建feature或者bug的分支,并且切换到该分支

```bash
git checkout -b <feature-branch-name> development
```

###  3. 完成开发的工作
修改一些文件，添加修改的文件到暂存区(staging area)

```bash
git add .
```

将修改后的文件提交到本地的版本库中

```bash
git commit -am 'Add a new feature'
```

### 4. 提交你的代码到中央版本库上
提交之前保证你本地的development分支的代码是最新的

```bash
git checkout development
git pull origin development
```

将你在branch上完成的代码修改合并到development分支上

```bash
git merge <feature-branch-name>
```

**or**

```bash
git rebase -i <feature-branch-name>
```

提交代码到中央版本库

```bash
git push
```

*删除本地创建的分支（可选）

```bash
git branch -d <feature-branch-name>
```


在Windows上使用Gitflow规范流程
--------------------------
### 1. 将Gitflow克隆到本地

```bash
git clone -recursive git://github.com/nvie/gitflow.git
```

### 2. 下载与msysgit集成Bin文件
[util-linux-ng-2.14.1-bin](http://sourceforge.net/projects/gnuwin32/files/util-linux/2.14.1/util-linux-ng-2.14.1-bin.zip/download)

[util-linux-ng-2.14.1-dep](http://sourceforge.net/projects/gnuwin32/files/util-linux/2.14.1/util-linux-ng-2.14.1-dep.zip/download)
### 3. 将Bin文件拷贝到msysgit的bin目录下
下载完成后分别将两个压缩包解压文件下bin目录中的getopt.exe，libintl3.dll和libiconv2.dll文件拷贝到msysgit安装目录下的bin目录中
### 4. 安装Gitflow工具
打开cmd命令行，进入已经克隆好的gitflow contrib目录中执行命令

```bash
D:\gitflow contrib>msysgit-install.cmd "C:\Program Files\Git".
```

### 5. 开始在console中使用Gitflow

```bash
usage: git flow <subcommand>

Available subcommands are:
   init      Initialize a new git repo with support for the branching model.
   feature   Manage your feature branches.
   release   Manage your release branches.
   hotfix    Manage your hotfix branches.
   support   Manage your support branches.
   version   Shows version information.

Try 'git flow <subcommand> help' for details.
```

详细的Gitflow使用方法参考[Git Flow Cheatsheet](http://danielkummer.github.io/git-flow-cheatsheet/index.zh_CN.html)


使用Gitflow之后的开发流程
--------------------------
### 1. 为本地代码库添加Git flow特性

```bash
git flow init
```

使用默认值进行初始化设定
### 2. 开始增加新特性/修复bug

```bash
git flow feature start <feature-branch-name>
```

###  3. 完成开发的工作
修改一些文件，添加修改的文件到暂存区(staging area)

```bash
git add .
```

将修改后的文件提交到本地的版本库中

```bash
git commit -am 'Add a new feature'
```

###  4. 完成新特性/修复bug

```bash
git flow feature finish <feature-branch-name>
```

###  5. 同步到中央代码库

```bash
git flow feature publish <feature-branch-name>
```

[详细说明参考](http://danielkummer.github.io/git-flow-cheatsheet/index.zh_CN.html/#features)


准备release
--------------------------
### 1. 创建release分支

```bash
git checkout -b <release-branch-name> development
```

### 2. 完成relase的相关工作

```bash
git add .
git commit -am 'Finish release related work'
```

### 3. 将relase分支合并到master和development分支，并且同步到中央版本库

```bash
git checkout master
git merge <release-branch-name>
git push
git checkout development
git merge <release-branch-name>
git push
git branch -d <release-branch-name>
```

### 4. 在主分支上添加tag，并且同步到中央服务器

```bash
git tag -a <version-number> -m 'Create 0.1 version release' master
git push --tags
```

[使用Gitflow准备release](http://danielkummer.github.io/git-flow-cheatsheet/index.zh_CN.html/#release)


创建hotfix
--------------------------
### 1. 从master分支上创建一个hotfix的新分支

```bash
git checkout -b <hotifx-branch-name> master
```

### 2. 修复问题

```bash
git add .
git commit -am 'Fix the crash bug'
```

### 3. 将relase分支合并到master和development分支，并且同步到中央版本库

```bash
git checkout master
git merge <hotifx-branch-name>
git push
git checkout development
git merge <hotifx-branch-name>
git push
git branch -d <hotifx-branch-name>
```

[使用Gitflow创建hotfix](http://danielkummer.github.io/git-flow-cheatsheet/index.zh_CN.html#hotfixes)


参考
--------------------------
[Gitflow工作流英文版](https://www.atlassian.com/git/workflows#!workflow-gitflow)

[快速开始](http://rogerdudler.github.io/git-guide/)

[如何使用Gitflow插件](http://danielkummer.github.io/git-flow-cheatsheet/index.zh_CN.html)

[Git文档](http://git-scm.com/book/en)

[我的Github工作流](https://github.com/vincenthou/vincenthou.github.io/issues/1)