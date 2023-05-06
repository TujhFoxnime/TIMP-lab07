* 1) Устанавливаем докер
*
* 2) проверяем работу докера с помощью sudo doker version
*
* 3) чтобы убрать sudo, добавляем пользвателя ос в группу с помощью: sudo usermod -aG docker egor
* \где docker-группа, а egor-пользователь
*
* 4) создаем пустые файлы:
* touch Dockerfile - для заупска докера
* touch hello_world.cpp - сама программа для вывода фразы
*
* 5) в докерфайле прописываем:
* FROM ubuntu:latest  - ос запуска
* WORKDIR /usr/src/app    - директория в котрой будет  запущен докер
* COPY . .   - первая точка - это откуда копируется, вторая - куда копируется (точка означает, что копирование будет осуществляться именно в этом файле)
* RUN apt-get update && \            -запуск программы вывода - обновление пакетов
*    apt-get install -y g++ && \     - добавляение компилятора
*    g++ -o hello hello_world.cpp   - компилятор выполнения - название операции - название файла в которой лежит программа
* CMD ["./hello"] - команда запуска
*
* 6) далее мы собираем образ:
* docker ps -a - посмотреть содержимые контейнеры
* docker images -посмотреть содержимые образы (оттуда мы и берем id)
* docker build . -сборка образа
* docker run <id_image> - запуск программы :
*
* egor@egor-120-1100er:~/TIMP-lab07$ sudo docker run 563ef8723dd3
* Hello World! - ВСЁ СРАБОТАЛО!
*
* docker rm <id_container> -удаление контейнера
* docker rmi <id_image> -удаление образа
*
* 7) далее создаем директорию .github/workflows для CI.yml
*
* 8) в CI.yml прописываем:
*
* name: Docker
*
* on:
*   push:
*     branches:
*       main
*
* jobs:
*   docker:
*     runs-on: ubuntu-latest
*
*     steps:
*       - uses: actions/checkout@v3
*
*       - name: Build  - имя операции
*         run: |
*           sudo docker build -t mytag .  - судо докер билд - сборка, далее указывается локальное местоположение файла
*           sudo docker run mytag -       - заупск проекта
*         
* 9) заливаем на гит
