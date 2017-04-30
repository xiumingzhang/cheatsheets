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
# rm all files
git rm -r --cached .

# add all files as per new .gitignore
git add .

# now, commit for new .gitignore to apply
git commit -m ".gitignore is now working"
```


### Make .gitignore ignore everything but a few files

```
# Ignore everything
*

# But not these files
!.gitignore
!script.pl
!template.latex
```


### List files current tracked by git

If you want to list all the files currently being tracked under the branch master, do

```
git ls-tree -r master --name-only
```