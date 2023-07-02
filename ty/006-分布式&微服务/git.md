

# Git

https://juejin.cn/post/6869519303864123399  主要是因为hexo d命令老是上传不到github上。所以尽量了解一下git操作和命令 遇到问题好排查解决。



## Git概念介绍

首先我们的了解Git通常的操作流程，网上流行的不错一张图👇

![Git经典流程图](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a1d538d63559402fbcfd82d68b08061c~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

首先在git init 时候会进行初始化版本库.git文件

- 版本库.git 
  - 当我们使用git管理文件时，比如`git init`时，这个时候，会多一个`.git`文件，我们把这个文件称之为版本库。
  - `.git文件`另外一个作用就是它在创建的时候，会自动创建master分支，并且将HEAD指针指向master分支。

- 工作区worksapce

  - 本地项目存放文件的位置

  - 可以理解成图上的workspace

- 暂存区 (Index/Stage)

  - 顾名思义就是暂时存放文件的地方，通过是通过add命令将工作区的文件添加到缓冲区  经典操作git add .

- 本地仓库（Repository）

  - 通常情况下，我们使用commit命令可以将暂存区的文件添加到本地仓库
  - 通常而言，HEAD指针指向的就是master分支

- 远程仓库（Remote）

  - 举个例子，当我们使用GitHub托管我们项目时，它就是一个远程仓库。
  - 通常我们使用clone命令将远程仓库代码拷贝下来，本地代码更新后，通过push托送给远程仓库。

------



## Git文件状态

- 通常我们需要查看一个文件的状态

```bash
git status
```

- ```
  Changes not staged for commit  表示得大概就是工作区有该内容，但是缓存区没有，需要我们`git add`
  ```

- ```
  Changes to be committed   一般而言，这个时候，文件放在缓存区了，我们需要`git commit`
  ```

- ```
  nothing to commit, working tree clean   这个时候，我们将本地的代码推送到远端即可
  ```

## Git工作区、缓存区、本地差异比较

![Git文件比较](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c779e736198247bfb0795b50dced0814~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)



## Git分支管理

![Git分支管理](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3bff7ddbc6a145f993c0841eb81c8998~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

## Git分支命名

![Git分支管理规范](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fd8abe5e5605411d8dbe5c4faa0054aa~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)



## Git Tags

1. tag对应某次commit节点, 是一个点，是不可移动的。
2. branch对应一系列commit，是很多点连成的一根线，有一个HEAD 指针，是可以依靠 HEAD 指针移动的。
3. 所以，两者的区别决定了使用方式，改动代码用branch ,不改动只查看用 tag。



## Git基本操作命令



### fetch

![Git命令fetch](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6c666ec139fe4dc5a08df6b811b9803d~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

```bash
 git fetch origin master:develop/mysql_sample_bug_feat   将远程master分支 拉去到本地新分支
```





### push

```bash
git push origin master:master
git push <远程主机名> <本地分支名>:<远程分支名>
```



### pull

```
git pull <远程主机名> <远程分支名>:<本地分支名>
git pull origin master:brantest        将远程主机 origin 的 master 分支拉取过来，与本地的 brantest 分支合并。
```

## Git merge冲突



