# 列举至少七个git指令，并简单说明他们的作用？

* git add
将此次变更的档案添加到缓冲区

* git commit
将已经加入缓冲区的档案提交到工作区

* git push
发送至远程仓库

* git fetch origin
每天于开发前执行 git fetch origin，获取当前所有分支的讯息

* git pull
从远程仓库更新本地端

* git checkout
切换分支

* git branch
针对分支进行操作（删除，重命名）
  * Specific git-branch actions:
  ```
  git branch -h

  eg: git branch -d branch-name
  or: git branch [<options>] [-r] (-d | -D) <branch-name>...
  or: git branch [<options>] (-m | -M) [<old-branch>] <new-branch>

  -d, --delete          delete fully merged branch
  -D                    delete branch (even if not merged)
  -m, --move            move/rename a branch and its reflog
  -M                    move/rename a branch, even if target exists
  ```
* git clone
克隆该专案所有的代码


# 共同遵守篇(主程 + 副程都得这么做)

## Step 1: 获取最新代码
每天于开发前执行 git fetch origin，获取当前所有分支的讯息
获取最新代码时，先 git checkout master ，然后 git pull origin master

## Step 2: 开发项目
现在你在master分支上，对代码进行任何改动之前，一定要切换到一个新的分支，在新分支上进行修改
分支命名规则 git checkout -b name-feature (姓名-功能)
记住一个原则，请勿直接在 master 开发并直接推送到 github ，容易出现双方代码不对齐的情况，并且会不断发生冲突，请详记!

## Step 3: 上传分支
上传之前，一定要在本地进行测试，确认没有bug才可以上传
git add .
git commit -m "这个分支做的功能"
git push origin name-feature
