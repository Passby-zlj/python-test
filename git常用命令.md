# git常用语法

![mmexport1519288114550](https://i.loli.net/2019/05/26/5cea7a37e528562269.jpg)

## 1. 基本操作

* git init 初始化
* git add "filename" 添加文件
* git commit -m "explain"  提交文件
* git status 查看当前状态
* git diff 查看差异
* git log 查看历史记录
* git log --pretty=oneline 单行查看历史记录
* git reset --hard HEAD^ 回退到上一版本
* git reflog 记录输入的所有命令
* git checkout -- "filename" 回退到最近一次git commit 或git add 的状态
* git reset HEAD "filename" 把暂存区的修改撤销掉
* git rm 删除版本库中的文件

>场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
>场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD  "filename"，就回到了场景1，第二步按场景1操作。
>场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

## 2. 关联远程库

* git remote add origin git@server-name:path/   repo-name.git 关联一个远程库
* git push -u origin master 第一次推送master分支的所有内容；
* git push origin master 推送此后的最新修改

>要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。
>Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。

## 3. 管理分支

* git branch 查看分支
* git checkout -b "name" 创建+切换分支
  1. 创建分支git branch "name"
  2. 切换分支：git checkout "name"
* git merge "name" 合并某分支到当前分支
* git branch -d "name"  删除分支
* git branch -D "name" 强行删除分支

>1. 合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。
>2. 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
>3. 当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。
>4. 开发一个新feature，最好新建一个分支

## 4. 多人合作

* git remote -v 查看远程库信息
* git push origin branch-name从本地推送分支
* git checkout -b branch-name origin/branch-name 在本地创建和远程分支对应的分支，使用本地和远程分支的名称最好一致
* git branch --set-upstream branch-name origin/branch-name 建立本地分支和远程分支的关联
* git pull从远程抓取分支

>因此，多人协作的工作模式通常是这样：
>
>1. git push origin "branch-name"推送自己的修改；
>2. 如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
>3. 如果合并有冲突，则解决冲突，并在本地提交；
>4. 没有冲突或者解决掉冲突后，再用git push origin "branch-name"推送就能成功！
>5. 如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to "branch-name" origin/"branch-name"。

## 5. 标签管理

* git tag "tagname"用于新建一个标签，默认为HEAD，也可以指定一个commit id；
* git tag -a "tagname" -m "blablabla..."可以指定标签信息；
* git tag可以查看所有标签。
* git push origin "tagname"可以推送一个本地标签；
* git push origin --tags可以推送全部未推送过的本地标签；
* git tag -d "tagname"可以删除一个本地标签；
* git push origin :refs/tags/"tagname"可以删除一个远程标签。
