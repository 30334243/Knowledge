## Решение ошибки <span style="color:red"> **Windows is hibernated, refused to mount**</span>
~~~
sudo ntfsfix /dev/sda1
~~~
или
~~~
sudo mount -t ntfs-3g -o remove_hiberfile /dev/sda1 /mnt/hdd
~~~
