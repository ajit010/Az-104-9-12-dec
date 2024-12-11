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
        
        
        It will display "running" status ..
        
        
    8. visit the ip-address of Linux-Vm to check apache2 default webapge ...
    
    

Exercise 6 :
    
    Create a VMSS (Virtual Machine Scaling Set)

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
 
    12. Go to Activity log under VMSS to check the scaling activity based on scaling condition ...

    13. Just like CPU utilization, you can add any metric to scaling condition ...

    14. You can use vertical scaling to resize the instances too.. (will apply on new instances only) ...


Exercise 7 :
    
    Create a  VPC and 2 subnets
    
    1. Create a VPC of CIDR range : (10.0.0.0/16)
        
    2. Create 2 subnets - subnet1 (10.0.1.0/24) and subnet2 (10.0.2.0/24)
    
    

Exercise 8 :
    
    Create Public Ip address :
    
    1. Create 3 public ip (lb-ip, vm1-ip and vm2-ip)
    
    2. Use Ipv4 , SKU - basic , ip assgnmnent - Dynamic ...
        


Exercise 9 :
    
    Create 2 VM and Load Balancer:
        
        
    1. Create Vm-1 and Vm-2 (ubuntu 22.04)
    
    2. Size- b1s
    
    3. Availibity set - create new and use same in both VMs
    
    4. Networking - select the existing network and default subnet and vm1-1 ip and vm-2 ip respectively
    
    5. Advanced - "User data"
    
        for vm1 -
        
        
        #!/bin/bash
        sudo apt-get update -y;
        sudo apt install apache2 -y;
        echo "Hello, welcome to 1st VM" | sudo tee /var/www/html/index.html;
        sudo chown www-data:www-data /var/www/htmlindex.html;
    
    
        for vm2 -
        
        #!/bin/bash
        sudo apt-get update -y;
        sudo apt install apache2 -y;
        echo "Hello, welcome to 2nd VM" | sudo tee /var/www/html/index.html;
        sudo chown www-data:www-data /var/www/htmlindex.html;
    
    
     6. Create both VMs and acess them using their Ips and check if they display correct msg
        
     7. Create a Load balancer 
    
     8. frontend config - lb-ip
        
        backend pool - select vnet - select both vms
        
        add a lb rule and health prope ...
        
        
     9. save this info and lb will be created ...
    
     10. Visit the front-end ip of LB to check distribution of traffic among VMs ...
    
        
    
Exercise 10 :
    
    
    Create Azure webapp :
        
        
    1. Search for App service >> webapp
    
    2. OS - windows, Runtime - .NET 8.0 (LTS)
    
    3. Pricing Model - Basic 
    
    4. Networking - allow public access
    
    5. Review + Create ...
    
    6. Once it is deployed, you will get a Domain name for azure webapp..
    
    7. Visit the domain url and it will display homepage of webapp ...
    
    
    
Exercise 11:
    
    
    Create a sample .Net application in Vs code and deploy to azure webapp
    
    
Exercise 12:
    
    Create Azure SQL Database :
        
        
    1. Create a db and db-server (basic sql auth. username and pswd)
    
    2. location - central india/canada central
    
    3. workload - dev (service tier - basic)
    
    4. backup+storage -- LRS
    
    5. networking - connectivity - public end point and enable both firewall rules
    
    6. keep default for rest of the config
    
    7. db and db-server will be created ...
    
    
    Add some data in db :
        
    query :
        
        
     CREATE TABLE Course
(
   CourseID int,   
   CourseName varchar(1000),
   Rating numeric(2,1)
);

INSERT INTO Course(CourseID,CourseName,Rating) VALUES(1, 'Docker and Kubernetes',4.5);

INSERT INTO Course(CourseID,CourseName,Rating) VALUES(2,'AZ-204 Azure Developer',4.6);

INSERT INTO Course(CourseID,CourseName,Rating) VALUES(3,'AZ-104 Administrator',4.7);

SELECT * FROM Course;    
     
    
    
============================================================================================================

Exercise 13:
    
    
    Create a Storage account :
        
        
    1. name - ajitsg22
    
    2. primary service - azure blob storage
    
    3. peformace tier - standard
    
    4. Data redundancy - LRS
    
    5. Networking -- enable public access
    
    6. Review and Create ...
    
    
    
    
