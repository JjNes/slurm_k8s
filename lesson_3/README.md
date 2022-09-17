# Урок 3: Deployment
### Создаем deployment
```shell
kubectl apply -f deployment.yaml
```
### Проверяем работу
```shell
kubectl get deployment
```
Вывод:
```shell
NAME             READY   UP-TO-DATE   AVAILABLE   AGE
my-deployment   2/2     2            2           76s
```

### Смотрим pod
```shell
kubectl get pod
```
Вывод:
```shell
NAME                             READY   STATUS    RESTARTS   AGE
my-deployment-f69cf9f56-dm9zd   1/1     Running   0          114s
my-deployment-f69cf9f56-wtw85   1/1     Running   0          114s
```

### Меняем образ контейнера
Меняем образ через редактирование "на лету"
```shell
kubectl edit deployment my-deployment
```
```shell
kubectl get pod
```
```shell
NAME                            READY   STATUS    RESTARTS   AGE
my-deployment-785555dc-wkkb5   1/1     Running   0          17s
my-deployment-785555dc-xl7nj   1/1     Running   0          8s
```
Видно, что поменялся хэш в названии подов. Кубер поднял поды с обновленным образом, а старые удалил. 
Сделаем вывод replicaset.
```shell
NAME                       DESIRED   CURRENT   READY   AGE
my-deployment-785555dc    2         2         2       3m17s
my-deployment-f69cf9f56   0         0         0       24m
```
Кубер не удалил стрый replicaset. Все это для того, чтобы можно было откатить изменения.
```shell
kubectl rollout undo deployment my-deployment
```
```shell
NAME                       DESIRED   CURRENT   READY   AGE
my-deployments-785555dc    0         0         0       6m47s
my-deployments-f69cf9f56   2         2         2       28m
```
### Чистим кластер
```shell
kubectl delete deployment --all 
```