1、开发新特性
```
# 开发 [升级器] 特性：
# 从 master 分支新建 feature/updater 分支，在此分支上开发 [升级器] 特性
$ git checkout master
$ git checkout -b feature/updater
$ git push --set-upstream origin feature/updater

# 开发 [同步器] 特性：
# 从 master 分支新建 feature/sync 分支，在此分支上开发 [同步器] 特性
$ git checkout master
$ git checkout -b feature/sync
$ git push --set-upstream origin feature/sync

# 开发过程中，如 master 有更新，则拉取 master 最新代码
$ git pull origin master
```

2、提测
```
# 从 master 分支新建 release/v1.0.1 分支，提测 feature/updater 和 feature/sync 两个特性
$ git checkout master
$ git checkout -b release/v1.0.1
$ git push --set-upstream origin release/v1.0.1

# 将 feature/updater 和 feature/sync 合并至 release/v1.0.1
$ git merge --no-ff feature/updater
$ git merge --no-ff feature/sync

# 提测过程中，如 master 有更新，则拉取 master 最新代码
$ git pull origin master
```

3、发布
```
# 测试完成，合并 release/v1.0.1 至 master
$ git checkout master
$ git merge --no-ff release/v1.0.1
$ git tag -a v1.0.1
$ git branch -d release/v1.0.1
```

4、修复线上 Bug
```
# 基于 master[v1.0.1] 创建 hotfix/PFWD-4340 分支
$ git checkout master
$ git checkout -b hotfix/PFWD-4340
$ git push --set-upstream origin hotfix/PFWD-4340

# 基于 master[v1.0.1] 创建 release/hotfix-PFWD-4340
$ git checkout master
$ git checkout -b release/hotfix-PFWD-4340
$ git push --set-upstream origin release/hotfix-PFWD-4340
# 合并 hotfix/PFWD-4340 至 release/hotfix-PFWD-4340
$ git checkout release/hotfix-PFWD-4340
$ git merget --no-ff hotfix/PFWD-4340
```


feature/updater
feature/sync

hotfix/PFWD-4340
