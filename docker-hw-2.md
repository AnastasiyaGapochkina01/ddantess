1) Запустить контейнер со следующими параметрами
- image `php:8.2-apache`
- имя `php-web-1`
- внутри контейнера по пути `/var/www/index.php` должен лежать файл с содержимым
```php
<?php
phpinfo();
?>
```
- маппинг портов `8000:80`

Проверить, что контейнер работоспособен
```bash
$ curl -I 127.0.0.1:8000
```
корректный ответ
```
HTTP/1.1 200 OK
Date: Thu, 10 Jul 2025 03:28:13 GMT
Server: Apache/2.4.62 (Debian)
X-Powered-By: PHP/8.2.29
Content-Type: text/html; charset=UTF-8
```
2) Запустить контейнер со следующими параметрами
- image: `python:3.12`
- имя `say-hello-py-1`
- внутри контейнера по пути `/app/main.py` должен лежать файл с содержимым
```python
#!/usr/bin/python
import socket
import os
import pwd
user_name = pwd.getpwuid(os.getuid())[0]
host_name = socket.gethostname()
print(f"Hello, {user_name} you inside in {host_name}")
```
Проверить, что контейнер работоспособен - зайти в контейнер и выполнить команду
```bash
python /app/main.py
```
корректный ответ
```
Hello, root you inside in 1adc7f445dc9
```
где `1adc7f445dc9` - id вашего контейнера
3) Создать image на основе `python:3.11-bookworm`:
- установить пакеты: `build-essential curl libsqlite3-0`
- скопировать файл `geolib.c` в директорию `/src/`
- скомпилировать командой
```bash
gcc -O3 -shared -o geolib.so -fPIC $(python3-config --cflags) geolib.c
```
запустить из image контейнер, зайти в него и проверить, есть ли в директории `/src` файл `geolib.so`
4) Запустить контейнер со следующими параметрами
- image: `redis`
- имя `cache-1`
- данные redis сохраняются в папку `~/redis-data` на хосте

Затем
- зайти в контейнер и выполнить
```
# redis-cli
> SET docker "works"
> GET docker
```
- остановить и удалить контейнер
- запустить новый контейнер из image `redis:8.0.3` с теми же данными
- зайти в новый контейнер и проверить, что заданное значение `docker` сохранилось
5) Запустить контейнер со следующими параметрами
- image: `postgres:15`
- имя `db-1`
- маппинг портов `6432:5432`
- пароль админа `mydbpass`

Затем
- попробовать подключиться к постгресу из другого контейнера
```
docker run -it --rm --link db-1:postgres postgres psql -h postgres -U postgres
```
