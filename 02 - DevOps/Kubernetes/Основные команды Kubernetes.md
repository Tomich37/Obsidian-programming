---
Тема: Python web
tags:
  - DevOps
  - k8s
  - review
Дата: 22-08-2025
sr-due: 2025-08-23
sr-interval: 1
sr-ease: 230
---
# Работа с объектами
```bash
kubectl get pods # список подов
kubectl get pods -n kube-system # список подов в namespace kube-system
kubectl get depoyments # список deployment'ов
kubectl get svc # список сервисов
kubectl get nodes #список нод
```
# Подробная информация
```bash
kubectl describe pod <name-pod> # подробная информация о поде
kubectl describe deployment <name-deploy> # информация по деплойменте
kubectl logs <name-pod> # логи контейнера
kubectl logs <name-pod> -c <conatiner-name> # если контейнеров несколько
kubectl logs <name-pod> --previous # логи упавшего контейнера
```
Пример того что может показать `kubectl describe pod <name-pod>`:
- **Conditions** (состояние пода: Scheduled, Ready, etc.)    
- **Containers** (статус каждого контейнера, exit code, reason)    
- **Events** (очень важно! например: `ImagePullBackOff`, `OOMKilled`, `CrashLoopBackOff`)
# Взаимодействие с подом
```bash
kubectl exec -it <name-pod> -- /bin/bash # завти внутрь контейнера
kubectl port-forward pod/<name-pod> 8080:80 # пробросить порт наружу
kubectl cp <name-pod>:/path/in/pod ./local # копирование файла из пода
```
# Управление ресурсами
```bash
kubectl apply -f manifest.yaml # применить конфиг
kubectl delete -f manifest.yaml # удалить конфиг
kubectl delete pod <name-pod> # удалить конкретный объект
```
# Namespaces
```bash
kubectl get ns # список пространств имен
kubectl create ns <name-namespace> # создать namespace
kubectl get pods -n <name-namespace> # смотреть поды в <name-namespace>
```
[[namespace]]
