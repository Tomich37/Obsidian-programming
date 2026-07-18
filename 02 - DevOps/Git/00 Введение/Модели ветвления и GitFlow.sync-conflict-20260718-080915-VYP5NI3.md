# Модели ветвления и GitFlow

[[00 Введение]]

Merge сохраняет ветвление и создаёт merge commit, если fast-forward невозможен. Rebase переносит коммиты на новую базу и переписывает их hash. Публичную общую историю без согласования не rebase'ят.

GitFlow использует долгоживущие `main` и `develop`, а также feature, release и hotfix branches. Модель удобна для релизных циклов, но тяжеловесна для частого continuous delivery.

Альтернативы:
- trunk-based development с короткоживущими ветками;
- GitHub/GitLab flow через feature branch и merge request;
- fork workflow, когда участники работают в собственных forks и открывают pull request.

Выбор зависит от частоты релизов, требований к поддерживаемым версиям и размера команды. Важнее единые правила review, CI и защиты основной ветки, чем название модели.
