# Ad hoc команды Ansible

[[00 Ansible]]

Ad hoc command выполняет одну разовую задачу без отдельного playbook. Подходит для проверки связи, сбора фактов, перезапуска сервиса или срочной однотипной операции. Для воспроизводимых изменений лучше playbook в Git.

```bash
# Проверяет доступность всех узлов inventory через модуль ping.
# Ожидаемо: SUCCESS и pong для доступных hosts либо причина ошибки SSH/Python.
ansible all -i inventory.ini -m ansible.builtin.ping

# Показывает uptime группы web без внесения изменений.
# Ожидаемо: stdout команды uptime по каждому узлу.
ansible web -i inventory.ini -m ansible.builtin.command -a 'uptime'
```
