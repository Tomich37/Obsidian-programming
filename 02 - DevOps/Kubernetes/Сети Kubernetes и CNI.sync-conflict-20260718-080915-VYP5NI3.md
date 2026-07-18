# Сети Kubernetes и CNI

[[00 Kubernetes]]

Сетевая модель предполагает, что каждый Pod получает IP и может общаться с другими Pod без NAT внутри кластера. Реализация зависит от CNI plugin: Calico, Cilium, Flannel и других.

CNI вызывается runtime/kubelet при создании sandbox Pod и настраивает interface, адрес, routes и dataplane. Service предоставляет стабильный virtual IP и набор endpoints; kube-proxy или eBPF dataplane направляет трафик к Pod. NetworkPolicy задаёт разрешённые ingress/egress связи, если CNI её поддерживает.

```bash
# Показывает Pod системных сетевых компонентов.
# Ожидаемо: CNI agents и DNS-компоненты в kube-system.
kubectl get pods -n kube-system -o wide

# Показывает Service и фактические endpoints его backend Pod.
# Ожидаемо: ClusterIP Service и адреса Pod в EndpointSlice.
kubectl get service,endpointslice -n <namespace>
```
