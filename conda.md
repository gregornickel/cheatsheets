# Conda

Most important commands of the conda package and environment manager.

## Virtual Environments

### Setup an Environment

- Create a new environment with a specific python version `conda create --name ENVNAME python=3.9`
- Create an environment from an `environment.yml` file `conda env create --file environment.yml`
- Delete an entire environment `conda remove --name ENVNAME --all`

### Work with Environments

- Activate a conda environment `conda activate ENVNAME`
- Deactivate current environment `conda deactivate`
- List all packages in the active environment `conda list`
- List all packages in a named environment `conda list --name ENVNAME`
- Search for a package (version number is optional) `conda search PKGNAME=1.0.4`
- Install package (no version number results in the most recent version) `conda install PKGNAME==1.0.4`

### Share Environments

- Create an `environment.yml` file `conda env export --name ENVNAME > environment.yml`
- Create a copy/clone of an environment `conda create --clone ENVNAME --name NEWENVNAME`

## Installation

Install Anaconda or miniconda on your system. On Mac you can use homebrew and install miniconda with `brew install --cask miniconda`.

- Verify installation `conda info`
- Update conda `conda update -n base conda`

