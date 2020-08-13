### Dockerfile
> FROM hello_from_igor #Здесь указываем от куда 

> WORKDIR /test #Название рабочей директории

> COPY . . #Куда копируем

> CMD «echo» «hello from igor». #Что выводим

Так же в докерфайл применяются и другие инструкции, например: 
- RUN = для выполнения команды из терминала контейнера.
- MAINTAINER = при необходимости здесь указываем имя автора и email.
- ADD = копирует файлы и папки в контейнер

### docker-compose.yml 
- имеет формат файла yml
- не забываем про отступы в два пробела

> version: "3"
> services:
> php_5.6: 
  > (--)build:
  > context: /Users/admin/LearnQA_Docker/dir_for_bind  #указываем путь, где находится файл
  > dockerfile: /Users/admin/LearnQA_Docker/dockerfile_1/Dockerfile  #указываем путь к ДокерФайлу php 5.6
  > image: php 5.6-cli  #указываем название образа, который получится в процессе билда
  > container_name:php_container_v1  #имя контейнера, который будет стартовать от образа
  > command: php counter.php

> php_5.3:
  > build:
  > context: /Users/admin/LearnQA_Docker/dir_for_bind  #указываем путь, где находится файл
  > dockerfile: /Users/admin/LearnQA_Docker/dockerfile_2/Dockerfile  #указываем путь к ДокерФайлу php 5.3
  > image: php 5.3-cli  #указываем название образа, который получится в процессе билда
  > container_name:php_container_v2  #имя контейнера, который будет стартовать от образа
  > command: php counter.php

 
