## Switch 
```bash
git switch main # switch exst

git switch -c feature/login # create and switch 
git switch -c feature/login develop # create feature/login starting from develop or remote origin/......

git switch -f branch # DONT DO IT - force switch
or
git restore .

git switch - # switch previous branch ( git checkout - )

git switch -c recovered-work <hashhh> # create a branch from a specific commit

# Detached HEAD 
#
# switch does NOT delete history
#
git switch --detach  HEAD or <hashh> # move HEAD to a commit

git switch -c fix-old-bug # fix bug

# Remote branches
git branch -r or -a
```

## Restore
```bash
git restore file # undo changes
git restore .  # undo everything
git restore --staged file # unstage ( git add .) 
git restore --source X file # restore from commit 
```