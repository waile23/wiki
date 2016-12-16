#git速查表


Git内都只有三种状态：已修改（modified），已暂存（staged）和已提交（committed）。已修改表示修改了某个文件，但还没有提交保存；已暂存表示把已修改的文件放在下次提交时要保存的清单中；已提交表示该文件已经被安全地保存在本地数据库中了。

对应三个工作区域：Git 的工作目录，暂存区域，以及本地仓库。

所谓的暂存区域只不过是个简单的文件，一般都放在 Git 目录中。有时候人们会把这个文件叫做索引文件，不过标准说法还是叫暂存区域。	

基本的 Git 工作流程如下：
1. 在工作目录中修改某些文件。
1. 对修改后的文件进行快照，然后保存到暂存区域。
1. 提交更新，将保存在暂存区域的文件快照永久转储到 Git 目录中。

我们可以从文件所处的位置来判断状态：如果是Git目录中保存着的特定版本文件，就属于已提交状态；如果作了修改并已放入暂存区域，就属于已暂存状态；如果自上次取出后，作了修改但还没有放到暂存区域，就是已修改状态。

``` bash
#设置全局的用户名及邮箱
$ git config --global user.name waile23
$ git config --global user.email waile23@163.com

#创建版本库
$ git clone <url> #克隆远程版本库
$ git init #初始化本地版本库

#修改和提交
$ git status #查看状态
$ git diff #查看变更内容
$ git add . #将所有已修改的文件保存到暂存区，文件变为已暂存
$ git add <file> #将指定的已修改的文件保存到暂存区，文件变为已暂存 
$ git add -u #将所有已经修改的文件保存到暂存区，文件变为已暂存
$ git commit -m “commit message” #提交已暂存文件
$ git commit --amend #修改最后一次提交
$ git rm <file> #取消git对文件的版本控制.
$ git rm --cached <file> #取消git对文件的版本控制，-–cached选项允许你把文件保留在你的工作目录中.（常用）
$ git mv <old> <new> #重命名文件（先删除旧文件，再添加新文件）（基本不用）。

#日志
$ git log --oneline --stat #查看日志，可以查看文件列表 显示每次更新的修改文件的统计信息
$ git log -p #按补丁显示每个更新间的差异
$ git log -g/git reflog  #可以查看所有的历史操作记录，如果通过git reset --hard 把记录回滚了，可以通过该命令查看历史操作，再通过git reset恢复

#撤消和重做
$ git checkout HEAD <file> #撤消指定的未提交(已修改，已暂存)文件的修改内容，即保证工作目录中的状态与已提交状态一致。
$ git revert <commit> #回滚至指定的提交(还没弄明白)

$ git reset HEAD <file> #取消已暂存的文件。即，撤销先前"git add"的操作。
$ git reset --hard HEAD #把工作目录中所有未提交(已修改，已暂存)的内容清空(当然这不包括未置于版控制下的文件 untracked files)。
$ git reset --hard <commit_id>(哈希值的前几个字符)彻底回退到某个版本，本地的源码也会变为该版本的内容。

根据–soft –mixed –hard，会对working tree和index和HEAD进行重置:
    git reset –mixed：此为默认方式，不带任何参数的git reset，即时这种方式，它回退到某个版本，只保留源码，回退commit和index信息
    git reset –soft：回退到某个版本，只回退了commit的信息，不会恢复到index file一级。如果还要提交，直接commit即可
    git reset –hard：彻底回退到某个版本，本地的源码也会变为上一个版本的内容
    
技巧： $ git reset --hard <commit_id> 与 git push origin HEAD --force 合用，彻底回退到某个版本并提交服务器（删除指定版本，在提交错误后可以使用该方法删除错误提交）

#分支与标签
$ git branch #显示所有本地分支
$ git branch <new-branch> #创建新分支  
$ git checkout <branch/tag> #切换到指定分支或标签  
$ git checkout -b <branch/tag> #相当于$ git branch <branch/tag>   $git checkout <branch/tag>  
$ git branch -d <branch> #删除本地分支
$ git tag #列出所有本地标签
$ git tag <tagname> #基于最新提交创建标签
$ git tag -d <tagname> #删除标签

#合并与衍合
$ git merge <branch> #合并指定分支到当前分支，新的版本
$ git rebase <branch> #衍合指定分支到当前分支，形成线性

#merge操作会生成一个新的节点，之前的提交分开显示。而rebase操作不会生成新的节点，是将两个分支融合成一个线性的提交。
#想要更好的提交树，使用rebase操作会更好一点。
#远程操作

$ git remote -v #查看远程版本库信息
$ git remote show <remote> #查看指定远程版本库信息
$ git remote add <remote> <url> #添加远程版本库
$ git fetch <remote> #从远程库获取代码
$ git pull <remote> <branch> #下载代码及快速合并
$ git pull <remote> <branch>:<local-branch>  取回remote的branch分支，与本地的local-branch分支合并,注意冒号后不能有空格  
$ git push <remote> <branch> #上传代码及快速合并
$ git push <remote> :<branch/tag-name> #删除远程分支或标签
$ git push --tags #上传所有标签


#生成ssh key
ssh-keygen -t rsa -C "邮箱"  #生成ssh key，然后根据提示连续回车即可在~/.ssh目录下得到id_rsa和id_rsa.pub两个文件，id_rsa.pub文件里存放的就是我们要使用的key。
ssh -T git@github.com #测试是否配置成功
```

##参考

[来源](https://gitcafe.com/GitCafe/Help/wiki/Git-%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4%E9%80%9F%E6%9F%A5%E8%A1%A8#wiki)

http://www.ruanyifeng.com/blog/2015/12/git-cheat-sheet.html

http://www.ituring.com.cn/article/202419

http://www.cnblogs.com/renkangke/archive/2013/05/31/conquerAndroid.html
