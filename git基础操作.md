## git

```
.gitignore  git仓库过滤文件,过滤不需要提交的文件或者文件夹
git init 初始化一个git仓库
git status  查看当前仓库的状态
git add   把需要提交的文件添加到本地缓存
git add .  把需要提交的所有工作区文件
git commit -m '提交信息'  //把本地缓存中的文件提交到本地仓库
```
```
git branch 分支名 //创建一个新分支
git checkout 分支名  //切换到指定的分支
git branch -d 分支名   //删除分支

git merge 分支名   把指定分支合并到当前分支上

git log      查看日志
git log --graph --pretty =oneline  --abbrev-commit  加入一些美化和图形的命令

回退到指定位置
git reset logid  --hard     //回推到指定的一次提交

git tag tagName    //给代码打标签,标签可以进行切换和直接发布

git reset   ( id )  --hard  回退到某一次提交

远程服务相关操作
git remove -v  //查看远程服务器信息
git pull origin master:master      //把远程分支的代码合并到本地
git push origin  master:master     //把本地的master分支推送到服务器的master分支
git clone  远程服务器地址           //把远程服务器的代码clone到本地
```
### git代码版本控制基础操作
    ```
    git add .                //把代码加入缓存
    git commit -m ''         //提交
    git branch  分支名        //创建分支
    git checkout    分支名    //切换分支
    git log   --参数          //查看日志
    git reflog               //查看本地所有日志
    git merge  分支名         //合并分支
    git tag  标签名          //创建tag
    ```
