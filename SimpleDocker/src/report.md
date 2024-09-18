## __Part 1. Готовый докер__
---
+ Скачивание __nginx__
![screens/pullngin.png](screens/pullngin.png)
+ Проверка докер образа __nginx__
![screens/nginximag.png](screens/nginximag.png)
+ Запуск образа
![screens/nginxrun.png](screens/nginxrun.png)
+ Проверка запуска контейнера
![screens/psdock.png](screens/psdock.png)
+ Вывод информации о контейнере
![screens/inspect.png](screens/inspect.png)
    + Размер контейнера: __141559565 байт__
    ![screens/sizecont.png](screens/sizecont.png)
    + Замапленные порты контейнера: __80__
    ![screens/portscont.png](screens/portscont.png)
    + __IP__ контейнера: __172.17.0.2__
    ![screens/IPcont.png](screens/IPcont.png)
+ Остановка работы контейнера и проверка остановки
![screens/stopdockps.png](screens/stopdockps.png)
+ Запуск докера с замапленными портами 80 и 443
![screens/80443.png](screens/80443.png)
+ Проверка страницы nginx
![screens/local80.png](screens/local80.png)
+ Перезагрузка контейнера и проверка запуска
![screens/restartps.png](screens/restartps.png)
## __Part 2. Операции с контейнером__
---
+ _Вход в контейнер с помощью_ __exec__
![screens/exec1.png](screens/exec1.png)
+ _Чтение файла_ __nginx.conf__
![screens/nginxcat.png](screens/nginxcat.png)
+ _Новый __nginx.conf__ на локальной машине с выдачей статуса страницы_
![screens/confP2.png](screens/confP2.png)
+ _Копирование файла nginx в контейнер и его перезагрузка_
![screens/cprest.png](screens/cprest.png)
+ _Проверка выдачи страницы со статусом сервера_
![screens/status.png](screens/status.png)
+ _Команда для экспорта контейнера в файл_
  * __docker export silly_swartz > container.tar__
+ _Команда для остановки контейнера_
  * __docker stop 65e1d42bb390 silly_swartz__
+ _Удаление образа_
  ![screens/delimag.png](screens/delimag.png)
+ _Удаление остановленного контейнера_

  ![screens/delcont.png](screens/delcont.png)
+ _Импорт контейнера обратно_
  ![screens/import.png](screens/import.png)
+ _Запуск контейнера_
  ![screens/runafter.png](screens/runafter.png)
+ _Проверка страницы со статусом_

  ![screens/status2.png](screens/status2.png)
## __Part 3. Мини веб-сервер__
---
* Страница веб-сервера на Си
  ![screens/webserver .png](screens/webserver.png)
* Запуск образа с замапленным 81 портом
  ![screens/3zapusk.png](screens/3zapusk.png)
* Обновление ОС внутри контейнера
![screens/3obnova.png](screens/3obnova.png)
* Копирование конфигурационного файла и веб-сервера в контейнер
  + __docker cp nginx.conf "ID_CONT":/etc/nginx/__
  + __docker cp webserver.c "ID_CONT":/__
+ Установка компилятора, библиотеки и FastCGI
  * __docker exec "ID_CONT" apt-get install -y gcc spawn-fcgi libfcgi-dev__
+ Компиляция мини-сервера с выводом "Hello world"
  + __docker exec "ID_CONT" gcc webserver.c -lfcgi -o server__
+ Запуск spawn-fcgi на 8080 порту
  + __docker exec "ID_CONT" spawn-fcgi -p 8080 server__
+ Перезагрузка nginx внутри контейнера
  + __docker exec "ID_CONT" nginx -s reload__
+ Проверка страницы

  ![screens/3curl.png](screens/3curl.png)
## __Part 4. Свой докер__
---
* Содержимое докерфайла

  ![screens/dockfile.png](screens/dockfile.png)
* Скрипт для запуска веб сервера

  ![screens/start.png](screens/start.png)
* Построение образа
  ![screens/build1.png](screens/build1.png)
* Запуск с маппингом 81 порта на 80 и маппингом папки __./nginx__ и проверка запуска
  ![screens/mapping.png](screens/mapping.png)
* Проверка страниц сервера
  ![screens/end4.png](screens/end4.png)
## __Part 5. Dockle__
---
* Установка Dockle на Мас: ___brew install goodwithtech/r/dockle___
* Сборка контейнера: ___docker build -t bird:p5 .___
* Ошибка хранения секретов: ___dockle -ak NGINX_GPGKEY bird:p5___
* Содержимое докерфайла:
  ![screens/dock5.png](screens/dock5.png)
+ Вывод dokcle
  ![screens/dockle.png](screens/dockle.png)
## __Part 6. Базовый Docker Compose__
---
* Содержимое файла __docker-compose.yml__

  ![screens/yaml.png](screens/yaml.png)
* Запуск образов и проверка страницы
  ![screens/composeup.png](screens/composeup.png)
