[TOC]
```
git init
git add .
git commit -m "sync"
git remote add origin https://github.com/yuuxeun/HUNAU_ACM_OJ
git push -u origin master
```



# Git教程

## git 常见命令

```
最常用的 git 命令有：
   add        添加文件内容至索引
   bisect     通过二分查找定位引入 bug 的变更
   branch     列出、创建或删除分支
   checkout   检出一个分支或路径到工作区
   clone      克隆一个版本库到一个新目录
   commit     记录变更到版本库
   diff       显示提交之间、提交和工作区之间等的差异
   fetch      从另外一个版本库下载对象和引用
   grep       输出和模式匹配的行
   init       创建一个空的 Git 版本库或重新初始化一个已存在的版本库
   log        显示提交日志
   merge      合并两个或更多开发历史
   mv         移动或重命名一个文件、目录或符号链接
   pull       获取并合并另外的版本库或一个本地分支
   push       更新远程引用和相关的对象
   rebase     本地提交转移至更新后的上游分支中
   reset      重置当前HEAD到指定状态
   rm         从工作区和索引中删除文件
   show       显示各种类型的对象
   status     显示工作区状态
   tag        创建、列出、删除或校验一个GPG签名的 tag 对象

```



## Shell版

### 配置

Git 允许我们在 .gitconfig 文件中保存全局设置. 这个文件位于用户的home目录. 每次提交都会保存作者和提交者的信息，这些信息都可以保存在全局配置中。

获取Git配置信息列表：

```
`git config --list`
```

配置用户名和Email

```
`# 配置全局用户名``git config --global user.name ``"Alan"``# 配置全局email``git config --global user.email ``"your.email@gmail.com"``# 设置push的全局默认操作为 matcheing 即匹配的情况下不会用户的push``git config --global push.default ``"matching"``# 查看配置列表``git config --list`
```

终端配置高亮

```
`git config --global color.status auto``git config --global color.branch auto`
```

设置默认编辑器
git会使用系统默认的编辑器，我们也可以手动设置这一选项

```
`git config --global core.editor vim `
```

除了全局配置之外，用户每次新建的git仓库也有自己的局部配置，位于 当前git项目的 .git 目录下。所有的git设置选项都在这个手册中能找到: [git 配置手册](https://www.kernel.org/pub/software/scm/git/docs/git-config.html)

### 创建文件夹

> 首先需要一个存放仓库的文件夹，我们可以通过以下代码来创建

```
`# 切换到 home 目录``cd` `~/` `# 创建一个存放的文件夹并切换到该目录下``mkdir` `~``/project_main``cd` `project_main` `# create a new directory``mkdir` `datafiles `
```

### 创建 Git 仓库

每一个Git库在刚创建的时候就会初始化一个 .git 文件夹来保存这个资料库的完整的历史信息，在 .git/config 文件包含当前资料库的配置信息。

如下代码则是在当前文件夹中创建了一个 git 资料库

```
`# 在当前文件夹下初始化一个 Git 资料库``git init `
```

输出：

```
`初始化空的 Git 版本库于 ``/home/project_main/``.git/`
```

### 添加一些内容

```
`# 切换到这个库下(刚刚init的文件夹)``cd` `~``/project_main` `# 创建一些文件``touch` `test01``touch` `test02``touch` `test03``# 再来个文件夹``mkdir` `datafiles``touch` `datafiles``/data``.txt` `# 使用 > 命令将 ls 命令的输出导入到test01中``ls` `> test01 `
```

### 查看库状态

git status 命令可以显示工作树状态，也就是文件的改变（添加、删除、部分修改等等）。它可以显示文件的合并冲突（当前库与远程库不一致）并且就对于这些改变用户可以做的事情而提出建议，例如将更改添加到索引或者删除等等。

```
`git status `
```

输出：

```
`# 位于分支 master``#``# 初始提交``#``# 未跟踪的文件:``#  （使用 "git add ..." 以包含要提交的内容）``#``#    datafiles/``#    test01``#    test02``#    test03``提交为空，但是存在尚未跟踪的文件（使用 ``"git add"` `建立跟踪）`
```

### 添加文件到 Git 索引

在将修改提交到 Git 库之前，你需要通过添加(add)操作来mark出你想要提交到Git索引的改变。这实际上是一个暂时的提交列表， 如果你后来又改变了其中的某一个文件，不用担心，这还不是正式提交，你只需要再add一次来更新你的提交列表就可以了（与远程库交互的时候，这样可以节省很多不必要的麻烦）。

```
`# 添加所有文件(夹)到当前 Git 库的索引（临时提交列表）``git add . `
```

接着可以再次运行 git status 命令来观察当前状态。

```
`git status`
```

输出：

```
`# 位于分支 master``#``# 初始提交``#``# 要提交的变更：``#  （使用 "git rm --cached ..." 撤出暂存区）``#``#    新文件：  datafiles/data.txt``#    新文件：  test01``#    新文件：  test02``#    新文件：  test03``#`
```

输出：

```
`# 位于分支 master``#``# 初始提交``#``# 要提交的变更：``#  （使用 "git rm --cached ..." 撤出暂存区）``#``#    新文件：  datafiles/data.txt``#    新文件：  test01``#    新文件：  test02``#    新文件：  test03``#``# 未跟踪的文件:``#  （使用 "git add ..." 以包含要提交的内容）``#``#    datafiles/data2.txt`
```

接着添加更改就是了：

```
`git add datafiles``/data2``.txt`
```

自己可以再通过 git status 查看一下临时提交列表。如果当前没有做任何修改，或者修改都已经提交那么这会显示：

```
`git status``# 位于分支 master``无文件要提交，干净的工作区`
```

### 正式提交到 Git 库

确定好了之后，你就可以正式提交了。这个操作会添加一个Git库中所有文件的快照。“-m”选项表示附加注释内容，如果你没有在命令中就使用 -m 附上注释，你的默认编辑器就会自动启动所以你也可以在编辑器中留下你想标注的信息。

```
`# 正式提交变更到本地资料库 ``# 同时附上标注信息 “项目初始化”``git commit -m ``"项目初始化"`
```

输出：

```
`[master（根提交） ee4b843] 项目初始化`` ``Committer: root ``您的姓名和邮件地址基于登录名和主机名进行了自动设置。请检查它们正确``与否。您可以通过下面的命令对其进行明确地设置以免再出现本提示信息：` `  ``git config --global user.name ``"Your Name"``  ``git config --global user.email you@example.com` `设置完毕后，您可以用下面的命令来修正本次提交所使用的用户身份：` `  ``git commit --amend --reset-author` ` ``5 files changed, 4 insertions(+)`` ``create mode 100644 datafiles``/data``.txt`` ``create mode 100644 datafiles``/data2``.txt`` ``create mode 100644 test01`` ``create mode 100644 test02`` ``create mode 100644 test03`
```

好吧，这是一个小插曲。这个git是博主刚装的新版的，提示我添加名称和邮件了。当然，读者不要对此不以为然，当你一个人用git的时候这个可能不大重要，但是多人操作一个项目的时候名称标识可是很重要的，希望大家养成习惯配置好这些选项。

```
`git config --global user.name ``"Lellansin"``git config --global user.email lellansin@gmail.com``# 没加 “-m” vim自动弹出来了 ":q"直接离开 (哈哈,博主又偷懒了)``git commit --amend --reset-author``[master 2401c44] 项目初始化`` ``5 files changed, 4 insertions(+)`` ``create mode 100644 datafiles``/data``.txt`` ``create mode 100644 datafiles``/data2``.txt`` ``create mode 100644 test01`` ``create mode 100644 test02`` ``create mode 100644 test03`
```

### 查看你的 Git 库

> 操作日志
>
> 我们所做的所有操作都已建了一个 本地 Git 库保存在 .git文件夹中，其中还包括我们所正式提交到库中的的所有文件(夹)的快照。（注意只是本地的库，不一定与远程库同步）

```
`# 查看 Git 操作日志``git log``# 以下是具体日志内容``# 其中的 Author（作者）还是博主刚刚临时改的（笑``commit 2401c44005fa2d81190c5105cfd164e490c71633``Author: Lellansin ``Date:  Sun Apr 21 22:49:56 2013 +0800` `  ``项目初始化`
```

当日志比较长的时候（如果你有按着本例的做实验那么很可能马上就碰到），git log 查看日志时模式与vim有些类似，需要按“q”退出，上下箭头和翻页键可以翻页，通过“/string”和“?string”可以查找字符串“string”区别是一个向下、一个向上。

备注：如果一次都没有提交可能出现 “fatal: bad default revision ‘HEAD’” 这样的提示。

### 删除文件以及修改提交

如果你删除了一个文件，那么 “git add . ” 命令不会将该文件加入提交列表

你可以使用 git rm 命令来从你的工作目录中删除一个文件，并将这个删除操作添加到下一个提交列表中。

```
`# 创建一个文件``touch` `delete_try.txt``# 添加到提交列表 并且同时("&&"操作) 提交这个列表``git add . && git commit -m ``"添加个文件来删删看 =。= "` `# 可以翻下日志``git log` `# 使用 Git 的移除命令``git ``rm` `delete_try.txt` `# 提交这个移除操作``git commit -m ``"删掉了 delete_try.txt 文件"` `# 日志君你好``git log`
```

我们直接看最后的日志吧（日志君辛苦了）：

```
`commit d5a781496af0bfd5d856f7ea9bec452b83b184dd``Author: Lellansin ``Date:  Sun Apr 21 23:29:13 2013 +0800` `  ``删掉了 delete_try.txt 文件` `commit d48fbf6a662b403f89c0bfba7fd811b7e86c3437``Author: Lellansin ``Date:  Sun Apr 21 23:27:31 2013 +0800` `  ``添加个文件来删删看 =。=` `commit 2401c44005fa2d81190c5105cfd164e490c71633``Author: Lellansin ``Date:  Sun Apr 21 22:49:56 2013 +0800` `  ``项目初始化`
```

或者你可以在使用 git commit 命令来提交的时候（git add 也是可以的）通过 “-a” 或者 “-A” 选项刷，来确认临时提交列表中的删除（否则有删除是不能提交的哦）。

```
`# 新建一个文件并且提交到 Git库中的版本控制中``touch` `wait_delete.txt``git add . && git commit -m ``"又建了一个待删的文件"` `# 删除这个文件``rm` `wait_delete.txt` `# 尝试用平常的方法来提交 --> 不起作用的 ^_^~``git add . && git commit -m ``"让我提交吧"` `输出：` `# 位于分支 master``# 尚未暂存以备提交的变更：``#  （使用 "git add/rm ..." 更新要提交的内容）``#  （使用 "git checkout -- ..." 丢弃工作区的改动）``#``#    删除：   wait_delete.txt``#``修改尚未加入提交（使用 ``"git add"` `和/或 ``"git commit -a"``）` `# 通过使用 -a 选项来刷新提交列表``git commit -a -m ``"文件 wait_delete.txt 现在终于删掉了"` `# 或者 你可以通过 add 命令 来确认临时列表中被删除的文件：``# git add -A . ``# git commit -m "文件 wait_delete.txt 这样也可以删滴" `
```

### 从临时列表中删除文件删除文件

你可以使用 git reset [filename] 命令来从临时列表中删除一个原本通过git add 命令添加的文件。

```
`# 创建一个文件并添加到临时提交列表``touch` `unwantedstaged.txt``git add unwantedstaged.txt` `# 不是日志君哦，当前临时列表的状态请使用 git status 来查看``git status` `# 从临时列表中删除``git reset unwantedstaged.txt` `# 状态君你也好 （笑``git status` `# 那么，作为善后我们最好删掉这个文件``rm` `unwantedstaged.txt `
```

### 通过 git amend 修正提交

git –amend 命令可以让我们修改上一次提交的注释信息。

假设我们上一次提交的信息写错了字。那么这个命令可以通过 –amend 参数来修正。

```
`# 假设你做了一些修改，现在要提交了``touch` `bug.txt``git add bug.txt` `git commit -m ``"我的信息不小心写错了"`
```

我们最好应该在提交还未被别人所分享之前使用 git –amend 命令。因为 git –amend 命令创建一个新的 commit ID 而别人已却经有可能在我们之后做了更多的操作。这种情况下他们需要将所做的操作迁移到这个新的提交上。

## SSH版

1. Linux中安装git:`sudo apt-get install git`
2. `$ git config --global user.name "Your Name"$ git config --global user.email "email@example.com"`
   这里用github的账号名和邮箱
3. 生成SSH 并在github上设置
   终端里cd 进入.ssh文件夹`cd ~/.ssh`并`ssh-keygen -t rsa -C "email@example.com"`生成SSH密匙，保存在.ssh/id_rsa.pub文件中。把生成的密匙复制粘贴到github–>settings–>SSH and GPG keys–>new SSH key中，保存
   不进行这一步会出现：

```
The authenticity of host 'github.com (192.30.255.112)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,192.30.255.112' (RSA) to the list of known hosts.
Permission denied (publickey).
fatal: 无法读取远程仓库。
请确认您有正确的访问权限并且仓库存在。1234567
```

1. cd进入要建为仓库的文件夹，
   - `git init` ——初始化
   - `git add .`——添加所有文件进入仓库
   - `git commit -m "wrote a readme file"`——提交至仓库
2. 从本地添加至云端仓库
   - `git remote add origin git@github.com:××/××.git`——××/××是你的账号名/仓库名，云端仓库名一定要和本地仓库名相同
   - `git push origin master`——把本地master分支的最新修改推送至GitHub
     上一步可能出现报错如下

```
Warning: Permanently added the RSA host key for IP address '192.30.255.113' to the list of known hosts.
To github.com:61305/spiderWeb.git
 ! [rejected]        master -> master (fetch first)
error: 无法推送一些引用到 'git@github.com:61305/spiderWeb.git'
提示：更新被拒绝，因为远程仓库包含您本地尚不存在的提交。这通常是因为另外
提示：一个仓库已向该引用进行了推送。再次推送前，您可能需要先整合远程变更
提示：（如 'git pull ...'）。
提示：详见 'git push --help' 中的 'Note about fast-forwards' 小节。12345678
```

那么安装提示输入`git pull`，出现

```
warning: 没有共同的提交
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
展开对象中: 100% (3/3), 完成.
来自 github.com:61305/spiderWeb
 * [新分支]          master     -> origin/master
当前分支没有跟踪信息。
请指定您要合并哪一个分支。
详见 git-pull(1)。

    git pull <远程> <分支>

如果您想要为此分支创建跟踪信息，您可以执行：

    git branch --set-upstream-to=origin/<分支> master

1234567891011121314151617
```

接着执行`git pull git@github.com:××/××.git master`
若出现报错

```
 * branch            master     -> FETCH_HEAD
fatal: 拒绝合并无关的历史
123
```

就输入`git pull git@github.com:××/××.git master --allow-unrelated-histories`
成功则提示

```
 * branch            master     -> FETCH_HEAD
Merge made by the 'recursive' strategy.
 README.md | 2 ++
 1 file changed, 2 insertions(+)
 create mode 100644 README.md
123456
```

那么继续输入`git push -u origin master`
可以打开登录github发现你的项目已经同步上去了



## [从现有仓库克隆](https://git-scm.com/book/zh/v1/Git-基础-取得项目的-Git-仓库#从现有仓库克隆)

如果想对某个开源项目出一份力，可以先把该项目的 Git 仓库复制一份出来，这就需要用到 `git clone` 命令。如果你熟悉其他的 VCS 比如 Subversion，你可能已经注意到这里使用的是 `clone` 而不是 `checkout`。这是个非常重要的差别，Git 收取的是项目历史的所有数据（每一个文件的每一个版本），服务器上有的数据克隆之后本地也都有了。实际上，即便服务器的磁盘发生故障，用任何一个克隆出来的客户端都可以重建服务器上的仓库，回到当初克隆时的状态（虽然可能会丢失某些服务器端的挂钩设置，但所有版本的数据仍旧还在，有关细节请参考第四章）。

克隆仓库的命令格式为 `git clone [url]`。比如，要克隆 Ruby 语言的 Git 代码仓库 Grit，可以用下面的命令：

```
$ git clone git://github.com/schacon/grit.git
```

这会在当前目录下创建一个名为`grit`的目录，其中包含一个 `.git` 的目录，用于保存下载下来的所有版本记录，然后从中取出最新版本的文件拷贝。如果进入这个新建的 `grit` 目录，你会看到项目中的所有文件已经在里边了，准备好后续的开发和使用。如果希望在克隆的时候，自己定义要新建的项目目录名称，可以在上面的命令末尾指定新的名字：

```
$ git clone git://github.com/schacon/grit.git mygrit
```

唯一的差别就是，现在新建的目录成了 `mygrit`，其他的都和上边的一样。

Git 支持许多数据传输协议。之前的例子使用的是 `git://` 协议，不过你也可以用 `http(s)://` 或者 `user@server:/path.git` 表示的 SSH 传输协议。我们会在第四章详细介绍所有这些协议在服务器端该如何配置使用，以及各种方式之间的利弊。