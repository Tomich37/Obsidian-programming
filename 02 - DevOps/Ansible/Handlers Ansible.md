# Handlers Ansible

[[00 Ansible]]

Handler — задача, которая запускается через `notify` только если уведомившая задача изменила состояние. Обычно handler перезапускает или reload'ит сервис после изменения конфигурации.

Несколько уведомлений одного handler в play приводят к одному запуску в конце play. `meta: flush_handlers` позволяет выполнить накопленные handlers раньше.

```yaml
# Копирование уведомляет handler только при фактическом изменении файла.
# Ожидаемо: nginx reload выполнится один раз в конце play, если шаблон изменился.
tasks:
  - name: Установить конфигурацию nginx
    ansible.builtin.template:
      src: nginx.conf.j2
      dest: /etc/nginx/nginx.conf
      mode: "0644"
    notify: Перезагрузить nginx

handlers:
  - name: Перезагрузить nginx
    ansible.builtin.service:
      name: nginx
      state: reloaded
```
