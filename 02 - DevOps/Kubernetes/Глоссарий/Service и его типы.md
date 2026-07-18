# Что такое Service и какие есть типы

[[00 Глоссарий]]

`Service` - стабильная сетвая точка доступа к pod'ам.

Pod может пересоздаться и получить новый IP, а Service остается постоянным и выбирает pod'ы по labels.

Типы Service:
- `ClusterIP` - доступ внутри кластера;
- `NodePort` - доступ через порт на каждой node;
- `LoadBalancer` - внешний балансировщик от облака;
- `ExternalName` - DNS alias на внешний адрес.

Команды:
```bash
# Показывает сервисы в текущем namespace.
# Ожидаемо: NAME, TYPE, CLUSTER-IP, EXTERNAL-IP, PORTS.
kubectl get svc

# Показывает подробности сервиса и endpoints.
# Ожидаемо: selector, ports, events и связанные endpoints.
kubectl describe svc <service>
```

Короткий ответ:

Service нужен, чтобы ходить к pod'ам через стабильный адрес, а не напрямую на IP pod'а.

