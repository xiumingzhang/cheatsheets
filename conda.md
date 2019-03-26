### List environments

```
conda env list
```


### List packages in environment

If activated

```
conda list
```

Else

```
conda list -n myenv
```


### Create environment

```
conda create -n myenv python=3.4
```

If from `.yml`

```
conda env create -f environment.yml
```


### Rename environment

```
conda create --name new_name --clone old_name
conda remove --name old_name --all # or its alias: `conda env remove --name old_name`
```


### Install packages to environment

```
conda install --name myenv scipy
```


### Rollback

Locate the version before the screwup with

```
conda list --revisions
```

Rollback with

```
conda install --revision <rev_id>
```

In the case of

```
CondaRevisionError: Cannot revert to <rev_id>, since <channel>::<package> is not in repodata.
```

you will need to see from the revision history which packages got updated, and then revert them one by one, with necessary channel flags, e.g.,

```
conda install blas=1.1 -c conda-forge
```
