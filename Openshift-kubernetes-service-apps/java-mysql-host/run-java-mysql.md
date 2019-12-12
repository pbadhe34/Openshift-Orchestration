
  Java micro-service with mysql backend
  oc apply -f MySql-PersistentVoulme.yml

  oc get pv

 oc apply -f MySql-PersistentVoulme-Claim.yml

  oc get pvc
  oc apply -f java-mysql-service-volume-loadbalancer.yml

  oc get svc

  user-app-service   LoadBalancer   172.30.175.9   172.29.109.115,172.29.109.115   8090:30042/TCP  

  oc describe svc  user-app-service
  -->
  Name:                     user-app-service
Namespace:                nodejs-echo
Labels:                   <none>
Annotations:              kubectl.kubernetes.io/last-applied-configuration={"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"name":"user-app-service","namespace":"nodejs-echo"},"spec":{"ports":[{"port":8090}],"...
Selector:                 app=user-app-pod
Type:                     LoadBalancer
IP:                       172.30.175.9
External IPs:             172.29.109.115
LoadBalancer Ingress:     172.29.109.115
Port:                     <unset>  8090/TCP
TargetPort:               8090/TCP
NodePort:                 <unset>  30042/TCP
Endpoints:                172.17.0.6:8090
Session Affinity:         None
External Traffic Policy:  Cluster
Events:
  Type    Reason      Age   From                Message
  ----    ------      ----  ----                -------


  The service is accesible at cluster ip : http://172.30.175.9:8090/users
  OR from end points as 
  http://172.17.0.6:8090/users

  NOT From localhost:30042/users

  OR from Node IP
  http://192.168.137.128:30042/users

  Expose the service External ip
 oc expose svc user-app-service

  oc get route

  oc describe route user-app-service

--> Name:			user-app-service
Namespace:		nodejs-echo
Created:		41 seconds ago
Labels:			<none>
Annotations:		openshift.io/host.generated=true
Requested Host:		user-app-service-nodejs-echo.127.0.0.1.nip.io
			  exposed on router router 41 seconds ago
Path:			<none>
TLS Termination:	<none>
Insecure Policy:	<none>
Endpoint Port:		8090

Service:	user-app-service
Weight:		100 (100%)
Endpoints:	172.17.0.6:8090


 After route exposite of service
  NOw recahable at http://user-app-service-nodejs-echo.127.0.0.1.nip.io/users
  or http://localhost:30042/users

  To remove the application 
  oc delete -f java-mysql-service-volume-loadbalancer.yml




  
