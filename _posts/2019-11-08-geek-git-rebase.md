---
title: Git Rebase
layout: default
categories: git-rebase
permalink: /:categories/
---

## Git Rebase

我们使用git的时候，偶尔会出现这么个情况，当你commit了多次之后发现，现在的某个change是应当属于属于之前的某个commit的。如果你想做正确的事情，如果你对自己要求严格，那么不是把该change随便合并到当前的commit，而是找到一个办法来把该change合并到前面它属于的那个commit。下面是具体的步骤：

1. Use `git stash` to store the changes you want to add.
2. Use `git rebase -i HEAD~10` (or however many commits back you want to see).
3. Mark the commit in question (a0865...) for edit by changing the word `pick` at the start of the line into `edit`. Don't delete the other lines as that would delete the commits.
4. Save the rebase file, and git will drop back to the shell and wait for you to fix that commit.
5. Pop the stash by using `git stash pop` or `git stash apply`.
6. Add your file with `git add`.
7. Amend the commit with `git commit --amend --no-edit`.
8. Do a `git rebase --continue` which will rewrite the rest of your commits against the new one.
9. Repeat from step 2 onwards if you have marked more than one commit for edit.

当然，合并之后原来的commit number也会跟着改变，这样当你想找到原来的change的时候也是可以做到的。
