好的，我将把之前的 Git 基本使用方法 Markdown 内容整理好，并提供一个可以直接复制粘贴到文件中的内容，然后告诉你如何将其保存在桌面上。

# Git 基本使用方法

## 1. 查看状态

```bash
# 检查目录状态，展示所有更改的文件
git status

# 将指定文件添加到暂存区
git add filename.txt

# 添加所有修改的文件到暂存区
git add .

# 提交添加到暂存区的更改到本地仓库
git commit -m "Initial commit"
2. 查看更改
# 查看文件的详细更改
git diff filename.txt

# 查看已暂存但未提交的更改
git diff --staged
3. 分支管理
创建和切换分支
# 列出所有本地分支
git branch

# 创建一条新分支
git branch new-feature

# 切换到某个分支
git checkout new-feature

# 新建并切换至新分支（即创建并检出）
git checkout -b new-feature
合并分支
# 切换回主分支
git checkout main

# 将另一个分支合并到当前分支
git merge new-feature

# 使用--no-ff参数强制合并时创建一个新的提交节点
git merge new-feature --no-ff -m "Merging new-feature"
删除分支
# 删除已合并的本地分支
git branch -d new-feature

# 强制删除未合并的本地分支
git branch -D new-feature
4. 远程仓库操作
推送和拉取
# 将本地更改推送到远程仓库的主分支
git push origin main

# 从远程获取最新更改并合并到当前分支
git pull origin main

# 拉取远程分支并合并到本地，但不自动合并
git fetch origin

# 合并远程某个分支到当前分支
git merge origin/new-feature
推送新分支
# 创建并推送本地新分支到远程仓库
git push -u origin new-feature
5. 日志和历史记录
# 查看提交日志
git log

# 检查每个文件在每次提交时的变化历史
git log -p

# 查看简要状态，如最近的几次提交
git log --oneline

# 检查分支合并图表
git log --graph --decorate --all
6. 撤销和回滚
撤销操作
# 撤消尚未暂存的更改
git checkout -- filename.txt

# 撤消已添加到暂存区但尚未提交的更改
git reset HEAD filename.txt  # 用于撤销暂存的文件，恢复到工作目录状态。

# 重置已提交的commit (谨慎使用)
git reset --hard <commit_hash> # 将当前分支重置到指定 commit，并丢弃后续的所有 commit。
7. 其他常用命令
# 克隆远程仓库
git clone <repository_url>

# 查看远程仓库信息
git remote -v

# 添加远程仓库
git remote add origin <repository_url>

# 标签 (Tag)
git tag <tag_name>  # 创建标签
git push origin --tags # 推送标签到远程仓库
重要提示：fixed first time
