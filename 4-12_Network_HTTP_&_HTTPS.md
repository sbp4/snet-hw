# Домашнее задание к занятию "4.12 HTTP/HTTPS"

**

### Задание 1.

Какие коды ответов HTTP лучше соответствуют описанным ситуациям?

- Данная страница не найдена;
- Страница была перенесена на новый сайт;
- Ресурс удален;
- Пользователь не авторизован для просмотра страницы;
- Превышен лимит запросов от пользователя.

*Приведите ответ в свободной форме.*

***Ответ:***

- 404 - Not Found;
- 301 - Moved Permanently; 
- 410 - Gone;
- 401 - Unauthorized;
- 429 - Too Many Requests

### Задание 2.

1. Установите Nginx.

`sudo apt-get install nginx`

2. Сгенерируйте сертификат для него указав `localhost` в качестве `CN`.

`sudo openssl req -x509 -newkey rsa:4096 -keyout /etc/nginx/cert.key -out /etc/nginx/cert.pem -days 365`

3. Отредактируйте модуль `http` в файле `/etc/nginx/nginx.conf`.

```
http {
    gzip on;
    server {
        listen 80 default_server;
        root   /var/www/public;
        listen  443 ssl http2 default_server;
        server_name  localhost;
        ssl_certificate  /etc/nginx/cert.crt;
        ssl_certificate_key /etc/nginx/cert.key;
        ssl_protocols   TLSv1 TLSv1.1 TLSv1.2;
        ssl_ciphers   HIGH:!aNULL:!MD5;
        location / {
            index index.html;
        }
    }
}
```

4. Создайте файл `/var/www/public/index.html` c содержимым.

```
<h>It works</h>
```

5. Зайдите на страницу в браузере, пропустив сообщение о неработающем сертификате.

*Пришлите скриншот работающей страницы https://localhost.*


***Ответ:***

<a href="https://ibb.co/V3V4B0p"><img src="https://i.ibb.co/cxJnTKX/2-0.png" alt="2-0" border="0"></a>

------

### Задание 3.

Измените конфигурацию сервера добавив переадресацию c Вашего сервера на сайт `netology.ru`.
```
location / {
  return 301 https://netology.ru;
}
```

*Используя curl сделайте запрос к своему серверу и в качестве ответа пришлите скриншот с 301 ответом.*


***Ответ:***

<a href="https://ibb.co/txL7s3G"><img src="https://i.ibb.co/KLKMqmP/3-0.png" alt="3-0" border="0"></a>

---

## Дополнительные задания (со звездочкой*)
Эти задания дополнительные (не обязательные к выполнению) и никак не повлияют на получение вами зачета по этому домашнему заданию. Вы можете их выполнить, если хотите глубже и/или шире разобраться в материале.

### Задание 4.

Используя документацию https://httpd.apache.org/docs/current/ установите `apache2` веб-сервер.

Сделайте задание 2, добившись аналогичной работы сервера.

*Пришлите получившуюся конфигурацию в качестве ответа.*

