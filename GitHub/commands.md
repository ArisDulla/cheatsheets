# Git Commands

## Generating a new SSH key
```bash
ssh-keygen -t ed25519 -C "your_email" -f ~/.ssh/github_work
```
passphrase

## Revert to Previous Commit
```bash
git log --oneline 

git reset --soft HEAD~1

git reset --hard fa79b99

git push -f origin main
```
## Add & Commit
```bash
git init

git add .

git commit -m "chore: initial commit"

git remote add origin http...

git push -u origin main
```
## Commit
```bash
git add .

git commit -m "feat: add login screen"

git push 
```
## Stashes - Pause Work
```bash
git status

git stash # Saved working directory and index state
git stash -u # Untracked file

git status # nothing to commit, working tree clean

git stash list 

git stash pop # from list
git stash pop stash@{0}

git stash apply --index # without deleting form list with “git add” state
git stash apply stash@{0} --index

git stash drop stash@{0} # delete

git stash show  # review
git stash show -p stash@{0} 

git stash push -m "work on login page"
git stash push -u -m "work on login page"

git stash push -m "message" file1 file2 # only specific files OR path
git stash push -- path/to/file

git stash clear # delete all

git stash branch bugfix stash@{0}
git stash branch bugfix # uses latest stash
------------------------------- 
| git checkout -b bugfix      |
| git stash apply stash@{0}   |
| git stash drop stash@{0}    |
-------------------------------
SOS COMMIT COMMIT SOS
---------------------------


git stash push -p # partial stash
git stash -a # includes ignored + untracked + tracked changes
```
```text
stash = temporary workspace
apply = restore but keep backup
pop = restore and remove
branch = turn stash into real work
```
