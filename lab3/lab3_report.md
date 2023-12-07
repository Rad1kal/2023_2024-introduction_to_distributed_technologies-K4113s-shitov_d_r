University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FICT](https://fict.itmo.ru)  
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)  
Year: 2023/2024  
Group: K4113s  
Author: Shitov Dmitry Romanovich  
Lab: Lab1  
Date of create: 16.10.2023  
Date of finished: 16.10.2023

## Лабораторная работа №3 "Сертификаты и "секреты" в Minikube, безопасное хранение данных."

### Описание

В данной лабораторной работе вы познакомитесь с сертификатами и "секретами" в Minikube, правилами безопасного хранения данных в Minikube.

### Цель работы

Познакомиться с сертификатами и "секретами" в Minikube, правилами безопасного хранения данных в Minikube.

### Ход работы

-   Brew устанавливает LibreSSL, а не OpenSSL. LibreSSL в настоящее время совместим с OpenSSL и работает, но? LibreSSL не определяется автоматически, поэтому Allegro CL необходимо сообщить, какая версия OpenSSL установлена.

```bash
export ACL_OPENSSL_VERSION=11
```

-   После устанавливаю OpenSSL:

```bash
brew install openssl
```

-   Генерирую ключ:

```bash
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout privateKey.key -out certificate.crt
```

-x509 — уточнение, что нам нужен именно самоподписанный сертификат;
-newkey — автоматическое создание ключа сертификата;
-days — срок действия сертификата в днях;
-keyout — путь (если указан) и имя файла ключа;
-out — путь (если указан) и имя файла сертификата.

-   Далее импортирую сертификат в minikube:

```bash
kubectl create secret tls tls-secret --cert=certificate.crt --key=privateKey.key
```
