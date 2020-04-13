# aws-ansible

# task
DevOps Task for Tuesday 14th April:
 
The client liked your presentations and has decided to take the next step.  Rob would like you to produce a proof of concept that demonstrates how AWS services can be used to implement a simple workload.

To this end you should take the simple MySQL ToDo list application (https://github.com/MikeAScott/spring-todo-list) that we deployed locally using Vagrant and deploy this in AWS.

1.	You may use any AWS services that you feel are appropriate
2.	You must configure servers, the application and database using Ansible.
a.	You may manually provision the servers and AWS service
3.	You should consider using an S3 bucket for storing the .war for the application to be deployed
a.	i.e. You may build the application package and deploy to S3 before configuring the App.
4.	You should follow good practice security and resilience guidelines (e.g. public and private subnets, multiple availability zones)
5.	You must prepare a short presentation that shows your architecture, the choices you made, and why you made them.
6.	You will have up to 20 minutes to present and demonstrate your solution
7.	Your audience will contain business and technical people so you should be prepared to answer questions on not just why you chose to use services, but also how they work, and be prepared to show code if asked.
8.	You should ensure your code and presentation is checked into GitHub with a README.
9.	You will be working in teams to complete this task. The teams are as follows:
10.	There is a lot to do so please plan carefully and balance your workloads.
a.	Play to each others strengths
b.	During the presentation please consider who will be presenting which parts.

A VPC will be set up with Internet and NAT Gateways, for you to use you will need to create everything else.
If you would prefer to deploy the application on a different database (e.g. Postgres or Aurora) please ask early and I may be able to port it.

The presentation will be at 10 am on Wednesday 15th April.
 
As ever use Google, AWS Documentation, Udemy, each other, and me.
