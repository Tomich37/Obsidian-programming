---
Тема: Python web
tags:
  - DevOps
  - Helm
  - review
Дата: 22-08-2025
sr-due: 2025-09-08
sr-interval: 11
sr-ease: 270
---
После создания чарта при помощи команды `helm create myapp` создается следующая структура (примерно):
```bash
myapp/
├── Chart.yaml        # метаданные чарта (имя, версия, описание)
├── values.yaml       # значения по умолчанию
└── templates/        # директория с шаблонами Kubernetes-манифестов
    ├── deployment.yaml
    ├── service.yaml
    └── _helpers.tpl  # вспомогательные шаблоны
```

Пример `values.yaml`:
```yaml
replicaCounts: 2

image:
	repository: nginx
	tag: "1.25"
	pullPolicy: IfNotPresent
	
service:
	type: ClusterIP
	port: 80
```

Пример шаблона `deployment.yaml`
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ .Release.Name }}-deployment
spec:
  replicas: {{ .Values.replicaCount }}
  selector:
    matchLabels:
      app: {{ .Release.Name }}
  template:
    metadata:
      labels:
        app: {{ .Release.Name }}
    spec:
      containers:
      - name: {{ .Chart.Name }}
        image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
        imagePullPolicy: {{ .Values.image.pullPolicy }}
        ports:
        - containerPort: {{ .Values.service.port }}
```

Пример шаблона `service.yaml`
```yaml
apiVersion: v1
kind: Service
metadata:
  name: {{ .Release.Name }}-service
spec:
  type: {{ .Values.service.type }}
  selector:
    app: {{ .Release.Name }}
  ports:
  - port: {{ .Values.service.port }}
    targetPort: {{ .Values.service.port }}
```

Что происходит при установке:
```bash
helm install my-nginx ./myapp
```
Helm берёт:
- шаблоны (`templates/*.yaml`)    
- подставляет значения из `values.yaml`    
- генерирует готовые YAML и применяет их в кластер    

То есть вместо ручного редактирования YAML ты управляешь только `values.yaml`.