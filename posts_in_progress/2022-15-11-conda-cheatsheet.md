---
layout: post
title: Conda Cheatsheet
---

Create enviroment yml file
```bash
conda list -e > enviroment.yml
```

Create new enviroment
```bash
mamba create -n 'enviroment'
```

Create new enviroment based on an yml file
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

Install a conda package in an activated enviroment
```bash
mamba install 'package' OR mamba install 'package' 'package2'
```

Free disk space of unused packages
```bash
 conda clean --all
 ```