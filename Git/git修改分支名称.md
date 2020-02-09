# git修改分支名称

 `git branch -a` #查看所有分支
`git branch -r` #查看远程分支
`git branch -vv` #查看本地分支所关联的远程分支 

假设分支名称为oldName
 想要修改为 newName

**1. 本地分支重命名(还没有推送到远程)**

```shell
git branch -m oldName newName
```

**2. 远程分支重命名 (已经推送远程-假设本地分支和远程对应分支名称相同)**

- a. 重命名远程分支对应的本地分支

```shell
git branch -m oldName newName
```

- b. 删除远程分支

```shell
git push --delete origin oldName
```

- c. 上传新命名的本地分支

```shell
git push origin newName
```

- d.把修改后的本地分支与远程分支关联

```shell
git branch --set-upstream-to origin/newName
```

