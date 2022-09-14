# Урок 1
### Создаем кластер
```shell
minikube start
```

### Создаем pod
```shell
kubectl create -f pod.yaml
```

### Проверяем работы
```shell
kubectl get pod
```
Вывод:
```shell
NAME     READY   STATUS    RESTARTS      AGE
my-pod   1/1     Running   2 (23s ago)   6m12s
```
### Смотрим описание pod 
```shell
kubectl describe pod my-pod
```
### Удаляем pod
```shell
kubectl delete pod my-pod
```