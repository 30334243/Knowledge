## Команды Docker
- Удалить все контейнеры:
~~~
docker rm $(docker ps -aqf status=exited)
~~~
- Удалить все образы:
~~~
docker rmi $(docker ps -aq)
~~~
