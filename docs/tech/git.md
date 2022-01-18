
# Git


## SSH 连接 Git

1. 启用身份验证

	```
	ssh-agent bash
	```
2. 添加密钥

  * 仅限当前会话：
		`ssh-add ~/.ssh/id_key`
		
  * 持久化：（保存到ssh的配置文件中）

		编辑`vim ~/.ssh/config`文件，添加以下：

```
Host github.com
    User git
    IdentityFile ~/.ssh/GitHub/GitHub_id_rsa
```

* 测试

```
ssh -T git@github.com
```
		

## 添加远程仓库

```
git remote -v 
git remote remove origin 
git remote add origin git@github.com:user/repo.git  
```


## 分支重命名

本地分支重命名：
```
git branch -m old-name new-name
```

删除旧远程分支，推送新本地分支：
```
git push origin :old-name new-name
```

设置upstream为新分支：
```
git push origin -u new-name
```

⚠️舍弃本地修改，从远程拉取。
```
git reset --hard origin/master
git pull origin master
```

ref:[Rename a local and remote branch in git](https://multiplestates.wordpress.com/2015/02/05/rename-a-local-and-remote-branch-in-git/)


### Cherry pick 从某一分支拉取特定的commit文件

合并所有commit可以用`git merge`，当只需要特定的commit时，可以用`cherry pick`。

用法：
```shell
git cherry-pick <commitHash>
```

### empty commit

创建空提交。

```shell
git commit --allow-empty -m "Trigger Build"
```

### 撤销远程修改

即便commit已经推送到远程，依然可以用revert的方法将远程的提交删除。

## 快捷键

[[https://gist.github.com/hutusi/e4f32e2bcd8d53ec86de8254ab0d5127|Git paging]]

## git 常用编写

* feat: 添加新特性、新功能（ feature ）
* fix: 修复 bug
* docs: 仅仅修改了文档
* style: 仅仅修改了空格、格式缩进、逗号等等，不改变代码逻辑
* refactor: 代码重构，没有加新功能或者修复 bug
* perf: 增加代码进行性能测试
* test: 增加测试用例
* chore: 改变构建流程、或者增加依赖库、工具等