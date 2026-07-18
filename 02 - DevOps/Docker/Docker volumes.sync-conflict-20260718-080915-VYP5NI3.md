# Docker volumes

[[00 Docker]]

Volume нужен, чтобы хранить данные вне жизненного цикла контейнера.

Без volume данные внутри контейнера могут потеряться при удалении контейнера.

Типы:
- named volume;
- bind mount;
- tmpfs mount.

Команды:
```bash
# Показывает Docker volumes.
# Ожидаемо: список volume names.
docker volume ls

# Показывает подробную информацию о volume.
# Ожидаемо: mountpoint, driver, labels.
docker volume inspect <volume>

# Запускает контейнер с named volume.
# Ожидаемо: данные /data будут храниться в volume mydata.
docker run -v mydata:/data nginx
```

Короткий ответ:

Volume выносит данные за пределы контейнера, чтобы они переживали пересоздание контейнера.

