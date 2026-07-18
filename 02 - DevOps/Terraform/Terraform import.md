# Terraform import

[[Terraform]]

`terraform import` добавляет существующий ресурс в Terraform state.

Важно:

Import не пишет HCL-код за тебя в старых подходах. Нужно описать ресурс в `.tf` и связать его с реальным ID.

Когда нужен:
- ресурс создали руками;
- нужно взять legacy-инфраструктуру под управление Terraform;
- state потерян частично;
- инфраструктуру переносим в IaC.

Команда:
```bash
# Импортирует существующий AWS instance в Terraform state.
# Ожидаемо: ресурс появится в state, после этого terraform plan покажет расхождения с HCL.
terraform import aws_instance.app i-1234567890abcdef0
```

Короткий ответ:

Terraform import нужен, чтобы связать уже существующий ресурс с Terraform state и дальше управлять им как кодом.
