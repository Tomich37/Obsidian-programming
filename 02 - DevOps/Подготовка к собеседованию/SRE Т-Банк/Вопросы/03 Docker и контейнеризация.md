# Docker и контейнеризация

[[00 Популярные вопросы]]

- **[7/10] От какого пользователя по умолчанию запускается контейнер и почему это плохо?** Ответ: [[02 - DevOps/Docker/Безопасность контейнеров Docker|Безопасность контейнеров Docker]].
- **[6/10] Как Docker изолирует контейнеры и какие механизмы Linux использует?** Ответ: [[02 - DevOps/Linux/Процессы/cgroups и namespaces|cgroups и namespaces]].
- **[6/10] Как уменьшить образ, если в Dockerfile много `COPY` и `RUN`?** Ответ: [[02 - DevOps/Docker/Оптимизация Docker-образов|Оптимизация Docker-образов]].
- **[6/10] Какие инструкции Dockerfile создают слои?** Ответ: [[02 - DevOps/Docker/Слои образа и кеш сборки|Слои образа и кеш сборки]].
- **[6/10] Что означают образы `<none>:<none>` в `docker images`?** Ответ: [[02 - DevOps/Docker/Образы и теги Docker|Образы и теги Docker]].
- **[5/10] Что такое Docker, зачем он нужен и какие механизмы Linux лежат в основе?** Ответ: [[02 - DevOps/Docker/Образ и контейнер|Образ и контейнер]] и [[02 - DevOps/Linux/Процессы/cgroups и namespaces|cgroups и namespaces]].
- **[5/10] Контейнер завершается с `/bin/bash: not found`. Как диагностировать проблему?** Ответ: [[02 - DevOps/Docker/Диагностика контейнера|Диагностика контейнера]].
- **[5/10] Можно ли ограничить CPU, RAM, I/O и сеть контейнера, как это реализовано?** Ответ: [[02 - DevOps/Docker/Ограничение ресурсов контейнера|Ограничение ресурсов контейнера]].
- **[5/10] Что такое слои Docker-образа?** Ответ: [[02 - DevOps/Docker/Слои образа и кеш сборки|Слои образа и кеш сборки]].
- **[5/10] Чем `ARG` отличается от `ENV`?** Ответ: [[02 - DevOps/Docker/Инструкции Dockerfile/ARG|ARG]] и [[02 - DevOps/Docker/Инструкции Dockerfile/ENV|ENV]].
- **[4/10] Что такое контейнер и образ, в чем концепция их использования?** Ответ: [[02 - DevOps/Docker/Образ и контейнер|Образ и контейнер]].
- **[4/10] Чем `ADD` отличается от `COPY`?** Ответ: [[02 - DevOps/Docker/Инструкции Dockerfile/ADD|ADD]] и [[02 - DevOps/Docker/Инструкции Dockerfile/COPY|COPY]].
- **[4/10] Почему не следует использовать тег `latest`?** Ответ: [[02 - DevOps/Docker/Образы и теги Docker|Образы и теги Docker]].
- **[3/10] Что делает инструкция `ENTRYPOINT`?** Ответ: [[02 - DevOps/Docker/Инструкции Dockerfile/ENTRYPOINT|ENTRYPOINT]].
- **[3/10] Чем `CMD` отличается от `ENTRYPOINT`?** Ответ: [[02 - DevOps/Docker/Инструкции Dockerfile/CMD ENTRYPOINT и RUN|CMD, ENTRYPOINT и RUN]].
- **[3/10] Какие задачи решает Docker Compose?** Ответ: [[02 - DevOps/Docker Compose/Docker Compose|Docker Compose]].
- **[3/10] Что такое Docker squash и когда его применять?** Ответ: [[02 - DevOps/Docker/Оптимизация Docker-образов|Оптимизация Docker-образов]].
- **[3/10] Чем `docker stop` отличается от `docker pause`?** Ответ: [[02 - DevOps/Docker/Жизненный цикл контейнера|Жизненный цикл контейнера]].
- **[3/10] Как остановить контейнер изнутри?** Ответ: [[02 - DevOps/Docker/Жизненный цикл контейнера|Жизненный цикл контейнера]].
- **[3/10] Какие best practices применяют при написании Dockerfile?** Ответ: [[02 - DevOps/Docker/Оптимизация Docker-образов|Оптимизация Docker-образов]] и [[02 - DevOps/Docker/Безопасность контейнеров Docker|Безопасность контейнеров Docker]].
- **[2/10] Что такое Kata Containers?** Ответ: [[02 - DevOps/Docker/Kata Containers|Kata Containers]].
- **[0/10] В каком виде хранятся образы, зачем нужны слои и что такое OverlayFS?** Ответ: [[02 - DevOps/Docker/Хранилище Docker и overlay2|Хранилище Docker и overlay2]].
- **[0/10] Почему внутри контейнера видны только его процессы?** Ответ: [[02 - DevOps/Linux/Процессы/cgroups и namespaces|PID namespace]].
- **[0/10] Как сопоставить каталоги в `/var/lib/docker` с контейнерами?** Ответ: [[02 - DevOps/Docker/Хранилище Docker и overlay2|Хранилище Docker и overlay2]].
- **[0/10] Как организовать сеть между двумя Docker-контейнерами?** Ответ: [[02 - DevOps/Docker/Docker network|Docker network]].
- **[0/10] Может ли контейнер самостоятельно перезапускаться?** Ответ: [[02 - DevOps/Docker/Жизненный цикл контейнера|Жизненный цикл контейнера]].

