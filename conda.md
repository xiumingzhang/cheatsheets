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
