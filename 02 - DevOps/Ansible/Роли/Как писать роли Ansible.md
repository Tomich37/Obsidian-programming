---
Тема: Ansible
tags:
  - DevOps
  - Ansible
  - review
Дата: 23-11-2023
sr-due: 2025-09-03
sr-interval: 6
sr-ease: 230
---
Создание роли в Ansible включает несколько шагов: от определения задач до организации файлов в правильной структуре. Роли можно создавать вручную или с помощью команды `ansible-galaxy init`
# Шаг 1: создание структуры роли
Используем `ansible-galaxy init`
Команда автоматически создает стандартную структуру для роли
```bash
ansible-galaxy init role_name
```

Результат:
```python
role_name/
├── tasks/          # Задачи роли
│   └── main.yml    # Главный файл задач
├── handlers/       # Хэндлеры (например, команды перезапуска)
│   └── main.yml
├── templates/      # Шаблоны (например, конфигурационные файлы)
├── files/          # Статические файлы (например, бинарники)
├── vars/           # Переменные роли
│   └── main.yml
├── defaults/       # Переменные по умолчанию
│   └── main.yml
├── meta/           # Метаинформация о роли (зависимости и т.д.)
│   └── main.yml
├── tests/          # Файлы для тестирования роли
├── README.md       # Документация роли

```
# Шаг 2: написание задач
Задачи роли определяются в `task/main.yml`. Это основной файл, где указываются действия, которые должна выполнять роль.

Пример для роли установки Nginx:
```yaml
---
- name: Установить Nginx
  apt:
    name: nginx
    state: present

- name: Настроить конфигурационный файл
  template:
    src: nginx.conf.j2
    dest: /etc/nginx/nginx.conf
  notify:
    - Перезапустить Nginx
```
# Шаг 3: добавление хэндлеров
Хэндлеры выполняются только тогда, когда их вызывает задача. Обычно это команды для перезапуска или обновления сервисов

Пример в `handlers/main.yml`:
```yaml
---
- name: Перезапустить Nginx
  service:
    name: nginx
    state: restarted
```
# Шаг 4: использование шаблонов
Если нужно динамически генерировать файлы, шаблоны создаются в `templates/`. Они используют синтаксис Jinja2.

Пример шаблона `templates/nginx.conf.j2`
```nginx
server {
    listen 80;
    server_name {{ server_name }};

    location / {
        root {{ document_root }};
        index index.html;
    }
}
```

Переменные `server_name` и `document_root` можно задать в `vars/main.yml`:
```yaml
---
server_name: example.com
document_root: /var/www/html
```
# Шаг 5: добавление переменных
Переменные роли можно задать в двух местах:
- `defaults/main.yml`: переменные по умолчанию, которые можно переопределить
- `vars/main.yml`: переменные, которые имеют более высокий приоритет

Пример `defaults/main.yml`:
```yaml
---
nginx_package: nginx
nginx_service: nginx
```
# Шаг 6: зависимости
Если роль зависит от других ролей, это указывается в `meta/main.yml`
```yaml
dependencies:
  - { role: common, vars: { some_var: value } }
```
# Использование роли
После написания роли необходимо добавить ее в плейбук. Например

Инвентарь (`inventory.ini`)
```ini
[web_servers]
192.168.1.100
```

Плейбук (`playbook.yml`)
```yaml
---
- hosts: web_servers
  become: yes
  roles:
    - nginx_setup
```

Запуск
```bash
ansible-playbook -i inventory.ini playbook.yml
```
