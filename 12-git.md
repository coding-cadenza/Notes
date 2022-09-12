### 什么是`git`

* Git是一款分布式源代码管理工具(版本控制工具)，我们写代码的时候可以让git帮我么们管理代码



### git特点

* Git易于学习， 占用空间小，性能快如闪电
* 具有便宜的本地分支、方便的暂存区和多个工作流等功能

### git与github、码云、gitlab的关系

* github、码云、gitlab都是在线的代码托管平台
  他们都支持git管理代码的方式
* ithub.com: 全球最大免费代码托管平台 
* 码云: 国内免费代码托管平台 
* gitlab:企业项目开发使用广泛



### 远程仓库相关命令

* 克隆仓库

  ```js
  git clone
  ```

* 查看远程仓库

  ```js
  git remote -v
  ```

* 添加远程仓库

  ```js
  git remote add [name] [url]
  ```

* 删除远程仓库地址

  ```js
  git remote rm [name]
  ```

* 拉取远程仓库

  ```js
  git pull [remotename] [localBranchName]
  ```

* 推送远程仓库

  ```js
  git push [remotename] [localBranchName]
  ```

* 如果向把本地test分支作为远程的master分支

  ```js
  git push origin test:master
  ```

  





### 初始化仓库

* 这个仓库会存放，git对我们项目代码进行备份的文件

* 命令

  ```js
  git init
  ```



### 配置

* 就是在git中设置当前使用的用户是谁

* 每一次备份都会把当前备份者的信息存储起来

  ```js
  git config --global user.name "CJF"
  git config --global user.email "@.com"
  ```

### 把代码存储到.git仓储

* 存放到暂存区

  ```js
  git add ./remdme.md   // 指定文件存放到暂存区
  git add ./      // 所有文件存放
  ```

* 将暂存区的文件提交到仓库

  ```git
  git commit -m "描述"
  ```

* 查看当前暂存区中没有被提交的文件

  ```js
  git status
  ```

  [![bwXAo9.png](https://s4.ax1x.com/2022/03/05/bwXAo9.png)](https://imgtu.com/i/bwXAo9)

### git中的忽略文件

* .gitignore,在这个文件中可以设置要被忽略的文件或者目录

  * 被忽略的文件不会被提交仓储里去

  * 在.gitignore中可以书写要被忽略的文件的路径，以/开头

    1. ```js
       /.idea   忽略指定文件
       ```

    2. ```js
       /js   忽略指定目录的所有文件
       ```

    3. ```js
       /js/*.js 忽略指定目录下所有指定后缀名的文件
       ```

### git pull和git fetch

* 相同点

  首先在作用上他们的功能是大致相同的，都是起到了更新代码的作用。

* 不同点

  1. fetch的时候本地的master没有变化，但是与远程仓关联的那个版本号被更新了，我们接下来就是在本地合并这两个版本号的代码。

  2. git pull看起来像git fetch+get merge，但是根据commit ID来看的话，他们实际的实现原理是不一样的。、

     > 但是有冲突的话还是会让你解决的

### 查看日志

*  查看历史提交的日志

  ```js
  git log
  ```

  [![bwXZJ1.png](https://s4.ax1x.com/2022/03/05/bwXZJ1.png)](https://imgtu.com/i/bwXZJ1)

* 简洁版的日志

  ```js
  git log --oneline
  ```

  [![bwXUQf.png](https://s4.ax1x.com/2022/03/05/bwXUQf.png)](https://imgtu.com/i/bwXUQf)





### 回退到指定版本

执行`git reset`命令时，该条版本号之后（时间作为参考点）的所有commit的修改都会退回到git缓冲区中

* 回退到上一次代码提交时的状态

  ```js
  git reset --hard Head~0
  ```

* 回退到上上次代码提交时

  ```js
  git reset --hard Head~1
  ```

* 可以通过版本号精确回退到某一次提交

  ```js
  git reset --hard [版本号]
  ```

* 可以查看每一次切换版本的信息

  >  可以利用这个撤销回退

  ```js
  git reflog
  ```







### 分支

* 默认有一个主分支master

* **查看分支**

  * 查看本地

    ```js
    git branch
    ```

  * 查看远程

    ```js
    git branch -r
    ```

* **创建分支**

  * 创建了一个dev分支

    > 在刚创建时dev分支里的东西和master分支里的东西是一样的

    ```js
    git branch dev
    ```

* **切换分支**

  ```js
  git checkout dev
  ```

* **创建并切换到新分支**

  ```
  git checkout -b [name]
  ```

* **删除分支**

  ```js
  git branch -d dev
  ```

* **合并分支**

  * 合并分支内容,把当前分支与指定的分支(dev),进行合并

  ```js
  git merge dev
  git rebase dev
  
  或者git merge master dev
  ```
  
* 撤销合并

  ```js
  git reset  --hard 版本号
  ```

  ```js
  git revert 版本号 -m回退
  ```

  





### git merge和git rebase的区别

图Feature为当前分支

* 使用merge的时候，会在当前分支中信件一个merge commit，将两个分支的联系串联在一起，也就是每次合并都会产生一个新的提交，且log里面

[![b0uiIs.png](https://s4.ax1x.com/2022/03/05/b0uiIs.png)](https://imgtu.com/i/b0uiIs)

* 如果用rebase方法，会将整个Feature分支移动到Master的顶端

  >  把被合并的分支Feature整个放到`另一个分支`前面，并更新另一个分支
  
  [![b0KNpq.png](https://s4.ax1x.com/2022/03/05/b0KNpq.png)](https://imgtu.com/i/b0KNpq)



### 团队开发协作中碰到的问题： 操作文件冲突(版本冲突)

* 先git pull 下拉远程仓库代码
* 然后再代码中找到发生冲突的代码
* 开发人员协商使用哪些代码
* 然后再git add . git commit -m “描述内容”
* git push 推送代码至远程仓库





### git仓库的三个组成部分是什么

* 工作区

  在 git 管理下的正常目录都算是工作区，我们平时的编辑工作都是在工作区完成

* 暂存区

  临时区域。里面存放将要提交文件的快照

* 历史记录区

  git commit 后的记录区。

[![b01PCd.png](https://s4.ax1x.com/2022/03/05/b01PCd.png)](https://imgtu.com/i/b01PCd)



### git reset 和git revert以及git checkout的区别

* **reset**
  * 可以将一个分支的末端指向之前的某个commit
  * 并且把这个commit之后的文件都回退到暂存区
  * 文件从历史记录区拿到暂存区，不影响工作区的内容

* **revert** 
  * revert 使用一个新的commit 来回滚你希望回滚的commit
  
  * 之前的历史仍保存完好
  
* **checkout**
  * 可以将 HEAD 移到一个新的分支，并更新工作目录
  * 是把文件从历史记录拿到工作区，不影响暂存区的内容，所以在切换分支之前最好先commit

### **解释 Forking 工作流程的优点**

* **Forking 工作流程** 与其他流行的 Git 工作流程有着根本的区别。它不是用单个服务端仓库充当“中央”代码库，而是为每个开发者提供自己的服务端仓库。Forking 工作流程最常用于公共开源项目中。
* Forking 工作流程的**主要优点**是可以汇集提交贡献，又无需每个开发者提交到一个中央仓库中，从而实现干净的项目历史记录。开发者可以推送（push）代码到自己的服务端仓库，而只有项目维护人员才能直接推送（push）代码到官方仓库中。
* 当开发者准备发布本地提交时，他们的提交会推送到自己的公共仓库中，而不是官方仓库。然后他们向主仓库提交请求拉取（pull request），这会告知项目维护人员有可以集成的更新。

###  Git 中 HEAD、工作树和索引之间的区别？

* **HEAD**是当前分支的最后一次提交的引用/指针
* **工作树**是你看到和编辑的（源）文件的目录树。

* **索引**是个在 /.git/index，单一的、庞大的二进制文件，该文件列出了当前分支中所有文件的 SHA-1（散列） 检验和、时间戳和文件名

### 能解释下 Gitflow 工作流程吗？

* **Gitflow** 工作流程使用两个并行的、**长期运行**的分支来记录项目的历史记录，分别是 `master`和`develop`分支。

* **Master**

  随时准备发布线上版本的分支，其所有内容都是经过全面测试和核准的（生产就绪）

* **Hotfix**维护（maintenance）或修复（hotfix）分支

  用于给快速给生产版本修复打补丁的。修复（hotfix）分支很像发布（release）分支和功能（feature）分支，除非它们是基于 master 而不是 develop 分支。

* **Develop**

  是合并所有功能（feature）分支，并执行所有测试的分支。只有当所有内容都经过彻底检查和修复后，才能合并到 master 分支。

* **Feature**

  每个功能都应留在自己的分支中开发，可以推送到 develop 分支作为功能（feature）分支的父分支。



###  什么时候应使用 `git stash`？

git stash 命令把你未提交的修改（已暂存（staged）和未暂存的（unstaged））保存以供后续使用，以后就可以从工作副本中进行还原。

### **如何从 git 中删除文件，而不将其从文件系统中删除？**

如果直接git rm会在文件中也删除

* git reset filename
* 也可以把文件加入.gitignore中



### Git工作流程

* 在工作目录中修改某些文件
* 将文件提交到暂存区
* 提交更新，将保存在暂存区域的文件快照永久转储到Git目录中

