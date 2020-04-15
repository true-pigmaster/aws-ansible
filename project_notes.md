Machine names starts with lck for example lck-web1
To Do:
1. Create Step by step guide to setup of how to set up the environment.

Quick Tasks
Day 0
L: Create Control Machine and try configure RDS through asnible
K: Creat web machine and make the tomcat running manuallyu with the app. 

Basic setup of the machines:
1. control open to ssh from the network - list of the ip addresses
2. web open on port 8080 from outsite and to ssh from within
3. db server open on for ssh and sql from within. 
waiting for mike's response about the database prefered setup

Like a log:
13.04 Lydia created S3Bucket for our config files. 
14.04 Created two subnets:
    lck-web-sn:      10.0.3.64
    lck-control-sn:  10.0.3.0
    created control machines with ip: 3.249.27.208
    created low balancer
    installed tomcat on two machines
    created security groups for low balanacer and RDS
15.04
    Applied roles to EC's that are allowing access to S3 Bucket and war file created by Mike
    Lydia created the PPT presentation (basic skeleton)
    accessed war file from S3 Bucket
    Deployed war file 
    created database connection