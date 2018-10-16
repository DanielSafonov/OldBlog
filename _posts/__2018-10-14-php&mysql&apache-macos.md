layout: post 
title: Установка и настройка MySQL, Apache и PHP в MacOS
tags: [macos, web]
image: web_server_macos.jpg
---

##Установка

1. Apache предустановлен в MacOS. Запускается командой:
```bash
$ sudo apachectl start
```
*Успешно запущенный apache можно проверить, перейдя по адресу `localhost` в адресной строке браузера.* 
2. PHP так же предустановлен, но по умолчанию выключен. <br/>
*Включение будет произведено позже.*
3. MySQL необходимо [скачать с официального сайта](https://dev.mysql.com/downloads/mysql/){:target="_blank"} и установить. <br/>
*Вводимый при установке пароль понадобится при работе с MySQL.*

<br/>

##Настройка

1. Включаем PHP в Apache и заменим директорию с сайтами:
```bash
# Переходим в директорию apache
$ cd /etc/apache2/ 
# Делаем бэкап дефолтного конфига
$ cp httpd.conf httpd.conf.bak
# Правим файл конфига
$ nano httpd.conf
# Расскоментируем строку с подключением php (удаляем '#')
LoadModule php7_module libexec/apache2/libphp7.so
# Находим строки DocumentRoot и Directory, заменяем путь на более удобный
DocumentRoot "/Users/paltusstas/Sites"
<Directory "/Users/paltusstas/Sites">
# Отключаем Forbidden - меняем значения Options и AllowOverride
Options Indexes FollowSymLinks Includes ExecCGI
AllowOverride All
# Перезапускам apache с новым конфигом
$ apachectl restart
```
Создаем директорию `Sites` в домашнем каталоге.
2. После установки MySQL, в Системных настройках MacOS появится соответствующая иконка, но мы будем пользоваться консолью.
```bash
# Добавляем пути к mysql в PATH
$ sudo nano /etc/paths
# Записать эти строки в конец файла
/usr/local/mysql/bin
/urs/local/mysql/bin/mysql
/usr/local/mysql/support-files
```
Перезапускаем терминал для обновления конфига.
Теперь по команде `$ mysql.server start` будет запускаться сервер MySQL без необходимости прописывать полный путь к директории с mysql.server.
<br/>
```bash
# Меняем вдадельца и права доступа к директории с MySQL
$ sudo chown -R mysql:mysql /usr/local/mysql
$ sudo chmod -R 775 /usr/local/mysql

# Переход в консоль MySQL под root пользователем
$ mysql -u root -p
```
<br/>

##Полезные команды

```bash
# Управление состоянием MySQL Server
$ mysql.server status
$ mysql.server stop
$ mysql.server start
$ mysql.server restart
# Переход в консоль MySQL под root пользователем
$ mysql -u root -p

#Управление состоянием Apache
$ apachectl status
$ apachectl stop
$ apachectl start
$ apachectl restart
```
