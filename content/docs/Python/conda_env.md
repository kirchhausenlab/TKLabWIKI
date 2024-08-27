---
title: "Using Conda Environment"
date: 2024-08-15
draft: false
---

## Using Conda Environment

### Explanation

Conda is a popular package and environment management system that allows you to create and manage isolated environments for different projects. This guide will walk you through the steps of using Conda to create and manage environments.

Conda works by creating isolated environments that contain their own set of packages and dependencies. This allows you to work on different projects with different requirements without conflicts. Conda also provides a package manager that makes it easy to install, update, and remove packages within an environment.

Conda is a more powerful and flexible tool compared to Python's built-in `venv` module. It supports multiple programming languages, not just Python, and can manage both Python and non-Python packages. Conda also provides pre-built packages for many scientific computing libraries, making it a popular choice for data science and machine learning projects.

## Installing Conda

To use Conda, you first need to install it on your system. Follow these steps to install Conda:

1. Visit the [Conda website](https://docs.conda.io/en/latest/miniconda.html) and download the appropriate installer for your operating system.
2. Run the installer and follow the instructions to complete the installation process.

## Install Miniconda for different OS

- # Windows

```powershell
(New-Object Net.WebClient).DownloadFile('https://repo.anaconda.com/miniconda/Miniconda3-latest-Windows-x86_64.exe', 'Miniconda3-latest-Windows-x86_64.exe')
"start Miniconda3-latest-Windows-x86_64.exe /InstallationType=JustMe /RegisterPython=0 /S /D=C:\Miniconda3"
```

- # Mac

```shell
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh
chmod +x Miniconda3-latest-MacOSX-x86_64.sh
bash Miniconda3-latest-MacOSX-x86_64.sh
$(HOME)/miniconda3/bin/conda init bash
source ~/.bashrc
```

- # Linux

```shell
curl -O https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
chmod +x Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
$(HOME)/miniconda3/bin/conda init bash
source ~/.bashrc
```

## Creating a Conda Environment

Once Conda is installed, you can create a new environment using the following command:

```shell
conda create --name myenv
```

Replace `myenv` with the desired name for your environment. Conda will create a new environment with the specified name.

## Activating a Conda Environment

To activate a Conda environment, use the following command:

```shell
conda activate myenv
```

Replace `myenv` with the name of the environment you want to activate. Once activated, any packages you install or commands you run will be isolated within this environment.

## Installing Packages in a Conda Environment

To install packages in a Conda environment, use the following command:

```shell
conda install package_name
```

Replace `package_name` with the name of the package you want to install. Conda will automatically resolve dependencies and install the specified package in the active environment.

## Listing Conda Environments

To list all the Conda environments available on your system, use the following command:

```shell
conda env list
```

This will display a list of all the environments along with their paths.

## Deactivating a Conda Environment

To deactivate the currently active Conda environment, use the following command:

```shell
conda deactivate
```

This will return you to the base environment.

## Removing a Conda Environment

To remove a Conda environment, use the following command:

```shell
conda env remove --name myenv
```

Replace `myenv` with the name of the environment you want to remove. Conda will delete the specified environment and all its associated packages.
