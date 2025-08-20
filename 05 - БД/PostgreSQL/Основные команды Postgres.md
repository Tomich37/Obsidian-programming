## Подключение

``` bash
psql -U username -d dbname   # подключение к базе 
psql -h host -p port -U username -d dbname   # с хостом и портом
```

Внутри `psql`:
```sql
\c dbname   -- переключиться на другую БД 
\q          -- выйти
```
## Работа с базами данных
```sql
CREATE DATABASE mydb;    -- создать базу 
DROP DATABASE mydb;      -- удалить базу 
\l                      -- список всех баз
```
## Работа с пользователями

```sql
CREATE USER myuser WITH PASSWORD 'mypassword';   -- создать пользователя 
DROP USER myuser;                                -- удалить пользователя 
ALTER USER myuser WITH SUPERUSER;                -- выдать права суперпользователя 
GRANT ALL PRIVILEGES ON DATABASE mydb TO myuser; -- дать доступ к БД
```
## Работа со схемами и таблицами
```sql
CREATE SCHEMA myschema;        -- создать схему 
DROP SCHEMA myschema CASCADE;  -- удалить со всеми объектами  
CREATE TABLE users (     
	id SERIAL PRIMARY KEY,     
	name TEXT NOT NULL,     
	age INT );  
	
DROP TABLE users;
```
## CRUD (данные)
```sql
INSERT INTO users (name, age) VALUES ('Alex', 25);   -- вставка 
SELECT * FROM users;                                 -- выборка 
UPDATE users SET age = 26 WHERE name = 'Alex';       -- обновление 
DELETE FROM users WHERE name = 'Alex';               -- удаление
```
## Просмотр структуры

```sql
\d                   -- список таблиц в текущей схеме 
\d users             -- описание таблицы 
\dt                  -- список таблиц 
\dn                  -- список схем 
\du                  -- список пользователей
```
## Транзакции
```sql
BEGIN;                      -- начать транзакцию 
UPDATE users SET age = 30; ROLLBACK;                   -- откат 
COMMIT;                     -- фиксация изменений
```
## Индексы
```sql
CREATE INDEX idx_users_name ON users(name);  -- индекс 
DROP INDEX idx_users_name;
```
## Резервное копирование и восстановление
```bash
pg_dump -U username mydb > backup.sql         # бэкап базы 
psql -U username -d mydb -f backup.sql        # восстановление
```