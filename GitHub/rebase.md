## Git Log
```bash
git log --oneline -6
git log --oneline --graph --all
git log -n 5
```
## Pull without merge commits.
```bash
git pull
A --- B -------- M
      \        /
       \-- C --

git pull --rebase
A --- B --- C'
```
## Interactive Rebase
```bash
git log --oneline

git rebase -i main # with editor AND It takes the commits from a branch and replays them on top of main.
git rebase main # without editor

git rebase -i HEAD~3 # pick the last 3 commits

# Common actions in the editor
pick
squash
s
# Save and set the new commit message in the editor

git push
git push --force-with-lease # required if the commits were already pushed before the rebase

-------
git rebase --abort
# conflict
git add .
git rebase --continue
```
## Fixup workflow (Merge squash)
```bash
edit file
git add .
git commit --fixup ff2441a
git rebase -i --autosquash main
git push --force-with-lease
```