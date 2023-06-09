# Контейнеризация

ДЗ по семинару № 1. 
студент: Горбунов Владимир Федорович. 

Задание: необходимо продемонстрировать изоляцию одного и того же приложения (как решено на семинаре - командного интерпретатора) в одном из различных пространствах имен.
Формат сдачи ДЗ: предоставить доказательства выполнения задания посредством ссылки на google-документ с правами на комментирование/редактирование.
Результатом работы будет: текст объяснения, логи выполнения, история команд и скриншоты (важно придерживаться такой последовательности).


Для начала нужно создать папку,  в которой будут размещаться файлы нашего нового пространства.

mkdir Space

mkdir Space/bin


Затем поместим туда исполняемые файлы командного интерпретатора bash.

cp /bin/bash Space/bin


Создадим там также папочки для хаанения зависимостей.

 mkdir Space/lib

 mkdir Space/lib64


Затем нужно посмотреть библотеки, от которых мы будем зависеть.

ldd /bin/bash

Затем эти зависимости копируем к себе в папку 

cp /lib/x86_64-linux-gnu/libtinfo.so.6 Space/lib

cp /lib/x86_64-linux-gnu/libc.so.6 Space/lib

cp /lib64/ld-linux-x86-64.so.2 Space/lib64


Затем посмотрим библотеки ls.

ldd /bin/ls

И скопировать их к себе в Space.

cp /lib/x86_64-linux-gnu/libselinux.so.1 Space/lib

cp /lib/x86_64-linux-gnu/libc.so.6 Space/lib

cp /lib/x86_64-linux-gnu/libpcre2-8.so.0 Space/lib

cp /lib64/ld-linux-x86-64.so.2 Space/lib64


Теперь можно попробовать поменять корень.

chroot Space/

<img width="2048" alt="Снимок экрана 2023-05-18 в 14 00 37" src="https://github.com/VladimirGorF/Conteinerization/assets/110591063/5106f6c6-7db3-4a3a-a9fb-696b6b2f698d">


Тепеь попробуем заизолироваться по сети. Для это посмотрим, что у нас с ними.

exit 

ip a

<img width="2048" alt="Снимок экрана 2023-05-18 в 14 10 51" src="https://github.com/VladimirGorF/Conteinerization/assets/110591063/af2cda74-fe66-4312-ba3b-4c345c85bd62">



Теперь применим команду.

unshare --net --pid --fork --mount-proc /bin/bash

Результат
<img width="2048" alt="Снимок экрана 2023-05-18 в 14 47 14" src="https://github.com/VladimirGorF/Conteinerization/assets/110591063/2a9af9bf-4e1b-4197-bbbe-a0d6d622ec77">

Теперь посмотрим процеессы. У нас появился процесс за номером 1. Значит мы в новом простанстве осущестялвяем самостоятельные процессы.

<img width="2048" alt="Снимок экрана 2023-05-18 в 14 48 21" src="https://github.com/VladimirGorF/Conteinerization/assets/110591063/7787c8af-bd52-4557-8ff9-939f499181c6">









