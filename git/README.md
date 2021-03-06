### 让你们clone laravel更快（by [overtrue](https://github.com/overtrue) ）
我们通常在克隆github上的项目时做法如下：

```git
git clone git@github.com:laravel/laravel.git
```

你会发现各种慢（如果该项目历史比较悠久，也就是说有很多commits），那么其实你clone的时候是把历史也拉下来。

可是我们需要这些东西吗？不需要，那么就加一个选项吧：

```git
git clone git@github.com:laravel/laravel.git --depth=1
```

--depth=1 是指只拉取最后一次的提交结果。

----

### 设置全局代理（来自网络）

```git
git config --global https.proxy https://user:password@address:port 
```

### clone某个特定分支

```git
mkdir $BRANCH 
cd $BRANCH 
git init 
git remote add -t $BRANCH -f origin $REMOTE_REPO 
git checkout $BRANCH 
```

### 比较某个文件和远程分支上的区别

```git
git diff localbranch remotebranch filepath 
```

### 在版本库所有版本中搜寻一条字符串

```git
git rev-list --all | ( 
    while read revision; do 
        git grep -F 'Your search string' $revision 
    done 
) 
```

### 向分支提交一个初始的空commit，保证完全复位

```git
1.创建一个新的空分支，例如：newroot

git checkout --orphan newroot 
git rm --cached -r . 
git clean -f -d 
2.创建空的commit

git commit --allow-empty -m '[empty] initial commit' 
3.重新发送分支的全部内容

git rebase --onto newroot --root master 
4.删除临时分支newroot

git branch -d newroot 
现在master就已经包含了一个空的root commit了。
```

### 如何修改一个特定的commit

```git
当你想在推送前重做你最后的commit时，可以使用修改命令（git commit --amend）。如果你想修改的不是最后一个commit呢？

这种情况下，你可以使用git rebase，例如，你想要修改bbc643cd commit，运行下面的命令：

$git rebase bbc643cd^ --interactive  
在默认的编辑器中选择并修改你期望修改的，然后保存修改并输入：

$ git add 
<
filepattern
>
  
现在你就可以使用

$git commit --amend 
来修改commit，之后使用

$ git rebase --continue  
返回之前最新的commit。
```
