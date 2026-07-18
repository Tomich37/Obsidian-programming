# Что такое Ingress

[[00 Глоссарий]]

`Ingress` - объект для входящего HTTP/HTTPS-трафика в кластер.

Он описывает правила:
- какой домен обслуживать;
- какой path куда отправлять;
- какой TLS-сертификат использовать.

Важно:

Ingress сам по себе не принимает трафик. Нужен Ingress Controller: nginx-ingress, Traefik, HAProxy Ingress, AWS Load Balancer Controller.

Команды:
```bash
# Показывает Ingress-объекты.
# Ожидаемо: HOSTS, ADDRESS, PORTS и AGE.
kubectl get ingress

# Показывает правила, TLS и события Ingress.
# Ожидаемо: backend service, paths, ошибки controller'а в events.
kubectl describe ingress <ingress>
```

Короткий ответ:

Ingress - это правила маршрутизации HTTP/HTTPS в Kubernetes, а реально применяет их Ingress Controller.

