

Follow the tutorial at https://kubernetes.io/docs/tutorials/stateless-application/guestbook/.

For logging and monitoring with ELK
https://kubernetes.io/docs/tutorials/stateless-application/guestbook-logs-metrics-with-elk/#start-up-the-php-guestbook-with-redis

******************************8
 To allow the pod/container processes to eun with normal user with sudo rights and permissions.
  oc login -u system:admin

  oc adm policy add-scc-to-user anyuid -n nodejs-echo -z default

  oc get po --all-namespaces=true

  Create service
  oc apply -f redis-master-service.yaml

    oc get svc

    oc describe svc redis-master

    oc get svc redis-master -o yaml

   oc get svc frontend-service -o yaml

  NOt that end points are are not defined.
  
  create deployment
  
   
  oc apply -f redis-master-deployment.yaml

    oc get deploy
    oc get pods

  oc describe po redis-master-deployment-6cb9989d7c-nv4bf
    

PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=redis-master-deployment-6cb9989d7c-nv4bf
REDIS_MASTER_PORT=tcp://172.30.140.246:6379
REDIS_MASTER_PORT_6379_TCP=tcp://172.30.140.246:6379
KUBERNETES_SERVICE_HOST=172.30.0.1
REDIS_MASTER_SERVICE_PORT=6379
REDIS_MASTER_PORT_6379_TCP_PORT=6379
REDIS_MASTER_PORT_6379_TCP_ADDR=172.30.140.246
REDIS_MASTER_PORT_6379_TCP_PROTO=tcp
KUBERNETES_PORT_443_TCP=tcp://172.30.0.1:443
KUBERNETES_PORT_443_TCP_ADDR=172.30.0.1
REDIS_MASTER_SERVICE_HOST=172.30.140.246
KUBERNETES_SERVICE_PORT=443
KUBERNETES_SERVICE_PORT_HTTPS=443
KUBERNETES_PORT=tcp://172.30.0.1:443
KUBERNETES_PORT_443_TCP_PROTO=tcp
KUBERNETES_PORT_443_TCP_PORT=443
GOSU_VERSION=1.11
REDIS_VERSION=5.0.7
REDIS_DOWNLOAD_URL=http://download.redis.io/releases/redis-5.0.7.tar.gz
REDIS_DOWNLOAD_SHA=61db74eabf6801f057fd24b590232f2f337d422280fd19486eca03be87d3a82b
HOME=/



 oc exec  redis-master-deployment-6cb9989d7c-nv4bf  -- printenv | grep SERVICE

  KUBERNETES_SERVICE_HOST=172.30.0.1
REDIS_MASTER_SERVICE_PORT=6379
REDIS_MASTER_SERVICE_HOST=172.30.140.246
KUBERNETES_SERVICE_PORT=443
KUBERNETES_SERVICE_PORT_HTTPS=443

  



The fonnt ends are slave host looks for service host named as 'REDIS_MASTER_SERVICE_HOST' in guestBook.php

  Deploy redis-slave-service 
  oc apply -f redis-slave-service.yaml
  oc get svc

  oc describe svc redis-slave
 -->No end points
 

  Deploy redis slve deployment
  oc apply -f redis-slave-deployment.yaml

  oc get deploy

  oc describe deploy redis-slave-deployment

  oc get po
 

   oc describe svc redis-slave

   Name:              redis-slave
Namespace:         nodejs-echo
Labels:            app=redis-slave-app
                   role=slave-role
                   tier=backend-service
Annotations:       kubectl.kubernetes.io/last-applied-configuration={"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"labels":{"app":"redis-slave-app","role":"slave-role","tier":"backend-service"},"name"...
Selector:          app=redis-pod,role=slave-pod,tier=backend-pod
Type:              ClusterIP
IP:                172.30.174.228
Port:              <unset>  6379/TCP
TargetPort:        6379/TCP
Endpoints:         172.17.0.6:6379,172.17.0.7:6379
Session Affinity:  None
Events:            <none>

  oc get po
  redis-master-deployment-6cb9989d7c-nv4bf   1/1       Running   0          21m
redis-slave-deployment-599d5d4d6d-rs6pt    1/1       Running   0          3m
redis-slave-deployment-599d5d4d6d-spd7c    1/1       Running   0          3m

  
  
  To find the env variables on redis-salve pods

  oc exec  redis-slave-deployment-599d5d4d6d-rs6pt   -- printenv

     PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HOSTNAME=redis-slave-deployment-599d5d4d6d-rs6pt
GET_HOSTS_FROM=dns
KUBERNETES_PORT=tcp://172.30.0.1:443
KUBERNETES_PORT_443_TCP=tcp://172.30.0.1:443
KUBERNETES_PORT_443_TCP_ADDR=172.30.0.1
REDIS_MASTER_PORT_6379_TCP_PROTO=tcp
REDIS_SLAVE_PORT_6379_TCP=tcp://172.30.174.228:6379
KUBERNETES_SERVICE_PORT_HTTPS=443
KUBERNETES_SERVICE_PORT=443
KUBERNETES_PORT_443_TCP_PORT=443
REDIS_SLAVE_PORT_6379_TCP_PORT=6379
KUBERNETES_SERVICE_HOST=172.30.0.1
KUBERNETES_PORT_443_TCP_PROTO=tcp
REDIS_MASTER_PORT_6379_TCP_ADDR=172.30.140.246
REDIS_SLAVE_SERVICE_PORT=6379
REDIS_SLAVE_PORT_6379_TCP_ADDR=172.30.174.228
REDIS_SLAVE_PORT_6379_TCP_PROTO=tcp
REDIS_MASTER_SERVICE_HOST=172.30.140.246
REDIS_MASTER_SERVICE_PORT=6379
REDIS_MASTER_PORT=tcp://172.30.140.246:6379
REDIS_MASTER_PORT_6379_TCP=tcp://172.30.140.246:6379
REDIS_MASTER_PORT_6379_TCP_PORT=6379
REDIS_SLAVE_SERVICE_HOST=172.30.174.228
REDIS_SLAVE_PORT=tcp://172.30.174.228:6379
REDIS_VERSION=3.0.3
REDIS_DOWNLOAD_URL=http://download.redis.io/releases/redis-3.0.3.tar.gz
REDIS_DOWNLOAD_SHA1=0e2d7707327986ae652df717059354b358b83358
HOME=/
  
 oc exec  redis-slave-deployment-599d5d4d6d-rs6pt   -- printenv  | grep SERVICE  
  KUBERNETES_SERVICE_PORT_HTTPS=443
KUBERNETES_SERVICE_PORT=443
KUBERNETES_SERVICE_HOST=172.30.0.1
REDIS_SLAVE_SERVICE_PORT=6379
REDIS_MASTER_SERVICE_HOST=172.30.140.246
REDIS_MASTER_SERVICE_PORT=6379
REDIS_SLAVE_SERVICE_HOST=172.30.174.228

  oc exec  redis-slave-deployment-599d5d4d6d-spd7c   -- printenv  | grep SERVICE     
  REDIS_MASTER_SERVICE_HOST=172.30.140.246
KUBERNETES_SERVICE_PORT=443
KUBERNETES_SERVICE_PORT_HTTPS=443
REDIS_SLAVE_SERVICE_PORT=6379
KUBERNETES_SERVICE_HOST=172.30.0.1
REDIS_MASTER_SERVICE_PORT=6379
REDIS_SLAVE_SERVICE_HOST=172.30.174.228


   Deploy front-end service app
    oc apply -f frontend-service.yaml

    oc get svc
    oc describe svc frontend-service
  -->No end points configured
 Deplpoy front-end deployment app
  oc apply -f frontend-deployment.yaml

  oc get deploy

  oc describe deploy frontend-deployment
  
  oc get po

  oc exec -it frontend-deployment-5666d7d4f4-vg9db /bin/bash

  Log of pod
  google-samples/gb-frontend:v4: Permission denied: AH00072: make_sock: could not bind to address 0.0.0.0:80

    Check the log of container inside pod
   oc logs frontend-deployment-5bfd957d8-jk8j2 -c php-app-container
 **88888********888888888**
  To see the entire satus of services/pods etc.
   oc status -v

  oc status --suggest

   ****************************************
  OC Cluster Issues
Current security policy prevents the containers from being run as the root user. Some images  may fail expecting to be able to change ownership or permissions on directories. The admin   can grant the access to run containers as arbitray user that need to run as the root user with this command:
    
      oc adm policy add-scc-to-user anyuid -n nodejs-echo -z default

    -->scc "anyuid" added to: ["system:serviceaccount:nodejs-echo:default"]

    
****************************

   Liveness probes
'  Result of oc status --suggest

  deployment/frontend-deployment has no liveness probe to verify pods are still running.
    try: oc set probe deployment/frontend-deployment --liveness ...
  * deployment/redis-master-deployment has no liveness probe to verify pods are still running.
    try: oc set probe deployment/redis-master-deployment --liveness ...
  * deployment/redis-slave-deployment has no liveness probe to verify pods are still running.
    try: oc set probe deployment/redis-slave-deployment --liveness ...
  * dc/nodejs-ex has no readiness probe to verify pods are ready to accept traffic or ensure deployment is successful.
    try: oc set probe dc/nodejs-ex --readiness ...
  * dc/nodejs-ex has no liveness probe to verify pods are still running.
    try: oc set probe dc/nodejs-ex --liveness ...
  ************************************************************
  To View details with 
 'oc describe <resource>/<name>' or list everything with 'oc get all'.
  ******************************8

  Logging and monitoring with ELK stack

  https://kubernetes.io/docs/tutorials/stateless-application/guestbook-logs-metrics-with-elk/#clone-the-elastic-examples-github-repo

  https://github.com/elastic/examples.git
  ********************************************
 End points : http://172.17.0.15:8090/, http://172.17.0.14:8090/, http://172.17.0.16:8090/

   reachable on Node virtual ip 172.30.87.168 port : 32013
  Reachable on node cluster ip-->172.30.87.168 port : 32013
  The service reachable on Node physical ip address : 192.168.137.128  Port : 32013 

  NOT Reachable on  localhost:32013   

 
 Load balancver Extrenal IP  172.29.79.207,172.29.79.207 Port : 32013
  NOT reachable on 172.29.79.207:32013
*********************************

 To expose the service  Extrenal IP add router service
oc adm router
error: router could not be created; service account "router" is not allowed to access the host network on nodes, grant access with: 
oc adm policy add-scc-to-user hostnetwork -z router
-->scc "hostnetwork" added to: ["system:serviceaccount:nodejs-echo:


oc adm router
info: password for stats user admin has been set to CtqLapsk0J
--> Creating router router ...
    serviceaccount "router" created
    warning: clusterrolebindings.authorization.openshift.io "router-router-role" already exists
    deploymentconfig.apps.openshift.io "router" created
    service "router" created

**********************************************************
Create Router from web console to expise the service 
web console address : https://127.0.0.1:8443/console/

 list thes services uidrr the project in which the service is deployed from the menu 
on left side for Applications-->Services and select the service
 frontend-service from the list and click on it.
 in The Route section-- > Click opn create Route
  Specify path,hostname and other params if required and clcik on create on bottom of the page.


****************************************888

  Service Router config

Route / Node Port 		Service Port 		Target Port 	Hostname 	
frontend-service / 32013 	8090/TCP 		8090 	http://frontend-service-nodejs-echo.127.0.0.1.nip.io   TLS Termination
--> Success
The service is now rreeachable from url : http://frontend-service-nodejs-echo.127.0.0.1.nip.io/

 also reachable on : localhost:32013   and 127.0.0.1:32013

To tst through the load balancer url

  http://frontend-service-nodejs-echo.127.0.0.1.nip.io/

 http://frontend-service-nodejs-echo.127.0.0.1.nip.io/guestbook.php?cmd=set&key=messages&value=data

http://frontend-service-nodejs-echo.127.0.0.1.nip.io?cmd=get&key=messages

   To write data to redis master
 http://frontend-service-nodejs-echo.127.0.0.1.nip.io/guestbook.php?cmd=set&key=user&value=data

 To read the data from reddis-slave
http://frontend-service-nodejs-echo.127.0.0.1.nip.io/guestbook.php?cmd=get&key=messages




****
 nslookup frontend-service-nodejs-echo.127.0.0.1.nip.io

-->Server:		192.168.137.2
Address:	192.168.137.2#53

Non-authoritative answer:
Name:	frontend-service-nodejs-echo.127.0.0.1.nip.io
Address: 127.0.0.1

  The service is reachable on 127.0.0.1:32013
 The ip 192.168.137.2 is Private Ip.

**************************8

  oc get pods
rontend-deployment-66767dd6c9-2qrdm       1/1       Running       0          6m
frontend-deployment-66767dd6c9-b28qf       1/1       Running       0          6m
frontend-deployment-66767dd6c9-mn7nb       1/1       Running       0          7m


  To scale up the number of frontend Pods:
   oc scale deployment frontend-deployment --replicas=5

 Aftre scaling 
   oc get pods

  frontend-deployment-66767dd6c9-2qrdm       1/1       Running       0          7m
frontend-deployment-66767dd6c9-57msx       1/1       Running       0          20s
frontend-deployment-66767dd6c9-b28qf       1/1       Running       0          7m
frontend-deployment-66767dd6c9-fp58f       1/1       Running       0          20s
frontend-deployment-66767dd6c9-mn7nb       1/1       Running       0          7m

  ******************************

 Redis slave error Can't handle RDB format version 9
 Failed trying to load the MASTER synchronization DB from disk
-->The redis version of redis-master and redis-slave images must be same.


 
   
