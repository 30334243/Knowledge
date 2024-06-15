## Docker без root
1. Создать группу **docker**:
~~~
sudo groupadd docker
~~~
2. Добавить пользователя в группу **docker**:
~~~
sudo usermod -aG docker $USER
~~~
3. Выйти из системы и зайти снова
