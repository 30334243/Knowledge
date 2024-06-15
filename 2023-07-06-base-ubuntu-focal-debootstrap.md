## Базовый образ Ubuntu-focal (debootstrap)
### ОС Ubuntu
1. Установка **debootstrap**  для установки базовой системы в установленной системе в выбранном подкатологе установленной системы:
~~~
sudo apt install debootstrap
~~~
2. Установка **docker** автоматического развертывания приложения в виде переносимых автономных контейнеров:
~~~
sudo apt install docker.io
~~~
3. Сборка **chroot**-окружения:
~~~
sudo debootstrap focal /var/docker-chroot https://mirror.leaseweb.com/ubuntu/
~~~
4. Создание образа:
~~~
sudo tar -C /var/docker-chroot -cpf - . | sudo docker import - ubuntu:focal--change "ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin" --change 'CMD ["/bin/bash"]'
~~~
5. Сохранить образ в **tar.gz**:
~~~
docker save --output ubuntu-focal.tar.gz ubuntu:focal
~~~
### OC любая другая
6. Загрузить образ:
~~~
docker load --input ubuntu-focal.tar.gz
~~~
7. Войти в созданный образ:
~~~
docker run -it --rm ubuntu-focal
~~~
