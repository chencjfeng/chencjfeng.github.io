---
title: git pull冲突解决
date: 2017-11-04 15:04:14
author: "chenJF"
tags: git
categories: 工具
---

### 导语：
> 在公司团队中写完代码就要提交到git上面，因为多人合作，先要将远端的代码pull更新到本地。往往这时候因为大家对同一个文件同一个地方做了操作，导致pull代码冲突发生，工程崩溃。提示错误信息如下：
~~~
error: Your local changes to 'c/environ.c' would be overwritten by merge.  Aborting.
Please, commit your changes or stash them before you can merge.
~~~
> 这个提示意思就是说更新下来的内容和本地修改的内容有冲突，先提交你改变的内容或者先将你本地修改的内容暂时存起来。
> 下面我们就分几步解决处理这个pull冲突问题.

### 1.存储本地修改的内容
~~~
git stash
~~~
这句命令就是将本地修改的代码做一份备份存储起来，可以用git stash list 查看刚刚备份保存的内容：
![git stash list.png](http://upload-images.jianshu.io/upload_images/4970496-84f5c1a7a77608c6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/600)
其中stash@{0}就是刚刚备份存储的标记

### 2.pull内容
将本地代码做了备份保存后，就可以pull远端代码
~~~
git pull
~~~

### 3.还原备份暂存的代码
~~~
git stash pop stash@{0}
~~~
stash@{0}是你刚刚备份存储的标记
这时候系统会提示类似以下的信息：
~~~
Auto-merging c/environ.c
CONFLICT (content): Merge conflict in c/environ.c
~~~
这个提示内容意思就是系统自动合并修改的内容，但是当中会有冲突，需要解决其中的冲突。

### 4.解决文件中的冲突内容
打开上面提示的冲突文件，会看到类似的内容：

![冲突提示.png](http://upload-images.jianshu.io/upload_images/4970496-92f347853efe0765.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/500)
其中Updated upstream和=======之间的内容是从远端pull下来的代码，=======和Stashed changes之间的内容则是你本地修改的内容。这时候，需要你修改决定留下哪些需要的内容。

最后，解决完冲突，就可以正常git提交了。
