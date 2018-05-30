# k8s-homework

作業一
---

* 啟動 minikube
``` bash
$ minikube start
```

* 建立所有的元件
``` bash
$ kubectl create -f . -R=true
pod "nginx-pod-1" created
pod "nginx-pod-2" created
pod "nginx-pod-3" created
service "nginx-svc" created
configmap "password" created
secret "account" created
```

* 查看 minikube ip
```bash
$ minikube ip
192.168.99.100
```

* 查看 k8s 指定的 nodePort
1. 方法一
```bash
$ kubectl get service nginx-svc
NAME        TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
nginx-svc   NodePort   10.96.111.126   <none>        80:32714/TCP   7m
````
2. 方法二
```bash
$ kubectl describe service nginx-svc
Name:                     nginx-svc
Namespace:                default
Labels:                   app=nginx
Annotations:              <none>
Selector:                 app=nginx,backend=go
Type:                     NodePort
IP:                       10.96.111.126
Port:                     <unset>  80/TCP
TargetPort:               80/TCP
NodePort:                 <unset>  32714/TCP
Endpoints:                172.17.0.5:80,172.17.0.6:80
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
```

* 可用 `http://<minikubeip>:<nodePort>/` 查看後端 nginx pod 的網頁，會隨機連到 nginx-pod-1、nginx-pod-2
```bash
$ curl http://192.168.99.100:32714
secret-account%

$ curl http://192.168.99.100:32714
cfgmap-password
```

* 可用 `kubectl logs -f <podName>` 查看 ngixn log
```bash
$ kubectl logs -f nginx-pod-1
```