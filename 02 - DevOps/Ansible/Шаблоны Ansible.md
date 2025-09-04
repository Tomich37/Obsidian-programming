---
Тема: Ansible
tags:
  - DevOps
  - Ansible
  - review
Дата: 23-11-2023
sr-due: 2025-08-29
sr-interval: 1
sr-ease: 210
---
Шаблоны в Ansible позволяют генерировать конфигурационные файлы, скрипты и другие текстовые файлы с использованием переменных. Это делается с помощью **Jinja2**, мощного шаблонизатора, который поддерживает циклы, условия, фильтры и многое другое.
### **Cоздание шаблона**
Шаблон — это файл с расширением `.j2` (например, `config.j2`). Внутри используются переменные Ansible, обрамленные двойными фигурными скобками (`{{ variable }}`).

Пример шаблона `nginx.conf.j2`
```jinja2
server {
    listen {{ web_server.port }};
    server_name {{ web_server.name }};
    
    location / {
        proxy_pass http://{{ web_server.backend }};
    }
}
```
### **Подключение шаблона в плейбуке**
Для работы с шаблонами используется модуль **`template`**, который копирует сгенерированный файл на целевой узел.
```yaml
- hosts: all
  vars:
    web_server:
      name: example.com
      port: 80
      backend: 192.168.1.10
  tasks:
    - name: Создание конфигурации Nginx
      template:
        src: templates/nginx.conf.j2
        dest: /etc/nginx/nginx.conf
```
### **Шаблоны с условиями**
В шаблонах можно использовать условия с `if` и `else`.
```jinja
{% if debug_mode %}
debug = true
{% else %}
debug = false
{% endif %}
```
Если в переменной `debug_mode` будет `true`, то в итоговом файле появится:
```text
debug = true
```
### **Шаблоны с циклами**
С помощью цикла `for` можно генерировать повторяющиеся части файла.
`hosts.j2`:
```jinja
{% for host in web_servers %}
server {{ host }}:80;
{% endfor %}
```
Плейбук:
```yaml
- hosts: all
  vars:
    web_servers:
      - server1.example.com
      - server2.example.com
  tasks:
    - name: Создание файла hosts
      template:
        src: templates/hosts.j2
        dest: /etc/hosts
```
Результат:
```text
server server1.example.com:80;
server server2.example.com:80;
```
### **Фильтры Jinja2**
Фильтры используются для модификации переменных. Вот несколько полезных примеров:
- **`lower`**: Приведение строки к нижнему регистру.
- **`upper`**: Приведение строки к верхнему регистру.
- **`default`**: Установка значения по умолчанию.
- **`join`**: Объединение списка в строку.
Пример:
```jinja
server_name {{ web_server.name | lower }};
allowed_ips {{ allowed_ips | join(', ') }};
```
### **Валидация шаблонов**
Перед использованием шаблона можно проверить его на синтаксические ошибки. Например, для Nginx:
```bash
nginx -t -c /etc/nginx/nginx.conf
```
