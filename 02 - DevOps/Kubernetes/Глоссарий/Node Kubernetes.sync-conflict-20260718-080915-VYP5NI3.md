# Node Kubernetes

[[00 Глоссарий]]

Node — рабочая машина кластера, физическая или виртуальная. На ней работают kubelet, container runtime, сетевой dataplane и пользовательские Pod.

Node содержит:
- labels для выбора узла;
- taints для ограничения планирования;
- capacity и allocatable ресурсы;
- conditions `Ready`, `MemoryPressure`, `DiskPressure`, `PIDPressure`;
- адреса и сведения о runtime/kubelet.

```bash
# Показывает nodes, их состояние, роли и версии.
# Ожидаемо: Ready/NotReady и основная информация по каждому узлу.
kubectl get nodes -o wide

# Показывает labels, taints, capacity, allocatable и conditions узла.
# Ожидаемо: подробная диагностическая карточка выбранной node.
kubectl describe node <node>
```
