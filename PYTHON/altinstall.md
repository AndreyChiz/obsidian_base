```sh
mkdir tmp
cd tmp
wget https://www.python.org/ftp/python/3.12.0/Python-3.12.0.tar.xz
tar xvf Python-3.12.0.tar.xz
cd Python-3.12.0/
sudo ./configure --enable-optimizations
make -j4
sudo make altinstall
cd /usr/local/bin/
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.11 1
sudo update-alternatives --install /usr/bin/python3 python3 /usr/local/bin/python3.12 2
sudo update-alternatives --list python3
sudo update-alternatives --config python3

python3.12 -m venv --copies myenv
```