# Git
## Notice
push上去的名字會是local目前使用的user.name跟user.email，不會是git server的帳號

## GitHub Quick setup
```
1. new project
$ echo "# project_name" >> README.md
$ git init
$ git add README.md
$ git commit -m "first commit"
$ git remote add origin https://github.com/xing312101/projectname.git
$ git push -u origin master

2. exist project
$ git remote add origin https://github.com/xing312101/projectname.git
$ git push -u origin master
```

## Git command remove credential
```
git config --unset-all credential.helper
git config --global --unset-all credential.helper
git config --system --unset-all credential.helper
```

## Config
```
git config --global --list
# 移除git user info on local
git config --global --unset-all user
```

## Rename branch
> ref : https://multiplestates.wordpress.com/2015/02/05/rename-a-local-and-remote-branch-in-git/

```
1. Rename your local branch.
git branch -m new-name
or
git branch -m old-name new-name

2. Delete the old-name remote branch and push the new-name local branch.
git push origin :old-name new-name

3. Reset the upstream branch for the new-name local branch.
git push origin -u new-name

```

## fork git
method 1. change remote
> https://help.github.com/en/articles/changing-a-remotes-url

```
git clone origin.git arcadenet-admin-tool
git remote -v
git remote set-url origin new_url.git
git remote -v
```
method 2. new git
```
1. git clone or copy directory
2. rm -rf .git
3. git init
```

## Commands
```
### git clone
$ git clone https://github.com/xing312101/projectname.git

### push code
# 將想要放進git的檔案加入到git
$ git add *
# 對此次想要push的code做註解，方便辨識此次修改的用意
$ git commit -am 'initial commit'
# 進行推code動作
$ git push -u origin master

### 從git更新code到local
$ git pull
$ git pull --rebase

### 確認目前local修改狀況或是否add
$ git status

### 未整理
git stash
git stash pop
git branch
git checkout
git checkout -b new_branch_name
git branch --delete
git reset
git reset HEAD^
git push --force
git tag
git tag name
git push origin tagname
git rebase

```
