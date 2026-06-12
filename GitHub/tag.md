## Tag releases
```bash
git tag -a v1.0.0 -m "Stable" # Create tag

git tag -a v1.0.0 <commit> -m "Stable" 

git push origin v1.0.0

git push --tags # all new tags
git push --all # + new branches , dont use it

git checkout v1.0.0 # HEAD → commit (v1.0.0) (detached state)
# Reset
git reset --hard v1.0.0 # HEAD → main → commit (v1.0.0)

git tag # list

git tag -d v1.0.0 # delete
# AND 
git push origin --delete v1.0.0 # remote


git ls-remote --tags origin # remote tags

git describe --tags # HEAD

# overwrite
git push -f origin v1.0.0
or
git push --force-with-lease origin v1.0.0

# new branch with starting point
git checkout -b fix-v1.0.0 v1.0.0

v1.0.0 → starting point
↓
new branch: fix-v1.0.0

git tag -a v1.0.1 -m "release"
```