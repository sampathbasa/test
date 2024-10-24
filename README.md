export PATH="$HOME/.pyenv/bin:$PATH"

eval "$(pyenv init --path)"

eval "$(pyenv init -)"

eval "$(pyenv virtualenv-init -)"

source ~/.bashrc  # or ~/.bash_profile

pyenv commands | grep virtualenv



pyenv virtualenv 3.8.10 jupyter_env

pyenv activate jupyter_env

pip install jupyterlab

jupyter lab

