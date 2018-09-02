## Git 学习笔记

#### 本地仓库操作

创建并切换分支,-b（例命名为dev）

```git
git checkout -b dev
/*
其等同于
git branch dev
git checkout dev
*/
```

查看当前分支

```git
git branch
```

合并分支（合并dev到当前分支）

```git
git merge dev
```

删除分支

```
git branch -d dev
```

查看远程仓库地址

```git
git remote -v
```

撤销修改(回到暂存区的状态)

```git
git checkout -- readme.txt
```

#### 远程仓库协作

1.创建 SSH Key（将地址换为自己的邮箱地址一路回车）

```Git
$ ssh-keygen -t rsa -C "youremail@gmail.com"
```

2.GitHub中或者Gitlab中添加个人公钥（user/.ssh/.pub）

> clone -b branchName url 可克隆对应分支
>
> clone 线上库master后，可先`git branch -a`查看线上分支，`git checkout -b dev origin/dev`来新建并关联线上分支

3.线上仓库与本地库关联（origin为为远程库的命名，michaelliao替换为线上平台账户名，projectname替换线上项目名）

```Git
$ git remote add origin git@github.com:michaelliao/projectname.git
```

> ps：如提示 `fatal: remote origin already exists.`,可 `$ git remote rm origin` 后再次关联。
>
> 如提示`fatal: refusing to merge unrelated histories`，需git pull之后再push，
>
> `git pull origin master --allow-unrelated-histories`

4.本地内容推送远程库

```Git
$ git push -u origin master
```

意为推送到origin的master分支





#### 解决冲突流程

1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！

如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。