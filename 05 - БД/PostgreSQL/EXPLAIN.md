# Как читать EXPLAIN

[[PostgreSQL]]

`EXPLAIN` показывает план выполнения SQL-запроса.

Для PostgreSQL:
```sql
-- Показывает план выполнения запроса без реального выполнения.
-- Ожидаемо: план с Seq Scan/Index Scan, cost и оценкой rows.
EXPLAIN SELECT * FROM users WHERE email = 'a@b.com';

-- Выполняет запрос и показывает реальную статистику выполнения.
-- Ожидаемо: actual time, actual rows и сравнение с оценками планировщика.
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
