# test

cd /usr/src
wget https://www.python.org/ftp/python/3.8.12/Python-3.8.12.tgz
tar xzf Python-3.8.12.tgz
cd Python-3.8.12

./configure --with-openssl=/usr/local/openssl11


make
sudo make altinstall

python3.8 -c "import ssl; print(ssl.OPENSSL_VERSION)"


jupyter lab --generate-config

