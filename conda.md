# Conda

Most important commands of the conda package and environment manager.

## Virtual Environments

### Setup an Environment

- See a list of all environments `conda env list`
- Create a new environment with a specific python version `conda create -n ENVNAME python=3.9`
- Create an environment from an `environment.yml` file `conda env create -f environment.yml`
- Delete an entire environment `conda remove --name ENVNAME --all`

### Work with Environments

- Activate a conda environment `conda activate ENVNAME`
  The active environment is shown in parentheses () at the beginning of your command prompt: `(ENVNAME) $`
- Deactivate current environment `conda deactivate`
- List all packages in the active environment `conda list`
- List all packages if the environment is not activated `conda list -n ENVNAME`
- See if a specific package is installed `conda list -n ENVNAME numpy`
- Search for a package (version number is optional) `conda search PKGNAME=1.0.4`
- Install package (no version number results in the most recent version) `conda install PKGNAME==1.0.4`
- To use pip in an environment, run: `conda install -n ENVNAME pip`

### Share Environments

- Create an `environment.yml` file `conda env export --name ENVNAME > environment.yml`
- Create a copy/clone of an environment `conda create --clone ENVNAME --name NEWENVNAME`

## Installation

Install Anaconda or miniconda on your system. On Mac you can use homebrew and install miniconda with `brew install --cask miniconda`.

- Verify installation `conda info`
- Update conda `conda update -n base conda`

