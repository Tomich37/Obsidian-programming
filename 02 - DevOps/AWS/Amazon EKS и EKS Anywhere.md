# EKS и EKS Anywhere

[[00 AWS]]

`EKS` - managed Kubernetes от AWS.

AWS управляет control plane:
- API Server;
- etcd;
- доступность control plane;
- обновления части компонентов.

Worker nodes могут быть:
- Managed Node Groups;
- self-managed EC2;
- Fargate;
- Karpenter-managed nodes.

`EKS Anywhere` - вариант Kubernetes для запуска on-premise или bare metal с подходом и tooling от AWS.

Разница:
- EKS работает в AWS и AWS управляет control plane;
- EKS Anywhere запускается вне AWS, и за инфраструктуру больше отвечает команда.

Короткий ответ:

EKS - Kubernetes как managed service в AWS. EKS Anywhere - способ использовать похожий стек вне AWS, например в своем ЦОДе.
