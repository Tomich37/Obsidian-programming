# Как разбирать OOMKilled и нехватку памяти

[[00 Linux - вопросы]]

`OOMKilled` означает, что процесс был убит из-за нехватки памяти. В Kubernetes это часто видно в статусе контейнера, в Linux - через сообщения ядра.

Проверки на Linux:
```bash
free -h
dmesg | grep -i oom
journalctl -k | grep -i oom
ps aux --sort=-%mem | head
```

Проверки в Kubernetes:
```bash
kubectl describe pod <pod>
kubectl logs <pod> --previous
kubectl top pod
```

Что выяснить:
- сколько памяти потребляет процесс;
- есть ли memory leak;
- какие лимиты выставлены;
- не слишком ли маленький limit;
- есть ли рост памяти со временем;
- не убивает ли приложение spike нагрузки.

Короткий ответ:

Я бы подтвердил OOM через `dmesg` или `kubectl describe`, посмотрел потребление памяти, лимиты и динамику роста. Дальше решал бы: увеличивать limit, оптимизировать приложение или искать утечку.

