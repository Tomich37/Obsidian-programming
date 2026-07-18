# ConfigMap и Secret

[[00 Глоссарий]]

`ConfigMap` хранит неконфиденциальную конфигурацию:
- параметры приложения;
- feature flags;
- config files;
- переменные окружения.

`Secret` хранит чувствительные данные:
- пароли;
- токены;
- ключи;
- credentials для registry.

Как подключают в pod:
- переменными окружения;
- файлами через volume;
- imagePullSecret;
- service account token.

Команды:
```bash
# Показывает ConfigMap в namespace.
# Ожидаемо: список configmap и возраст.
kubectl get configmap

# Показывает Secret в namespace.
# Ожидаемо: NAME, TYPE, DATA, AGE; значения не выводятся.
kubectl get secret

# Показывает подробности Secret.
# Ожидаемо: тип и ключи data; значения будут base64, не открытый текст.
kubectl describe secret <secret>
```

Короткий ответ:

ConfigMap - обычная конфигурация, Secret - чувствительные данные. Оба можно передавать в pod как env или файлы.

