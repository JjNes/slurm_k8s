# Урок 2: ReplicaSet
### Создаем replicaset
```shell
kubectl apply -f replicaset.yaml
```
### Проверяем работу
```shell
kubectl get rp
```
Вывод:
```shell
NAME            DESIRED   CURRENT   READY   AGE
my-replicaset   2         2         2       36s
```

### Смотрим pod
```shell
kubectl get pod
```
Вывод:
```shell
NAME                  READY   STATUS    RESTARTS   AGE
my-replicaset-8zmkh   1/1     Running   0          92s
my-replicaset-99w2z   1/1     Running   0          92s
```
### Удалим один pod
```shell
kubectl delete pod my-replicaset-8zmkh
```
Вывод:
```shell
pod "my-replicaset-8zmkh" deleted
```
Проверяем:
```shell
kubectl get pod 
```
Количество подов не изменилось. Но по времени жизни видно, что один из подов запущен 4 секунды назад. Кубер поддерживает указанное количество реплик, что бы с ними не происходило.
```shell
NAME                  READY   STATUS    RESTARTS   AGE
my-replicaset-8685c   1/1     Running   0          4s
my-replicaset-99w2z   1/1     Running   0          4m15s
```

### Увеличиваем количество реплик
```shell
kubectl scale --replicas 3 replicaset my-replicaset 
```
```shell
NAME                  READY   STATUS    RESTARTS   AGE
my-replicaset-4plmq   1/1     Running   0          47s
my-replicaset-8685c   1/1     Running   0          28m
my-replicaset-99w2z   1/1     Running   0          32m
```

### Меняем образ контейнера
```shell
kubectl set image replicaset my-replicaset nginx=quay.io/testing-farm/nginx:1.13
```
```shell
kubectl describe replicaset my-replicaset
```
```shell
Containers:
   nginx:
    Image:        quay.io/testing-farm/nginx:1.13
```
Но это мы поменяли шаблон. Поды остались со старой версией. Новые уже будут создаваться в новой версией ораза.

### Чистим кластер
```shell
kubectl delete replicaset --all 
```