# Route53

[[00 AWS]]

`Route53` - DNS-сервис AWS.

Что умеет:
- hosted zones;
- DNS records;
- domain registration;
- health checks;
- routing policies.

Типовые routing policies:
- simple;
- weighted;
- latency-based;
- failover;
- geolocation.

Пример:

Домен `example.com` обслуживается hosted zone в Route53. Запись `A` или `CNAME` указывает на Load Balancer, а пользователи через DNS получают адрес сервиса.

Короткий ответ:

Route53 - управляемый DNS в AWS. Он хранит зоны и записи, а также может маршрутизировать трафик по latency, весам или failover-логике.
