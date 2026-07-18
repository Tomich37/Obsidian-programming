# Модули и плагины Ansible

[[00 Ansible]]

Модуль выполняет конкретное действие: управляет пакетом, файлом, сервисом, cloud resource. Обычно модуль передаётся на managed node, выполняется и возвращает JSON-результат.

Плагин расширяет поведение самого Ansible: connection, callback, lookup, filter, inventory, strategy, vars и другие точки расширения. Например, SSH connection plugin определяет способ подключения, а callback plugin меняет вывод.

Основные примитивы Ansible: inventory, play, task, module, variable, fact, template, role, handler, collection и plugin.
