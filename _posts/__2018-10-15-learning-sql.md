layout: post 
title: SQL HowTo
tags: [sql]
image: sql.jpg
---

SQL
Технопарк MailRu - Базы данных
см. перевод статьи это или нет
https://tproger.ru/translations/sql-recap/  
https://proglib.io/p/sql-for-20-minutes/ 
https://proglib.io/p/sql-digest/
http://samoychiteli.ru/document29118.html
https://tproger.ru/translations/java-jdbc-example/
https://tproger.ru/translations/sql-nosql-database-models/
http://progopedia.ru/language/sql/
https://www.w3schools.com/sql/default.asp
http://sqlfiddle.com
https://proglib.io/p/sql-practice-sites/
https://proglib.io/p/structured-query-language/

CREATE DATABASE months_test; //Создать новую БД
SHOW DATABASES; //Вывести список созданных БД
USE months_test; //Выбрать БД
CREATE TABLE months_list(id int(2), name varchar(10), days int(2)); //Создать таблицу из 3 колонок - id (int длинной 2 цифры), name (char длинной 10 символов), days ((int длинной 2 цифры))
SHOW TABLES; //Вывести список таблиц БД
DESCRIBE months_list; //Вывести таблицу БД
INSERT INTO months_list VALUES(1, 'January', 31); //Заполнить строку таблицы
SELECT * FROM months_list; //Вывести таблицу


