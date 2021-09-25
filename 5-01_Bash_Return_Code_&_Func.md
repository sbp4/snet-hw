# Домашнее задание к занятию "5.1 Базовое программирование на Bash. Коды возврата, функции." 


------
### Задание 1.

Напишите скрипт, который выводит на экран все числа от 1 до 100, которые делятся на 3.

*Пришлите получившийся скрипт в качестве ответа.*

***Ответ:***

#!/bin/bash

i=1
while [[ $i -le 33 ]]; do
    echo $(($i * 3))
    i=$(($i + 1))
done


------
### Задание 2.

Напишите скрипт, который каждые 5 секунд будет выводить на экран текущее время и содержимое файла `/proc/loadavg`.

*Пришлите получившийся скрипт в качестве ответа.*

***Ответ:***

#!/bin/bash

while sleep 5; 
do
  date '+%H:%M:%S' && cat /proc/loadavg;
done


------
### Задание 3.

Напишите функцию для подсчета среднего размера файла в директории. 

 - путь к директории должен передаваться параметром;
 - функция должна проверять, что такая директория существует, после чего выводить на экран средний размер файла в ней;
 - при подсчете необходимо исключить подиректории и символьные ссылки.

*Примечание:* Вывести размер файла можно с помощью `stat -c "%s" filename`.

*Пришлите получившийся код в качестве ответа.*

***Ответ:***

#!/bin/bash

directory_stat () {  
    if [[ -d $name ]]; then
       file_quan=`ls -la $name | grep "^-" | wc -l`
       file_size=`ls -la $name | grep "^-" | du -s | cut -f1`
       echo "$(($file_size/$file_quan))"
    fi
}

echo "insert directory name"
read name
directory_stat

------
## Дополнительные задания (со звездочкой*)

Эти задания дополнительные (не обязательные к выполнению) и никак не повлияют на получение вами зачета по этому домашнему заданию. Вы можете их выполнить, если хотите глубже и/или шире разобраться в материале.

### Задание 4.

Напишите свой калькулятор.

В нем реализуйте простейшие арифметические операции:  «+»; «-»; «*»; «/».
 
Считывание параметров реализуйте с помощью `read` и `select`.

*Примечение:* постарайтесь максимально защититься от ошибок, т.к. пользователи любят написать строку вместо числа.

*Пришлите получившийся скрипт в качестве ответа.*

***Ответ:***
