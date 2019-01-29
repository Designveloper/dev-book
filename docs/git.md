Git
===

Guide for using git version control.

* [General rules](./git#maintainance)

General rules
-------------

* Do not include any files or folders that are only specific to your
development environment. E.g:
  * IDE generated folders (`.idea`, ...)
  * Files logged from run time (`console.log`,...)
  * ...
* Delete local feature branches, and delete/merge remote feature branches after
merging.
* Rebase to get changes from main branch frequently while working on feature
branches.
* Should follow [Conventional Commits](
https://www.conventionalcommits.org/en/v1.0.0-beta.2/) to have good commit
messages.
* For large projects that requires complex release process, consider applying
[Git flow](https://danielkummer.github.io/git-flow-cheatsheet)
* Name your branches properly so that everyone can understand: `feature/sign-up`
, `fix/login-issue`,...

Work on task
------------

Create local branch from main branch (`master` or `develop`).
```bash
git checkout master
git pull origin master
git checkout -b <branch-name>
```

Frequently pull new code from main branch while working on feature branches.
```bash
git pull origin master --rebase
```

Or
```bash
git fetch origin
git rebase origin/master
```

Push your branch to remote.
```bash
git push origin <branch-name>
```

Create pull request on your Git version control tool (Github, Bitbucket, GitLab,
...)

Merge PR
--------

Squash your multiple commits by [Rebasing interactively](
https://help.github.com/articles/about-git-rebase/#rebasing-commits-against-a-branch)
before creating pull request (this is optional step).
```bash
git fetch origin
git rebase origin/master -i
```

Force push feature branch to remote.
```bash
git push origin <branch-name> -f
```

Merge PR using Git web tool.

If you want to merge it manually, you should merge using `--no-ff` option to
reserve merge commit message on git commit tree.
```bash
git fetch origin
git checkout master
git pull origin master
git merge <branch-name> --no-ff
git push origin master 
```

Delete local feature branch after merging.
```bash
git branch -D <branch-name>
```  

Delete remote branch (optional, as some Git tool has option to auto-close
merged branches).
```bash
git push origin --delete <branch-name>
```
