1. 常见指令：
   1. mkdir + string :创建一个目录，注意选择创建的位置，路径不能包含中文，可以用右键点击git-bash。
   2. cd + string ：change directory 切换到该目录下
   3. pwd :告诉现在所处目录的位置
   4.  git init : 创建一个新仓库。
   5. git add + 文件名(必须在git的目录之下)*注意大小写，在vi读文件的时候大小写好像都可以识别文件，但是add文件的时候必须要分清大小写，否则git无法识别文件但是又不会报错，结果是文件不会更改*
   6. git commit -m "本次提交的说明"
   7. ls或者dir 命令可以用于查看当前目录的文件
   8. vi +文件名 = 打开目录文件下的某文件，再次按下i 可以进入编辑模式，进行删减或者其他操作。修改完成后按下ESC按键回到命令模式，如果想保存并退出输入 ：wq ,如果不想保存退出只保存按 ：w ,如果放弃所有更改按下 ：q! 放弃修改并退出。：e!放弃修改但是不退出。
   9. git status 输出当前的状态（修改与否，提交与否）
   10. git diff + 文件名 查看文件的区别
   11. git reset --hard HEAD 返回到上一个版本，当前版本号为HEAD，上一个版本号为HEAD^，前一百个版本号为HEAD~100。如果没有 --hard，即 git reset HEAD <file> 代表将暂存区的文件回退回工作区
   12. 当回溯回了前面的版本号之后，想要返回到当前版本号，需要git reset --hard 版本号（具体前几位）
   13. git reflog 记录每一次命令
   14. git rm + 文件名 删除文件
   15. repository 远程仓库
   16. git checkout --file 回溯文件到最近一次git commit 或者 git add d时候的状态，注意没有--意味着切换分支。
   17. git remote add origin git@github.com:Maxwellqzh/learngit.git 将自己的远程仓库存到github上。
   18. git push -u origin master 将本地的git第一次发到github里面， 以后上传只用git push origin master 即可
   19. 删除远程库，当添加的库写错了，写错了想删除远程库，可以用
       git remote rm <name> 命令，使用前，建议先用 git remore -v 查看远程库信息。
   20. git clone git@github.com:Maxwellqzh/<文件名>，克隆一个本地库
   21. git clone https://github.com/jquery/jquery.git e:/myJQuery/ 克隆到希望的目录位置
   22. 创建分支
        git checkout -b dev 创建一个dev分支，并且切换到该分支
        git checkout dev 切换到dev分支
        git branch dev 创建一个dev分支、
        git branch 查看当前分支
   23. 分支合并：
        git merge dev：合并指定分支到当前分支
   24. git branch -d dev 删除分支
   25. git switch -c dev 同样是切换分支
   26. git log --graph --pretty=oneline --abbrev-commit 带参数的log，可以看见分支的合并情况
   27. git stash 将当前工作区储存，储存之后可以用git stash list 查看储存的工作区，需要恢复时用git stash apply stash@{n}恢复其中stash@{n}是在git stash list 查看到的储存编号，但是需要再用git stash drop来删除，或者直接用 git stash pop 恢复同时删除
   28. git cherry-pick + 修改编号 命令，只将某一次修改的重放
   29. 强行丢弃git branch -D <name>
   30. 打标签：git tag <name>(切换到需要打标签的分支上，提交时相当于把commit加上一个名字)
   31. git tag <name> + commit编号 可以对过去的版本进行编号
   32. git tag 查看标签，以字母排序
   33. git show <tagname> 查看标签信息
   34. git tag -a <name> -m "introduction" + commit号 可以创建带有说明的标签
   35. git tag -d <name> 删除标签
   36. git push origin <tagname> 将本地的标签推送到远程
   37. git push origin -tags 一次性推送全部尚未推送的标签到远程
   38. 如果标签已经推送到远程，想要删除，需要先从本地删除 git tag -d v0.9 再远程删除 git push origin :refs/tags/<name>
   39. git pull 拉取远程主机的master与本地的branch合并。使用方法是 git pull <远程主机名（origin）><远程分支名>：<本地分支名>，如果是与当前分支合并可以省略本地分支名