# pyenv
> reference: https://github.com/pyenv/pyenv

> https://realpython.com/intro-to-pyenv/

> commands: https://github.com/pyenv/pyenv/blob/master/COMMANDS.md

## prepare environment
> https://github.com/pyenv/pyenv/wiki#suggested-build-environment

### for Mac OS X
```
brew install openssl readline sqlite3 xz zlib

brew update
brew install pyenv

## for .zsh shell, Make sure that your terminal app runs the shell as a login shell.
echo 'eval "$(pyenv init --path)"' >> ~/.zprofile
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
```

## Basic GitHub Checkout
### for Bash shell
```
# clone git
$ git clone https://github.com/pyenv/pyenv.git ~/.pyenv

# setup environment
#!!!!! ubuntu 改 ~/.profile or ~/.bashrc
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
# 放 .bashrc
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc

# Add pyenv init to your shell
$ echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bash_profile
# 放 .bashrc
$ echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bashrc

# Restart your shell so the path changes take effect.
$ exec "$SHELL"

# Install Python build dependencies
reference: https://github.com/pyenv/pyenv/wiki

# Install Python versions into $(pyenv root)/versions
$ pyenv install 2.7.8
```

## pyenv-virtualenv
```
brew install pyenv-virtualenv
```

## Usage
> https://realpython.com/intro-to-pyenv/

```
pyenv local $version
pyenv which python
pyenv which pip

if the version not change, run below method or restart terminal:
$ pyenv activate <environment_name>
$ pyenv deactivate

by name not python version number
$ pyenv virtualenv 3.6.8 projectName
$ pyenv local projectName
$ python -V
```

