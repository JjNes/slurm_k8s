# Создаем кластер
minikube start

# Создаем pod
kubectl create -f pod.yaml

# Проверям работу
kubectl get pod

NAME     READY   STATUS    RESTARTS      AGE
my-pod   1/1     Running   2 (23s ago)   6m12s

# Смотрим описание pod 
kubectl describe pod my-pod

# Удаляем 
kubectl delete pod my-pod