# Git的使用

## 创建版本库

### 创建根目录

```
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit
```

```
pwd：用于显示当前目录
```

![1705504440973](C:\Users\Lincoln\AppData\Roaming\Typora\typora-user-images\1705504440973.png)

### 创建仓库

```
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
```

### 添加文件

把文件添加到仓库:

```
$ git add readme.txt
```

```
$ git commit -m "wrote a readme file"
[master (root-commit) eaadf4e] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```

```
git commit:把文件提交到仓库
```

当然可以同时提交多份文件，即：

```
$ git add file2.txt file3.txt
```

![1705504469283](C:\Users\Lincoln\AppData\Roaming\Typora\typora-user-images\1705504469283.png)

## 时光机穿梭

### 版本回退

```
git status：掌握仓库当前的状态
```

```
git diff：查看修改的部分
```

```
git log：显示从最近到最远的提交日志
```

```
git reset:将当前版本回退到上个版本
```

```
$ git reset --hard + commit后的几位
```

### 工作区和暂存区

把文件往Git版本库添加：

```
git add：把文件修改添加到暂存区
```

```
git commit：把暂存区的所有内容提交到当前分支
```

当修改一个文件或添加一个文件时需要重新git add，此时文件就从暂存区提交到分支

### 管理修改

必须先git add后才能git commit，这样文件才能提交成功

### 撤销修改

```
git checkout -- readme.txt：把文件readme.txt撤销
```

```
注：--很重要！
```

```
git reset HEAD <file>：可以把暂存区的修改撤销掉，重新放回工作区
```

三种情况：

1.文件只在工作区未进行add

使用

```
git restore <file>
```

使工作区文件回退

2.文件已加add但未使用commit

使用

```
git reset HEAD <file>
```

把暂存区的修改撤销掉（unstage），重新放回工作区

注git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用`HEAD`时，表示最新的版本。

3.已经提交了不合适的修改到版本库

没有推送到远程库的前提下，版本回退

### 删除文件

删除：

```
rm 文件名
```

此时工作区与版本库不一致

1.文件从版本库中删除

用命令`git rm`删掉，并且`git commit`

2.删错了，把误删的文件恢复到最新版本

```
git checkout -- ：用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”
```

## 远程仓库

先创建SSH KEY：

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

`id_rsa`是私钥，不能泄露出去

`id_rsa.pub`是公钥，可以放心地告诉任何人

![1705673422434](C:\Users\Lincoln\AppData\Roaming\Typora\typora-user-images\1705673422434.png)

### 添加远程库

在本地的learngit仓库下运行

```
$ git remote add origin git@github.com:自己名字/learngit.git
```

远程库的名字是origin

注：可用

```
$ ssh -T git@github.com
```

检查是否成功连接上Github

首次推送时使用

```
$ git push -u origin master
```

此后使用

```
$ git push origin master
```

可以先用

```
$ git remote -v
```

检查远程库信息

然后使用

```
$ git remote rm origin
```

删除远程库与本地的绑定关系

### 从远程库克隆

使用

```
$ git clone git@github.com:自己名字/gitskills.git
```

克隆本地库

## 分支管理

### 创建与合并分支

创建并切换到分支：

```
$ git checkout -b dev
```

```
-b：创建并切换
```

相当于：

```
$ git branch dev
$ git checkout dev
```

查看当前分支：

```
$ git branch
```

当前分支前面会标一个`*`号

把dev分支的工作成果合并到master上：

```
$ git merge dev
```

删除`dev`分支：

```
$ git branch -d dev
```

查看`branch`：

```
$ git branch
```

当然，用`switch`更科学：

```
$ git switch -c dev
```

```
$ git switch master
```

![1705742678655](C:\Users\Lincoln\AppData\Roaming\Typora\typora-user-images\1705742678655.png)

### 解决冲突

在准备新分支开发时各分支分别有新的提交，git无法执行快速合并，这种合并可能会有冲突：

```
$ git merge feature1
```

这时候需要手动解决冲突后再提交

也可以用git log看到分支的合并情况：

![1705754430489](C:\Users\Lincoln\AppData\Roaming\Typora\typora-user-images\1705754430489.png)

### 分支管理策略

在`Fast forward`模式下，删除分支后，会丢掉分支信息。合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。

注：

```
git log
```

可用q键退出

### BUG分支

修bug时先创建bug分支，然后进行修复，然后合并，最后删除

当工作到一半时使用

```
$ git stash
```

储藏当前的工作现场，等以后恢复现场在工作

```
git stash list：查看刚才的工作现场
```

恢复有两种方法：

1.用`git stash apply`恢复，但是恢复后，stash内容并不删除，需要用`git stash drop`来删除

2.用`git stash pop`，恢复的同时把stash内容也删了

可以用`cherry-pick`命令复制一个特定的提交到当前分支

例如：

```
$ git cherry-pick 4c805e2
```

### Feature分支

当开发新feature分支时，如果要丢弃一个还没有合并过的分支，可以通过`git branch -D <name>`强行删除

### 多人协作

用git remote或者git remote -v查看远程库的信息（后者更详细）

推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上，如果要推送其他分支，就从

```
$ git push origin master
```

改成

```git
$ git push origin dev
```

抓取分支时，可以：

```
$ git clone git@github.com:michaelliao/learngit.git
```

默认情况下只能看到本地的master

如果要在dev分支上开发，就必须创建远程origin的dev到本地：

```
$ git checkout -b dev origin/dev
```

这样就能在dev上修改并push到远程

如果和其他人的推送冲突，先用`git pull`把最新的提交从`origin/dev`抓下来，然后，在本地合并，解决冲突，再推送：

```
$ git pull
```

如果失败，是因为没有指定本地`dev`分支与远程`origin/dev`分支的链接，根据提示，设置`dev`和`origin/dev`的链接：

```
$ git branch --set-upstream-to=origin/dev dev
```

再pull，这次pull成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的[解决冲突](http://www.liaoxuefeng.com/wiki/896043488029600/900004111093344)完全一样。解决后，提交，再push：

```
$ git commit -m "fix env conflict"
```

```
$ git push origin dev
```

### Rebase

```
git rebase:把分叉的提交历史“整理”成一条直线，看上去更直观。缺点是本地的分叉提交已经被修改过了。
```

## 标签管理

### 创建标签

1.先切换到需要打标签的分支上

2.`git tag <name>`就可以打一个新标签

3.可以用命令`git tag`查看所有标签

默认标签是打在最新提交的commit上的

当以往的commit忘记打标签时，找到历史提交的commit id，然后打上

```
$ git log --pretty=oneline --abbrev-commit
```

```
$ git tag <name> + 对应的commit id
```

注：标签不是按时间顺序列出，而是按字母排序的。

可以用`git show <tagname>`查看标签信息

还可以创建带有说明的标签，用`-a`指定标签名，`-m`指定说明文字

例：

```
$ git tag -a v0.1 -m "version 0.1 released" 1094adb
```

```
git show <tagname>：看说明文字
```

### 操作标签

如果标签打错了，可以用

```
$ git tag -d <name>
```

删除

```
git push origin <tagname>：推送某个标签到远程
```

```
git push origin --tags：一次性推送全部尚未推送到远程的本地标签
```

如果标签已经推送到远程，先从本地删除：

```
$ git tag -d <name>
```

然后，从远程删除。删除命令也是push，但是格式如下：

```
$ git push origin :refs/tags/<name>
```

## 自定义Git

### 忽略特殊文件

忽略文件的原则是：

1. 忽略操作系统自动生成的文件，比如缩略图等；

2. 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的`.class`文件；

3. 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

   在文本编辑器里“保存”或者“另存为”就可以把文件保存为`.gitignore`

当添加文件到Git添加不了，原因是这个文件被`.gitignore`忽略了：

想添加该文件可以用`-f`强制添加到Git：

```
$ git add -f 文件名
```

或者`.gitignore`写得有问题，需要找出来到底哪个规则写错了，可以用`git check-ignore`命令检查：

```
$ git check-ignore -v 文件名
```

有时`.*`这个规则把`.gitignore`也排除了，并且`文件`需要被添加到版本库，但是被`*.class`规则排除了，希望不要破坏`.gitignore`规则，可以添加两条例外规则：

```
# 排除所有.开头的隐藏文件:
.*
# 排除所有.class文件:
*.class

# 不排除.gitignore和文件:
!.gitignore
!文件
```

格式：`!`+文件名

### 配置别名

```
$ git config --global alias.st status
```

`--global`参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用。

配置Git的时候，加上`--global`是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用，每个仓库的Git配置文件都放在`.git/config`文件中：

```
$ cat .git/config 
```

别名就在`[alias]`后面，要删除别名，直接把对应的行删掉即可。

如果改错了，可以删掉文件重新通过命令配置。

### 使用SourceTree

