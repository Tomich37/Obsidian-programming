# Backup и репликация MySQL

[[00 MySQL]]

`mysqldump` создаёт логический backup. На большой активной базе он может долго читать данные, создавать нагрузку на CPU/I/O, удерживать snapshot/locks и генерировать большой текстовый файл. Восстановление также обычно медленнее физического backup.

Альтернативы:
- физический hot backup, например Percona XtraBackup;
- snapshot диска/тома при согласованной процедуре;
- backup с replica, чтобы снизить влияние на primary;
- binlog для point-in-time recovery.

Классическая source-replica репликация:
1. На source включены binary logs и уникальный `server_id`.
2. Делается согласованный baseline backup.
3. Replica восстанавливает backup и получает координаты binlog/GTID.
4. Replica подключается специальным пользователем и применяет изменения.
5. Контролируются lag, ошибки и целостность.

Термины master/slave устарели; в современной документации используют source/replica.
