
To find the PID of process running on port

netstat -ltnp | grep -w ':80' 

tcp6       0      0 :::80                   :::*                    LISTEN     1795/nginx.conf 


sudo ps -ef

To kill the process iwth PID
sudo  kill 1795
