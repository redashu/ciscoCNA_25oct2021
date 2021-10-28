# Rev of CNA as of now

<img src="cna.png">

### a closure look to k8s 

<img src="etcd.png">

### pod to k8s 

<img src="pod1.png">

### k8s auto pod yaml generation 

```
kubectl  run  ashuwebpod  --image=dockerashu/ashuwebapp:v1  --port 80 --dry-run=client  -o yaml 
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: ashuwebpod
  name: ashuwebpod
spec:
  containers:
  - image: dockerashu/ashuwebapp:v1
    name: ashuwebpod
    ports:
    - containerPort: 80
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  kubectl  run  ashuwebpod  --image=dockerashu/ashuwebapp:v1  --port 80 --dry-run=client  -o yaml   >myapp.yaml 
 
 ```
 
 ### Deleting all the POD 
 
 ```
 kubectl delete pod  ashupod-1   
pod "ashupod-1" deleted
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  kubectl delete pods --all
pod "ashtiwa2pod-1" deleted
pod "deepupod1" deleted
pod "deepupod11" deleted
pod "hello" deleted
pod "hello1-node2" deleted
pod "rajpod1" deleted
pod "saranran" deleted
pod "vaibhav-1" deleted

```
### Deploy pod 

```
 kubectl  apply -f  myapp.yaml 
pod/ashuwebpod created
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  kubectl get  po 
NAME           READY   STATUS    RESTARTS      AGE
ashuwebpod     1/1     Running   0             4s
hello1-node2   1/1     Running   1 (18h ago)   59s
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  kubectl get  po  -o wide
NAME           READY   STATUS    RESTARTS      AGE   IP                NODE    NOMINATED NODE   READINESS GATES
ashuwebpod     1/1     Running   0             12s   192.168.166.169   node1   <none>           <none>
hello1-node2   1/1     Running   1 (18h ago)   67s   192.168.104.17    node2   <none>           <none>
```
### Problem with POD 

<img src="prob.png">

### k8s deployment 

<img src="dep.png">

### creating deployment YAML 

```
kubectl  create deployment  ashuweb  --image=dockerashu/ashuwebapp:v1  --dry-run=client  -o yaml 
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: ashuweb
  name: ashuweb
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ashuweb
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: ashuweb
    spec:
      containers:
      - image: dockerashu/ashuwebapp:v1
        name: ashuwebapp
        resources: {}
status: {}
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  kubectl  create deployment  ashuweb  --image=dockerashu/ashuwebapp:v1  --dry-run=client  -o yaml  >deployment.yaml 

```

###

```
kubectl apply -f  deployment.yaml 
deployment.apps/ashuweb created
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  kubectl  get deployment 
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
ashuweb   1/1     1            1           8s
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  kubectl  get  po 
NAME                       READY   STATUS    RESTARTS      AGE
ashuweb-7764fc5df4-wznzn   1/1     Running   0             20s
hello1-node2               1/1     Running   1 (18h ago)   3m26s
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  kubectl delete po ashuweb-7764fc5df4-wznzn
pod "ashuweb-7764fc5df4-wznzn" deleted
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  kubectl  get  po                          
NAME                       READY   STATUS    RESTARTS      AGE
ashuweb-7764fc5df4-nd2j2   1/1     Running   0             4s
hello1-node2               1/1     Running   1 (18h ago)   3m38s

```

### scaling pod 

```
 kubectl  scale  deployment  ashuweb  --replicas=3
deployment.apps/ashuweb scaled
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  kubectl get deploy                               
NAME         READY   UP-TO-DATE   AVAILABLE   AGE
ashuweb      3/3     3            3           4m12s
chandra      1/1     1            1           95s
deepuweb     1/1     1            1           67s
rajweb       1/1     1            1           84s
saranweb     1/1     1            1           2m9s
vaibhavweb   1/1     1            1           106s
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  kubectl get po                                   
NAME                          READY   STATUS    RESTARTS      AGE
ashuweb-7764fc5df4-bhcgx      1/1     Running   0             14s
ashuweb-7764fc5df4-nd2j2      1/1     Running   0             3m54s
ashuweb-7764fc5df4-sh5kw      1/1     Running   0             14s

```

### all the deployments 

```
59s
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  kubectl delete deployment  ashuweb 
deployment.apps "ashuweb" deleted
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  kubectl delete deployment  --all   
deployment.apps "ashtiwaweb" deleted
deployment.apps "chandra" deleted
deployment.apps "deepuweb" deleted
deployment.apps "rajweb" deleted
deployment.apps "saranweb" deleted

```

### exposing deployment to access application in k8s

```
kubectl  get deployment                                              
NAME         READY   UP-TO-DATE   AVAILABLE   AGE
ashtiwaweb   3/3     3            3           8m12s
ashuweb      3/3     3            3           8m8s
deepuweb     2/2     2            2           41s
rajweb       2/2     2            2           7m53s
saranweb     3/3     3            3           6m1s
vaibhavweb   2/2     2            2           6m58s
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  kubectl  expose   deployment ashuweb  --type LoadBalancer  --port 80  
 ✘ fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  
 ✘ fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  kubectl  get  service 
NAME         TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
ashtiwaweb   LoadBalancer   10.100.136.191   <pending>     80:32404/TCP   13s
ashuweb      LoadBalancer   10.102.243.176   <pending>     80:30610/TCP   33s
kubernetes   ClusterIP      10.96.0.1        <none>        443/TCP        5d20h
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  kubectl  get  svc     
NAME         TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
ashtiwaweb   LoadBalancer   10.100.136.191   <pending>     80:32404/TCP   18s
ashuweb      LoadBalancer   10.102.243.176   <pending>     80:30610/TCP   38s
kubernetes   ClusterIP      10.96.0.1        <none>        443/TCP        5d20h
vaibhavweb   LoadBalancer   10.104.239.132   <pending>     80:30697/TCP   1s

```

### updating new image 

```
 kubectl  set  image  deployment  ashuweb  ashuwebapp=dockerashu/ashuwebapp:v2 
 
                                             name of container 
 ```
 
 
### DB 

<img src="db.png">

### DB in CNA 

<img src="dbaas.png">

### better to use CNA model cloud service for RDBMS 

<img src="db11.png">

### CNA starndart to containers

<img src="std.png">

### K8s app to external Db 

<img src="externaldb.png">

### Deploy web app 

```
kubectl  create  deployment   ashuwebapp  --image=wordpress:4.8-apache --dry-run=client  -o yaml  >frontendapp.yaml 

```

### creating db sec

```
 kubectl  create  secret generic  dbsec1  --from-literal  sqlpass="Rhel098)(*"
 
```

### creating INTernal DNS 

```
kubectl  create  service  externalname   ashudb --external-name ciscodb.cqypbbo9r82r.us-east-1.rds.amazonaws.com  --tcp 3306  --dry-run=client -o yaml 
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    app: ashudb
  name: ashudb
spec:
  externalName: ciscodb.cqypbbo9r82r.us-east-1.rds.amazonaws.com
  ports:
  - name: "3306"
    port: 3306
    protocol: TCP
    targetPort: 3306
  selector:
    app: ashudb
  type: ExternalName
status:
  loadBalancer: {}

```

###

```
mysql -u admin  -h ashudb  -p 
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 74
Server version: 8.0.23 Source distribution

Copyright (c) 2000, 2021, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> exit;
Bye

```

### Devops intro 

<img src="dev1.png">

### IAC 

<img src="iac.png">





