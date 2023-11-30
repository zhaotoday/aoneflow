1、开发新特性
```
# 从 master（主干分支）新建 feature/updater（升级特性分支）
$ git checkout master
$ git checkout -b feature/updater
$ git push --set-upstream origin feature/updater

# 从 master（主干分支）新建 feature/sync（同步器特性分支）
$ git checkout master
$ git checkout -b feature/sync
$ git push --set-upstream origin feature/sync

$ git pull origin master

```
2、提测
```
# 创建发布分支，提测 feature/updater 和 feature/sync 两个特性
# 合并过程中若与当前发布分支其他特性存在较大冲突，需与相关开发配合解决冲突
$ git checkout master
$ git checkout -b release/v1.0.1
$ git push --set-upstream origin release/v1.0.1

# 将 feature/updater 和 feature/sync 合并至 release/v1.0.1
$ git merge --no-ff feature/updater
$ git merge --no-ff feature/sync

# 提测过程中发现主干分支存在更新，同步最新 master 至 release/v1.0.1
# 合并中若存在较大冲突需与相关开发配合解决冲突
$ git pull origin master
```

3、发布
```
# 合并 release/v1.0.1 至 master
$ git checkout master
$ git merge --no-ff release/v1.0.1
$ git tag -a v1.0.1
$ git branch -d release/v1.0.1
```

4、修复线上 Bug
```
# 基于 master[v1.0.1] 创建 hotfox/v1.0.1
$ git checkout master
$ git checkout -b hotfix/v1.0.1
$ git push --set-upstream origin hotfix/v1.0.1

# 基于 master[v1.0.1] 创建 release/hotfix-v1.0.1
$ git checkout master
$ git checkout -b release/hotfix-v1.0.1
$ git push --set-upstream origin release/hotfix-v1.0.1
```


feature/updater
feature/sync

hotfix/PFWD-4340
