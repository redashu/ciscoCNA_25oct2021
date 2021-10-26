#  Day 2 

## to Deploy webapplication 
<img src="app.png">

### to deploy web app in CLOud model  -- we can choose Delivery models

<img src="IAAS_PAAS.png">

### Instance connection via ssh 

```
ssh -i Desktop/ashutoshhkey.pem  ec2-user@18.224.139.150
The authenticity of host '18.224.139.150 (18.224.139.150)' can't be established.
ECDSA key fingerprint is SHA256:6SNbP8GmSt7UInx61qm5zhFVNdXw8yD824uBIkvU1r4.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '18.224.139.150' (ECDSA) to the list of known hosts.

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-2/
3 package(s) needed for security, out of 15 available
Run "sudo yum update" to apply all updates.
-bash: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory
[ec2-user@ip-172-31-31-215 ~]$ 
[ec2-user@ip-172-31-31-215 ~]$ whoami
ec2-user


```

### Download webapp and install httpd app server

```
[root@ip-172-31-17-13 ~]# history 
    1  yum  install  httpd  
    2  yum  install httpd
    3  yum  install httpd -ty
    4  yum install httpd 
    5  git  clone  https://github.com/yenchiah/project-website-template
    6  yum  install  git 
    7  history 
[root@ip-172-31-17-13 ~]# yum  install  git 
Failed to set locale, defaulting to C
Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
Package git-2.32.0-1.amzn2.0.1.x86_64 already installed and latest version
Nothing to do
[root@ip-172-31-17-13 ~]# git  clone  https://github.com/yenchiah/project-website-template
Cloning into 'project-website-template'...
remote: Enumerating objects: 937, done.
remote: Total 937 (delta 0), reused 0 (delta 0), pack-reused 937
Receiving objects: 100% (937/937), 1.07 MiB | 10.51 MiB/s, done.
Resolving deltas: 100% (585/585), done.
[root@ip-172-31-17-13 ~]# ls
project-website-template


```

### copy webapp code to /var/www/html/

```
[root@ip-172-31-17-13 ~]# cp -rf  project-website-template/*  /var/www/html/
[root@ip-172-31-17-13 ~]# 
[root@ip-172-31-17-13 ~]# 
[root@ip-172-31-17-13 ~]# cd  /var/www/html/
[root@ip-172-31-17-13 html]# ls
LICENSE  README.md  css  embedding.html  empty.html  img  index.html  js  menu.html  vid  widgets.html
[root@ip-172-31-17-13 html]# 



```

### starting app server

```
cd  /var/www/html/
[root@ip-172-31-17-13 html]# ls
LICENSE  README.md  css  embedding.html  empty.html  img  index.html  js  menu.html  vid  widgets.html
[root@ip-172-31-17-13 html]# systemctl start httpd
[root@ip-172-31-17-13 html]# systemctl status httpd
● httpd.service - The Apache HTTP Server
   Loaded: loaded (/usr/lib/systemd/system/httpd.service; disabled; vendor preset: disabled)
   Active: active (running) since Tue 2021-10-26 05:58:56 UTC; 5s ago
     Docs: man:httpd.service(8)
 Main PID: 3691 (httpd)
   Status: "Processing requests..."
   CGroup: /system.slice/httpd.service
           ├─3691 /usr/sbin/httpd -DFOREGROUND
           ├─3692 /usr/sbin/httpd -DFOREGROUND
           ├─3693 /usr/sbin/httpd -DFOREGROUND
           ├─3694 /usr/sbin/httpd -DFOREGROUND
           ├─3695 /usr/sbin/httpd -DFOREGROUND
           └─3696 /usr/sbin/httpd -DFOREGROUND

Oct 26 05:58:56 ip-172-31-17-13.us-east-2.compute.internal systemd[1]: Starting The Apache HTTP Server...
Oct 26 05:58:56 ip-172-31-17-13.us-east-2.compute.internal systemd[1]: Started The Apache HTTP Server.

```

