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

