# Reflog

## Recover a lost commit after reset
```bash
git reset --hard HEAD~1 # Lost last commit

git reflog # list
git show HEAD@{1} or d4d4d4d

git reset --hard d4d4d4d or HEAD@{1} 
or
git checkout -b recovered-work d4d4d4d # new branch
git switch -c recovered-work d4d4d4d # new branch
```
## Recover a deleted branch
```bash
git branch -D feature/login # Lost branch

git reflog

git checkout -b feature/login <hashhhh>
```
## Undo a bad rebase
```bash
git rebase main 

git reflog
-----------------------------------
HEAD@{0}: rebase finished
.....
HEAD@{6}: rebase start
HEAD@{7}: commit: Before rebase
------------------------------------

git reset --hard HEAD@{7}
```
