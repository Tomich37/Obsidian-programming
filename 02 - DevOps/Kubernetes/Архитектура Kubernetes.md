# Архитектура Kubernetes

[[00 Kubernetes]]

Кластер состоит из control plane и worker nodes.

Control plane:
- `kube-apiserver` — единая точка входа в Kubernetes API, аутентификация и валидация;
- `etcd` — согласованное хранилище состояния кластера;
- `kube-scheduler` — выбирает node для новых Pod;
- `kube-controller-manager` — запускает reconciliation loops контроллеров;
- `cloud-controller-manager` — интеграция с API облака при необходимости.

Worker node:
- `kubelet` — получает PodSpec и обеспечивает запуск Pod;
- container runtime через CRI — запускает контейнеры;
- `kube-proxy` или eBPF dataplane — реализует Service-маршрутизацию;
- CNI plugin — настраивает сеть Pod;
- CSI plugin — подключает внешние хранилища.

Все изменения проходят через API server. Компоненты не «командуют» друг другу напрямую, а наблюдают желаемое и фактическое состояние и постепенно их согласуют.

```bash
# Показывает компоненты control plane как Pod в kube-system.
# Ожидаемо: kube-apiserver, scheduler, controller-manager и другие системные Pod.
kubectl get pods -n kube-system -o wide

# Показывает nodes и их состояние.
# Ожидаемо: Ready/NotReady, роли, версия kubelet и возраст узлов.
kubectl get nodes -o wide
```
