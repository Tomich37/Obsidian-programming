# Minikube

[[00 Kubernetes]]

Minikube создаёт локальный Kubernetes-кластер для обучения и разработки. Он может запускать node в VM, Docker или другом driver и автоматически настраивает kubeconfig.

Это не production-платформа: обычно кластер небольшой, отказоустойчивость и интеграции упрощены. Для локальных тестов также применяют kind и k3d.

```bash
# Запускает локальный кластер с выбранным driver.
# Ожидаемо: созданный cluster, настроенный kubectl context и Ready node.
minikube start --driver=docker

# Показывает состояние локального control plane и kubelet.
# Ожидаемо: Running/Configured для компонентов minikube.
minikube status
```
