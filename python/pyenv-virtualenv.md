# pyenv-virtualenv
> reference: https://github.com/pyenv/pyenv-virtualenv

## install
```
# Check out pyenv-virtualenv
$ git clone https://github.com/pyenv/pyenv-virtualenv ~/.pyenv/plugins/pyenv-virtualenv

# pyenv virtualenv-init for auto-active
$ echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bash_profile
# 放 .bashrc
$ echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc

# Restart your shell to enable pyenv-virtualenv
$ exec "$SHELL"
```

## usage
> reference: https://github.com/pyenv/pyenv-virtualenv#usage

```
# Using pyenv virtualenv with pyenv
$ pyenv virtualenv 2.7.10 my-virtual-env-2.7.10

# Create virtualenv from current version
$ pyenv virtualenv venv34

# 將專案指令到這個virtualenv
$ pyenv shell hdp

# 查全部的virtualenvs，可用來確認當下的專案是否有設定好virtualenv
$ pyenv virtualenvs

# 設定載入 virtualenv
※ 在bash設定 eval "$(pyenv virtualenv-init -)"
※ 就可以在.python-version設定完整名稱自動載入 ex. 3.7.1/envs/hdp 看pyenv virtualenvs
$ pyenv activate <name>
$ pyenv deactivate
```
