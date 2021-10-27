# CNA standards

<img src="cna.png">

### Docker architecture 

<img src="darch.png">

### After connecting from vscode we can do docker request

```
[ashutoshh@ip-172-31-31-134 ~]$ docker  images
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
[ashutoshh@ip-172-31-31-134 ~]$ docker  pull   alpine 
Using default tag: latest
latest: Pulling from library/alpine
a0d0a0d46f8b: Pull complete 
Digest: sha256:e1c082e3d3c45cccac829840a25941e679c25d438cc8412c2fa221cf1a824e6a
Status: Downloaded newer image for alpine:latest
docker.io/library/alpine:latest
[ashutoshh@ip-172-31-31-134 ~]$ docker  images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
alpine       latest    14119a10abf4   2 months ago   5.6MB
[ashutoshh@ip-172-31-31-134 ~]$ 


```

### Docker registry 

<img src="reg.png">

###   CAAS

<img src="caas.png">

### creating container 

<img src="contt.png">

### Building my first webapp docker image 

```
[ashutoshh@ip-172-31-31-134 myapps]$ cd  project-website-template
[ashutoshh@ip-172-31-31-134 project-website-template]$ ls
css         embedding.html  img         js       menu.html  vid
Dockerfile  empty.html      index.html  LICENSE  README.md  widgets.html
[ashutoshh@ip-172-31-31-134 project-website-template]$ docker  build -t ashuwebapp:v1  .  
Sending build context to Docker daemon  2.215MB
Step 1/4 : FROM nginx
latest: Pulling from library/nginx
b380bbd43752: Pull complete 
fca7e12d1754: Pull complete 
745ab57616cb: Pull complete 
a4723e260b6f: Pull complete 
1c84ebdff681: Extracting     666B/666B

```

### Image build stands OCI 

<img src="oci.png">

### standard for pushing image to docker hub 

<img src="push.png">

### pushing image to docker hub 

```
 21  docker  tag  ashuwebapp:v1  dockerashu/ashuwebapp:v1  
   22  docker  images
   23  docker  login  
   24  docker  push  dockerashu/ashuwebapp:v1
   
```

### COntainer related problems 

<img src="crr.png">

### container orchestration engine 

<img src="carch.png">

### k8s architecture 


<img src="k8s1.png">

### ks8 internal 
<img src="k8s2.png">


### auth to k8s master 

```
kubectl  get  nodes  --kubeconfig Desktop/admin.conf 
NAME         STATUS   ROLES                  AGE    VERSION
masternode   Ready    control-plane,master   6d4h   v1.22.2
node1        Ready    <none>                 6d4h   v1.22.2
node2        Ready    <none>                 6d4h   v1.22.2
```

### Pod Design 

<img src="pod1.png">

### POD 1 

```
apiVersion: v1
kind: Pod
metadata:
 name: ashupod-1 
spec: 
 containers:
 - name: ashuc1  # name of container 
   image: dockerashu/ashuwebapp:v1 # image from docker hub 
   ports:
   - containerPort: 80 # nginx app is having default 80 port

```

### Deploy it 

```
kubectl  apply -f  ashupod1.yaml 
pod/ashupod-1 created
 fire@ashutoshhs-MacBook-Air  ~/Desktop/myapp  kubectl  get  pods
NAME        READY   STATUS    RESTARTS   AGE
ashupod-1   1/1     Running   0          5s
```

###

```
kubectl  get  pods -o wide
NAME        READY   STATUS    RESTARTS   AGE    IP                NODE    NOMINATED NODE   READINESS GATES
ashupod-1   1/1     Running   0          115s   192.168.166.165   node1   <none>           <none>
saranran    1/1     Running   0          98s    192.168.166.175   node1   <none>           <none>

```





