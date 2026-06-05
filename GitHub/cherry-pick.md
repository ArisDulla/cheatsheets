## List branches
```bash
git branch
```
## Copy a commit from another branch to main
```bash
git checkout main 

git cherry-pick e123456 

git cherry-pick A B C
git cherry-pick A..D
git cherry-pick A^..D 

git cherry-pick -e <commit-hash> # edit commit message

git cherry-pick -n <commit-hash> # Apply WITHOUT COMMIT

git push origin main

# conflict 
git add .
git cherry-pick --continue

git cherry-pick --skip
git cherry-pick --abort
```
## Example
```bash 
git cherry-pick -n A B C
git reset # remove staging
git add .
git commit -m "combined fix"
```
## Moves HEAD to previous or specified commit, 
```text
git reset                # previous commit, unstages changes, keeps working directory (safe default behavior)

git reset --mixed HEAD~2 # unstages files, keeps working directory changes (default behavior)

git reset --soft HEAD~3  # keeps changes staged (ready to recommit)

git reset --hard HEAD~4  # clears staging area AND working directory (DESTRUCTIVE: deletes uncommitted changes)
```