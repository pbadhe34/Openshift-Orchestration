UFW instetad of fiurewall on Unbunbtu 16.04

https://hostpresto.com/community/tutorials/install-and-configure-ufw-firewall-on-ubuntu-16-04/

 sudo ufw status  on Ubuntu mcs

sudo ufw allow 22/tcp

sudo ufw allow 8443/tcp
sudo ufw allow 53/udp

sudo ufw allow 8053/udp


I1112 19:22:37.966334   31592 run_self_hosted.go:181] Waiting for the kube-apiserver to be ready ...

E1112 19:27:38.392709   31592 run_self_hosted.go:571] API server error: Get https://127.0.0.1:8443/healthz?timeout=32s: dial tcp 127.0.0.1:8443: connect: connection refused ()
Error: timed out waiting for the condition
    :: sudo ufw enable
     sudo ufw status
   :: sudo ufw allow 8443/tcp

 Allow all incomig connections


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


  > sudo ufw statusStatus: active

To                         Action      From
--                         ------      ----
9090                       ALLOW       Anywhere                  
22                         ALLOW       Anywhere                  
10248                      ALLOW       Anywhere                  
10248/tcp                  ALLOW       Anywhere                  
22/tcp                     ALLOW       Anywhere                  
8443/tcp                   ALLOW       Anywhere                  
53/udp                     ALLOW       Anywhere                  
8053/udp                   ALLOW       Anywhere                  
Anywhere                   ALLOW       172.17.0.0/16             
9090 (v6)                  ALLOW       Anywhere (v6)             
22 (v6)                    ALLOW       Anywhere (v6)             
10248 (v6)                 ALLOW       Anywhere (v6)             
10248/tcp (v6)             ALLOW       Anywhere (v6)             
22/tcp (v6)                ALLOW       Anywhere (v6)             
8443/tcp (v6)              ALLOW       Anywhere (v6)             
53/udp (v6)                ALLOW       Anywhere (v6)             
8053/udp (v6)              ALLOW       Anywhere (v6)    


																																																																																																																							
