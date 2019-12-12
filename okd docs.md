https://docs.okd.io/3.11/welcome/index.html


https://docs.okd.io/3.11/install_config/router/index.html

 Try the examples
https://docs.okd.io/3.11/getting_started/administrators.html#try-it-out

https://docs.okd.io/3.11/install_config/router/customized_haproxy_router.html


https://docs.okd.io/3.11/install_config/router/default_haproxy_router.html#deploy-router-create-router

https://docs.okd.io/3.11/dev_guide/expose_service/expose_internal_ip_router.html

https://docs.okd.io/3.11/cli_reference/basic_cli_operations.html#expose

https://docs.okd.io/3.11/admin_guide/managing_pods.html

https://github.com/sclorg/nodejs-ex

 192.168.10.128

 oc expose svc/nodejs-ex --hostname=192.168.10.128
   

 oc expose svc/quotes-service-lb  --hostname=192.168.10.128

oc get routes
NAME                HOST/PORT        PATH      SERVICES            PORT       TERMINATION   WILDCARD
node-route          192.168.10.128   /app      nodejs-ex           8080-tcp                 None
quotes-service-lb   192.168.10.128             quotes-service-lb   8080                     None

