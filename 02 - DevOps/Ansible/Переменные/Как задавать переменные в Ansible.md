---
Тема: Ansible
tags:
  - DevOps
  - Ansible
  - review
Дата: 23-11-2023
sr-due: 2025-08-23
sr-interval: 3
sr-ease: 250
---
Переменные в Ansible - это ключевой механизм для управления динамическими данными. Они позволяют сделать плейбуки и роли гибкими и универсальными. Переменные могут быть определены на разных уровнях и в разных форматах.
# Как задавать переменные
1. **Внутри плейбука**
   Переменные можно объявить в плейбуке с помощью ключа `vars`
```yaml
- hosts: all
  vars:
    app_port: 8080
    app_name: my_app
  tasks:
    - name: Печать переменных
      debug:
        msg: "Приложение {{ app_name }} работает на порту {{ app_port }}"
```
2. **В отдельном YAML-файле**
   Переменные можно вынести в отдельный файл и подключить с помощью ключа `var_files`
```python
playbook.yml
vars/
└── settings.yml
```
Содержимое `vars/settings.yml`
```yaml
app_port: 8080
app_name: my_app
```
Плейбук:
```yaml
- hosts: all
  vars_files:
    - vars/settings.yml
  tasks:
    - name: Печать переменных
      debug:
        msg: "Приложение {{ app_name }} работает на порту {{ app_port }}"
```
3. **В инвентаре**
   Переменные можно определить прямо в файле инвентаря
INI:
```ini
[web_servers]
192.168.1.100 app_port=8080 app_name=my_app
```

YAML:
```yaml
all:
  children:
    web_servers:
      hosts:
        192.168.1.100:
          app_port: 8080
          app_name: my_app
```
4. **В `groups_vars` и `host_vars`**
Для разных групп или отдельных узлов можно использовать папки `groups_vars/` и `host_vars/`
Структура:
```python
group_vars/
└── web_servers.yml
host_vars/
└── 192.168.1.100.yml
```
Содержимое `group_vars/web_servers.yml`:
```yaml
app_port: 8080 app_name: my_web_app
```
Содержимое `host_vars/192.168.1.100.yml`:
```yaml
app_port: 9090 app_name: my_host_app
```
5. **В командной строке**
Переменные можно передать через флаг `--extra-vars` при запуске плейбука
```bash
ansible-playbook playbook.yml -i inventory.ini --extra-vars "app_name=my_app app_port=9090"
```
# Иерархия приоритета переменных
Если одна и та же переменная задана в нескольких местах, используется следующая иерархия (от наивысшего к низшему приоритету):
1. **Переменные из командной строки (`--extra-vars`)**.
2. **Переменные для задачи (ключ `vars` в задаче)**.
3. **Переменные для плейбука (ключ `vars` в плейбуке)**.
4. **Переменные из `host_vars` для конкретного узла**.
5. **Переменные из `group_vars` для группы**.
6. **Переменные из файла `vars_files`**.
7. **Переменные по умолчанию (ключ `defaults` в роли)**.