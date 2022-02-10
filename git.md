### Change remote (e.g., if the repo. was renamed)

```bash
git remote set-url origin git@github.com:xiumingzhang/new.git
```


### Keep working on an unsubmitted commit

```bash
git commit --amend
```


### Undo last commit

If you don't want to keep your changes that you made, do

```bash
git reset --hard HEAD^
```

If you want to keep your changes, do

```bash
git reset --soft HEAD^
```


### Resync git repo with a new .gitignore


```bash
cd "$repo_root"
git rm -r --cached .
git add .
git commit -m "Resync with new .gitignore"
```


### Make .gitignore ignore everything but a few files

```bash
# Ignore everything in root, except these files
/*
!.gitignore
!.bash_profile
!.gitconfig
!.inputrc
!.vimrc
!README.md

# Don't ignore .ssh folder
!.ssh/

# Ignore everything there except one file
.ssh/*
!.ssh/config
```


### List files current tracked by git

If you want to list all the files currently being tracked under the branch master, do

```bash
git ls-tree -r master --name-only
```


### List commits

```bash
git log
```


### See what has been changed by a commit

```bash
git show <commit>
```

Just filenames?

```bash
git show --name-only <commit>
```


### Compare what has changed between two commits

```bash
git diff <commit>^ <commit>
```


### Find the deleted from commit history

```bash
git log -S<string>
```

Then you can find the most recent commit that essentially did the deletion.
