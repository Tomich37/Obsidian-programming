# Workload-ресурсы Kubernetes

[[00 Глоссарий]]

- `Pod` — минимальная единица запуска.
- `ReplicaSet` поддерживает заданное количество одинаковых Pod.
- `Deployment` управляет ReplicaSet и обеспечивает rollout/rollback stateless-приложения.
- `StatefulSet` даёт Pod стабильные имена, порядок запуска и постоянные volumes; нужен stateful-нагрузкам.
- `DaemonSet` запускает Pod на каждой подходящей node; типичные примеры — log agent, node exporter, CNI agent.
- `Job` выполняет конечную задачу до успешного завершения.
- `CronJob` создаёт Job по расписанию.

Deployment обычно не создаёт Pod напрямую: он создаёт ReplicaSet, а ReplicaSet поддерживает Pod. StatefulSet отличается стабильной идентичностью Pod и управляемым порядком операций.

```bash
# Показывает иерархию Deployment, ReplicaSet и Pod через ownerReferences.
# Ожидаемо: у Pod владельцем будет ReplicaSet, а у ReplicaSet — Deployment.
kubectl get deploy,rs,pods -o wide

# Показывает DaemonSet и число желаемых/готовых Pod на nodes.
# Ожидаемо: DESIRED обычно соответствует числу подходящих узлов.
kubectl get daemonset -A
```
