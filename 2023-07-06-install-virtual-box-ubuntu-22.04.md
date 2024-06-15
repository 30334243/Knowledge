## Установка VirtualBox ubuntu 22.04
~~~
sudo apt install gcc-12 g++-12
sudo ln -s /usr/bin/gcc-12 /usr/bin/gcc
sudo ln -s /usr/bin/g++-12 /usr/bin/g++-12
sudo apt install linux-headers-`uname -r` dkms virtualbox-dkms
sudo apt install virtualbox-ext-pack
~~~~~~
