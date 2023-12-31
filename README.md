#### 分支
AoneFlow 只使用三种分支类型：主干分支（master）、特性分支（如：feature/updater）、发布分支（release/v1.0.0），以及三条基本规则。

#### 基本规则
- 1、开始工作前，从主干创建特性分支；
- 2、通过合并特性分支，形成发布分支；
- 3、发布到线上正式环境后，合并相应的发布分支到主干，在主干添加标签，同时删除该发布分支关联的特性分支。

#### 命令
1、开发新特性
```
# 开发 [升级器] 特性：
# 基于 master 分支新建 feature/updater 分支，在此分支上开发 [升级器] 特性
$ git checkout master
$ git checkout -b feature/updater
$ git push --set-upstream origin feature/updater

# 开发 [同步器] 特性：
# 基于 master 分支新建 feature/sync 分支，在此分支上开发 [同步器] 特性
$ git checkout master
$ git checkout -b feature/sync
$ git push --set-upstream origin feature/sync

# 开发过程中，如 master 有更新，则拉取 master 最新代码
$ git pull origin master
```

2、提测
```
# 基于 master 分支新建 release/v1.0.1 分支，提测 feature/updater 和 feature/sync 两个特性
$ git checkout master
$ git checkout -b release/v1.0.1
$ git push --set-upstream origin release/v1.0.1

# 测试过程中，在 feature 分支上修复 Bug，并更新到 release 分支
$ git checkout release/v1.0.1
$ git pull origin feature/updater
$ git pull origin feature/sync

# 将 feature/updater 和 feature/sync 合并至 release/v1.0.1，可能需要处理两个特性分支的代码冲突
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
$ git branch -d feature/updater
$ git branch -d feature/sync
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
