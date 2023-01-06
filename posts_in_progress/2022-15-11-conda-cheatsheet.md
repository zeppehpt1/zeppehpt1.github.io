
Create enviroment yml
```bash
conda list -e > enviroment.yml
```

Create new enviroment
mamba create -n 'enviroment'

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
mamba install 'package' OR mamba install package package2
```