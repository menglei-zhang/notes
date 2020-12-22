### git 不等于 GitHub
git 是一门技术（软件）
git 本身是在Linux上跑的
GitHub 是基于git扩展的服务 存取服务

工作区 workspace
暂存区 index
仓库区 repository
github远程仓库  

### git
git init   // 将一个目录转变成一个 Git 仓库
git remote rm origin

git add -A   // 添加到暂存区
git status   // 
git commit -m"first"   // 提交
git log
git clone https://github.com/menglei-zhang/hello-world.git
git diff   // 
git push
git log --g=oneline
git reset --hard HEAD^
git reflog
git reset --hard ...
## 分支
git branch    // 查看分支
git branch aaa    // 创建aaa分支（aaa为分支名）
git checkout aaa  // 切换到aaa分支
git merge aaa     // 把aaa分支合并
git branch -d aaa   // 删除aaa分支
git remote -v
git remote add upstream https://github.com/menglei-zhang/hello-world
git fetch upstream
get merge upstream/master    // master为主分支

查看连接到哪个远程库
git remote -v

删除存在的已连接的远程库并加入新库地址
git remote rm origin
git remote add origin https://github.com/menglei-zhang/test.git
git push -u origin master


.gitignore
node_modules
.idea
.vscode
.git


README.md
// 项目说明

git 提交代码到远程分支
1.提交单个文件
　　git add  工程名的下一级开始写路径直到文件名
2.提交全部文件
　　git add .（后面有一个点）
3.执行commit提交
　　git commit -m "文字描述"（单引号和双引号都可以）
4.方案一：合并远程分支代码（如果在此之前有别人提交了代码，需要先合并代码才能够push）
　　git fetch origin 
　　(git remote update有的时候可能需要同步一下远程和本地）
　　git merge origin/远程分支名　　
5.方案二：合并远程分支代码
　　git pull origin 远程分支名
（PS：方案一和方案二选择一个即可）
6.执行push推送代码
　　git push origin 本地分支名:远程分支名