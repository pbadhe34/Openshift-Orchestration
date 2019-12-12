

 Pyhton-redis-app

  

  oc apply -f RedisPersistenceVolume.yml

  oc get pv

  oc apply -f RedisPersistenceVolumeClaim.yml

  oc get pvc
  
  oc apply -f py-app-service-volume-LoadBalancer.yml

 To remove thee application
  oc delete  -f py-app-service-volume-LoadBalancer.yml

  oc get po

  oc exec  py-app-deployment-68f5899fd-5v6nk -- printenv | grep SERVICE

  REDIS_SERVICE_SERVICE_HOST=172.30.152.23

  oc describe svc redis-service
  ClusterIP = 172.30.152.23

  oc exec  azure-vote-deployment-68d87c9f5f-rj5tq -- printenv | grep AZURE

  REDIS_SERVICE_SERVICE_HOST=172.30.152.23

  oc exec py-app-deployment-76d49fbc4f-7rrn5  -- printenv | grep SERVICE
  REDIS_SERVICE_SERVICE_HOST=172.30.152.23


  Execute on container in the pod

  oc exec azure-vote-deployment-58dc5b6b8b-flb8n -c azure-vote-app-container  -- printenv | grep redis

  oc exec azure-vote-deployment-68d87c9f5f-jpdcn  -- printenv


   
PY_APP_SERVICE_LB_PORT_8090_TCP_PROTO=tcp
 
PY_APP_SERVICE_LB_SERVICE_HOST=172.30.220.153
PY_APP_SERVICE_LB_PORT_8090_TCP_ADDR=172.30.220.153
REDIS_SERVICE_SERVICE_PORT=6379
REDIS_SERVICE_PORT_6379_TCP_PROTO=tcp
REDIS_SERVICE_PORT_6379_TCP_PORT=6379
REDIS_SERVICE_PORT_6379_TCP_ADDR=172.30.152.23
ROUTER_SERVICE_PORT_443_TCP=443

REDIS_SERVICE_SERVICE_HOST=172.30.152.23

 
PY_APP_SERVICE_LB_PORT=tcp://172.30.220.153:8090
PY_APP_SERVICE_LB_PORT_8090_TCP=tcp://172.30.220.153:8090
 

PY_APP_SERVICE_LB_SERVICE_PORT=8090
PY_APP_SERVICE_LB_PORT_8090_TCP_PORT=8090
REDIS_SERVICE_PORT=tcp://172.30.152.23:6379
REDIS_SERVICE_PORT_6379_TCP=tcp://172.30.152.23:6379
KUBERNETES_SERVICE_HOST=172.30.0.1
ROUTER_SERVICE_PORT_80_TCP=80
ROUTER_SERVICE_PORT_1936_TCP=1936


  oc describe svc redis-service

 -->PClusgterIP : 172.30.152.23


  *88888********888888888**
  To see the entire satus of services/pods etc.
   oc status -v

  oc status --suggest

   ****************************************

  svc/py-app-service-lb - 172.30.220.153:8090


  oc describe svc py-app-service-lb
  IP:				172.30.220.153
 External IPs:             172.29.67.231
 LoadBalancer Ingress:     172.29.67.231
Port:                     <unset>  8090/TCP
TargetPort:               8090/TCP
NodePort:                 <unset>  30193/TCP
Endpoints:                172.17.0.6:8090,172.17.0.7:8090,172.17.0.8:8090
Session Affinity:         None
External Traffic Policy:  Cluster

  app accesible at cluster ip : http://172.30.220.153:8090
  With localhost ip : http://192.168.137.128:31740
 as well as http://localhost:31740
  With Extrenal IP : http://172.29.67.231:30193
  with end points on local machine

  http://172.17.0.6:8090
  http://172.17.0.7:8090
  http://172.17.0.890
  http://172.17.0.8090


  To expose the service use
  oc expose service py-app-service-lb


  oc describe route py-app-service-lb
  
  oc exec py-app-deployment-76d49fbc4f-7rrn5 cat /etc/resolv.conf
-->nameserver 172.30.0.2
search nodejs-echo.svc.cluster.local svc.cluster.local cluster.local localdomain
options ndots:5

  Connect to pod  
  oc rsh py-app-deployment-76d49fbc4f-7rrn5
# cat /etc/resolv.conf
nameserver 172.30.0.2
search nodejs-echo.svc.cluster.local svc.cluster.local cluster.local localdomain
options ndots:5


firewall-cmd --permanent --new-zone dockerc
firewall-cmd --permanent --zone dockerc --add-source $(docker network inspect -f "{{range .IPAM.Config }}{{ .Subnet }}{{end}}" bridge)
firewall-cmd --permanent --zone dockerc --add-port 8443/tcp --add-port 53/udp --add-port 8053/udp
firewall-cmd --reload
  



