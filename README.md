pip3 install virtualenv

virtualenv -p /usr/bin/python3.7 jupyter_env

source jupyter_env/bin/activate

pip install jupyterlab

jupyter lab
