##### 初始化仓库
配置git：
	name:`git config --global user.name "tongzhiyuan"`
	email:`git config --global user.email "3184796337@qq.com"`
git status - 查看当前仓库的状态
```cmd
C:\Users\dell\OneDrive\桌面\vue-course\git-demo>git status
fatal: not a git repository (or any of the parent directories): .git
```
git init  - 初始化项目
```cmd
C:\Users\dell\OneDrive\桌面\vue-course\git-demo>git init
Initialized empty Git repository in C:/Users/dell/OneDrive/桌面/vue-course/git-demo/.git/

Warning: Your console font probably doesn't support Unicode. If you experience strange characters in the output, consider switching to a TrueType font such as Consolas!
```
这一步会生成一个隐藏的.git文件
![[1.png]]
在现实开发中一般不用,一般会用远程仓库
再次使用git status
```cmd
C:\Users\dell\OneDrive\桌面\vue-course\git-demo>git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)

C:\Users\dell\OneDrive\桌面\vue-course\git-demo>
```
### 文件状态
git中的文件有两种状态：未跟踪和已跟踪。未跟踪指文件没有被git所管理，已跟踪指文件已被git管理。已跟踪的文件又有三种状态：未修改、修改和暂存。

暂存，表示文件修改已经保存，但是尚未提交到git仓库。

未修改，表示磁盘中的文件和git仓库中文件相同，没有修改。

已修改，表示磁盘中文件已被修改，和git仓库中文件不同。

可以通过`git status`来查看文件的状态
##### 未跟踪-->暂存(已跟踪,类似在缓存中)
```cmd
C:\Users\dell\OneDrive\桌面\vue-course\git-demo>git status
On branch master

No commits yet

Untracked files:  `刚刚添加到项目的文件是未跟踪状态`
  (use "git add <file>..." to include in what will be committed)
        1.txt

nothing added to commit but untracked files present (use "git add" to track)

C:\Users\dell\OneDrive\桌面\vue-course\git-demo>
```
`git add  `   切换到暂存状态 add * 所有文件都变成暂存
```cmd
C:\Users\dell\OneDrive\桌面\vue-course\git-demo>git add 1.txt

C:\Users\dell\OneDrive\桌面\vue-course\git-demo>git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   1.txt


C:\Users\dell\OneDrive\桌面\vue-course\git-demo>
```
##### 暂存-->未修改
`git commit -m "message"`  -m 表示一个注释  将暂存的文件提交到仓库
`git commit -a -m "同时提交这两个文件"`  提交所有暂存的文件
```cmd
C:\Users\dell\OneDrive\桌面\vue-course\git-demo>git commit -m "第一次提交"
[master (root-commit) 695e026] 第一次提交
 1 file changed, 1 insertion(+)
 create mode 100644 1.txt
```
```cmd
C:\Users\dell\OneDrive\桌面\vue-course\git-demo>git status
On branch master
nothing to commit, working tree c
```
##### 未修改-->已修改
修改文件后
```cmd
C:\Users\dell\OneDrive\桌面\vue-course\git-demo>git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   1.txt     (已修改)

no changes added to commit (use "git add" and/or "git commit -a")
```
你需要先`git add`,后`git commit`,才能将文件重新变成未修改状态
```cmd
C:\Users\dell\OneDrive\桌面\vue-course\git-demo>git add 1.txt

C:\Users\dell\OneDrive\桌面\vue-course\git-demo>git commit 1.txt
[master 76337b8] 第二次提交文件
 1 file changed, 2 insertions(+), 1 deletion(-)

```
`git log`   获取提交日志
```cmd
C:\Users\dell\OneDrive\桌面\vue-course\git-demo>git log
commit 3005b575611ef8ff05c9417d642be3e99ddc3e45 (HEAD -> master)
Author: tongzhiyuan <3184796337@qq.com>
Date:   Sun Mar 26 21:23:37 2023 +0800

    第三次修改

commit 76337b81340edc4a4dadf7de2949a9d6db6f3c27
Author: tongzhiyuan <3184796337@qq.com>
Date:   Sun Mar 26 21:14:19 2023 +0800

    第二次提交文件

commit 695e026fb082c2aac425033deb4ceaf2af5d543e
Author: tongzhiyuan <3184796337@qq.com>
Date:   Sun Mar 26 21:06:01 2023 +0800

    第一次提交

```
#### 常用的命令
1. 恢复文件
```cmd
git restore .\1.txt 重置上一次commit,恢复文件

git restore --staged <filename> 取消暂存,但文件还是没有恢复需要在执行一次 git restore



```
2. 删除文件
```cmd
git rm  <filename>  删除文件,提交了才能真删除

git rm  <filename> -f 强制删除

```
3. 移动文件(重命名文件)
```cmd
s> git mv .\1.txt 3.txt
PS C:\Users\dell\OneDrive\桌面\vue-course\class> git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    1.txt -> 3.txt

PS C:\Users\dell\OneDrive\桌面\vue-course\class> 
```
#### 分支(重要)
gil在存储文件时，每一次代码代码的提交都会创建一个与之对应的节点，i就是通过一个一个的节点来记录代码的状态的。节点会构成一个树状结构，树状结构就意味着这个树会存在分支，默认情况下仓库只有一个分支，命名为master，在使用git时，可以创建多个分支，分支与分支之间相互独立，在一个分支上修改代码不会影响其他的分支。
![[2.png]]

```cmd 
git branch 查看当前分支

git branch <branch name> 创建分支

git switch <branch name> 切换分支

git branch -d <branch name> 删除分支

git switch -c <branch name> 创建并切换分支
```
在开发时,我们都是在自己的分支上开发代码,开发结束后,需要自己的代码合并到主分支上
```cmd 
1. git switch mester      快速分支
   git merge <branch name> 
```

![[Pasted image 20230415214210.png]]
![[Pasted image 20230415214240.png]]


### 变基（rebase）


   在开发中除了通过 merge 来合并分支外，还可以通过变基来完成分支的合并。

   我们通过 merge 合并分支时，在提交记录中会将所有的分支创建和分支合并的过程全部都显示出来，这样当项目比较复杂，开发过程比较波折时，我必须要反复的创建、合并、删除分支。这样一来将会使得我们代码的提交记录变得极为混乱。


   原理（变基时发生了什么）：

  

   1. 当我们发起变基时，git 会首先找到两条分支的最近的共同祖先

   2. 对比当前分支相对于祖先的历史提交，并且将它们提取出来存储到一个临时文件中

   3. 将当前部分指向目标的基底

   4. 以当前基底开始，重新执行历史操作

  

   变基和 merge 对于合并分支来说最终的结果是一样的！但是变基会使得代码的提交记录更整洁更清晰！注意！大部分情况下合并和变基是可以互换的，但是如果分支已经提交给了远程仓库，那么这时尽量不要变基。

  

   ### 远程仓库（remote）

  

   目前我对于 git 所有操作都是在本地进行的。在开发中显然不能这样的，这时我们就需要一个远程的 git 仓库。远程的 git 仓库和本地的本质没有什么区别，不同点在于远程的仓库可以被多人同时访问使用，方便我们协同开发。在实际工作中，git 的服务器通常由公司搭建内部使用或是购买一些公共的私有 git 服务器。我们学习阶段，直接使用一些开放的公共 git 仓库。目前我们常用的库有两个：GitHub 和 Gitee（码云）
   将本地库上传 git：

```bash

    git remote add origin https://github.com/lilichao/git-demo.git

    # git remote add <remote name> <url>

  

    git branch -M main

    # 修改分支的名字的为main

  

    git push -u origin main

    # git push 将代码上传服务器上

    ```

   将本地库上传 gitee：

   ```bash

    git remote add gitee https://gitee.com/ymhold/vue-course.git

    git push -u gitee main

    ```

   ### 远程库的操作的命令


   ```bash

    git remote # 列出当前的关联的远程库

    git remote add <远程库名> <url> # 关联远程仓库

    git remote remove <远程库名>  # 删除远程库

    git push -u <远程库名> <分支名> # 向远程库推送代码，并和当前分支关联

    git push <远程库> <本地分支>:<远程分支>

    git clone <url> # 从远程库下载代码

  

    git push # 如果本地的版本低于远程库，push默认是推不上去

    git fetch # 要想推送成功，必须先确保本地库和远程库的版本一致，fetch它会从远程仓库下载所有代码，但是它不会将代码和当前分支自动合并

             # 使用fetch拉取代码后，必须要手动对代码进行合并

    git pull  # 从服务器上拉取代码并自动合并

  

    ```


   注意：推送代码之前，一定要先从远程库中拉取最新的代码

   ### tag 标签
-   当头指针没有执行某个分支的头部时，这种状态我们称为分离头指针（HEAD detached），分离头指针的状态下也可以操作操作代码，但是这些操作不会出现在任何的分支上，所以注意不要再分离头指针的状态下来操作仓库。

-   如果非得要回到后边的节点对代码进行操作，则可以选择创建分支后再操作

    ```bash

    git switch -c <分支名> <提交id>

    ```

  
-   可以为提交记录设置标签，设置标签以后，可以通过标签快速的识别出不同的开发节点：


    ```bash

    git tag

    git tag 版本

    git tag 版本 提交id

    git push 远程仓库 标签名

    git push 远程仓库 --tags

    git tag -d 标签名 # 删除标签

    git push 远程仓库 --delete 标签名 # 删除远程标签

    ```


    ### gitignore

-   默认情况下，git 会监视项目中所有内容，但是有些内容比如 node_modules 目录中的内容，我们不希望它被 git 所管理。我们可以在项目目录中添加一个`.gitignore`文件，来设置那些需要 git 忽略的文件。

### github 的静态页面

-   在 github 中，可以将自己的静态页面直接部署到 github 中，它会给我们提供一个地址使得我们的页面变成一个真正的网站，可以供用户访问。

-   要求：

    -   静态页面的分支必须叫做：gh-pages

    -   如果希望页面可以通过 xxx.github.io 访问，则需要将库的名字配置为 xxx.github.io

  

### docusaurus

  

-   facebook 推出的开源的静态的内容管理系统，通过它可以快速的部署一个静态网站

  

-   使用：

  

    -   网址：

  

        -   https://docusaurus.io/

  

    -   安装

  

        -   `npx create-docusaurus@latest my-website classic`

  

    -   启动项目

  

        -   `npm start`或`yarn start`

  

    -   构建项目

  

        -   `npm run build`或`yarn build`

        -

  

    -   配置项目：

  

        -   docusaurus.config.js 项目的配置文件

  

    -   添加页面：

  

        -   在 docusaurus 框架中，页面分成三种：1.page，2.blog，3.doc

  

    -   案例地址：

  

        -   https://github.com/lilichao/lilichao.github.io





















