# Aws-Ansible Case Study.

## Files
- aws_second_presentation.pptx - Power point presentation that will be presented to a client with our comments. 
- playbooks - folder containing ansible playbooks that are used for automated deployment of the web application with configuration of the database instance,
- dist - a compiled "war" file used for deployment of the application with tomcat server.

## **Step by step guide (more or less detailed)**
1. Create AWS account. 
2. Create VPC
3. Create internet and nat gateways. 
4. Create S3 Bucket. 
5. Create routing table with internet gateway
6. Create first public subnet with previously created routing table (internet gateway) allowing access from outside. 
7. Create EC2 instance (**Control**) that will be controlling deployment of application through ansible and will be accessible from outside. 
    - create and assign securirty group that will allow ssh connection from outside.
    - assign public subnet with route table (internet gateway) and generate public ip address.
    - generate private key that will be used to authenticate connections to your instances. 
8. Create a rout table with nat gateway, then when creating a private subnet assign the newly created route table (nat gateway) to subnet, it will allow outside communication required for updates and installing new packages. 
8. Create EC2 instance (**Web**) that will be hosting the internet application. 
    - assing previously created private subnet
    - create and assign a new security group that will allow communication from security group assigned to **Control** on port 22. 
    - use the same private key (or you can generate another one on your own)
9. Connect to your machines. 
   - locate the generated private key (**prikey**),
   - open git bash (or any other conesole that has access to ssh client),
   - use following commands in a folder with a key (it has to be done with first connectioin to **Web** through **Control**):
     - `eval $(ssh-agent -s)`
     - `ssh-add` `**prikey**` - in git bash
     - `ssh -A  ec2-user@ip` - in git bash 
     - `ssh-add -L` - on the mashin after connecting for the first time
     - after all of that your private key will be on machine, now `ssh {ip of the `**Web**`}` machine,
10. On **Web** run following commands:
    - `sudo yum update -y` - to update the pacakges that are already installed, 
    - `sudo yum install tomcat tomcat-webapps -y` to isntall tomcat and webapps,
    - `sudo systemctl enable tomcat` - to enable startup of tomcat service with every start of the machine,
    - `sudo systemctl start tomcat` - to manually start the tomcat service,
    - `sudo systemctl status tomcat` - to check the state of the service, desired is active (running), now `curl localhost:8080` if we will see a lot of text with linx and html tags it means that it works, 
    - Extra (if needed):
      - `echo "<h1>Web Server 1</h1>" >> /usr/share/tomcat/webapps/ROOT/index.html` will create index.html file that will help us identify the server that we are actually connected to. 
      - the html file has a higher priority then the jsp file that is there by default, 
      - we can check other apps (later in a browser) by typinng "{adddress of low balances or public address - default in this guide balancer}/sample or {...}/examples
11. Create a new role with policy that allow access (from **Web**) to S3 Bucket to previously uploaded files, 
12. Assing the role to **Web**, and when connected to **Web** execute:
    - `aws s3 ls s3://{bucket name}/` - to list files in bucket that you have created, if successfull it means that all permissions and security, 
    - navigate to tomcat webapps folder: `cd /usr/share/tomcat/webapps/`
    - execute `sudo aws s3 cp s3://{bucket}/{filename.war} .` to download the war file to current directory. 
    - if tomcat is running it should automatically create {filename} folder with deployed app. 

## **Task**

DevOps Task for Tuesday 14th April:
The client liked your presentations and has decided to take the next step.  Rob would like you to produce a proof of concept that demonstrates how AWS services can be used to implement a simple workload.

To this end you should take the simple MySQL ToDo list application (https://github.com/MikeAScott/spring-todo-list) that we deployed locally using Vagrant and deploy this in AWS.

1.	You may use any AWS services that you feel are appropriate
2.	You must configure servers, the application and database using Ansible.
    -	You may manually provision the servers and AWS service
3.	You should consider using an S3 bucket for storing the .war for the application to be deployed
    -i.e. You may build the application package and deploy to S3 before configuring the App.
4.	You should follow good practice security and resilience guidelines (e.g. public and private subnets, multiple availability zones)
5.	You must prepare a short presentation that shows your architecture, the choices you made, and why you made them.
6.	You will have up to 20 minutes to present and demonstrate your solution
7.	Your audience will contain business and technical people so you should be prepared to answer questions on not just why you chose to use services, but also how they   work, and be prepared to show code if asked.
8.	You should ensure your code and presentation is checked into GitHub with a README.
9.	You will be working in teams to complete this task. The teams are as follows:
10.	There is a lot to do so please plan carefully and balance your workloads.
    - Play to each others strengths
    - During the presentation please consider who will be presenting which parts.

A VPC will be set up with Internet and NAT Gateways, for you to use you will need to create everything else.
If you would prefer to deploy the application on a different database (e.g. Postgres or Aurora) please ask early and I may be able to port it.

The presentation will be at 10 am on Wednesday 15th April.
 
As ever use Google, AWS Documentation, Udemy, each other, and me.

# Authors:
## Lydia Clavina George
## Kamil Nowak