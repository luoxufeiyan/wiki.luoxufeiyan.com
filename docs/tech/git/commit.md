# Commit 提交

## empty commit 空提交

创建空提交，在需要触发一些 CI 条件的时候比较有用。

```shell
git commit --allow-empty -m "Trigger Build"
```

## Co-author 合著提交

在通过 commit 进行提交时，在添加 commit message 时，可以通过 `Co-authored-by` 来添加合著人。

在编写提交信息时，先不闭合引号，先添加两个空行，然后输入 `Co-authored-by: name <name@example.com>`，然后输入合著人的信息，在合著人消息之后，再闭合引号。

有多个合著人时，保持一行一个合著人。

例如：

```shell
$ git commit -m "Refactor usability tests.
>
>
Co-authored-by: lxfy <hi@luoxufeiyan.com>
Co-authored-by: name <name@example.com>"
```

## Change the author of a commit 改变某次提交的作者

修改某一次 git 提交时候的作者信息，在帮别人提交代码的时候会很有用。

```shell
git commit --author="LXFY <admin@luoxufeiyan.com>"
```

或者 使用 amend 参数，改变前一次提交的作者信息。

```shell
git commit --amend --author="LXFY <admin@luoxufeiyan.com>"
```
