# Authoritative и recursive DNS

[[00 Протоколы]]

`Recursive resolver` - DNS-сервер, к которому обычно обращается клиент.

Он сам проходит цепочку DNS-запросов:
1. root DNS;
2. TLD-серверы;
3. authoritative DNS зоны;
4. возвращает ответ клиенту.

`Authoritative DNS` - сервер, который является источником правды для конкретной зоны.

Пример:

Для домена `example.com` authoritative server хранит записи `A`, `AAAA`, `MX`, `TXT` этой зоны.

Команды:
```bash
# Показывает DNS-трассировку от root до authoritative серверов.
# Ожидаемо: цепочка DNS-серверов и финальный ответ.
dig +trace example.com

# Запрашивает NS-записи домена.
# Ожидаемо: список authoritative name servers для зоны.
dig NS example.com
```

Короткий ответ:

Recursive resolver ищет ответ за клиента, authoritative server хранит окончательные записи конкретной DNS-зоны.

