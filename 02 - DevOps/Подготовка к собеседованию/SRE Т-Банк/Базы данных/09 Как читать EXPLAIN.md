# Как читать EXPLAIN

[[00 Базы данных - вопросы]]

`EXPLAIN` показывает план выполнения SQL-запроса.

Для PostgreSQL:
```sql
EXPLAIN SELECT * FROM users WHERE email = 'a@b.com';
EXPLAIN ANALYZE SELECT * FROM users WHERE email = 'a@b.com';
```

На что смотреть:
- `Seq Scan` - последовательное чтение таблицы;
- `Index Scan` - чтение через индекс;
- `Nested Loop`, `Hash Join`, `Merge Join` - способы join;
- `cost` - оценка стоимости;
- `rows` - оценка количества строк;
- `actual time` - реальное время в `EXPLAIN ANALYZE`;
- расхождение estimated/actual rows.

Что важно:

`Seq Scan` не всегда плохо. Для маленькой таблицы или большой доли строк последовательное чтение может быть быстрее индекса.

Короткий ответ:

EXPLAIN нужен, чтобы понять, как БД выполняет запрос: читает всю таблицу или индекс, как делает join и где тратит время.

