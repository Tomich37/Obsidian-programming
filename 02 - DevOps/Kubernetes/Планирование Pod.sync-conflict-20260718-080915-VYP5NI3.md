# Планирование Pod

[[00 Kubernetes]]

Scheduler фильтрует подходящие nodes и выбирает лучшую по requests, constraints и scoring.

- `nodeName` напрямую фиксирует node и фактически обходит обычный выбор scheduler;
- `nodeSelector` требует точного совпадения labels;
- node affinity задаёт обязательные и предпочтительные правила;
- pod affinity/anti-affinity размещает Pod рядом с другими Pod или разносит их;
- taint отталкивает Pod, а toleration разрешает ему планироваться на такую node, но не гарантирует выбор;
- topology spread constraints распределяют реплики по зонам и узлам.

```yaml
# Требует node с label disktype=ssd.
# Ожидаемо: scheduler выберет только подходящую node или оставит Pod Pending.
nodeSelector:
  disktype: ssd

# Разрешает Pod размещаться на node с соответствующим taint NoSchedule.
# Ожидаемо: taint перестанет запрещать планирование, но node ещё должна пройти остальные проверки.
tolerations:
  - key: dedicated
    operator: Equal
    value: sre
    effect: NoSchedule
```

Для диагностики Pending Pod смотрят `kubectl describe pod`: в Events scheduler указывает недостаток ресурсов, несовпадение affinity или отсутствие toleration.
