# Kubernetes API versions

[[00 Глоссарий]]

В Kubernetes у ресурсов есть `apiVersion`.

Примеры:
- `v1` - стабильное core API;
- `apps/v1` - Deployment, StatefulSet, DaemonSet;
- `batch/v1` - Job, CronJob;
- `networking.k8s.io/v1` - Ingress, NetworkPolicy.

Стадии API:
- `alpha` - экспериментально, может ломаться;
- `beta` - протестировано лучше, но семантика еще может меняться;
- stable `v1` - стабильно и подходит для production.

Команды:
```bash
# Показывает доступные API-группы и версии в кластере.
# Ожидаемо: список вроде apps/v1, batch/v1, networking.k8s.io/v1.
kubectl api-versions

# Показывает все типы ресурсов, которые понимает кластер.
# Ожидаемо: NAME, SHORTNAMES, APIVERSION, NAMESPACED, KIND.
kubectl api-resources
```

Короткий ответ:

apiVersion говорит, через какой Kubernetes API описан ресурс. Для production лучше использовать стабильные версии, а не alpha/beta без необходимости.

