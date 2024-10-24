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


#!/usr/bin/python
import sys
try:
    import yum
except ImportError as e:
    print(
        """
        ** There was a problem importing one of the Python modules required to run yum.
        The error leading to this problem was: {}
        Please install a package which provides this module, or verify that the module is installed correctly.
        It's possible that the above module doesn't match the current version of Python, which is: {}

        If you cannot solve this problem yourself, please go to the yum FAQ at: 
        http://y.baseurl.org/wiki/Faq
        """.format(e, sys.version),
        file=sys.stderr
    )
    sys.exit(1)

sys.path.insert(0, '/usr/share/yum-cli')
try:
    import yummain
    yummain.user_main(sys.argv[1:], exit_code=True)
except KeyboardInterrupt as e:
    print("\nExiting on user cancel.", file=sys.stderr)
    sys.exit(1)

```
#1/us/bin/python import sys try:
import yum
except ImportError:
print ›› sys.stderr,
"**
There was a problem importing one of the Python modules required to run yun. The error leading to this problem was:
Xs
Please install a package which provides this module, or verify that the module is installed correctly.
It's possible that the above module doesn't match the current version of Python, which is:
If you cannot solve this problem yourself, please go to the yum fag at :
http://y.baseur1.org/wiki/Faq
***% (sys. exc_value, sys. version)
sys. exit (1)
sys. path. insert(0, '/usr/share/yum-cli*) try:
import yummain
yummain. user _main(sys. argv[1:], exit_code=True)
except KeyboardInterrupt, e:
print » sys. stderr,
\\nExiting on user cancel."
sys. exit (1)
```


curl -O http://amazonlinux.default.amazonaws.com/2/core/latest/x86_64/packages/yum-3.4.3-167.amzn2.0.3.noarch.rpm
sudo rpm -ivh --replacepkgs yum-3.4.3-167.amzn2.0.3.noarch.rpm
yum --version
