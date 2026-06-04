
## Create branch
```bash
git checkout -b newBranch

git add .

git push --set-upstream origin newBranch
```
## Merge
```bash
git checkout newBranch

git pull 

git checkout main

git merge newBranch

git push  
```
## Conflicts
```bash
Edit file

git add file

git commit -m "fix: resolve merge conflict"

git push
```
## Delete Branch
```bash
git branch -d newBranch

git push origin --delete newBranch
```
## Remote changes without merging  
```bash
git fetch origin
git status
git diff origin/newBranch  
```
## Merge
```bash
git merge origin/newBranch
```
```text
A --- B --- C (main)
      \       
       D --- E (feature)

A --- B --- C ------ M
      \             /
       D --- E ----
```
## Rebase
```bash
git rebase main
git rebase --abort
```
```text
A --- B --- C (main)
             \
              D' --- E' (feature)
```
## Graph
```bash
git log --oneline --graph --decorate --all
git graph

(( git config --global alias.graph "log --graph --oneline --decorate --all" ))
```