# Операторы Kubernetes

[[00 Kubernetes]]

Operator объединяет custom resource definition и controller. Пользователь описывает желаемое состояние предметной области, например кластер PostgreSQL, а controller выполняет reconciliation: создаёт ресурсы, обновляет конфигурацию, делает backup/failover и публикует status.

Оператор полезен, когда эксплуатационные знания можно формализовать. Он сложнее Helm chart: Helm в основном рендерит и применяет манифесты, а operator постоянно наблюдает объект и реагирует на изменения и сбои.

```bash
# Показывает установленные CustomResourceDefinition.
# Ожидаемо: список API-типов, часть которых обслуживают операторы.
kubectl get crd

# Показывает controller/operator Pod во всех namespaces по имени.
# Ожидаемо: найденные operator-компоненты или пустой список.
kubectl get pods -A | grep -i operator
```
