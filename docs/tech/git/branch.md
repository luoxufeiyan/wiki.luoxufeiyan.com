# Branch 分支

创建分支： `git branch <name>`

切换分支： `git checkout <name>` 。切换分支后，Git 会将工作目录改动到当前的分支上。

创建分支并立刻切换到这个分支： `git checkout -b <name>`

删除分支： `git branch -d <name>` 。如果分支没有被合并，Git 默认会给出确认提示。

### 删除远程分支

```shell
$ git push <remote_name> --delete <branch_name>
```

例如： `git push origin --delete test`

或者更简便的：

```shell
$ git push <remote_name> :<branch_name>
```

例如： `git push origin :test`

ref: [version control - How do I delete a Git branch locally and remotely? - Stack Overflow](https://stackoverflow.com/a/2003515)

## 分支重命名

本地分支重命名：

```shell
git branch -m old-name new-name
```

删除旧远程分支，推送新本地分支：

```shell
git push origin :old-name new-name
```

设置 upstream 为新分支：

```shell
git push origin -u new-name
```

⚠️ 舍弃本地修改，从远程拉取。

```shell
git reset --hard origin/master
git pull origin master
```

ref:[Rename a local and remote branch in git](https://multiplestates.wordpress.com/2015/02/05/rename-a-local-and-remote-branch-in-git/)


## change url for git remote

```shell
git remote -v
# View existing remotes
# origin  https://my.old.repo.com/user/repo.git (fetch)
# origin  https://my.old.repo.com/user/repo.git (push)

git remote set-url origin https://new.com/user/repo.git
# Change the 'origin' remote's URL

git remote -v
# Verify new remote URL
# origin  https://new.com/user/repo.git (fetch)
# origin  https://new.com/user/repo.git (push)
```