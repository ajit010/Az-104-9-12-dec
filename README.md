# Az-104-9-12-dec

Azure Administrator : Az-104
    
    
Break 1 : 11:30 to 11:45
            
Break 2 :  1:30 to 2:15
            
Break 3 :  3:30 to 3:45
            
            
Exercise 1 :
    
    
    Set up Budget and Alerts :
    
    Create a budget in Azure and add some alert rules and  recipient email id..
    

Exercise 2 :
    
    Create a windows - based VM
    
    1. OS - windows server 2019 datacenter - x64 gen2
    
       AZ - No infra redundancy
    
    2. username and pswd  - must save somewhere
    
    3. Size - B2s ( 2 vcpu and 4 gb RAM )
    
    4. storage - 127 gb - Premium SSD
    
    5. Networking - default
    
    6. Ports - 3389, 80
    
    
    Review and Create ...
    
    
    
Exercise 3 :   
    
    RDP to Windows VM -- 
    
    1. download the rdp file from "connect" option in VM
    
    2. Login using username and password
    
    3. Try to ping remote VM from host machine ... 
    
    (Add ICMPv4 protocol in VM sg and disable firewall in remote VM )
    
    
Exercise 4 :   
    
    Install IIS server :
        
    1. Login to windows vm and under "server dashboard"
    
    2. Click on add roles and features
    
    3. Click on Next > Next > add a role " web server IIS "
    
    4. Click on next and install
    
    5. Use the localhost on remote machine and ip address of VM in host machine to visit the homepage of iis server..
    
    6. Also, do not forget to add port 80 in security-group of VM ...
    
    
====================================================================================================================



    
Exercise 5 :
    
    Create a Linux-based VM
    
    1. OS image - ubuntu 22.04 x64 gen 2
    
    2. size - B1s
    
    3. Use SSH key pair instead of username/pswd in authentication
    
    4. rest of settings- keep as default ..
    
    5. download ssh private key file ...
    
    6. Open cmd in your machine, and use command :
        
        cd downloads
        
        (downloads is a folder where key apir will be saved  .. could be different in your system)
        
    7. run coomands :
        
        ssh -i keypair-filename username@public-ip-of-vm
        
     
    
    Install apache2 web-server :
        
        sudo apt update -y
        
        sudo apt install apache2 -y
        
        sudo systemctl status apache2
        
        
        >> IT will display "running" status ..
        
        
    > Visit the ip-address of Linux-Vm to check apache2 default webapge ...
    
    
==============================================================================================================



Exercise 6 :
    
   VMSS (Virtual Machine Scaling Set)

   1. orchestration - uniform
    
   2. size - b1s

   3. os image - ubuntu 22.04
    
   4. scaling mode - autoscaling

    scaling policy - > 70, add one and <40 , decrease one
    
    mininmum, desired = 2 and max = 4
    
   5. networking - select the interface and enable the public-ip

   6. add ports - http(80) ans ssh (22)
    
   7. Under "Advanced section" add user data :



User data script -


#!/bin/bash
sudo apt-get update -y;
sudo apt install apache2 -y;
echo "Hello, welcome to VM" | sudo tee /var/www/html/index.html;
sudo chown www-data:www-data /var/www/htmlindex.html;



   8. Rest - keep as default and create

   9. visit the ip addresss of both machines of vmss and you will get same msg displayed...
    
   10. SSH into both of machines :
    
     ssh username@public-ip-vm
        
     sudo apt install stress
    
     sudo stress --cpu 10 --timeout 900
        
   11. after few minutes (10-12 min), look at the cpu utilization and no. of instances in vmss
 
   12. 






        
        
        
    
    
    
    
    
    
    
    
    
    
