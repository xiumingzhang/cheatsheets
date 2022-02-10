### List environments

```bash
conda env list
```


### List packages in environment

If activated

```bash
conda list
```

Else

```bash
conda list -n myenv
```


### Create environment

```bash
conda create -n myenv python=3.4
```

If from `.yml`

```bash
conda env create -f environment.yml
```


### Remove environment

```bash
conda remove --name old_name --all # or its alias: `conda env remove --name old_name`
```


### Rename environment

```bash
conda create --name new_name --clone old_name
conda remove --name old_name --all # or its alias: `conda env remove --name old_name`
```


### Install packages to environment

```bash
conda install --name myenv scipy
```


### Check, add, or remove channels

```bash
conda config --get channels
conda config --add channels anaconda
conda config --remove channels anaconda
```


### Rollback

Locate the version before the screwup with

```bash
conda list --revisions
```

Rollback with

```bash
conda install --revision <rev_id>
```

In the case of

```bash
CondaRevisionError: Cannot revert to <rev_id>, since <channel>::<package> is not in repodata.
```

you will need to see from the revision history which packages got updated, and then revert them one by one, with necessary channel flags, e.g.,

```bash
conda install blas=1.1 -c conda-forge
```
