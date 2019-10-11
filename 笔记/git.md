### git 本地代码提交到gitHub 上

直接开始正题，git 提交的步骤：
1. git init //初始化仓库

git add .(文件name) //添加文件到本地仓库

git commit -m “first commit” //添加文件描述信息

git remote add origin + 远程仓库地址 //链接远程仓库，创建主分支

git push -u origin master //把本地仓库的文件推送到远程仓库

要想解决以上错误，只需要在4，5之间使用git pull origin master即可

遇到问题：

正确步骤：
1. git init //初始化仓库

git add .(文件name) //添加文件到本地仓库

git commit -m “first commit” //添加文件描述信息

git remote add origin + 远程仓库地址 //链接远程仓库，创建主分支

git pull origin master // 把本地仓库的变化连接到远程仓库主分支

git push -u origin master //把本地仓库的文件推送到远程仓库