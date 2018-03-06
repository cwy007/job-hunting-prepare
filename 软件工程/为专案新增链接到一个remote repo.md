# 查看专案的remote 链接
```
$ git remote -v
origin	git@github.com:cwy007/rails101.git (fetch)
origin	git@github.com:cwy007/rails101.git (push)
```

# 改变远端的 url
git remote set-url
接受两个参数：
1. 一个存在的remote name，例如：origin，或者 upstream
2. remote 的新的 url
* 使用https
`https://github.com/USERNAME/REPOSITORY.git`
* 使用ssh
`git@github.com:USERNAME/REPOSITORY.git`

完整的用法：
git remote set-url origin git@github.com:USERNAME/REPOSITORY.git

# 参考链接：
https://help.github.com/articles/changing-a-remote-s-url/


# git remote add

```shell
$ git remote add origin https://github.com/user/repo.git
# Set a new remote
$ git remote -v
# Verify new remote
origin  https://github.com/user/repo.git (fetch)
origin  https://github.com/user/repo.git (push)
```
