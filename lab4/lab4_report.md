# Лабораторная работа №4 "Сети связи в Minikube, CNI и CoreDNS"

## Общая информация

University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)

Year: 2022/2023

Group: K4112c

Author: Orel Daniil Maximovich

Lab: Lab3

Date of create: 30.10.2022

Date of finished:

## Ход работы

### Запуск minikube кластера с несколькими нодами (Nodes) и CNI плагином calico

Для запуска кластера minikube с 2 нодами и плагином CNI, была использована следующая команда: 

```bash
$ minikube start --driver=docker --nodes 2 -p multinode-cluster --network-plugin=cni
```

После запуска кластера были созданы 2 ноды:

```bash
$ k get nodes

# Output
NAME                    STATUS   ROLES           AGE     VERSION
multinode-cluster       Ready    control-plane   2m45s   v1.25.2
multinode-cluster-m02   Ready    <none>          2m8s    v1.25.2
```

Развертывание calico:
```bash
$ kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/v3.24.3/manifests/calico.yaml

$ kubectl get po -n kube-system -l=k8s-app=calico-node

# Output:
NAME                READY   STATUS    RESTARTS   AGE
calico-node-mtmrt   1/1     Running   0          4m57s
calico-node-rcj29   1/1     Running   0          4m57s
```

### Добавление меток для нод

```bash
$ kubectl label nodes multinode-cluster zone=east
$ kubectl label nodes multinode-cluster-m02 zone=west
```
