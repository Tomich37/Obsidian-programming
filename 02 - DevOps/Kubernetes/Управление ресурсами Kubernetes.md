# Requests, limits и QoS

[[00 Kubernetes]]

`requests` — ресурсы, которые scheduler учитывает при размещении Pod. Это не резерв физической памяти, но обещанный минимум для планирования.

`limits` — верхняя граница:
- CPU limit приводит к throttling через cgroup;
- превышение memory limit обычно заканчивается OOM kill контейнера.

QoS-классы:
- `Guaranteed` — requests равны limits для CPU и memory всех контейнеров;
- `Burstable` — задана часть requests/limits;
- `BestEffort` — ничего не задано; такие Pod обычно удаляются первыми при давлении памяти.

```yaml
# Гарантирует учёт 250m CPU и 256Mi RAM при планировании и задаёт верхние границы.
# Ожидаемо: CPU выше 1 core будет throttled, а превышение 512Mi может вызвать OOMKilled.
resources:
  requests:
    cpu: 250m
    memory: 256Mi
  limits:
    cpu: "1"
    memory: 512Mi
```

```bash
# Показывает requests, limits, QoS и последние события Pod.
# Ожидаемо: секции Containers и Events с причиной OOMKilled или scheduling failure.
kubectl describe pod <pod> -n <namespace>
```
