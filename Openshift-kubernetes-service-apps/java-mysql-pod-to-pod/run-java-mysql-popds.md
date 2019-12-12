  Java microservice app pod with MySQL pod
  oc apply -f MySql-PersistentVoulme.yml
  oc get pv

  oc apply -f MySql-PersistentVoulme-Claim.yml

  oc get pvc
  
 Deploy mysql pod
  oc apply -f mysql-pod.yml

  oc get pods


  Deploy java service pod
  oc apply -f java-user-pod.yml
   oc get po

  oc describe pod java-user-service

  oc describe pod java-user-service | grep IP

  172.17.0.7

  oc exec -it java-user-service /bin/bash



  oc exec java-user-service -- printenv

    oc exec mysql -- printenv

  -->
  HOSTNAME=mysql
MYSQL_ROOT_PASSWORD=MyRootPass123
MYSQL_DATABASE=userservice
ROUTER_SERVICE_PORT_443_TCP=443
ROUTER_PORT_80_TCP_PORT=80
ROUTER_PORT_1936_TCP_PORT=1936
ROUTER_PORT_1936_TCP_ADDR=172.30.30.69
KUBERNETES_SERVICE_HOST=172.30.0.1
ROUTER_SERVICE_PORT=80
ROUTER_PORT=tcp://172.30.30.69:80
ROUTER_PORT_443_TCP_PROTO=tcp
ROUTER_PORT_443_TCP_PORT=443
ROUTER_PORT_1936_TCP=tcp://172.30.30.69:1936
KUBERNETES_SERVICE_PORT_HTTPS=443
KUBERNETES_PORT_443_TCP_PROTO=tcp
ROUTER_SERVICE_PORT_1936_TCP=1936
ROUTER_PORT_80_TCP_PROTO=tcp
ROUTER_PORT_80_TCP_ADDR=172.30.30.69
ROUTER_PORT_443_TCP=tcp://172.30.30.69:443
ROUTER_PORT_443_TCP_ADDR=172.30.30.69
KUBERNETES_PORT_443_TCP=tcp://172.30.0.1:443
ROUTER_PORT_80_TCP=tcp://172.30.30.69:80
ROUTER_SERVICE_PORT_80_TCP=80
ROUTER_PORT_1936_TCP_PROTO=tcp
KUBERNETES_SERVICE_PORT=443
KUBERNETES_PORT=tcp://172.30.0.1:443
KUBERNETES_PORT_443_TCP_PORT=443
KUBERNETES_PORT_443_TCP_ADDR=172.30.0.1
ROUTER_SERVICE_HOST=172.30.30.69
GOSU_VERSION=1.7
MYSQL_MAJOR=5.6
MYSQL_VERSION=5.6.46-1debian9
HOME=/root

  


  Access the application with pod ip as http://172.17.0.7:8090/users


  


