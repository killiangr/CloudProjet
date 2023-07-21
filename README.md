# CAPSTONE-PROJECT-SE1 
**Killian GRAINDORGE, Baptiste BILLY-GAGNAIRE, Thibaud DANDOY**
#

**VPC**

* let's start by creating a VPC for the project with 10.0.0.4/16 ipv4 CDR <br><br> ![image](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/1.png) 
#
**Network**
* After we create a public subnet to link our vpc
<br><br>
![image](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/2.png)
<br><br>
* And allow ipv4 auto-assign ip to find it later on internet.
<br><br>
![image](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/9.png) 
<br><br>
* Now we create an internet gateway to connect from internet to our vpc.
<br><br>
![image](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20145618.png)
<br><br>
* We create a routing table and edit the rules that allow incoming traffic to our vpc from the internet.
<br><br>
![image](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20145802.png) 
<br><br>
#
**Security & Cloud9**
* We create a security group, to block all incoming traffic and allow it on only three ports for http, https and ssh protocols.
<br><br>
![image](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20150029.png)
<br><br>
* We create an ec2 instance from cloud9, after we link it to the vpc and the public network. We chosed the ssh secure shell connexion
<br><br>
![image](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20150145.png)
<br><br>
* With cloud9 console and ssh connexion we install apache2, php, mariadb, and download the website of the subject on /var/www/html and change the owner of it to allow execution ot the php.
<br><br>
![image](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20151031.png)
<br><br>
* So now the ec2 instance is created and we need to connect it to our security group, we modified the security group setting.
<br><br>
![image](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20151910.png)
<br><br>
#
**Website view**
<br><br>
![run well](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20152137.png)
#
**Database**
* Now we create a Maria DB instance and setup the password.
<br><br>
![image](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20152315.png)
<br><br>
* We need to establish a link with our EC2 instance. And we also link the databse to our vpc.
<br><br>
![image](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20152342.png)
<br><br>
* We create automatically a private subnet for our DB and we give the access to our VPC security group.
<br><br>
![image](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20152434.png)
<br><br>
* An AWS view where we can see that three self-managed private subnets were created in the process.
<br><br>
![image](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20153226.png)
<br><br>
* We import the data from the SQL file that you give us on our DB using cloud 9 shell of our ec2 instance.
<br><br>
![image](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20154200.png)
<br><br>
* We create three parameters to save username, password, endpoint and table name in the parameter store of AWS System Manager.
<br><br>
![image](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20154557.png)
<br><br>
* We create an endpoint to link the website code to the DB.
<br><br>
![image](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20154821.png)
<br><br>
#
**IAM**
* We create an IAM role to allow our PHP website on our EC2 instance to access on our webserver.
<br><br>
![image](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20155747.png)
<br><br>
* We attached the role to our ec2 instance.
<br><br>
![image](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/Capture%20d'%C3%A9cran%202023-07-14%20155954.png)
<br><br>
#
**List of countries and the data**
<br><br>
![list of countries](https://github.com/killiangr/CloudProjet/blob/main/AWS_Site/43.png)

# IAM policies
**Question 1:**
<br><br>
![image](img-policies/policy1.png)
<br><br>
EC2 instances
* “ec2:RunInstances”: allows the user to launch new EC2 instances.
* “ec2:TerminateInstances”: allows the user to terminate EC2 instances.
* “arn:aws:ec2:us-east-1:123456789012:instance/*: allows all actions on all EC2 instances in the specified region (us-east-1) for the account ID 123456789012.
<br><br>

S3 instances
* “s3:GetObject”: allows the user to retrieve S3 objects
* “s3:PutObject”: allows the user to upload S3 objects
* “arn:aws:s3:::example-bucket/*”: allows actions on all objects within the example-bucket S3 bucket. 
<br><br>

**Question 2:**
<br><br>
![image](img-policies/policy2.png)
<br><br>
* “aws:RequestRegion”: “us-west-2” : allows access to VPC-related information only if the requested AWS region is set to “us-west-2”.
<br><br>

**Question 3:**
<br><br>
![image](img-policies/policy3.png)
<br><br>
Actions allowed on “example-bucket”:<br>
* “s3:GetObject”: allows the user to retrieve objects from the “example-bucket”.<br>
* “s3:PutObject”: allows the user to upload objects into the “example-bucket”.<br>
* “s3:ListBucket”: allows the user to list objects within the “example-bucket”.<br>
<br><br>

Specified prefixes in the condition:<br>
* “documents/*”: allows access to objects in the “bucket-example” that have the “document” prefix.<br>
* “images/*”: allows access to objects in the bucket-example” that have the “images” prefix.<br>
<br><br>

**Question 4:**
<br><br>
![image](img-policies/policy4.png)
<br><br>

Allowed actions:<br>
* “iam:CreateUser”: allows the user to create IAM users.<br>
* “iam:DeleteUser”: allows the user to delete IAM users.<br>
<br><br>

Resource ARNs:<br>
* Follows the following template “arn:aws:iam::123456789012:user/${aws:username}”<br>
* “${aws:username} is dynamically replaced by the username of the user currently connected. Ensures the users will only perform their allowed actions on their own IAM user resource.<br>
<br><br>

**Question 5:**
<br><br>
![image](img-policies/policy5.png)
<br><br>
* This policy grant access to all actions that start with Get “iam:Get*” and all actions that start with List “iam:List*”.<br>
* It does not allow to create anything. For that we would need to add “iam:Create*” to the actions allowed.<br>
<br><br>

“iam:Get*” allows:
* “Iam:GetGroup”: allows to retrieve a list of IAM users that are in the specified IAM group.<br>
* “iam:GetRole”: allows to retrieve information about the specified role (role’s path, GUID, ARN, role’s trust policy).<br>
*“iam:GetUser”: allows to retrieve information about the specified IAM user (user’s creation date, path, unique ID and ARN). <br>
<br><br>

**Question 6:**
<br><br>
![image](img-policies/policy6.png)
<br><br>
The actions “ec2:RunInstances” and “ec2:StartInstances” are denied to the user this policy is assigned to. However all actions not lister in the actions will be allowed to the user. <br>
<br><br>
Say that the policy included an additional statement object, like this example:
<br><br>
![image](img-policies/policy7.png)
<br><br>
The “allow” statement takes precedence over the “deny” effect. Therefore, the user will have access to all actions on ec2 instances and the actions defined before will not be taken into account. You would be able to terminate an instance as you would have all actions allowed on ec2 instances.<br>
