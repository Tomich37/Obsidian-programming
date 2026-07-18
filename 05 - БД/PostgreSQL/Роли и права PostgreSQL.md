# Роли и права PostgreSQL

[[PostgreSQL]]

В PostgreSQL пользователь и группа представлены одной сущностью `ROLE`. Роль с атрибутом `LOGIN` может подключаться, а роли без LOGIN удобно использовать как группы прав.

Права выдаются через `GRANT` на database, schema, table, sequence и функции. Наследование ролей уменьшает количество индивидуальных grants.

```sql
-- Создаёт групповую роль без права входа.
-- Ожидаемо: роль app_readers появится в каталоге ролей.
CREATE ROLE app_readers NOLOGIN;

-- Создаёт пользователя и включает его в группу читателей.
-- Ожидаемо: app_user сможет подключаться и наследовать права app_readers.
CREATE ROLE app_user LOGIN PASSWORD 'change-me';
GRANT app_readers TO app_user;

-- Выдаёт чтение всех текущих таблиц схемы public.
-- Ожидаемо: участники app_readers смогут выполнять SELECT.
GRANT SELECT ON ALL TABLES IN SCHEMA public TO app_readers;
```
