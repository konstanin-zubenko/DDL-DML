# Домашнее задание к занятию «Работа с данными (DDL/DML)» Зубенко Константин

## Задание 1

1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.  
1.2. Создайте учётную запись sys_temp.  
1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)  
1.4. Дайте все права для пользователя sys_temp.  
1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)  
1.6. Переподключитесь к базе данных от имени sys_temp.  
Для смены типа аутентификации с sha2 используйте запрос:  
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';  
1.7. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.  
1.8. Восстановите дамп в базу данных.  
1.9. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.

## Решение 1

1.1.	Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.
```
sudo apt install wget lsb-release gnupg
wget -c https://dev.mysql.com/get/mysql-apt-config_0.8.34-1_all.deb
sudo dpkg -i mysql-apt-config_0.8.34-1_all.deb
sudo apt update
sudo apt install mysql-server
sudo systemctl status mysql
sudo systemctl enable mysql
mysql -u root –p
```


1.2.	Создайте учётную запись sys_temp.
```
CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY 'password';
```


1.3.	Выполните запрос на получение списка пользователей в базе данных. (скриншот)
```
SELECT user FROM mysql.user;
```
![](https://github.com/konstanin-zubenko/DDL-DML/blob/main/img/300.png)


1.4.	Дайте все права для пользователя sys_temp.
```
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost' WITH GRANT OPTION;
```


1.5.	Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)
```
SELECT * FROM information_schema.user_privileges WHERE GRANTEE="'sys_temp'@'localhost'";
```
![](https://github.com/konstanin-zubenko/DDL-DML/blob/main/img/301.png) 

```

1.6.	Переподключитесь к базе данных от имени sys_temp.
```
SYSTEM mysql -u sys_temp -p
SELECT user();
```

 
1.7.	По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.
```
wget https://downloads.mysql.com/docs/sakila-db.zip
unzip sakila-db.zip
```


1.8.	Восстановите дамп в базу данных.

```
source /home/cozu/sakila-db/sakila-schema.sql
source /home/cozu/sakila-db/sakila-data.sql
SHOW DATABASES;
```

 ![](https://github.com/konstanin-zubenko/DDL-DML/blob/main/img/303.png).


1.9. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)
```
SHOW TABLES;
```

![](https://github.com/konstanin-zubenko/DDL-DML/blob/main/img/304.png).
 
## Задание 2

Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц.  
Пример: (скриншот/текст)  
```
Название таблицы | Название первичного ключа
customer         | customer_id
```
## Решение 2

```
SELECT TABLE_NAME, COLUMN_NAME FROM INFORMATION_SCHEMA.key_column_usage WHERE table_schema = 'sakila' AND CONSTRAINT_NAME = 'PRIMARY';
```
![](https://github.com/konstanin-zubenko/DDL-DML/blob/main/img/306.png).
