# git-op
Git命令大全
﻿git常用命令
	创建或收集项目
		git init
		git clone <url>
	本地仓库操作
		git add
			git add . 
			git add *
			git add <filename1> <filename2> .....
			git add
		git status
			git status -s
			git status
		git diff
			git diff --coched
			git diff
			git diff HEAD
			git diff --stat
		git commit
			git commit -m '<备注>'
			git commit -am '<备注>'
		git reset
			git reset HEAD -- <filename>
			git reset --soft HEAD~
			git reset --hard
				git reset --hard HEAD~<数字> 
				git reset --hard <SHA-1> 
				git reset --hard HEAD@{<数字>}
			git reset
		git rm
			git rm -f <filename>
			git rm --cached <filename>
			git rm --cached -r <folder>
			git checkout <SHA-1> -- <filename>
		git stash
			git stash
			git stach -u <filename>
			git stash list
			git stash apply stash@{<数字>}
			git stash pop stash@{<数字>}
			git stash drop stash@{1}
	git全局设置
		git config --global user.name <yourname>
		git config --global user.email <you@somedomain.com>
	推送或更新项目
		git push
			git push <仓库名> HEAD~<数字>:<分支名称>
			git push <仓库名> <branchname>
		git fetch
			git fetch <仓库名> --tags
			git fetch <remote> tag <tag-name>
			git fetch
				git fetch <仓库名>
			git pull
		git remote
			git remote
			git remote -v
			git remote add [<仓库名>] [url]
			git remote rm <仓库名>
			git remote rename [<旧仓库名>] [<新仓库名>]
			git remote set-url <仓库名> <新url>
	branch和merge
		git branch
			git branch <branchname>
			git branch
			git branch -v
			git checkout -b <branchname>
			git branch -d <branchname>
			git push <remote-name>:<branchname>
			git push <remote-name> <local-branch>:<remote-branch>
		git checkout
			git checkout <branchname>
		git merge
			git merge <branchname>
		git log
			git log
				git log --oneline
					git log --oneline --graph
						git log --oneline --graph --decorate
				git log <branchname>
				git log --oneline <branchname1> ^<branchname2>
		git tag
			git tag -a <版本号>
			git tag -a <版本号> <SHA-1>
                        git tag -d <版本号>
                        git push --delete origin <tagname>
                        git tag -l
                            git tag -l <匹配表达式>
                        git show <版本号>
                        git push origin <tagname>
                        git checkout -b <branchname> <tagname>
	检查或比较
		git log
			git log --<authorname>
			git log --since={<时间>} --before={<时间>}
		git reflog
		git diff
		git ls-tree -r <branchname>--name-only



备注：
git init 
进入目标文件夹，shift+右键打开CMD，输入该指令，将会增加一个.git文件，并使该文件夹转化为一个仓库

git clone <url>
clone项目，url可以在github上的项目主页那里找到。一般在上一层目录里输入指令，git会自动帮你创建一个与项目同名的文件夹。PS：clone是克隆所有历史，也包括所有branch，所有commit

git add（类别说明）
将新文件或对文件的修改添加到stage区(gitignore文件除外)，是commit前必须做的，他的作用是协助用户在commit前做好分类，stage作为一个缓冲区，而commit是要记录SHA-1值的，用于回滚，不能随意增删

git add .
添加目录下的所有文件或修改，包括子文件夹里的文件，用在根目录时，添加所有文件

git add *
添加指定目录下的所有文件（*为目录），与git add .不同的是，后面可以跟后缀，如：git add *.html,他就会遍历所有html文件，而不是js，css文件

git add <filename1> <filename2> .....
添加当前目录下的指定文件

git add
只用git add，就只会添加修改过的文件，没有修改的文件不会加到stage里

git status（类别说明）
将你的本地文件与最新的commit里的内容比较，看看有无增删改，*仅显示文件状态，不显示具体修改了哪些代码*

git status -s
将信息简要概括，仅在文件的前面显示缩写字母，标示出是否有增删改

git status
详细列出信息

git diff（类别说明）
与status不同的是，*显示具体文件里的具体代码改动*

git diff --coched
显示stage里的文件改动信息，这些信息将作为紧接下来的commit信息提交到本地仓库，与git status不同的是，该命令具体到代码的修改

git diff
直接用git diff命令不能查看stage里的文件信息，而是列出本地文件与最近一次commit版本的差异

git diff HEAD
将stage和本地文件的改动都列出来（与最近一次commit比较），可以理解为是git diff和git diff --coched的结合体

git diff stat
以数字统计方式显示文件的改动，可以添加到git diff HEAD等命令后面，如git diff HEAD --stat

git ls-tree -r <branchname>--name-only 
查看被跟踪的文件，PS：写入.gitignore文件虽然不被更新，但他依然还是add，被跟踪的，要彻底点就要使用git rm --cached；

git commit（类别说明）
将stage里的文件信息提交到仓库，commit后git会记录下相应的SHA-1值，以后reset就是根据这些SHA-1值来回滚的

git commit -m '<注释>'
将Stage里的东西提交到本地仓库，加备注，如果不写 -m ，就弹出文本，记录详细备注

git commit -am '<注释>'
不经过Stage，直接将本地文件的改动提交到本地仓库，加备注，如果不写 -m ，就弹出文本，记录详细备注

git reset（类别说明）
撤销本地仓库的更新（如commit），其功能十分强大

git reset <filename> <filename>
当你错将文件提交到stage时，可以用这个命令撤销add操作

git reset --soft HEAD~
如果你commit后发现了错误，想撤销，这时可以用软撤销, HEAD~表示上上次commit后的版本，也就是撤销最近一次commit，并将这些文件改动返回Stage，不会对文件造成影响

git reset --hard（类别说明）
硬撤销，与soft相比，是真"硬"，他会将你stage区，unstage区（本地文件发生的，还未add的举动）里的内容全部清空，并将你的本地文件内容回滚到所选择的commit版本后

git reset --hard HEAD~<数字> 
HEAD就是清空unstage和stage，将文件的最新改动（还未commit的内容）清空，将本地文件还原为最近一次commit后的样子，HEAD~就是上上次commit，HEAD~2就是上上上次commit

git reset --hard <SHA-1> 
每次commit都有SHA-1值，你可以不用数第几个，直接硬撤销到某个commit后的版本,你也可以用这个命令*撤销reset*，不过你得记住SHA-1值，如果你记不住，也可以用*git reflog*查看更新记录：P

git reset --hard HEAD@{<数字>}
可以不用SHA-1值，git reflog以链表方式记录更新操作，会记录下HEAD顺序，所以当你想撤销reset操作时，可以方便点，输入HEAD的排序

git reset
清空stage区，文件改动不受影响（区别于硬撤销），就是给你次机会重新将文件编排好再add进stage区，是*git reset --mixed HEAD*的缩写

git rm（类别说明）
移除文件，比reset暴力

git rm -f <filename>
彻底干掉你的文件，缓冲区和本地硬盘文件都删掉，慎用

git rm --cached <filename>
仅仅从git仓库中中踢走文件，本地文件保留，注意，github上只会显示仓库里的文件，也就是说不会再显示你rm后的文件；

git rm --cached -r <folder>
移除本地文件夹，r参数是指recursive，即递归移除文件夹下的文件；

git checkout <SHA-1> -- <filename>
如果你不慎用git rm -f删除了本地文件，你可以用存在该文件的commit的SHA-1来恢复被删除的文件

git stash（类别说明）
一个临时存储室，区别于"本地文件——staging area——仓库"这样的正规路径，是当小伙伴找你研究项目时，你将文件改动信息临时存储的地方，不会影响任何东西

git stash
将你当前所有的文件改动存到stash中

git stach -u <filename>
如果你还没有将文件add进stage区，以前的git版本就会先要求你add进去，而现在加个-u就可以了

git stash list
查看stash区里的目录，最近的存入是存在0位置

git stash apply stash@{<数字>}
无

git stash pop stash@{<数字>}
拿回stage后，删除stash里的数据

git stash drop stash@{<数字>}
无



git branch（类别说明）
分支操作，可以从任何分支和master中执行，继承被分支的历史

git branch <branchname>
创建分支，注意创建分支时，被分支的分支不会留下记录，但新的分支会有创建时间，以及那个时间点以前的被分支的所有历史

git branch
只用git branch命令会输出所有的branch，并标注你当前所在的branch

git branch -v
输出每个分支最近的一次commit的SHA-1值

git checkout -b <branchname>
git checkout 和git branch命令的结合，作用是：创建分支并切换到该分支

git branch -d <branchname>
删除分支，删除分支不会影响其他与之merge的分支里的历史和内容，不会在reflog、log中留下记录

git checkout -b <branch> <SHA-1>
恢复被删除的branch, 不过你要输入存在着该branch的commit的SHA-1

git push <remote-name>:<branchname>
只是快速将远程分支删除或添加

git push <remote-name> <local-branch>:<remote-branch>
将本地分支改动推送到远程分支

git checkout（类别说明）
分支切换命令，切换分支后，本地文件会自动改变为该分支的最后一次commit

git checkout <branchname>
切换到某个分支

git merge（类别说明）
分支融合命令，merge后分支依然存在，你也可以选择merge后马上删除，要注意的是，两个分支的同一处修改点会发生冲突，需要手动选择修正，对于冲突，可以选择vim <filename>,然后git diff显示冲突，当然也可以手动解决咯，然后删除文件里的conflict信息，解决了conflict后，只需在分支上add和commit就可以了，注意：用git log不会在被分支中显示分支信息，但用merge后，会拿到被融合分支的全部commit历史

git merge <branchname>
融合分支，但你要先切换到主分支，然后再选择要与之融合的分支，融合后获取该branch的所有commit历史



git log <branchname>
输出该branch的所有commit历史，如果是分支，也会继承主branch的历史

git log --oneline <branchname1> ^<branchname2>
输出branch1有，但branch2没有的commit历史，^是比较的意思

git tag（类别说明）
用于记录下你某个时刻的版本号，这是可以提供下载的，就像我们平时下载的软件版本一样

git tag -a <版本号>
从你当前分支的最近commit开始，将所有历史打包为一个版本

git tag -a <版本号> <SHA-1>
如果你忘记打包了，可以找回以前的某个commit打包

git tag -d <版本号>
将本地特定的tag删除

git push --delete origin <tagname>
将远程仓库的tag删除

git tag -l
将你的所有tag列出来

git tag -l <匹配表达式>
将某个系列的版本列出来，匹配表达式就跟regex差不多，如：git tag -l "v1.8.5*", 就会列出所有前缀为v1.8.5的版本

git show <版本号>
列出某个tag的信息

git push origin <tagname>
将tag推送到远程仓库

git checkout -b <branchname> <tagname>
你不能直接切换到某个tag(tag是不可修改的)，但你可以通过创建一个branch来操作某个特定tag，但由于是可commit的，这可能会对tag的内容造成影响，当然内容怎么修改也只是在该branch的范围内，对原来的tag不构成影响

git fetch（类别说明）
将远程仓库与本地仓库同步，同步回来的branch你不能checkout，但可以merge，可以diff，也可以log，不过当你对branch操作时，要用<仓库名>/<分支名>，如：git log github/master ^master（github是仓库名，默认是origin）

git fetch <仓库名> --tags
抓取所有tag

git fetch <remote> tag <tag-name>
抓取远程仓库的特定tag

git fetch
将远程仓库的变化同步到本地仓库

git fetch <仓库名>
同步特定的仓库

git remote（类别说明）
用于操作远程仓库

git remote
仅用git remote只输出你当前远程仓库的代号

git remote -v
输出所有代号对应的远程仓库链接

git remote add [<仓库名>] [url]
仓库名任意，默认是"origin"

git remote rm <仓库名>
删除远程仓库，只是断开你与远程仓库的链接

git remote rename [<旧仓库名>] [<新仓库名>]
改名字

git remote set-url <仓库名> <新url>
重设仓库URL




git push（类别说明）
推送本地仓库版本信息到remote仓库

git push origin HEAD~<数字>:<分支名称>
推送你想要的版本（commit版本）到远程仓库的某个分支，HEAD可以搭配数字，应该也可以用SHA-1值代替，origin是远程仓库名

git push <仓库名> <branchname>
更新分支信息到远程仓库

git log
git log显示所在分支中的所有commit历史（reset后删掉的不算，要用reflog恢复），是从你最近一次commit出发，迭代输出上次commit，上上次commit，也就是当前commit前的历史，当你reset后，log会发生改变


git log --oneline
显示git log的简短版

git log --oneline --graph
以图表的方式显示当前分支的commit历史，可以很方便地看出branch的创建和merge

git log --oneline --graph --decorate
不知道是干啥的

git reflog
git reflog是命令记录，会记录下你的所有本地仓库更新记录，不区分branch，不同于log，log会根据你reset后的commit而删掉以后的commit改动，而reflog则会记住你的所有操作，包括reset，撤销reset等一切更新本地仓库的记录，并将其SHA-1记录下来，*通常用于撤销reset*

git log --<authorname>
输出特定作者的所有logs

git log --since={<时间>} --before={<时间>}
输出某段时间内的log

git config（类别说明）
用于配置你的git

git config --global user.name <yourname>
设置你的用户名，用于commit时提供认证

git config --global user.email <you@somedomain.com>
设置你的邮箱，用于commit认证
