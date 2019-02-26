### Undo last commit

If you don't want to keep your changes that you made, do

```
git reset --hard HEAD^
```

If you want to keep your changes, do

```
git reset --soft HEAD^
```


### Resync git repo with a new .gitignore


```
cd "$repo_root"
git rm -r --cached .
git add .
git commit -m "resync with new .gitignore"
```


### Make .gitignore ignore everything but a few files

```
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

```
git ls-tree -r master --name-only
```


### List commits

```
git log
```


### See what has been changed by a commit

```
git show <commit>
```

Just filenames?

```
git show --name-only <commit>
```


### Compare what has changed between two commits

```
git diff <commit>^ <commit>
```


### Find the deleted from commit history

```
git log -S<string>
```

Then you can find the most recent commit that essentially did the deletion.
