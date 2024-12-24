#Macos 安装
### 1. 安装 homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 2. 安装 mkdocs
```bash
pip install mkdocs-material

zsh: command not found: pip

where pip3
/usr/local/bin/pip3
/usr/local/bin/pip3
/usr/bin/pip3
```
尝试用pip3安装

```bash
pip3 install mkdocs-material


[notice] A new release of pip is available: 24.2 -> 24.3.1
[notice] To update, run: python3.13 -m pip install --upgrade pip
error: externally-managed-environment

× This environment is externally managed
╰─> To install Python packages system-wide, try brew install
    xyz, where xyz is the package you are trying to
    install.
    
    If you wish to install a Python library that isn't in Homebrew,
    use a virtual environment:
    
    python3 -m venv path/to/venv
    source path/to/venv/bin/activate
    python3 -m pip install xyz
    
    If you wish to install a Python application that isn't in Homebrew,
    it may be easiest to use 'pipx install xyz', which will manage a
    virtual environment for you. You can install pipx with
    
    brew install pipx
    
    You may restore the old behavior of pip by passing
    the '--break-system-packages' flag to pip, or by adding
    'break-system-packages = true' to your pip.conf file. The latter
    will permanently disable this error.
    
    If you disable this error, we STRONGLY recommend that you additionally
    pass the '--user' flag to pip, or set 'user = true' in your pip.conf
    file. Failure to do this can result in a broken Homebrew installation.
    
    Read more about this behavior here: <https://peps.python.org/pep-0668/>

note: If you believe this is a mistake, please contact your Python installation or OS distribution provider. You can override this, at the risk of breaking your Python installation or OS, by passing --break-system-packages.
hint: See PEP 668 for the detailed specification.

```
推荐方式是使用虚拟环境

```bash
python3 -m venv ~/venv
source ~/venv/bin/activate
##permanent add to ~/.zshrc
echo 'export PATH="~/venv/bin/venv/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
python3 -m pip install mkdocs-material
```
备选方式安装pipx

```bash
brew install pipx
pipx install mkdocs-material
```
验证安装

```bash
mkdocs --version
## list all commands
mkdocs -h
```