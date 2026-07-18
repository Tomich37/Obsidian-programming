# Volume PV PVC и StorageClass

[[00 Глоссарий]]

`Volume` - хранилище, подключенное к pod.

Обычный volume живет в рамках pod и может пропасть при удалении pod, если это временный тип.

`PersistentVolume` (`PV`) - постоянное хранилище на уровне кластера.

`PersistentVolumeClaim` (`PVC`) - запрос приложения на постоянное хранилище.

`StorageClass` описывает, как динамически создавать PV: через cloud disk, Ceph, NFS, EBS и другие backend'ы.

Команды:
```bash
# Показывает persistent volumes в кластере.
# Ожидаемо: CAPACITY, ACCESS MODES, RECLAIM POLICY, STATUS.
kubectl get pv

# Показывает persistent volume claims в namespace.
# Ожидаемо: STATUS Bound/Pending, VOLUME, CAPACITY.
kubectl get pvc

# Показывает доступные StorageClass.
# Ожидаемо: provisioner, reclaim policy, volume binding mode.
kubectl get storageclass
```

Короткий ответ:

PVC - запрос на диск, PV - сам диск в кластере, StorageClass - правило, как такие диски создавать.

