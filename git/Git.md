### Git安装

配置名字与email

`git config --global user.name "NAME"`

`git config --global user.email "EMAIL"`

### 创建版本库

#### 初始化Git仓库

`git init`

#### 添加文件到Git仓库

` git add <file> `  添加文件至暂存区

` git commit -m <message> `  提交文件至仓库

` git status  `  查看工作区状态

` git diff `  查看文件修改内容

跟踪文本文件的改动，二进制文件无法跟踪文件变化，注意word文件

### 时光穿梭机

#### 版本回退

` git log `   查看历史提交

` git reflog `    查看命令历史

`git reset --hard commit_id ` 版本穿梭

`HEAD`表示当前版本，`HEAD^`表示上一个版本

Git版本回退只是把指向HEAD的指针指向别的版本，并更新工作区的文件

#### 工作区和暂存区

##### 工作区

在电脑里能看见的目录

##### 版本库

工作区中的`.git`目录

暂存区(stage)在版本库中 

![git-repo](.\image\stage.jpg)

#### 撤销修改

##### 工作区撤销修改

`git checkout -- <file>`

##### 暂存区撤销修改

`git reset Head <file>`

#### 删除文件

`git rm <file>`

### 远程仓库

#### 配置

1. 创建SSH Key   `ssh-keygen`
2. 登录GitHub - Account Settings - Add SSH Key

用于识别是谁推送的提交

#### 添加远程仓库

`git remote add origin git@server-name:path/repo-name.git`  关联远程仓库

`git push -u origin master`   第一次推送master分支内容

`git push -u origin master`  推送分支

#### 从远程仓库克隆

`git clone` 

Git支持多种协议，包括https，但ssh协议速度最快

### 分支管理

#### 创建与合并分支

|                                |                                                              |
| ------------------------------ | ------------------------------------------------------------ |
| ![branch](.\image\marster.png) | Git用`master`指向最新的提交，再用`HEAD`指向`master`，每次提交，`master`分支都会向前移动一步 |
| ![branch](.\image\dev1.png)    | 创建新的分支，例如`dev`时，Git新建了一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev` |
| ![branch](.\image\dev2.png)    | 针对`dev`分支对工作区的修改和提交，比如新提交一次后，`dev`指针往前移动一步，而`master`指针不变 |
| ![branch](.\image\merge.png)   | 完成dev`上的工作后把`dev`合并到`master`上，直接把`master`指向`dev`的当前提交 |
| ![branch](.\image\delete.png)  | 合并完分支后，可以删除`dev`分支，即把`dev`指针给删掉         |

查看分支：`git branch`     在当前分支前会标*号

创建分支：`git branch <name>`

切换分支：`git checkout <name>`或者`git switch <name>`

创建+切换分支：`git checkout -b <name>`或者`git switch -c <name>`

合并某分支到当前分支：`git merge <name>`

删除分支：`git branch -d <name>`

#### 解决冲突

Git无法自动合并分支时，必须首先解决冲突

`git log --graph`  查看分支合并图

#### 分支管理策略

`master`分支仅用来发布新版本，`dev`分支用来工作

`git merge`时采用`Fast forward`模式，这种模式下删除分支会丢掉分支信息

`--no-off`方式禁用`Fast forward`合并分支会提交一个新的`commit`

`git merge --no-off -m 'message'`

#### bug分支

修复bug时会创建新的bug分支进行修复，然后合并，删除分支

`git stash` 存储工作区

`git stash list` 查看stash的内容

`git stash apply` 恢复工作区内容，但不删除stash内容

`git stash pop` 恢复工作区内容，并删除stash内容

`git stash drop` 删除stash内容

`git cherry-pick <commit_id>` 复制提交至当前分支，并自动提交

#### Feature分支

`git branch -D <name>` 丢弃没有合并过的分支

#### 多人协作

`git remote` 查看远程仓库信息，远程仓库默认名称origin

`git pull`抓取远程分支，合并解决冲突

`git push` 推送分支

`git checkout -b branch-name origin/branch-name`  在本地创建和远程分支对应得分支

`git branch --set-upstream branch-name origin/branch-name` 建立本地分支和远程分支的关联

#### rebase

`git rebase` 把本地未push的分叉提交历史整理成直线

### 标签管理

#### 创建标签

标签：版本库的快照，指向某个commit的指针

`git tag -a <name> -m 'message'`创建新标签，默认打在最新提交的commit上

`git tag <name> commit_id` 在指定commit上打标签

`git tag` 查看所有标签

`git show <tagname>` 查看标签信息

#### 操作标签

`git tag -d <tagname>` 删除本地标签

`git push origin <tagname>` `git push origin --tags` 推送本地标签

`git push origin :refs/tags/<tagname` 删除远程标签

