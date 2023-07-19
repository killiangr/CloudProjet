# CAPSTONE-PROJECT-SE1 
**Killian GRAINDORGE, Baptiste BILLY-GAGNAIRE, Thibaud DANDOY**
#

**VPC**

* let's start by creating [a VPC](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20145351.png) for the project with 10.0.0.4/16 ipv4 CDR

**Network**
* After we create [a public subnet](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20145502.png) to link our vpc and allow [ipv4 auto-assign ip](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20145543.png) to find it later on internet.
* Now we create an [internet gateway](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20145618.png) to connect from internet to our vpc.
* We create a routing table and [edit](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20145802.png) the rules that allow incoming traffic to our vpc from the internet.
    
**Security & Cloud9**
* We create a [security group](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20150029.png), to block all incoming traffic and allow it on only three ports for http, https and ssh protocols.
* We create an ec2 instance from cloud9, after we [link it to the vpc and the public network](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20150145.png). We chosed the ssh secure shell connexion
* With [cloud9 console](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20151031.png) and ssh connexion we install apache2, php, mariadb, and download the website of the subject on /var/www/html and change the owner of it to allow execution ot the php.
* So now the ec2 instance is created and we need to connect it to our security group, we [modified the security group setting](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20151910.png).
#
**Website view**
![run well](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20152137.png)

#
**Database**
* Now we create a [Maria DB instance](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20152315.png) and setup the password.
* We need to [establish a link with our EC2 instance](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20152342.png). And we also link the databse to our vpc.
* We [create automatically](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20152434.png) a private subnet for our DB and we give the access to our VPC security group.
* An AWS view where we can see that [three self-managed private subnets were created](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20153226.png) in the process
* We [import the data from the SQL](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20154200.png) file that you give us on our DB using cloud 9 shell of our ec2 instance.
* We [create three parameters](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20154557.png) to save username, password, endpoint and table name in the parameter store of AWS System Manager
* We create an [endpoint](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20154821.png) to link the website code to the DB

**IAM**
* We [create an IAM role](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20155747.png) to allow our PHP website on our EC2 instance to access on our webserver.
* We [attached the role](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20155954.png) to our ec2 instance
#
**List of countries and the data**
![list of countries](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20160138.png)

