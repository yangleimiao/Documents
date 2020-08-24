上传本地项目到github的第二种方法
本地项目中执行 `git init` ，使其变成一个git仓库，本地项目文件夹中会多一个.git目录
执行`git add .`
执行 `git commit -m "注释" `
关联github仓库，github中新建项目，复制地址，执行
` git remote add origin https://github.com/yangleimiao/spring-in-action.git` 
上传本地代码前先执行
`git pull --rebase origin master` ，github中的readme等文件下载到本地
再上传 `git push origin master`

列出所有本地分支
`git branch`

列出所有远程分支 
`git branch -r `

新建一个分支，但依然停留在当前分支
`git branch [branch-name]`

新建一个分支，并切换到该分支
`git checkout -b [branch]`

新建一个分支，与指定的远程分支建立追踪关系
`git branch --track [branch] [remote-branch]`

删除分支
`git branch -d [branch-name]`

删除远程分支
`git push origin --delete [branch-name]`
`git branch -dr [remote/branch]`





把远程分支拉到本地

`git fetch origin dev`

在本地创建分支dev并切换到该分支

`git checkout -b dev origin/dev`



`git pull origin dev`













