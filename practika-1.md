# Практическое занятие №1. Введение, основы работы в командной строке

Цель работы: Научиться выполнять простые действия с файлами и каталогами в Linux из командной строки. Сравнить работу в командной строке Windows и Linux.

## Задача 1

Вывести отсортированный в алфавитном порядке список имен пользователей в файле passwd (вам понадобится grep).

Решение:
```
labex:project/ $ grep -o '^[^:]*' /etc/passwd | sort
_apt
avahi
backup
bin
colord
daemon
games
gnats
irc
labex
list
lp
mail
man
messagebus
mongodb
mysql
news
nobody
proxy
pulse
redis
root
rtkit
saned
sshd
sync
sys
systemd-network
systemd-resolve
systemd-timesync
tcpdump
usbmux
uucp
www-data

```
## Задача 2

Вывести данные /etc/protocols в отформатированном и отсортированном порядке для 5 наибольших портов, как показано в примере ниже:

```
[root@localhost etc]# cat /etc/protocols ...
142 rohc
141 wesp
140 shim6
139 hip
138 manet
```
Решение:
```
labex:project/ $ grep -v '^#' /etc/protocols | awk '{print $2, $1}' | sort -rn | head -5
142 rohc
141 wesp
140 shim6
139 hip
138 manet
```

## Задача 3

Написать программу banner средствами bash для вывода текстов, как в следующем примере (размер баннера должен меняться!):

```
[root@localhost ~]# ./banner "Hello from RTU MIREA!"
+-----------------------+
| Hello from RTU MIREA! |
+-----------------------+
```
bash:
```bash
#!/bin/bash
if [ $# -eq 0 ]; then
    echo "Использование: $0 \"текст для вывода\""
    exit 1
fi

text="$*"
len=$(( ${#text} + 2 ))
line=$(printf '+%*s+' "$len" "" | tr ' ' '-')

echo "$line"
echo "| $text |"
echo "$line"
```
Terminal:
```
labex:project/ $ nano banner
labex:project/ $ chmod +x banner
labex:project/ $ ./banner 'Hello from RTU MIREA!'
+-----------------------+
| Hello from RTU MIREA! |
+-----------------------+
labex:project/ $ 
```

## Задача 4

Написать программу для вывода всех идентификаторов (по правилам C/C++ или Java) в файле (без повторений).

Пример для hello.c:

```
h hello include int main n printf return stdio void world
```
Решение:

idents.sh
```idents.sh
#!/bin/bash
if [ $# -eq 0 ]; then
    echo "Использование: $0 <файл>"
    exit 1
fi

grep -oE '[A-Za-z_][A-Za-z0-9_]*' "$1" | sort -u | tr '\n' ' '
echo
```
hello.c
```hello.c
#include <stdio.h>

int main(void) {
    int n = 5;
    printf("Hello, world!\n");
    return 0;
}
```
Terminal
```
labex:project/ $ nano idents.sh
labex:project/ $ chmod +x idents.sh        
labex:project/ $ nano hello.c
labex:project/ $ ./idents.sh hello.c
h Hello include int main n printf return stdio void world 
```


## Задача 5

Написать программу для регистрации пользовательской команды (правильные права доступа и копирование в /usr/local/bin).

Например, пусть программа называется reg:

```
./reg banner
```

В результате для banner задаются правильные права доступа и сам banner копируется в /usr/local/bin.

Решение:
reg
```reg
#!/bin/bash
if [ $# -ne 1 ]; then
    echo "Использование: $0 <файл>" >&2
    exit 1
fi
if [ ! -f "$1" ]; then
    echo "Ошибка: файл '$1' не найден" >&2
    exit 1
fi
sudo install -m 755 "$1" /usr/local/bin/
echo "Команда '$1' успешно зарегистрирована в /usr/local/bin"
```
banner
```banner
echo -e '#!/bin/bash\necho "this banner"' > banner
```
Tirminal
```
labex:project/ $ nano reg
labex:project/ $ chmod +x reg
labex:project/ $ nano banner
labex:project/ $ ./reg banner
Команда 'banner' успешно зарегистрирована в /usr/local/bin
```
Terminal

## Задача 6

Написать программу для проверки наличия комментария в первой строке файлов с расширением c, js и py.

## Задача 7

Написать программу для нахождения файлов-дубликатов (имеющих 1 или более копий содержимого) по заданному пути (и подкаталогам).

## Задача 8

Написать программу, которая находит все файлы в данном каталоге с расширением, указанным в качестве аргумента и архивирует все эти файлы в архив tar.

## Задача 9

Написать программу, которая заменяет в файле последовательности из 4 пробелов на символ табуляции. Входной и выходной файлы задаются аргументами.

## Задача 10

Написать программу, которая выводит названия всех пустых текстовых файлов в указанной директории. Директория передается в программу параметром. 




