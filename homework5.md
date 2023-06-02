Студент Горбунов Владимир

Урок 5. Docker Compose и Docker Swarm

Задание 1:

1) создать сервис, состоящий из 2 различных контейнеров: 1 - веб, 2 - БД
Задание со звездочкой - повышенной сложности, это нужно учесть при выполнении (но сделать его необходимо).
** не обязательно 2) необходимо создать 3 сервиса в каждом окружении (dev, prod, lab)
** не обязательно 3) по итогу на каждой ноде должно быть по 2 работающих контейнера
4) выводы зафиксировать


Создадим docker-compose.yaml

version: "3.9"

services:
  db:
    image: mysql:latest
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: 1

  wordpress:
    image: wordpress:latest
    ports:
      - "8000:81"
    restart: always
  
Запустим развертывание контейнеров из нашего yaml-файла.

  docker-compose up -d
  
Посмотрим что получилось.
  docker-compose ps -a
  
  <img width="2048" alt="Снимок экрана 2023-06-02 в 13 31 07" src="https://github.com/VladimirGorF/Conteinerization/assets/110591063/da594e72-14a1-4282-b072-12fff4cb9496">

  
  
  
  
