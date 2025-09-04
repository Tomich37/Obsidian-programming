---
Тема: Ansible
tags:
  - DevOps
  - Ansible
  - review
Дата: 23-11-2023
sr-due: 2025-09-11
sr-interval: 17
sr-ease: 270
---
Инвентарь (inventory) - это файл или система, которая указывает Ansible, на какие узлы (серверы, устройства) выполнять задачи. В нем перечисляются управляемые узлы и их параметры, такие как IP-адреса, пользователи, группы, переменные и многое другое
# Типы инвентаря
1. Статический инвентарь
	1. Это файл (обычно `ini`, `yaml` или `json`), в котором 
2. Динамический инвентарь
	1. Это скрипт или плагин, который получает список узлов в реальном времени, например, из облачных провайдеров (AWS, GCP, Azure)
# Статический инвентарь
## Пример в формате INI:
```ini
[web_servers]
192.168.1.100 ansible_user=admin
192.168.1.101 ansible_user=root ansible_ssh_pass=password

[db_servers]
db1.example.com
db2.example.com ansible_port=2222
```

**Объяснение:**
- `192.168.1.100`, `192.168.1.101`: IP-адреса узлов в группе `web_servers`.
- `db1.example.com`, `db2.example.com`: имена хостов в группе `db_servers`.
- Параметры:
    - `ansible_user`: пользователь для подключения.
    - `ansible_ssh_pass`: пароль для подключения по SSH.
    - `ansible_port`: нестандартный порт SSH
## Пример в формате yaml
```yaml
all:
  children:
    web_servers:
      hosts:
        192.168.1.100:
          ansible_user: admin
        192.168.1.101:
          ansible_user: root
          ansible_ssh_pass: password
    db_servers:
      hosts:
        db1.example.com: {}
        db2.example.com:
          ansible_port: 2222
```
# Группы узлов
Узлы в инвентаре можно объединять в группы для удобного управления
1. `web_servers`: узлы с веб-серверами
2. `db_servers`: узлы с БД

Группы могут содержать вложенные подгруппы:\
```ini
[all_servers: children]
web_servers
db_servers
```
Теперь `all_servers` включает узлы из обеих групп

# Как узнать инвентарь при запуске?
По умолчанию Ansible использует файл `inventory` в текущей папке или `/etc/ansible/hosts`
Чтобы явно указать другой файл, используется флаг `-i`
# Добавление переменных для узлов и групп
1. Переменные для отдельных узлов: указываются в инвентаре рядом с хостом
```ini
192.168.1.100 ansible_user=admin my_custom_var=hello
```
2. Переменные для группы: создаются отдельные файлы в папке `group/vars`
```
group_vars/
└── web_servers.yml
```
Пример web_servers.yml:
```yaml
my_group_var: world
```
3. Переменные для конкретного узла: создаются в папке `hosts_vars/`
```
host_vars/
└── 192.168.1.100.yml
```
Пример `192.168.1.100.yml`
```yaml
my_host_var: hello
```
# Как проверить инвентарь
Чтоб увидеть какие узлы доступны:
```bash
ansible-inventory -i inventory.ini --list
```

Чтоб проверить подключение к узлам:
```bash
ansible all -i inventory.ini -m ping
```
