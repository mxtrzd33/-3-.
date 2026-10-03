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
```bash

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

Terminal
```
labex:project/ $ nano reg
labex:project/ $ chmod +x reg
labex:project/ $ nano banner
labex:project/ $ ./reg banner
Команда 'banner' успешно зарегистрирована в /usr/local/bin
```

## Задача 6

Написать программу для проверки наличия комментария в первой строке файлов с расширением c, js и py.

check.sh
```bash

#!/bin/bash

dir="${1:-.}"

find "$dir" -type f \( -name '*.c' -o -name '*.js' -o -name '*.py' \) -print0 | while IFS= read -r -d '' file; do
    first=$(head -n 1 "$file")
    case "$file" in
        *.py) pattern='^[[:space:]]*#' ;;
        *)    pattern='^[[:space:]]*(//|/\*)' ;;
    esac

    if [[ $first =~ $pattern ]]; then
        echo "$file: comment found"
    else
        echo "$file: NO comment"
    fi
done
EOF
```
Terminal
```
abex:project/ $ nano check.sh
labex:project/ $ chmod +x check.sh
labex:project/ $ ./check.sh
labex:project/ $ ./check.sh
./hello.c: NO comment
```


## Задача 7

Написать программу для нахождения файлов-дубликатов (имеющих 1 или более копий содержимого) по заданному пути (и подкаталогам).

dublicat

```bash

#!/bin/bash

dir="${1:-.}"

find "$dir" -type f -exec md5sum {} + | sort | uniq -w32 --all-repeated=separate
```
Terminal
```
labex:project/ $ nano dublicat
labex:project/ $ chmod +x dublicat
labex:project/ $ mkdir t && echo abc > t/a && echo abc > t/b && echo xyz > t/c
labex:project/ $ ./dublicat t
0bee89b07a248e27c83fc3d5951213c1  t/a
0bee89b07a248e27c83fc3d5951213c1  t/b
```

## Задача 8

Написать программу, которая находит все файлы в данном каталоге с расширением, указанным в качестве аргумента и архивирует все эти файлы в архив tar.

archiv
```bash

#!/bin/bash

if [ $# -lt 1 ]; then
    echo "Usage: $0 extension [dir]" >&2
    exit 1
fi

ext="$1"
dir="${2:-.}"
archive="archive_${ext}.tar"

find "$dir" -type f -name "*.${ext}" -print0 | tar -cvf "$archive" --null -T -
```
Terminal
```
labex:project/ $ nano archiv
labex:project/ $ chmod +x archiv
labex:project/ $ ./archiv c
./hello.c
```

## Задача 9

Написать программу, которая заменяет в файле последовательности из 4 пробелов на символ табуляции. Входной и выходной файлы задаются аргументами.

zad9
```bash

#!/bin/bash

if [ $# -lt 2 ]; then
    echo "Usage: $0 input_file output_file" >&2
    exit 1
fi

sed 's/    /\t/g' "$1" > "$2"
```
Terminal
```
labex:project/ $ nano zad9
labex:project/ $ chmod +x zad9
labex:project/ $ ./zad9 hello.c hellonew.c  
```


## Задача 10

Написать программу, которая выводит названия всех пустых текстовых файлов в указанной директории. Директория передается в программу параметром. 

zad10
```bash

#!/bin/bash

find "${1:-.}" -type f -name "*.txt" -empty
```
Terminal
```
abex:project/ $ nano zad10
labex:project/ $ chmod +x zad10
labex:project/ $ touch t/101.txt t/102.txt t/103.txt; ./zad10 t
t/101.txt
t/102.txt
t/103.txt
```





