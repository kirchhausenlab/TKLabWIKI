---
title: "Poetry: Python Dependency Management Made Easy"
date: 2024-08-15
draft: false
---

## Poetry

### Explanation

Poetry is a tool for dependency management and packaging in Python. It allows you to declare the libraries your project depends on and it will manage (install/update) them for you.

Poetry uses a file called `pyproject.toml` to declare your project dependencies. It then creates a virtual environment and installs the specified dependencies in that environment. Poetry also locks the versions of your dependencies to ensure reproducibility.

Poetry simplifies the process of managing Python projects. It handles dependency resolution, virtual environment creation, and package management in one tool. This makes it easier to set up consistent development environments and share your project with others.

With Poetry, you can easily:

- Manage project dependencies
- Create and manage virtual environments
- Build and publish packages
- Handle dependency conflicts
- Lock dependencies for reproducible builds

### Benefits

- **Dependency Resolution**: Automatically resolves and installs project dependencies.
- **Virtual Environment Management**: Creates and manages virtual environments for you.
- **Reproducibility**: Uses a lock file to ensure consistent installations across different systems.
- **Build and Publish**: Simplifies the process of building and publishing Python packages.

### Installation

<img src ="https://user-images.githubusercontent.com/25181517/192158606-7c2ef6bd-6e04-47cf-b5bc-da2797cb5bda.png" width="15" height="15">

1. **Install pyenv**:

   ```bash
   curl https://pyenv.run | bash
   ```

2. **Set up your shell environment**:

   ```bash
   export PYENV_ROOT="$HOME/.pyenv"
   [[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
   eval "$(pyenv init -)"
   eval "$(pyenv virtualenv-init -)"
   ```

3. **Restart your shell**:
   ```bash
   source ~/.bashrc
   ```

#### Install Python with pyenv

<img src ="https://user-images.githubusercontent.com/25181517/183423507-c056a6f9-1ba8-4312-a350-19bcbc5a8697.png" width="12" height="12">

1. **Install Python 3.10**:

   ```bash
   pyenv install 3.10
   ```

2. **If you encounter errors, install these dependencies**:

   ```bash
   sudo apt-get install -y make build-essential libssl-dev zlib1g-dev \
   libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm libncurses5-dev \
   libncursesw5-dev xz-utils tk-dev libffi-dev liblzma-dev python-openssl
   ```

3. **Verify the installation**:
   ```bash
   pyenv versions
   ```

#### Install Poetry

1. **Create a virtual environment and install Poetry**:

   ```bash
   python3 -m venv $VENV_PATH
   $VENV_PATH/bin/pip install -U pip setuptools
   $VENV_PATH/bin/pip install poetry
   ```

2. **Create a new project and install dependencies**:

   ```bash
   poetry new my-project
   cd my-project
   poetry install
   ```

3. **Add project-specific dependencies**:

   ```bash
   poetry add pandas numpy matplotlib seaborn torch torchvision seaborn wandb ipykernel tifffile loguru loky h5py cloudpickle
   ```
