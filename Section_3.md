### Dockerfile
> FROM hello_from_igor #Здесь указываем откуда 

> WORKDIR /test #Название рабочей директории

> COPY . . #Куда копируем

> CMD «echo» «hello from igor». #Что выводим

Так же в докерфайл применяются и другие инструкции, например: 
- RUN = для выполнения команды из терминала контейнера.
- MAINTAINER = при необходимости здесь указываем имя автора и email.
- ADD = копирует файлы и папки в контейнер

### docker-compose.yml 
- имеет формат файла yml
- не забываем про отступы.
- (--) два пробела
- (----) четыри пробела

> version: "3"

> services:

> (--)php_5.6: 

  > (----)build:
  
  > (------)context: /Users/admin/LearnQA_Docker/dir_for_bind  #указываем путь, где находится файл
  
  > (------)dockerfile: /Users/admin/LearnQA_Docker/dockerfile_1/Dockerfile  #указываем путь к ДокерФайлу php 5.6
  
  > (----)image: php 5.6-cli  #указываем название образа, который получится в процессе билда
  
  > (----)container_name:php_container_v1  #имя контейнера, который будет стартовать от образа
  
  > (----)command: php counter.php

> (--)php_5.3:

  > (----)build:
  
  > (------)context: /Users/admin/LearnQA_Docker/dir_for_bind  #указываем путь, где находится файл
  
  > (------)dockerfile: /Users/admin/LearnQA_Docker/dockerfile_2/Dockerfile  #указываем путь к ДокерФайлу php 5.3
  
  > (----)image: php 5.3-cli  #указываем название образа, который получится в процессе билда
  
  > (----)container_name:php_container_v2  #имя контейнера, который будет стартовать от образа
  
  > (----)command: php counter.php
  
## Еще немного из курса Docker от LearnQA 
 
##### Файл docker-compose должен начинаться с тега версии.
##### Мы используем "3" так как это - самая свежая версия на момент написания этого кода.

version: "3"

##### Следует учитывать, что docker-composes работает с сервисами.
##### 1 сервис = 1 контейнер.
##### Раздел, в котором будут описаны сервисы, начинается с 'services'.

services:

##### Сервис - контейнер, созданный из Dockerfile
##### Назвать его можно так, как хочется.
##### Понятное название сервиса помогает определить его роль.
##### Здесь мы, для именования соответствующего сервиса, используем ключевое слово 'python'.
  
python:

##### Ключевое слово "build" позволяет задать
##### путь к файлу Dockerfile, который нужно использовать для создания образа,
##### который позволит запустить сервис.
##### Здесь . соответствует текущему пути

build: . #указываем название образа, который получится в процессе билда
    
image: python_counter_service

container_name: python_counter_container  #имя контейнера, который будет стартовать от образа

##### Команда, которую нужно запустить после создания образа.
##### Следующая команда означает запуск python-скрипта
    
command: python counter.py
## Пример:
```
version: "3"

services:
  selenium:
    image: selenium/standalone-chrome:3.141.59
    container_name: selenium_server_works
    ports:
      - "4444:4444"
    logging:
      driver: none
  
  test_runner:
    build:
      context: /Users/<USER_NAME>/LearnQA_Docker/Autotests
      dockerfile: /Users/<USER_NAME>/LearnQA_Docker/compose_2/Dockerfile
    image: tests_run
    container_name: tests_works
    network_mode: "host"
 ```
 
 ### Mount bind и Mount volume, примеры запуска:
 ##### bind
```docker run -it --mount type=bind,src=$(pwd)/dir_for_bind/,target=/bind/ ubuntu bash```

##### volume
```docker run -it --mount type=volume,src=my_volume,target=/volume/ ubuntu bash```

### help
```docker container --help```

##### Запустить контейнер ubuntu и перейти в нее
```docker run -it ubuntu bash```

##### Список запущенных контейнеров
```docker container ls```

```docker ps # алиас для предыдушей записи```

##### Список всех контейнеров
```docker ps -a```

##### Удалить контейнер (если он остановлен)
```docker container rm [CID]```

##### Удалить все остановленные контейнеры
```docker container prune```

##### Запустить открепленный контейнер с именем
```docker run -it --name ubuntu_1 -d ubuntu bash```

##### Перейти в контейнер
```docker attach [CID]```

##### Выйти из контейнера не останавливая его
```CTRL+P``` , ```CTRL+Q```

##### Остановить контейнер
```docker container stop [CIP]```

##### Запустить контейнер
```docker container start [CIP]```

##### Запустить контейнер с удалением его из списка после остановки
```docker run -it --rm --name ubuntu_1 -d ubuntu bash```
 
 
 
 
