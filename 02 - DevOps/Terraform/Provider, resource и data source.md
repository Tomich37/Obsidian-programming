# Provider resource data source

[[Terraform]]

`Provider` - плагин, через который Terraform работает с внешней системой: AWS, Kubernetes, GitLab, Cloudflare.

`Resource` - объект, которым Terraform управляет.

Примеры:
- VM;
- security group;
- bucket;
- load balancer;
- DNS record.

`Data source` - чтение уже существующих данных без управления ими.

Пример:

Взять существующую VPC как data source и создать security group внутри нее как resource.

Короткий ответ:

Provider подключает Terraform к API, resource создает и меняет объект, data source только читает существующую информацию.
