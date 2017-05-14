title : Git 学习笔记
date  : 2017/5/12

---

# Git 安装（ Windows ）

下载、默认安装完成后，运行 Git Bash ，弹出类似命令行窗口，说明安装成功。然后做最后一步设置，在命令行中输入：
```
$ git config --global user.name "your name"
$ git config --global user.email "email@example.com"
```
这里只是做一个识别区分而已。其中 `git config` 命令的 ` --global` 参数，表示这台机器上所有的 Git 仓库都会使用这个配置，当然也可以指定仓库另行配置。

# 创建版本库

### 第一步，创建空目录
```
$ mkdir learngit
$ cd learngit
$ pwd
/e/GitRepository/learngit
```
`mkdir` 命令用于在当前目录下创建目录；

`cd` 命令用于切换到指定目录；

`pwd` 命令用于显示当前目录。

### 第二步，初始化一个 Git 仓库

通过 `git init` 命令把这个目录变成 Git 可以管理的仓库：
```
$ git init
Initialized empty Git repository in E:/GitRepository/learngit/.git/
```
仓库建好之后，当前目录下多了一个 `.git` 目录，是 Git 来跟踪管理版本库的，不可手动修改。
    
### 第三步，把文件添加到版本库

要真正使用版本控制系统，就要以纯文本的方式编写文件，并且最好使用标准的 UTF-8 编码。

* 不要使用 Windows 自带的记事本编辑任何文本文件。建议使用 Notepad++ 或 EditPlus 代替记事本，并把编码设置为 UTF-8 without BOM 即可。

编写一个 txt 文件，放到 learngit 目录（或子目录）下，因为这是一个 Git 仓库。

接下来把文件添加到仓库，需要两步：

1. 用命令 `git add` 告诉 Git ，把文件添加到仓库，执行后没有任何显示说明添加成功：
```    
$ git add readme.txt
```

2. 用命令 `git commit` 告诉 Git ，把文件提交到仓库，其中 `-m` 后面输入的是本次提交的说明，方便过后阅读：
```
$ git commit -m "wrote a readme file"
[master (root-commit) da2a5bd] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```

Git 添加文件需要 `add` 和 `commit` 两步是因为 `commit` 可以一次提交很多文件，所以可以多次 `add` 不同的文件：
```
$ git add file1.txt
$ git add file2.txt
$ git commit -m "add 3 files."
```

# 时光机穿梭

修改 readme.txt 文件内容后，运行 `git status` 命令，该命令可以查看工作区的当前状态，比如是否修改了文件、是否有准备提交的修改：
```
$ git status
On branch master
Changes not staged for commit:
   (use "git add <file>..." to update what will be committed)
   (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

如果想看具体修改的内容，需要用 `git diff` 命令，顾名思义就是查看 difference ：
```
$ git diff readme.txt 
diff --git a/readme.txt b/readme.txt
index 46d49bf..9247db6 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
 Git is free software.
```

接下来再提交到仓库，同样分为两步： `git add` 和 `git commit` ，期间可以使用 `git status` 查看状态变化：
```
$ git add readme.txt
```
```
$ git status
On branch master
Changes to be committed:
   (use "git reset HEAD <file>..." to unstage)

       modified:   readme.txt

```
```
$ git commit -m "add distributed"
[master ea34578] add distributed
 1 file changed, 1 insertion(+), 1 deletion(-)
```
```
$ git status
On branch master
nothing to commit (working directory clean)
```

## 版本回退

使用 `git log` 命令，可以显示提交日志，显示中的那一大串数字就是 commit id ，即版本号：
```
$ git log
commit 253c2ae647eb6842b23ff63729eb7e83ace25974
Author: Ling <294844972@qq.com>
Date:   Thu May 11 20:05:52 2017 +0800

    append GPL

commit 261f71f4496d9ed7246d0edd4966831b63bb00a6
Author: Ling <294844972@qq.com>
Date:   Thu May 11 19:57:02 2017 +0800

    add diistributed

commit da2a5bdce104924ed546262972f4db36d4415e69
Author: Ling <294844972@qq.com>
Date:   Thu May 11 19:23:41 2017 +0800

    wrote a readme file
```
```
$ git log --pretty=oneline
253c2ae647eb6842b23ff63729eb7e83ace25974 append GPL
261f71f4496d9ed7246d0edd4966831b63bb00a6 add diistributed
da2a5bdce104924ed546262972f4db36d4415e69 wrote a readme file
```

在 Git 中， `HEAD` 表示当前版本，也就是最新版本，上一个版本就是 `HEAD^` ，上上一个版本就是 `HEAD^^` ，如果是往上 100 个版本就可以写成 `HEAD~100` 。

现在把当前版本回退到上一个版本，使用 `git reset` 命令：
```
$ git reset --hard HEAD^
HEAD is now at 261f71f add diistributed
```

然后使用 `cat` 命令查看内容：
```
$ cat readme.txt
Git is a distrributed version control system.
Git is free software.
```

这时看下版本库的状态：
```
$ git log
commit 261f71f4496d9ed7246d0edd4966831b63bb00a6
Author: Ling <294844972@qq.com>
Date:   Thu May 11 19:57:02 2017 +0800

    add diistributed

commit da2a5bdce104924ed546262972f4db36d4415e69
Author: Ling <294844972@qq.com>
Date:   Thu May 11 19:23:41 2017 +0800

    wrote a readme file
```

最新的版本已经找不到了，想要回去可以使用命令 `git reset --hard commit_id` ，即最新版本的版本号（前几位就好）回到指定版本：
```
$ git reset --hard 253c2ae64
HEAD is now at 253c2ae append GPL
```

Git 提供了命令 `git reflog` 来记录每一次命令，可以查到版本号：
```
$ git reflog
253c2ae HEAD@{0}: reset: moving to 253c2ae64
261f71f HEAD@{1}: reset: moving to HEAD^
253c2ae HEAD@{2}: commit: append GPL
261f71f HEAD@{3}: commit: add diistributed
da2a5bd HEAD@{4}: commit (initial): wrote a readme file
```

## 工作区和暂存区

名词解释：

* 工作区：电脑中可以看到的目录，如 learngit 文件夹；

* 版本库：工作区中的隐藏目录 `.git` ，是 Git 的版本库，其中存放有暂存区 stage 、 Git 自动创建的第一个分支 master 、指向 master 的指针 HEAD 。

前边讲到往 Git 版本库中添加文件时分两步执行，其实就是：1. 用 `git add` 把需要提交的文件修改放到暂存区；2. 用 `git commit` 将暂存区的所有修改全部提交到当前分支。

全部提交后再次查看工作区状态，可以看到显示工作区是“干净”的：
```
$ git status
On branch master
nothing to commit, working tree clean
```

## 管理修改

Git 管理的是修改不是文件，所以 add 到暂存区的是修改不是文件，进行修改后想要提交到 commit 都要先 add 到暂存区。

## 撤销修改

1. 当改乱了工作区某个文件，想直接丢弃工作区的修改时，用命令 `git checkout -- file` 。

2. 当改乱了工作区某个文件还添加到了暂存区，想丢弃修改时，用命令 `git reset HEAD file` 回到 1 ，再按 1 操作。

3. 已经将修改提交到版本库，想要撤销本次提交时，参考**版本回退**一节，不过前提是没有推送到远程库。

## 删除文件

误删文件后,可以用 `git checkout -- file` 命令从版本库中提交的版本；

如果确实要从版本库中删除该文件，可是使用 `git rm` 命令删掉并且 `git commit` 。

# 远程仓库

1. 注册 GitHub 账号。

2. 创建 SSH Key 。在用户主目录下查看 .ssh 目录，目录下有 id\_rsa 和 id\_rsa.pub 两个文件，分别是**私钥**和**公钥**。如果找不到 .ssh 目录，需要打开 Git Bash（Windows下）创建 SSH Key ：
```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

3. 登录 GitHub，在设置中添加 Key（ Title 任意，Key 文本框中粘贴 id_rsa.pub 的内容）。

## 添加远程库

1. 在 GitHub 上创建一个新的仓库（远程库的名字为 origin ，是 Git 默认的叫法）；

2. 使用命令 `git remote add origine git@github.com:username/reponame.git` 关联远程库;

3. 使用命令 `git push -u origin master` 推送 master 分支的所有内容到远程库上；

4. 之后，每次本地提交后可以使用命令 `git push origin master` 推送最新修改。

* 第一次使用Git的 `clone` 或者 `push` 命令连接 GitHub 时会出现 SSH 警告，是因为 Git 使用 SSH 连接，而 SSH 连接在第一次验证 GitHub 服务器的 Key 时，需要确认 GitHub 的 Key 的指纹信息是否真的来自 GitHub 的服务器，输入 “yes 回车”即可。

## 从远程库克隆

确定被克隆的仓库的地址后，使用 `git clone` 命令克隆到当前目录下：

```
$ git clone git@github.com:michaelliao/gitskills.git
Cloning into 'gitskills'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (3/3), done.
```

克隆完成后进入目录可以看到克隆完成：
```
$ cd gitskills
$ ls
README.md
```

## BUG
>$ git push -u origin master
error: src refspec master does not match any.
error: failed to push some refs to 'https://github.com/Ling00000/MarkDownNote.git'

就是因为第一次推送的时候，没有先 `commit` ，所以 git 找不到任何可以推送的东西。 