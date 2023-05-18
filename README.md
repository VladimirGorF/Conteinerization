# Контейнеизация

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
root@vg-VirtualBox:/home/vg# mkdir Space/lib
root@vg-VirtualBox:/home/vg# mkdir Space/lib64


Затем нужно посмотреть библотеки от которых мы будем зависеть.
ldd /bin/bash

Затем эти зависимости копиуем к себе в папку 
vg@vg-VirtualBox:~$ cp /lib/x86_64-linux-gnu/libtinfo.so.6 Space/lib
vg@vg-VirtualBox:~$ cp /lib/x86_64-linux-gnu/libc.so.6 Space/lib
vg@vg-VirtualBox:~$ cp /lib64/ld-linux-x86-64.so.2 Space/lib64

Затем нужно посмотреть библотеки от которых мы будем зависеть.
ldd /bin/ls

И скопировать их к себе в Space.
vg@vg-VirtualBox:~$ cp /lib/x86_64-linux-gnu/libselinux.so.1 Space/lib
vg@vg-VirtualBox:~$ cp /lib/x86_64-linux-gnu/libc.so.6 Space/lib
vg@vg-VirtualBox:~$ cp /lib/x86_64-linux-gnu/libpcre2-8.so.0 Space/lib
vg@vg-VirtualBox:~$ cp /lib64/ld-linux-x86-64.so.2 Space/lib64

Тепеь можно попровбовать поменять корень.
chroot Space/
<img width="2048" alt="Снимок экрана 2023-05-18 в 14 00 37" src="https://github.com/VladimirGorF/Conteinerization/assets/110591063/5106f6c6-7db3-4a3a-a9fb-696b6b2f698d">




