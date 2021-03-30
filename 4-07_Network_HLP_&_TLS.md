# Домашнее задание к занятию "4.7 Высокоуровневые протоколы"

------

### Задание 1.

Какие порты используются протоколами:
- Telnet;
- SSH;
- FTP;
- SNMP;

*Приведите ответ в виде списка портов.*

***Ответ:***

1. Telnet - по-умолчанию 23 порт TCP;
2. SSH - по-умолчанию 22 порт TCP;
3. FTP - по-умолчанию 20 и 21 порт TCP;
4. SNMP - по-умолчанию 161 и 162 порт UDP, с использованием шифрования DLTS или TLS - 10161 и 10162 порт UDP;

------

### Задание 2.

Какой по счету уровень модели OSI называется прикладным (`application layer`)?

*Зашифруйте ответ с помощью ключа: {5, 21}.*

***Ответ:***

7

------

### Задание 3.

Создайте свой корневой сертификат, добавьте его в систему. 

Затем подпишите им свой сертификат.


**1. Генерируем ключ**

```
- openssl genrsa -out ca.key 2048
```

***Ответ:***

<a href="https://ibb.co/rQjwwsw"><img src="https://i.ibb.co/fXgxxvx/3-1.png" alt="3-1" border="0"></a>

**2. Генерируем корневой сертификат. Поля в сертификате указываем любые.**

```
- openssl req -x509 -new -nodes -key ca.key -sha256 -days 720 -out ca.pem
```

***Ответ:***

<a href="https://ibb.co/jrnsXdy"><img src="https://i.ibb.co/QKytwZP/3-2.png" alt="3-2" border="0"></a>

**3. Сразу же сделаем сертификат в форме `crt`**

```
- openssl x509 -in ca.pem -inform PEM -out ca.crt
```

***Ответ:***

<a href="https://ibb.co/0KggtLJ"><img src="https://i.ibb.co/T1VVLGh/3-3.png" alt="3-3" border="0"></a>

**4. Далее установим сертификат в систему. Ниже пример для `Ubuntu`/`Debian` систем**

```
- sudo cp ca.crt /usr/local/share/ca-certificates/myca.crt && sudo update-ca-certificates
```

***Ответ:***

<a href="https://ibb.co/yS2F4sy"><img src="https://i.ibb.co/Vm6YwBS/3-4.png" alt="3-4" border="0"></a>

**5. Приступим к выпуску самого сертификата:**

**5.1. Генерируем ключи**

```
- openssl genrsa -out certificate.key 2048
```

***Ответ:***

<a href="https://ibb.co/V9K6Pxv"><img src="https://i.ibb.co/YQrgqXt/3-5.png" alt="3-5" border="0"></a>

**5.2. На основе ключа создаем `CSR`**

```
- openssl req -new -key certificate.key -out certificate.csr
```

***Ответ:***

<a href="https://ibb.co/mJ1YZm7"><img src="https://i.ibb.co/1Zhpy3x/3-6.png" alt="3-6" border="0"></a>

**5.3. Подписываем `CSR` нашим корневым сертификатом. Тем самым создаем конечный сертификат.**

```
- openssl x509 -req -in certificate.csr -CA ca.pem -CAkey ca.key -CAcreateserial -out certificate.crt -days 360 -sha256
```

***Ответ:***

<a href="https://ibb.co/4NmGwLn"><img src="https://i.ibb.co/nkgvqyN/3-7.png" alt="3-7" border="0"></a>

**6. Проверяем валидность сертификата**

```
- openssl verify certificate.crt
```

***Ответ:***

<a href="https://ibb.co/QcDQ0vY"><img src="https://i.ibb.co/dcmMZ4k/3-8.png" alt="3-8" border="0"></a>


*В качестве ответа приложите снимки экрана.*

------
