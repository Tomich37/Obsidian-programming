# Хранилище Docker и overlay2

[[00 Docker]]

Образы состоят из read-only слоёв. При запуске контейнер получает writable layer поверх образа. Драйвер `overlay2` объединяет lower layers образа и upper layer контейнера в единое merged-представление OverlayFS.

Docker хранит внутренние данные в `DockerRootDir`, обычно `/var/lib/docker`. Имена каталогов storage driver не обязаны совпадать с container ID, поэтому связь нужно смотреть через `docker inspect`, а не редактировать каталоги вручную.

```bash
# Показывает корневой каталог Docker и используемый storage driver.
# Ожидаемо: Docker Root Dir и Storage Driver, например overlay2.
docker info --format 'root={{.DockerRootDir}} driver={{.Driver}}'

# Показывает пути writable/merged слоёв контейнера, если драйвер их публикует.
# Ожидаемо: объект GraphDriver.Data с UpperDir, MergedDir и WorkDir для overlay2.
docker inspect --format '{{json .GraphDriver.Data}}' <container>

# Показывает, сколько места занимают образы, контейнеры, volumes и build cache.
# Ожидаемо: таблица TYPE, TOTAL, ACTIVE, SIZE и RECLAIMABLE.
docker system df
```
