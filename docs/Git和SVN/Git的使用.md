* [1.Github ID 更名后如何把旧的ID的commit记录跟新的GitHub ID一起显示](#1-Github ID 更名后如何把旧的ID的commit记录跟新的GitHub ID一起显示)

# 1. Github ID 更名后如何把旧的ID的commit记录跟新的GitHub ID一起显示  
　　我们知道如果GitHub更改名字后如果不做任何处理则前面名字提交的记录不会再显示在帐号初始页面提交记录的小格子里，满满的小绿格顿时变为灰色的，这时候我们
要怎么把旧名字的提交记录也显示出来呢？  
　　这是GitHub的官方文档https://help.github.com/articles/changing-author-info/  
实际操作如下：  
1.首先更改本地电脑上git的帐号配置  
```
git config --global user.email "youremail@google.com"
git config --global user.name "your name"
```
2.使用脚本改变repo的Git历史
注意：执行这段脚本会重写 repo 所有协作者的历史。完成以下操作后，任何 fork 或 clone 的人必须获取重写后的历史并把所有本地修改 rebase 入重写后的历史中。

在执行这段脚本前，你需要准备的信息：

欲修改的旧的邮箱地址

正确的用户名和邮箱地址

(1).打开终端

(2).创建一个你的 repo 的全新裸 clone （repo.git 替换为你的项目，下同）
git clone --bare https://github.com/user/repo.git
cd repo.git
(3)复制粘贴脚本，并根据你的信息修改以下变量：
OLD_EMAIL
CORRECT_NAME
CORRECT_EMAIL

脚本：
```
#!/bin/sh

git filter-branch --env-filter '

OLD_EMAIL="your-old-email@example.com"
CORRECT_NAME="Your Correct Name"
CORRECT_EMAIL="your-correct-email@example.com"

if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```
(4)按 Enter 执行脚本。

(5)查看新 Git 历史有没有错误。

(6)把正确历史 push 到 Github：（push 有困难时记得修改 DNS 或者搭梯子）
git push --force --tags origin 'refs/heads/*'

