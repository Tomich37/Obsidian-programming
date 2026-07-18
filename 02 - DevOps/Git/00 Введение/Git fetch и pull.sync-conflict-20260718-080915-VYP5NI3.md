# Git fetch и pull

[[00 Введение]]

`git fetch` загружает новые objects и обновляет remote-tracking branches, но не меняет текущую ветку и рабочее дерево.

`git pull` сначала выполняет fetch, затем интегрирует upstream в текущую ветку через merge или rebase в зависимости от параметров и конфигурации.

```bash
# Загружает изменения origin без изменения текущей ветки.
# Ожидаемо: обновятся origin/main и другие remote-tracking branches.
git fetch origin

# Показывает коммиты, появившиеся в origin/main после fetch.
# Ожидаемо: список удалённых коммитов, которых ещё нет в текущем HEAD.
git log --oneline HEAD..origin/main

# Загружает и переносит локальные коммиты поверх upstream без merge commit.
# Ожидаемо: линейная локальная история либо остановка на конфликте.
git pull --rebase
```
