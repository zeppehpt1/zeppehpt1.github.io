---
layout: post
title: Conda/mamba cheatsheet
---

My personal advice:
- Directly install mamba into a fresh new conda environment or install miniforge in the first place (then mamba is installed per default)
- install pip in the <del>default (base)</del> target enviroment
- install pip packages *only* if they aren't available on conda

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
mamba env create --file requirements.yaml
```

List your enviroments
```bash
conda info --envs
conda env list
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

Show current solver
```bash
conda config --show-sources
```

Change solver to libmamba solver
```bash
conda --set solver libmamba
```

Change solver to classic solver
```bash
conda --set solver classic
```

Free disk space of unused packages
```bash
 conda clean --all
 ```