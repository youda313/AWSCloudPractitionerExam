---
description: Preparation for AWS Cloud Practitioner Exam
---

# Initial page

### TODO: Generate Json file to feed the exam training app

### walkthrough[`https://dev.to/katieraby/how-to-pass-the-aws-certified-cloud-practitioner-exam-in-2020-3d31`](https://dev.to/katieraby/how-to-pass-the-aws-certified-cloud-practitioner-exam-in-2020-3d31)

### Other repositories[`https://github.com/yafeunteun/aws-cloud-practitioner-certification-notes`](https://github.com/yafeunteun/aws-cloud-practitioner-certification-notes)[`https://gist.github.com/sheilnaik/2b2a7f8b26b74099a783d7694350a05e`](https://gist.github.com/sheilnaik/2b2a7f8b26b74099a783d7694350a05e)\`\`

### 1\) Around the World with AWS

#### Region

* Geographic area consisting of 2 or more availability zones

#### Availability Zone

* A data center

#### Edge Location

* CDN Endpoints for CloudFront
* Many more edge locations than regions

### 2\) ECS - Elastic Container Service

Docker or AWS Fargate 

Each Instance in a cluster will have a Docker Deamon and an ECS agent

### 3\) ECR - Elastic Container Registry 

Store and manage your docker images

To begin the authorisation process to communicate your docker client with your default registry :  
`aws ecr get-login --region <region> --no-include-email`

use the output of the previous command with the following  
docker login command will produce an authorisation token used within the registry for 12 hours`docker login -u AWS -p <password> https://<aws_account_ID>.dkr.ecr.region.amazonaws.com`

Policies associated to ECR:  
AmazonEC2ContainerRegistryFullAccess  
AmazonEC2ContainerRegistryPowerUser  
AmazonEC2ContainerRegistryReadOnly

MAke sure in the policy to add a 'principal' in the policy to provide access to the ECR and 'ecr:GetAuthorizationToken' API call

Use push/pull command to store/retrieve your docker images

### 4\) EKS -  Elastic Container Service for Kubernetes

Master plane vs worker nodes



1. Create an EKS Service Role: Before you begin working with EKS you need to configure and create am IAM service-role that allows EKS to provision and configure specific resources.  This role only needs to be created once and can be used for all other EKS clusters created going forward. The role needs to have the following permissions policies attached to the role: **AmazonEKSServicePolicy** and **AmazonEKSClusterPolicy**
2. Create an EKS Cluster VPC: Using AWS CloudFormation you need to create a and run a CloudFormation stack based on the following template: https://amazon-eks.s3-us-west-2.amazonaws.com/cloudformation/2019-02-11/amazon-eks-vpc-sample.yaml which will configure a new VPC for you to use with EKS
3. Install **kubectl** and the **AWS-IAM-Authenticator**: 
4. Create your EKS Cluster: Using the EKS console you can now create your EKS cluster using the details and information from the VPC created in step 1 and 2
5. Configure kubectl for EKS: Using the `update-kubeconfig` command via the AWS CLI you need to create a kubeconfig file for your EKS cluster
6. Provision and configure Worker Nodes: Once your EKS cluster shows an ‘Active’ status you can launch your worker nodes using CloudFormation based on the following template: https://amazon-eks.s3-us-west-2.amazonaws.com/cloudformation/2019-02-11/amazon-eks-nodegroup.yaml
7. Configure the Worker Node to join the EKS Cluster: Using a configuration map downloaded here:

curl -O [https://amazon-eks.s3-us-west-2.amazonaws.com/cloudformation/2019-02-11/aws-auth-cm.yaml](https://amazon-eks.s3-us-west-2.amazonaws.com/cloudformation/2019-02-11/aws-auth-cm.yaml)

You must edit it and Replace the &lt;ARN of instance role \(not instance profile\)&gt; with the NodeInstanceRole value from step 6

You EKS Cluster and worker nodes are now configured ready for your to deploy your applications with Kubernetes.

### 5\) AWS Elastic Beanstalk

AWS Elastic Beanstalk is an AWS managed service that allows you to upload the code of your web application, along with the environment configurations, which will then allow Elastic Beanstalk to automatically provision and deploy the appropriate and necessary resources required within AWS to make the web application operational. These resources can include other AWS services and features, such as EC2, Auto Scaling, application health-monitoring, and Elastic Load Balancing, in addition to capacity provisioning. This automation and simplification makes it an ideal service for engineers who may not have the familiarity or the necessary skills within AWS to deploy, provision, monitor, and scale the correct environment themselves to run the developed applications. Instead, this responsibility is passed on to AWS Elastic Beanstalk to deploy the correct infrastructure to run the uploaded code. This provides a simple, effective, and quick solution to deploying your web application.

![](.gitbook/assets/image.png)

If the application manages and handles HTTP requests, then the app will be run in a web server environment. If the application does not process HTTP requests, and instead perhaps pulls data from an SQS queue, then it would run in a worker environment.

### 6\) AWS Lambda

Firstly, AWS Lambda needs to be aware of your code that you need run so you can either upload this code to AWS Lambda, or write it within the code editor that Lambda provides. Currently, AWS Lambda supports Notebook.js, JavaScript, Python, Java, Java 8 compatible, C\#, .NET Core, Go, and also Ruby. It's worth mentioning that the code that you write or upload can also include other libraries. Once your code is within Lambda, you need to configure Lambda functions to execute your code upon specific triggers from supported event sources, such as S3. As an example, a Lambda function can be triggered when an S3 event occurs, such as an object being uploaded to an S3 bucket. Once the specific trigger is initiated during the normal operations of AWS, AWS Lambda will run your code, as per your Lambda function, using only the required compute power as defined. AWS records the compute time in milliseconds and the quantity of Lambda functions run to ascertain the cost of the service.

Lambda function =&gt; your own code  
Event sources =&gt; aws service can be use to trigger a function  
Trigger  
Downstream resources  
Log Stream

### 7\) AWS Batch

For use of vast amount of compute power in a cluster of resources

### 8\) Amazon Lightsail

for small businesses or single users

### 9\) S3

5TB as max storage

There are a number of different storage classes within S3, all of which offer different performance features and costs. And it's down to you to select the storage class that you require for the data. These classes are as follows.   
Standard,   
Standard Infrequent Access,   
Intelligent Tiering,   
One Zone Infrequent Access,   
Reduced Redundancy =&gt; But this Reduced Redundancy option is no longer recommended by AWS

![Storage classes](.gitbook/assets/image%20%281%29.png)



### 10\) Amazon Glacier

Long term storage, there is a cost associated to retrieve data

Vault and Archive type of storage \(only vault is available from the web console\)

![](.gitbook/assets/image%20%282%29.png)

### 11\) EC2 instance storage

Local storage from the EC2 instance - \(ephemeral storage\)

Ideal as cache or buffer

### 12\) Amazon Elastic Block Store \(EBS\)

Can only be attached to one EC2 instance

Persistent against stopping and deletion of the EC2 instance

Can create a new volume from a snapshot

### 13\) Amazon Elastic File System

Shared file system - only compatible with NFS \(windows not supported\)

### 14\) Amazon Cloudfront

Content Delivery Network \(CDN\)

### 15\) AWS Storage Gateway

File, Volume and tape gateway from on premises storage to AWS services

can be used as a backup storage for on premises backup

### 16\) AWS Snowball

Securely transfer petabytes of data in and out of AWS

snowball is resistant to dust water and tampering

HIPAA compliant

Use of shipping devices via inked marked devices









