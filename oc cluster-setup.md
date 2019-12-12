

Edit /etc/docker/daemon.json file and add the following:

root/.docker/config.json

sudo gedit /etc/docker/daemon.json 

{
   "insecure-registries": [
     "172.30.0.0/16"
   ]
}

sudo systemctl daeon-reload

sudo systemctl restart docker

sudo systemctl status docker																		 																																				   
 **Create a non-root user docker
 ** How to add another node to openshift cluster with oc

journalctl -xe : for all logs
journalctl -xeu docker																

 
Allow all incomig connections set with firewall


firewall-cmd --permanent --new-zone dockerc
firewall-cmd --permanent --zone dockerc --add-source 172.17.0.0/16
  sudo ufw allow from 172.17.0.0/16  
firewall-cmd --permanent --zone dockerc --add-port 8443/tcp
  sudo ufw allow 8443/tcp
firewall-cmd --permanent --zone dockerc --add-port 53/udp

  sudo ufw allow 53/udp
firewall-cmd --permanent --zone dockerc --add-port 8053/udp
  sudo ufw allow 8053/udp
firewall-cmd --reload

firewall-cmd --zone=public --list-ports

Download OC client tools ver 3.11
https://www.okd.io/download.html

https://github.com/openshift/origin/releases/download/v3.11.0/openshift-origin-client-tools-v3.11.0-0cbc58b-linux-64bit.tar.gz

Extract it.
From the folder
sudo mv oc /usr/local/bin/oc
sudo mv kubectl /usr/local/bin/kubectl

From Terminal
From Client tools v3.11
  sudo ./oc cluster up

  OPsndhift docker images for cluster

 openshift/origin-node            v3.11               249ca97e388f        3 weeks ago         1.19GB
openshift/origin-control-plane   v3.11               3fad55d0b2bc        3 weeks ago         831MB
openshift/origin-hypershift      v3.11               9918b48caff6        3 weeks ago         551MB
openshift/origin-hyperkube       v3.11               593fa6cbb593        3 weeks ago         510MB
openshift/origin-cli             v3.11               c5caf3700de6        3 weeks ago         385MB
openshift/origin-pod             v3.11               d8af79d5fbe2        3 weeks ago         263MB



sudo ./oc cluster status

  sudo ./oc get nodes

/********************
netstat -ltnp | grep -w ':80' 

tcp6       0      0 :::80                   :::*                    LISTEN      1795/nginx.conf 


 sudo ps -ef

sudo  kill 1795
***************************************

 Stop all containers
sudo docker stop $(sudo docker ps -aq)
 Remove all containers

sudo docker rm $(sudo docker ps -aq)

  sudo docker container ls -a

dell@kmaster:~/Downloads/Openshift-Origin-ClientV3/openshift-origin-client-tools-v3.11.0-0cbc58b-linux-64bit$ sudo ./oc cluster up
Getting a Docker client ...
Checking if image openshift/origin-control-plane:v3.11 is available ...
Creating shared mount directory on the remote host ...
Determining server IP ...
Checking if OpenShift is already running ...
Checking for supported Docker version (=>1.22) ...
Checking if insecured registry is configured properly in Docker ...
Checking if required ports are available ...
Checking if OpenShift client is configured properly ...
Checking if image openshift/origin-control-plane:v3.11 is available ...
Starting OpenShift using openshift/origin-control-plane:v3.11 ...
I1112 19:43:22.168351   12522 flags.go:30] Running "create-kubelet-flags"
I1112 19:43:26.129331   12522 run_kubelet.go:49] Running "start-kubelet"
I1112 19:43:28.065210   12522 run_self_hosted.go:181] Waiting for the kube-apiserver to be ready ...