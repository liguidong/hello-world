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



#### 远程仓库协作

1.创建 SSH Key（将地址换为自己的邮箱地址一路回车）

```Git
$ ssh-keygen -t rsa -C "youremail@gmail.com"
```

2.GitHub中或者Gitlab中添加个人公钥（user/.ssh/.pub）

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