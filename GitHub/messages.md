## Types of Commit Messages
```text
feat:     new feature, change authentication flow
fix:      bug fix
docs:     documentation changes (README, notes, etc.)
style:    formatting changes (spaces, indentation, no logic change)
refactor: code changes without adding features or fixing bugs

test:     add/update tests (unit, integration, e2e)
chore:    maintenance tasks (dependencies, setup, config)
perf:     performance improvements
ci:       GitHub Actions / pipeline changes

build:    build system or dependency changes
revert:   revert a previous commit
init:     initial project setup

security: security fixes
wip:      work in progress (temporary)

deps:     update dependencies
config:   update application settings
env:      add production environment variables

hotfix:   fix production issues
ux:       improve login screen spacing, UI/UX improvements (layout, spacing, usability)
```

## Examples
```text
git commit -m "feat(auth): add login screen"
git commit -m "fix(api): crash on startup"
git commit -m "docs(readme): update git cheatsheet"
git commit -m "style(ui): format code"
git commit -m "refactor(db): clean repository layer"

git commit -m "test(auth,unit): add unit tests for login"
git commit -m "chore(deps): update dependencies"
git commit -m "perf(api): improve API response time"
git commit -m "ci(github): add github actions pipeline"

git commit -m "build(gradle): update gradle version"
git commit -m "revert(auth): undo login changes"
git commit -m "init(core,project,setup): project setup"

git commit -m "security(auth,jwt,token): fix authentication vulnerability"
git commit -m "wip(feature): login screen in progress"

git commit -m "deps(android): update retrofit and okhttp versions"
git commit -m "config(api): update API base URL for staging"
git commit -m "env(prod,crash,urgent): add .env production variables"

git commit -m "hotfix(prod): fix crash when user logs out"
git commit -m "ux(ui,layout,spacing): improve button spacing on login screen"
```