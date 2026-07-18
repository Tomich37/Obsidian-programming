# Обновление Deployment и rollout

[[00 Kubernetes]]

Изменение image или Pod template меняет hash шаблона Deployment. Controller создаёт новый ReplicaSet и выполняет rollout. При стратегии `RollingUpdate` количество одновременно недоступных и дополнительных Pod регулируют `maxUnavailable` и `maxSurge`.

Если readiness probe не проходит, новые Pod не становятся Ready и rollout может остановиться. Старый ReplicaSet сохраняется для rollback в пределах `revisionHistoryLimit`.

```bash
# Меняет image контейнера в Deployment и запускает новый rollout.
# Ожидаемо: deployment.apps/<name> image updated.
kubectl set image deployment/<deployment> <container>=<image>:<tag> -n <namespace>

# Следит за завершением rollout.
# Ожидаемо: successful rollout либо timeout/ошибка готовности новых Pod.
kubectl rollout status deployment/<deployment> -n <namespace>

# Откатывает Deployment к предыдущей revision.
# Ожидаемо: начнётся обратный rollout на прошлый Pod template.
kubectl rollout undo deployment/<deployment> -n <namespace>
```
