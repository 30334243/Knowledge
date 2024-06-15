## Поиск hex последовательности в диретории**
~~~
LANG=C grep -UL "\x1a\x43\x47\x50" *
~~~
- **"-U or --binary"** ***do not strip CR characters at EOL (MSDOS/Windows)***
- **"-L"** ***print only names of FILEs with no selected lines***
## Поиск hex последовательности в диретории и копирование в директорию
~~~
LANG=C grep -UL "\x1a\x43\x47\x50" * | xargs -d "\n" cp -t ~/
~~~
