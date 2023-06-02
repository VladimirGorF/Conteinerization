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
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: 1
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: 1

  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    ports:
      - "8000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: 1
      WORDPRESS_DB_NAME: wordpress
volumes:
  db_data: {}
  
Запустим развертывание контейнеров из нашего yaml-файла.

  docker-compose up -d
  
  
  
  
  
