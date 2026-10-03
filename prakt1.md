## Задача 1

Вывести отсортированный в алфавитном порядке список имен пользователей в файле passwd (вам понадобится grep).

```
cut -d ':' -f 1 passwd | sort
```
ИЛИ
```
grep -o "^[^:]*" passwd | sort           
```

## Задача 2

Вывести данные /etc/protocols в отформатированном и отсортированном порядке для 5 наибольших портов, как показано в примере ниже:

[root@localhost etc]# cat /etc/protocols ...

142 rohc

141 wesp

140 shim6

139 hip

138 manet

```
awk '{print $2, $1}' protocols | sort -rn | head -5
```

## Задача 3

Написать программу banner средствами bash для вывода текстов, как в следующем примере (размер баннера должен меняться!):

[root@localhost ~]# ./banner "Hello from RTU MIREA!"

+-----------------------+

| Hello from RTU MIREA! |

+-----------------------+

Перед отправкой решения проверьте его в ShellCheck на предупреждения.

```
nano banner

#!/bin/bash
text="$1"
dashes=$(echo "$text" | tr '[:print:]' '-')
echo "+--${dashes}--+"
echo "|  ${text}  |"
echo "+--${dashes}--+"

^X
Y
Enter

chmod +x banner
./banner 'Hellooooo!'
```

## Задача 4

Написать программу для вывода всех идентификаторов (по правилам C/C++ или Java) в файле (без повторений).

Пример для hello.c:

h hello include int main n printf return stdio void world

```
nano exercise4

#!/bin/bash
file="$1"
cat "$file" | tr -cs 'a-zA-Z_' '\n' | sort -u | tr '\n' ' '
echo ""

^X
Y
Enter

chmod +x exercise4

nano hello.c

#include <stdio.h>
int main() {
    printf("hello world\n");
    return 0;
}

^X
Y
Enter

./exercise4 hello.c

```

## Задача 5

Написать программу для регистрации пользовательской команды (правильные права доступа и копирование в /usr/local/bin).

Например, пусть программа называется reg:

./reg banner

В результате для banner задаются правильные права доступа и сам banner копируется в /usr/local/bin.

```
nano reg

#!/bin/bash
file="$1"
chmod +x "$file"
sudo cp "$file" /usr/local/bin/
echo "Done."

^X
Y
Enter

chmod +x reg
./reg exercise4
exercise4 hello.c

```

## Задача 6

Написать программу для проверки наличия комментария в первой строке файлов с расширением c, js и py.

```
nano exercise6

#!/bin/bash
first_line=$(head -1 "$1")
if [[ "$1" == *.c || "$1" == *.js ]]; then
    if [[ "$first_line" == //* ]]; then
        echo "There is comment";
    else
        echo "No comment";
    fi
elif [[ "$1" == *.py ]]; then
    if [[ "$first_line" == \#* ]]; then
        echo "There is comment";
    else
        echo "No comment";
    fi
fi

^X
Y
Enter

chmod +x exercise6
./exercise6 hello.c

```

## Задача 7

Написать программу для нахождения файлов-дубликатов (имеющих 1 или более копий содержимого) по заданному пути (и подкаталогам).

```
nano exercise7

#!/bin/bash
dir="$1"
find "$dir" -type f -printf "%f\t%p\n" | sort | awk -F'\t' 'count[$1]++ {print $2}'

^X
Y
Enter

chmod +x exercise7
./exercise7 /etc/

```

## Задача 8

Написать программу, которая находит все файлы в данном каталоге с расширением, указанным в качестве аргумента и архивирует все эти файлы в архив tar.

```
nano exercise8

#!/bin/bash
ext="$1"
tar -cvf archive.tar *."$ext"

^X
Y
Enter

chmod +x exercise8
./exercise8 c

```

## Задача 9

Написать программу, которая заменяет в файле последовательности из 4 пробелов на символ табуляции. Входной и выходной файлы задаются аргументами.

```
nano exercise9

#!/bin/bash
input_file="$1"
output_file="$2"
sed 's/    /\t/g' "$input_file" > "$output_file"

^X
Y
Enter

chmod +x exercise9
./exercise9 hello.c hello_tab.c


```

## Задача 10

Написать программу, которая выводит названия всех пустых текстовых файлов в указанной директории. Директория передается в программу параметром.

```
nano exercise10

#!/bin/bash
find "$1" -type f -size 0

^X
Y
Enter

chmod +x exercise10
./exercise10 /etc/
```
