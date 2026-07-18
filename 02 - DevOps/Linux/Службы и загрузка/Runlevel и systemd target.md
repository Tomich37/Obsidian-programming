# Runlevel и systemd target

[[00 Службы и загрузка Linux]]

`Runlevel` - старый способ описать режим работы системы в SysV init.

Типовые runlevel:
- `0` - shutdown;
- `1` - single-user/rescue;
- `3` - multi-user без графики;
- `5` - multi-user с графикой;
- `6` - reboot.

В `systemd` вместо runlevel используют `target`.

Примеры target:
- `rescue.target`;
- `multi-user.target`;
- `graphical.target`;
- `reboot.target`;
- `poweroff.target`.

Команды:
```bash
# Показывает текущий systemd target.
# Ожидаемо: multi-user.target или graphical.target.
systemctl get-default

# Устанавливает target по умолчанию без графики.
# Ожидаемо: следующая загрузка пойдет в multi-user.target.
systemctl set-default multi-user.target

# Переключает систему в rescue mode.
# Ожидаемо: система остановит лишние сервисы и перейдет в rescue.
systemctl isolate rescue.target
```

Короткий ответ:

Runlevel - старое понятие SysV init, а в systemd его заменили target'ы. По смыслу это режимы работы системы.

