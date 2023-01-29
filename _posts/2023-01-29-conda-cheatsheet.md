---
layout: post
title: Conda cheatsheet
---

General stuff:
- Directly install mamba into a new conda enviroment or install mambaforge in the first place (mamba is per default installed)
- install pip in the default (base) enviroment
- install pip packages only if they aren't available on conda

Create enviroment yml file
```bash
conda list -e > enviroment.yml
```

Create new enviroment
```bash
mamba create -n 'enviroment'
```

Create new enviroment based on a yml file
```bash
mamba env create --file rnaquant_env.yaml
```

List your enviroments
```bash
conda info --envs
```

List all packages of the currently used and activated enviroment
```bash
mamba list
```

List specific conda package
```bash
mamba list 'package'
```


Delete a conda enviroment
```bash
conda remove --name myenv --all 
```

Install a single conda package in a activated enviroment (1)
```bash
mamba install 'package'
```

Install multiple conda packages in a activated enviroment (2)
```bash
mamba install 'package' 'package2'
```

Install a specific version of a package
```bash
mamba install 'package=3.2'
```

Free disk space of unused packages
```bash
 conda clean --all
 ```