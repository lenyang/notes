#git仓库
##git命令：
### 一、 github添加、删除远程仓库
    git remote用于管理远程仓库
    git remote 不带参数时可以参看远程仓库名称
    git remote -v 可以查看远程仓库名称和网址
    git remote add  仓库名  仓库地址  添加远程仓库，同时设置远程仓库的名字，一般仓库名称是origin，当然你也可以写成其他的名字

### 二、 github添加、删除本地分支
    一个项目在本地的仓库可以有好几分支。分支是用于项目版本的管理，不同分支上的代码版本可以不同。
    git branch 用于管理分支
    git branch 可以查看本地仓库的分支情况（前面带星号的分支是你当前所处的分支）。
    git branch 分支名        创建分支
    git checkout 分支名      切换到特定分支
    以上两个命令可以合成一个命令 ：git  checkout -b 分支名 相当于创建分支后还切换到新创建的分支
    git branch -d 分支名   删除某个分支
    如果我们的现在工作在br分支下，所以不能删除该分支。所以必须先用 git checkout 分支名切换到其他分支后，才能删除br。
    git merge 分支名   合并某个分支到现在的所处的分支
    git remote rm  origin       删除名字为origin的远程仓库

### 三、 github添加、删除远程分支
    
    git branch -r 可以查看远程仓库的分支情况
    origin的远程仓库下有一个dev分支
    git branch -a 可以查看所以分支的情况，即本地分支和远程分支
    上面部分是本地分支，下面红色的部分是远程分支：remotes/
    远程分支的创建不能通过git branch 进行。而是在git  push的时候默认执行。
    所以，我们需要先了解一下git push的用法。
    git push <远程主机名>  <本地分支名>：<远程分支名>
    需注意的是，分支的推送顺序写法是<来源地>：<目的地>
    如果省略远程分支名则表示将本地分支推送到与之存在“追踪关系”的远程分支（通常两张同名），如果远程分支不存在，则会被新建。
    我们先查看远程仓库中的分支，只有一个dev
    远程仓库便多了一个名为des的分支
    远程分支的删除也不能用git branch，同样采用git push
    git push <远程主机名> --detete <删除分支名>
    或者：
    git push <远程主机名>   :<远程分支名>
    省略本地分支名相当于推送了一个空的本地分支到远程分支上，就相当于删除了远程分支
    当然，同删除本地分支一样，这时，我们也可能出现无法删除的情况
    现在，我的远程仓库有两个分支：
    这是因为在我们的远程仓库中master是默认分支，所以无法删除。所以我们需要将远程仓库中的默认分支改为另外的分支。当然，如果你现在的远程仓库中只有一个分支，则肯定是不能进行改变的，那我们可以先按照上述方法创建一个新的分支之后再更改。这里我有两个分支，所以无需更改。
    进入github的远程仓库，点击如下界面中的setting
    设置branch中的default branch，更改为master之外的分支，这里我设置的dev，然后点击一下update后确认。
    这样就把远程仓库的默认分支更改了
    然后我们再执行删除master分支的操作
    就成功了

###四、 git fetch、pull命令的用法
    
    这里我顺带记录一下git pull和fech两个命令的用法
    git fetch <远程仓库>
    这个命令用于取回远程仓库上的更新到本地仓库，默认是取回远程仓库上的所有更新，如果要取回指定分支上的内容，可以使用：
    git fetch <远程仓库> <分支名>
    这样取回的分支是不会影响本地仓库中的代码，通常用于查看他人进程。
    取回远程分支之后，可以在远程分支的基础上创建新的分支
    也可以将远程分支和本地分支合并：
    git merge origin/dev 或者 git rebase origin/dev
    表示将当前分支与远程分支合并
    git pull <远程主机名> <远程分支>：<本地分支>
    相当于将origin远程仓库中dev分支上的内容与本地master分支合并。
    如果远程分支是与当前分支合并，可以省略冒号后的内容
    相当于将origin远程仓库中dev分支上的内容与本地当前分支合并。


>注意 ：
1、git上传中文文件名问题，
2、git 使用gitigore屏蔽push上传文件问题 

###二、gitbook的使用

##三、git命令
    Git图形化界面我用的还可以，但是命令就不太会了，索性和大家一起学习下Git命令的用法...

    一般来说，日常使用只要记住下图6个命令，就可以了。但是熟练使用，恐怕要记住60～100个命令。
![GIT](image/git/git001.png)
    下面是我整理的常用 Git 命令清单。几个专用名词的译名如下。

            Workspace：工作区
            Index / Stage：暂存区
            Repository：仓库区（或本地仓库）
            Remote：远程仓库

    一、新建代码库


        # 在当前目录新建一个Git代码库
        $ git init

        # 新建一个目录，将其初始化为Git代码库
        $ git init [project-name]

        # 下载一个项目和它的整个代码历史
        $ git clone [url]

    二、配置

    Git的设置文件为.gitconfig，它可以在用户主目录下（全局配置），也可以在项目目录下（项目配置）。


        # 显示当前的Git配置
        $ git config --list

        # 编辑Git配置文件
        $ git config -e [--global]

        # 设置提交代码时的用户信息
        $ git config [--global] user.name "[name]"
        $ git config [--global] user.email "[email address]"

    三、增加/删除文件


        # 添加指定文件到暂存区
        $ git add [file1] [file2] ...

        # 添加指定目录到暂存区，包括子目录
        $ git add [dir]

        # 添加当前目录的所有文件到暂存区
        $ git add .

        # 添加每个变化前，都会要求确认
        # 对于同一个文件的多处变化，可以实现分次提交
        $ git add -p

        # 删除工作区文件，并且将这次删除放入暂存区
        $ git rm [file1] [file2] ...

        # 停止追踪指定文件，但该文件会保留在工作区
        $ git rm --cached [file]

        # 改名文件，并且将这个改名放入暂存区
        $ git mv [file-original] [file-renamed]

    四、代码提交


        # 提交暂存区到仓库区
        $ git commit -m [message]

        # 提交暂存区的指定文件到仓库区
        $ git commit [file1] [file2] ... -m [message]

        # 提交工作区自上次commit之后的变化，直接到仓库区
        $ git commit -a

        # 提交时显示所有diff信息
        $ git commit -v

        # 使用一次新的commit，替代上一次提交
        # 如果代码没有任何新变化，则用来改写上一次commit的提交信息
        $ git commit --amend -m [message]

        # 重做上一次commit，并包括指定文件的新变化
        $ git commit --amend [file1] [file2] ...

    五、分支


        # 列出所有本地分支
        $ git branch

        # 列出所有远程分支
        $ git branch -r

        # 列出所有本地分支和远程分支
        $ git branch -a

        # 新建一个分支，但依然停留在当前分支
        $ git branch [branch-name]

        # 新建一个分支，并切换到该分支
        $ git checkout -b [branch]

        # 新建一个分支，指向指定commit
        $ git branch [branch] [commit]

        # 新建一个分支，与指定的远程分支建立追踪关系
        $ git branch --track [branch] [remote-branch]

        # 切换到指定分支，并更新工作区
        $ git checkout [branch-name]

        # 切换到上一个分支
        $ git checkout -

        # 建立追踪关系，在现有分支与指定的远程分支之间
        $ git branch --set-upstream [branch] [remote-branch]

        # 合并指定分支到当前分支
        $ git merge [branch]

        # 选择一个commit，合并进当前分支
        $ git cherry-pick [commit]

        # 删除分支
        $ git branch -d [branch-name]

        # 删除远程分支
        $ git push origin --delete [branch-name]
        $ git branch -dr [remote/branch]

    六、标签


        # 列出所有tag
        $ git tag

        # 新建一个tag在当前commit
        $ git tag [tag]

        # 新建一个tag在指定commit
        $ git tag [tag] [commit]

        # 删除本地tag
        $ git tag -d [tag]

        # 删除远程tag
        $ git push origin :refs/tags/[tagName]

        # 查看tag信息
        $ git show [tag]

        # 提交指定tag
        $ git push [remote] [tag]

        # 提交所有tag
        $ git push [remote] --tags

        # 新建一个分支，指向某个tag
        $ git checkout -b [branch] [tag]

    七、查看信息


        # 显示有变更的文件
        $ git status

        # 显示当前分支的版本历史
        $ git log

        # 显示commit历史，以及每次commit发生变更的文件
        $ git log --stat

        # 搜索提交历史，根据关键词
        $ git log -S [keyword]

        # 显示某个commit之后的所有变动，每个commit占据一行
        $ git log [tag] HEAD --pretty=format:%s

        # 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
        $ git log [tag] HEAD --grep feature

        # 显示某个文件的版本历史，包括文件改名
        $ git log --follow [file]
        $ git whatchanged [file]

        # 显示指定文件相关的每一次diff
        $ git log -p [file]

        # 显示过去5次提交
        $ git log -5 --pretty --oneline

        # 显示所有提交过的用户，按提交次数排序
        $ git shortlog -sn

        # 显示指定文件是什么人在什么时间修改过
        $ git blame [file]

        # 显示暂存区和工作区的代码差异
        $ git diff

        # 显示暂存区和上一个commit的差异
        $ git diff --cached [file]

        # 显示工作区与当前分支最新commit之间的差异
        $ git diff HEAD

        # 显示两次提交之间的差异
        $ git diff [first-branch]...[second-branch]

        # 显示今天你写了多少行代码
        $ git diff --shortstat "@{0 day ago}"

        # 显示某次提交的元数据和内容变化
        $ git show [commit]

        # 显示某次提交发生变化的文件
        $ git show --name-only [commit]

        # 显示某次提交时，某个文件的内容
        $ git show [commit]:[filename]

        # 显示当前分支的最近几次提交
        $ git reflog

        # 从本地master拉取代码更新当前分支：branch 一般为master
        $ git rebase [branch]

    八、远程同步


        # 下载远程仓库的所有变动
        $ git fetch [remote]

        # 显示所有远程仓库
        $ git remote -v

        # 显示某个远程仓库的信息
        $ git remote show [remote]

        # 增加一个新的远程仓库，并命名
        $ git remote add [shortname] [url]

        # 取回远程仓库的变化，并与本地分支合并
        $ git pull [remote] [branch]

        # 上传本地指定分支到远程仓库
        $ git push [remote] [branch]

        # 强行推送当前分支到远程仓库，即使有冲突
        $ git push [remote] --force

        # 推送所有分支到远程仓库
        $ git push [remote] --all

    九、撤销

        # 恢复暂存区的指定文件到工作区
        $ git checkout [file]

        # 恢复某个commit的指定文件到暂存区和工作区
        $ git checkout [commit] [file]

        # 恢复暂存区的所有文件到工作区
        $ git checkout .

        # 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
        $ git reset [file]

        # 重置暂存区与工作区，与上一次commit保持一致
        $ git reset --hard

        # 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
        $ git reset [commit]

        # 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
        $ git reset --hard [commit]

        # 重置当前HEAD为指定commit，但保持暂存区和工作区不变
        $ git reset --keep [commit]

        # 新建一个commit，用来撤销指定commit
        # 后者的所有变化都将被前者抵消，并且应用到当前分支
        $ git revert [commit]

        # 暂时将未提交的变化移除，稍后再移入
        $ git stash
        $ git stash pop

    十、其他
        # 生成一个可供发布的压缩包
        $ git archive


