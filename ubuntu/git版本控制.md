# git做版本控制

在不同服务器中跑代码，需要对代码做版本控制，上传到远程服务器



## 在github新建repository

**在网页中新建对应的库**

- 得到云端仓库的地址“git@xxxxx.git”

**新服务器要上传公钥到github上**

- ssh-keygen生成密钥
- 复制内容到github上

**配置用户信息**

```bash
git config --global user.name "Collebt"
git config --global user.email "1054541662@qq.com"
```

**与远程仓库建立连接**

```bash
git remote -n name git@xxxx.git
git remote add name git@xxxx.git #create
git remote add master git@github.com:Collebt/code_aux_my.git #my example
```



## vscode中建立本地库

```bash
git init
```

commit后上传到本地库

点击左下角的上传

## 提交版本

```bash
git commit -a -m "add file"
```



## 版本的发布和更新

发布版本

```
git clone git@xxx.git #从服务器克隆一个库并上传
```



## 云端仓库的管理

```bash
git remote show #显示仓库名称
git remote add xxx #增加仓库xxx
git remote remove xxx #删除仓库xxx
```



## branch 管理

```bash
git branch #显示现有分支
git branch xxx #创建新分支，不会进入分支
git checkout xxx #移动到对应分支
git branch -d xxx #删除分支
```

对其他分支的更改不会改变主分支，要想把更改提交到主分支，需要切换回主分支，然后使用合并

```bash
git checkout main
git merge test
```





## add git ignore

To untrack a *single* file, ie stop tracking the file but not delete it from the system use:

```
git rm --cached filename
```

To untrack *every* file in `.gitignore`:

First ***\*commit\**** any outstanding code changes, and then run:

```
git rm -r --cached .
```

This removes any changed files from the index(staging area), then run:

```
git add .
```

Commit it:

```
git commit -m ".gitignore is now working"
```

To undo `git rm --cached filename`, use `git add filename`
