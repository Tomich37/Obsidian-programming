# Как создаётся Pod

[[00 Kubernetes]]

После `kubectl apply` происходит цепочка:
1. `kubectl` отправляет объект в kube-apiserver.
2. API server выполняет authentication, authorization, admission и schema validation.
3. Желаемое состояние сохраняется в etcd.
4. Controllers создают недостающие объекты, например ReplicaSet и Pod.
5. Scheduler назначает новому Pod подходящую node и записывает binding через API.
6. Kubelet на node получает PodSpec.
7. Runtime через CRI получает image и запускает sandbox/контейнеры.
8. CNI настраивает сеть, CSI и kubelet подключают volumes.
9. Kubelet публикует status и результаты probes через API server.

```bash
# Показывает Pod, назначенную node, IP и состояние контейнеров.
# Ожидаемо: NODE заполнится после scheduler, STATUS изменится Pending -> Running.
kubectl get pod <pod> -n <namespace> -o wide

# Показывает события Pod в хронологическом порядке.
# Ожидаемо: Scheduled, Pulling, Pulled, Created и Started либо причина ошибки.
kubectl events -n <namespace> --for pod/<pod>
```
