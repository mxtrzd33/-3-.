# Практическое занятие №1. Введение, основы работы в командной строке

Цель работы: Научиться выполнять простые действия с файлами и каталогами в Linux из командной строки. Сравнить работу в командной строке Windows и Linux.

## Задача 1

Вывести отсортированный в алфавитном порядке список имен пользователей в файле passwd (вам понадобится grep).

<img width="1004" height="626" alt="image" src="https://github.com/user-attachments/assets/9c61e177-5dc3-4c2f-9a1f-f0789c04d273" />
<img width="1004" height="601" alt="image" src="https://github.com/user-attachments/assets/79f5ab92-a842-45b7-a71e-361ca860c91e" />

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
<img width="1004" height="158" alt="image" src="https://github.com/user-attachments/assets/03faf9ea-dc20-4d85-929b-87b97dc92eb4" />

## Задача 3

Написать программу banner средствами bash для вывода текстов, как в следующем примере (размер баннера должен меняться!):

```
[root@localhost ~]# ./banner "Hello from RTU MIREA!"
+-----------------------+
| Hello from RTU MIREA! |
+-----------------------+
```
<img width="764" height="58" alt="image" src="https://github.com/user-attachments/assets/66e00f7e-f314-4981-85d5-dcc1440f3c57" />
<img width="1004" height="285" alt="image" src="https://github.com/user-attachments/assets/d96ef556-fbbc-4b17-9da2-eb9f34ddbd13" />
<img width="827" height="50" alt="image" src="https://github.com/user-attachments/assets/90947dec-621b-4373-a0a6-efa3363116d0" />
<img width="1004" height="343" alt="image" src="https://github.com/user-attachments/assets/c6b1de6d-b6af-4147-bf15-c0a138365546" />


## Задача 4

Написать программу для вывода всех идентификаторов (по правилам C/C++ или Java) в файле (без повторений).

Пример для hello.c:

```
h hello include int main n printf return stdio void world
```
<img width="1016" height="34" alt="image" src="https://github.com/user-attachments/assets/e9a9c8fc-ca04-44f3-be7c-de7184919665" />
<img width="974" height="231" alt="image" src="https://github.com/user-attachments/assets/78e4f657-5cab-430b-8e08-fbf8f0cafd5c" />
<img width="1004" height="87" alt="image" src="https://github.com/user-attachments/assets/b817e226-4050-482e-98db-7b23fcd4c0e2" />


## Задача 5

Написать программу для регистрации пользовательской команды (правильные права доступа и копирование в /usr/local/bin).

Например, пусть программа называется reg:

```
./reg banner
```

В результате для banner задаются правильные права доступа и сам banner копируется в /usr/local/bin.

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




