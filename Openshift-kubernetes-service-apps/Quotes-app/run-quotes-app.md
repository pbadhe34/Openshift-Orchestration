 Run Qoutes-appp with NodePort service

   oc cluster status

  oc adm policy add-scc-to-user anyuid -n nodejs-echo -z default

  oc get po --all-namespaces=true

 
  oc apply -f qoutes-app-NodePort.yml

  oc get svc

  oc get svc
NAME                TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)                   AGE
quotes-service-np   NodePort    172.30.78.78   <none>        8080:31000/TCP     

  oc describe svc  quotes-service-np 

  Selector:               app=quotes-pod
Type:                     NodePort
IP:                       172.30.78.78
Port:                     <unset>  8080/TCP
TargetPort:               8080/TCP
NodePort:                 <unset>  31000/TCP
Endpoints:                172.17.0.6:8080,172.17.0.7:8080,172.17.0.8:8080
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>



  oc get deploy

  oc get po


  To see the entire satus of services/pods etc.
   oc status -v

  oc status --suggest

  View details with 'oc describe <resource>/<name>' or list everything with 'oc get all'.

  Access the quotes app with pod ip
  172.17.0.6:8080/api/quote
  172.17.0.7:8080/api/quote
  172.17.0.8:8080/api/quote

  With clusterip of service  : 172.30.78.78:8080
  curl http://172.30.78.78:8080/api/quote
  Repeat with curl to check chnaging ip address of pod displkayed in the respoinse


  With Node IP : 192.168.137.128:31000/api/quote

  curl http://192.168.137.128:31000/api/quote

************************************************************

Run Qoutes-appp with LoadBalancer service

  oc apply -f qoutes-app-loadBalancer.yml

  oc get svc
NAME                TYPE           CLUSTER-IP      EXTERNAL-IP                   PORT(S)                   AGE
quotes-service-lb   LoadBalancer   172.30.199.82   172.29.163.63,172.29.163.63   8080:32000/TCP            6s

  oc describe svc quotes-service-lb 

  Name:                   quotes-service-lb
Namespace:                nodejs-echo
Labels:                   <none>
Annotations:              kubectl.kubernetes.io/last-applied-configuration={"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"name":"quotes-service-lb","namespace":"nodejs-echo"},"spec":{"ports":[{"nodePort":320...
Selector:                 app=quotes-app-lb-pod
Type:                     LoadBalancer
IP:                       172.30.199.82
External IPs:             172.29.163.63
LoadBalancer Ingress:     172.29.163.63
Port:                     <unset>  8080/TCP
TargetPort:               8080/TCP
NodePort:                 <unset>  32000/TCP
Endpoints:                172.17.0.6:8080,172.17.0.7:8080,172.17.0.8:8080 + 1 more...


   Access the quotes app with pod ip
  http://172.17.0.6:8080/api/quote
  http://172.17.0.7:8080/api/quote
  http://172.17.0.8:8080/api/quote
 http:// 172.17.0.9:8080/api/quote

  With clusterIp : http://172.30.199.82:8080/api/quote

  curl http://172.30.199.82:8080/api/quote

  With Node Ip : 192.168.137.128:32000/api/quote

  curl 192.168.137.128:32000/api/quote

  With ExternalIP : http://172.29.163.63:3200/api/quote

  NOT accesible With http://localhost:32000/api/quote

  Expose the service with external ip by adding router.


  Firts find out routes exposed
  oc get routes

   oc delete route ronte-name


  oc expose service quotes-service-lb
  oc describe  route quotes-service-lb

  NOw accesible With http://localhost:32000/api/quote

  and with host address as quotes-service-lb-nodejs-echo.127.0.0.1.nip.io/api/quote

  curl http://quotes-service-lb-nodejs-echo.127.0.0.1.nip.io/api/quote

  oc delete  route quotes-service-lb
 

 

