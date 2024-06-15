## Скрипт автоматической сборки
  Автоматизация клонирования, сборка, изменения и добавление
(по определенным условиям) проекта.
1. Создать файл **build.py**
~~~
touch build.py
~~~
2. Импортировать модуль для работы с операционной системой
~~~
import os
~~~
3. Импортировать модуль для запуска внешних программа из кода **Python**
~~~
import subprocess
~~~
4. Установить модуль изменения цвета строк в терминале
~~~
pip install sty
~~~
5. Импортировать модуль **sty**
~~~
from sty import fg,bg,ef,rs
~~~
6. Добавить функцию заглушку
~~~
def Empty():None
~~~
7. Добавить функцию сборки cmake проекта
~~~
def SimpleCmake():
  subprocess.run(["cmake",".."])
  subprocess.run(["cmake","--build","."])
~~~
8. Добавить основную функцию **Build**
~~~
def Build(name,repo,func,cmake):
    if os.path.exists(name):
        print('{}"{}" уже существует{}'.format(fg.yellow,name,fg.rs))
        return
    
    cur_dir = os.path.abspath(os.curdir)

    subprocess.run(["git","clone",repo])
    os.chdir(name)

    func()

    if not os.path.exists("build"):
        os.mkdir("build")

    os.chdir("build")

    cmake()

    os.chdir(cur_dir)
~~~
