---
date:
  created: 2024-12-30
  updated: 2024-12-31
categories:
  - Git
readtime: 1
authors:
  - charlie
---
# GIT commands 

## 重命名本地分支
```bash
git branch -m new-branch-name
```

- m 是 move 的简写，用于重命名分支。
- new-branch-name 是你想要的新分支名。
## 删除本地分支
```bash
git branch -d new-branch-name
```
## 创建一个名为 dev-xxx 的本地分支，并将它与远程分支 origin/release 进行跟踪
1.不切换到dev-xxx，直接创建
```bash
git checkout -b dev-xxx origin/release
```
2.创建dev-xxx，切换到dev-xxx
```bash
git branch dev-xxx --track origin/release
```
3. Git 2.23 + 以上，切换到dev-xxx
```bash
git switch -c dev-xxx origin/release
```
## set upstream
```bash
# git branch --set-upstream-to=<remote-branch> <local-branch>

git branch --set-upstream-to=origin/release dev-xxx
```
## view remote branch
```bash
git branch -vv
```
## git view remote 
```bash
git remote -v
```

## git reset
### soft reset
1. 仅重置 HEAD，不改变暂存区和工作区的内容。
2. 变更内容仍然保留在暂存区（staging area）。
```bash
git reset --soft <commit>
```
将最近的一次提交撤销，但保留改动
```bash
git reset --soft HEAD~1
```
假设当前分支是 dev-xxx，origin/release 是一个远程分支。执行以下命令：
当前分支的 HEAD 移动到 origin/release 的提交位置
```bash
git reset --soft origin/release
```
### mixed reset（default）
1. 重置 HEAD 和暂存区（staging area），但不改变工作区的内容。
2. 变更仍然保留在工作区中
3. 清除暂存区内容，但保留未提交的修改以便重新组织
```bash
git reset --mixed <commit>
```
### hard reset
1. 彻底重置 HEAD、暂存区和工作区，所有改动都会丢失
2. 非常危险，无法恢复
3. 完全放弃提交和工作区的所有更改，恢复到指定提交的状态·
```bash
git reset --hard <commit>
```

## git status
```bash
git status
```
### Untracked files
假设你在工作区创建了一个新文件 newfile.txt，但还没有添加到暂存区。执行 git status 时，你可能会看到如下输出
```bash
$ git status
On branch dev-xxx
Untracked files:
(use "git add <file>..." to include in what will be committed)

        newfile.txt
```

next actions
1. 提交到暂存区
git add newfile.txt
2. 忽略
编辑 .gitignore 文件，添加文件名或路径：
3. 删除文件
rm newfile.txt
4. 如果你想删除所有的未跟踪文件，可以使用 git clean 命令。这个命令会移除工作区中的所有未被 Git 跟踪的文件（慎用！）
git clean -f
### Changes not staged for commit
1. 你修改了一个文件，但尚未使用 git add 将其加入暂存区。
2. 你删除了文件，但是还没有通过 git rm 命令将删除操作标记为暂存。
```bash
git status
On branch dev-xxx
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)

        modified:   example.txt
        deleted:    old_file.txt
```
next actions
1. 将修改添加到暂存区
git add example.txt
2. 取消修改，恢复文件到上次提交的状态
git restore example.txt
3. 删除文件并将删除操作标记为暂存
git rm old_file.txt
4. 查看文件差异
git diff example.txt

## fast-forward
在 Git 中，fast-forward（快速前进）是一种合并（merge）操作，表示当前分支没有分叉，且目标分支的所有提交都在当前分支的基础上。这时，Git 会直接将当前分支的指针“快速前进”到目标分支的位置，而不需要创建额外的合并提交。

Fast-forward 合并的场景
当你有一个直线的提交历史时，Git 会执行 fast-forward 合并。例如，假设你在 main 分支上工作，创建了一个新的分支 feature，并在 feature 分支上做了几次提交。然后，main 分支没有任何新的提交，此时将 feature 分支合并回 main 分支时，会发生 fast-forward 合并。

示例流程
假设你有以下的提交历史：
```text
A---B---C (main)
          \
           D---E (feature)
```
你当前在 main 分支上。
在 feature 分支上进行了提交 D 和 E。
然后，假设 main 分支在此期间没有新的提交。如果你执行合并操作：
```bash
git checkout main
git merge feature
```

此时，Git 会执行 fast-forward 合并，因为 main 分支没有进行任何新提交，合并操作将只是将 main 的指针直接“移动”到 feature 分支的最后一个提交（即提交 E）。结果是，main 分支看起来就像直接包含了 feature 分支的所有提交。

新的历史图会是这样的：
```text
A---B---C---D---E (main, feature)
```
为什么会发生 Fast-forward 合并
没有分叉：fast-forward 合并的前提是没有分叉，即 main 分支没有与 feature 分支并行开发的提交。
线性历史：在这种情况下，Git 只是将当前分支指向目标分支，不需要创建额外的合并提交。
如何避免 Fast-forward 合并
如果你希望在合并时始终创建一个新的合并提交（即使 main 分支没有新的提交），可以使用 --no-ff 选项来禁用 fast-forward 合并：
```bash
git merge --no-ff feature
```

这样即使没有分叉，Git 也会创建一个新的合并提交，从而保留合并的历史记录。合并后，Git 会显示一个新的合并提交，并且历史图会变成这样：
其中 M 是合并提交。

```text
A---B---C---M (main)
          \ /
           D---E (feature)
```
## git pull rebase

config 
```bash
git config --global pull.rebase true
git config pull.rebase true
```
rebase 产生冲突
解决冲突后
```bash
git add <resolved_files>
git rebase --continue
```


autostash
自动stash 和pop
```bash
git pull --rebase --autostash
```
## git push --force
<span style="color: red;">Warning：远程分支不可以是多人协作的分支</span>
```bash
git push --force(-f)
```
在 Git 中，git push -f（即 force push）用于强制推送本地分支到远程仓库，覆盖远程分支的历史。通常，git push 会拒绝推送本地分支到远程分支，如果远程分支的提交历史与本地分支不一致，防止数据丢失。但使用 git push -f 时，Git 会直接覆盖远程分支的历史，而不会拒绝推送。  

git push -f 允许你重写远程分支的历史，特别是在以下几种情况下：  

1. 清理提交历史：如果你在本地做了多个提交并希望将其合并成更少的、更简洁的提交（比如通过 git rebase），使用 git push -f 可以将重写后的提交推送到远程仓库，替代原有的历史。
2. 修复错误的提交：如果你误推送了错误的提交或敏感信息到远程仓库，使用 git push -f 可以推送修正后的历史，覆盖错误的提交。
3. 保留清晰的分支历史：
在团队协作中，可能希望保持一个干净的分支历史，避免不必要的合并提交或临时提交。通过使用 rebase 来整理提交历史，再结合 git push -f 推送更新，可以确保远程分支的历史更加简洁、线性。

4. 处理拉取请求（Pull Request）中的问题：
在处理拉取请求时，开发者可能需要调整自己的提交历史（例如合并多个提交或重新排序提交）。这时，可以通过本地的 rebase 或 amend 来修改历史，然后使用 git push -f 强制推送更新的历史到远程分支。

5. 清理远程分支：
如果你正在维护一个开发分支并且合并后不再需要该分支时，git push -f 可以删除该分支的历史记录，减少冗余的提交或“垃圾提交”在远程仓库中的存在。

## git cherry-pick 
git cherry-pick 负责将提交从一个分支合并到另一个分支。 
```bash
git cherry-pick <commit-hash>

```
### Encounter a Conflict
If Git detects conflicts, it will pause the cherry-pick process and provide a message like this:  

```bash
error: could not apply <commit-hash>
hint: After resolving the conflicts, mark the resolution with:
hint:   git cherry-pick --continue
```
You can check the status of your repository with:  

```bash
git status
```
### Resolve Conflicts
Open the files listed in the git status output. Conflicted sections will look like this  
```text
<<<<<<< HEAD
// Code from your current branch
=======
 // Code from the cherry-picked commit
>>>>>>> <commit-hash>

```
### Mark the Resolved Files
Save the file after resolving the conflicts.  
```bash
git add <file>
```
### Continue the Cherry-Pick
Once you've resolved a file, mark it as resolved with:  
```bash
git cherry-pick --continue
```
### Abort (if necessary)

```bash
git cherry-pick --abort
```

### Tips to Avoid or Manage Conflicts
- Before cherry-picking, inspect the commit with:
  ```bash
    git show <commit-hash>
    ```

- Rebase your branch to align with the source branch, reducing the chances of conflicts.
