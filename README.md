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

### 17\) VPC

5 VPC  / region max

5 address are reserved in private networks example with 10.0.1.0/24:  
10.0.1.0  
10.0.1.1 -&gt; AWS routing  
10.0.1.2 -&gt; AWS DNS  
10.0.1.3 -&gt; AWS future  
10.0.1.255



### 18\) Exam Question

\#5AWS General

What does AWS design concept of "loose coupling" mean?To automate system recovery processes**B**To design a system that minimizes interdependencies**C**To break large data processing tasks into several small, separate tasks**D**To provide an identity only enough access to complete its assigned tasks

**Explanation**

Loose coupling means that complex applications should be broken down into small, loosely coupled components with as few interdependencies as possible. This way, a change in one component does not cause failures in a cascading manner through other system components. [https://d0.awsstatic.com/white...](https://d0.awsstatic.com/whitepapers/AWS_Cloud_Best_Practices.pdf)

\#9AWS General

Which of the following **is not** a benefit of AWS cloud computing?**A**increase speed and agility**B**no expense maintaining data centers**C**increase workload consistencytrade capital expense for variable expense

**Explanation**

The only choice listed that is not a direct benefit of AWS cloud computing is improved system workload/traffic consistency. In fact, the inconsistent nature of many online applications and business systems is a reason why cloud computing can be beneficial to many companies. The other choices listed are all established benefits listed by AWS. [https://d0.awsstatic.com/white...](https://d0.awsstatic.com/whitepapers/aws-overview.pdf)

\#13

Which service below **is not** directly related to traceability?AWS Config**B**CloudTrail**C**CloudWatch**D**Trusted Advisor

**Explanation**

Traceability is the ability to audit, monitor and log your environment, and is key to establish automated responses to events. AWS Config is directly related to auditing and compliance, CloudTrail to logging, and CloudWatch to monitoring. Trusted Advisor is related to the implementation of security best practices, but is not related to tracing the cause of specific incidents in AWS. [https://d1.awsstatic.com/white...](https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf)

\#14KMS

Key Management Service \(KMS\) is used to manage encryption keys in your AWS environment. How can you audit the changes made on KMS?**A**KMS provides history to each key changes; you can track the changes done on each key using key history.**B**KMS has full audit and compliance integration with CloudTrail; this is where you can audit all changes performed on KMS.**C**KMS provides full audit details as part of KMS console which can be accessed through web interface and APIs.KMS will log all changes in a special S3 bucket that is created the first time KMS service is being used.

**Explanation**

KMS is fully integrated with CloudTrail which provides audit and compliance features on all actions performed in KMS. [https://cloudacademy.com/amazo...](https://cloudacademy.com/amazon-web-services/amazon-web-services-key-management-service-kms-course/key-management-service-basics.html)

\#16CloudFront

Which of the following is true of the security of your origin server in Amazon Cloudfront?**A**The HTTP server is responsible for ensuring the security of your origin server.**B**Amazon S3 bucket is responsible for ensuring the security of your origin server.The domain server is responsible for ensuring the security of your origin server.**D**You are responsible for ensuring the security of your origin server.

**Explanation**

In Amazon CloudFront, you are responsible for ensuring the security of your origin server. You must ensure that CloudFront has permission to access the server and that the security settings are appropriate to safeguard your content. [http://docs.aws.amazon.com/Ama...](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-creating.html)

\#17RDS

Will I be charged when an Amazon RDS DB instance is idle?**A**Yes, you will be charged.Yes, you will charged but only if the instance is running in VPC.**C**Yes, you will charged but only if the instance is running in GovCloud.**D**No, you'll not be charged for idle instances.

**Explanation**

Unexpected charges on your account can be the result of a simple misunderstanding, or an indication of a resource configuration issue. Here are some things to check: 

Idle instances Amazon Elastic Compute Cloud \(Amazon EC2\) and Amazon Relational Database Service \(Amazon RDS\) instances accrue hourly charges as soon as you launch the instance, and continue accruing until you explicitly terminate the instance. If you launch an instance and then sign out of your account without terminating the instance, it will continue running and accruing charges. Using more than one region 

The AWS Management Console displays only one region at a time. If you accrue charges but aren't able to see any running instances under the EC2 tab in the console, you may want to review the other regions by selecting each of them from the drop-down menu in the upper left corner of the console page. [https://aws.amazon.com/billing...](https://aws.amazon.com/billing/new-user-faqs/)

\#18Glacier

A user is uploading a backup of data to S3 Glacier for the purpose of disaster recovery \(DR\). The data stored in S3 Glacier is part of a larger data recovery plan that involves other AWS services.

There is a relatively small set of data \(100 MB\) that needs to be restored immediately when a DR plan is executed, and the organization is planning RTO of 1 hour.  Assuming the data size meets the requirements for any of the given retrieval options below, which S3 Glacier data retrieval option would you plan in a DR situation?**A**Use Bulk retrievals**B**

Use Expedited Retrievals with Provisioned CapacityUse Standard retrievals**D**

Use Expedited retrievals without Provisioned Capacity

**Explanation**

There are three retrieval options with Amazon S3 Glacier:

* Expedited — There are two types of Expedited retrievals: On-Demand and Provisioned. On-Demand requests are similar to EC2 On-Demand instances and are available most of the time. Provisioned requests are guaranteed to be available when you need them, which is recommended for a DR plan.
* Standard — Standard retrievals allow you to access any of your archives within several hours. 
* Bulk — Bulk retrievals are Amazon S3 Glacier’s lowest-cost retrieval option, which you can use to retrieve large amounts, even petabytes, of data inexpensively in a day. Bulk retrievals typically complete within 5–12 hours.

 [http://docs.aws.amazon.com/ama...](http://docs.aws.amazon.com/amazonglacier/latest/dev/introduction.html)

\#25S3

A user has archived data to Amazon S3 Glacier. How much data can the user restore from Glacier for free every month?Up to 5 GB per month**B**Up to 10 GB per month**C**Up to 20 GB per month**D**5 percent of your total data stored on S3 per month, or 5 GB of data

**Explanation**

As part of the AWS Free Usage Tier, you can retrieve up to 10 GB of your Amazon Glacier data per month for free. The free tier allowance can be used at any time during the month and applies to Standard retrievals. [http://aws.amazon.com/s3/faqs/...](http://aws.amazon.com/s3/faqs/#How_will_I_be_charged_when_restoring_large_amounts_of_data_from_Amazon_Glacier)

\#26EC2

Which storage option is hosted by Amazon EC2 instances themselves?**A**Amazon S3**B**Amazon Instance Store VolumesAmazon EFS**D**Amazon EBS

**Explanation**

Amazon EC2 supports the following storage options: 

1. Amazon Elastic Block Store \(Amazon EBS\) 
2. Amazon EC2 Instance Store 
3. Amazon Simple Storage Service \(Amazon S3\) 
4. Amazon Elastic File System \(EFS\)

However, only Instance Store Volumes are hosted by and included as part of the EC2 service itself. [http://docs.amazonwebservices....](http://docs.amazonwebservices.com/AWSEC2/latest/UserGuide/Storage.html)

\#29

Which of the following is a feature available exclusively for Enterprise-level support?Customer Service**B**Support forums**C**Service health checks**D**White-glove case routing

**Explanation**

Enterprise-level Support customers have access to these additional features that normal AWS customers do not: 

* Application architecture guidance: consultative partnership supporting specific use cases and applications
* Infrastructure event management: short-term engagement with AWS Support to partner with your technical and project resources to gain a deep understanding of your use case and provide architectural and scaling guidance for an vent
* AWS Concierge
* Technical account manager
* White-glove case routing
* Management business reviews

 [http://docs.aws.amazon.com/aws...](http://docs.aws.amazon.com/awssupport/latest/user/getting-started.html)

\#30Direct Connect

With \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ you can transfer your business critical data directly from your datacenter, office, or colocation environment to and from AWS bypassing your Internet Service Provider and removing network congestion.**A**AWS Direct Connect**B**Amazon Data PipelineAWS Storage Gateway**D**Amazon CloudWatch

**Explanation**

With AWS Direct Connect, you can transfer your business critical data directly from your datacenter, office, or colocation environment to and from AWS, bypassing your Internet Service Provider and removing network congestion.  
 [http://aws.amazon.com/directco...](http://aws.amazon.com/directconnect/details/)

\#31

You have a time-sensitive development question and you decide that you need some support from AWS. Which of the following severity levels will be an appropriate choice for you to resolve the issue?**A**Business-critical system down**B**System impairedGuidance**D**Production system down

**Explanation**

In regards to AWS support, if you have a problem which meets any of the following, it is considered a system impaired priority.

* You can work around the problem
* Non-critical functions of your application are behaving abnormally.
* You have a time-sensitive development question. \(Developer, Business, and Enterprise\)

 [http://docs.aws.amazon.com/aws...](http://docs.aws.amazon.com/awssupport/latest/user/getting-started.html)

\#32AWS General

What does the phrase 'stop guessing capacity' mean?**A**To use elastic IP addresses to increase high availability**B**To implement self-healing processesTo set correct data storage lifecycles**D**Automate deployments based on performance metrics

**Explanation**

One of the best practices of the reliability pillar of the Well-Architected Framework is to 'stop guessing capacity.' This looks at the use of Auto Scaling to prevent the need to predict and guess your capacity and demand requirement which aids in a better end-user experience. [https://d1.awsstatic.com/white...](https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf)

\#36AWS General

How does AWS define cloud computing?**A**The on-demand delivery of IT resources through a cloud services platform via the Internet with pay-as-you-go pricing.**B**A pool of servers offering compute resources that are designed to be issued exclusively to individual tenants \(users and organizations\).The term used to describe virtualized technology.**D**A physical pool of compute, storage and network resources that can’t be accessed over the internet.

**Explanation**

Cloud computing provides a simple way to access servers, storage, databases and a broad set of application services over the Internet. A cloud services platform such as Amazon Web Services owns and maintains the network-connected hardware required for these application services, while you provision and use what you need via a web application. [https://d0.awsstatic.com/white...](https://d0.awsstatic.com/whitepapers/aws-overview.pdf)

\#44ELB Route53

Which of the following traditional disaster recovery methods runs your site in AWS as well as on your existing on-site infrastructure, in an active-active configuration?**A**AWS Production to an AWS DR SolutionWarm standby solution**C**Active-passive solution**D**Multi-site solution

**Explanation**

In AWS, a multi-site solution runs in AWS as well as on your existing on-site infrastructure, in an active-active configuration. [http://media.amazonwebservices...](http://media.amazonwebservices.com/AWS_Disaster_Recovery.pdf)

\#45AS

Which of the choices below **best describes** what Auto Scaling is well suited for?**A**Both for applications that have stable demand patterns and that experience hourly, daily, or weekly variability in usage.Only for applications that experience hourly, daily, or weekly variability in usage.**C**Both for applications that use frameworks and SDKs to enhance its customer relationship.**D**Only for applications with a stable usage pattern but extremely high workload.

**Explanation**

Auto Scaling is well suited to both applications that have stable demand patterns and that experience hourly, daily, or weekly variability in usage. Whether the demand is predictable or unpredictable auto scaling can be a good choice. If the demand is predictable and long term you may choose reserved instances. If the demand is unpredictable you may choose on-demand or even spot instance \(if you can afford to have an instance lost unexpectedly\). [http://aws.amazon.com/autoscal...](http://aws.amazon.com/autoscaling/)

\#46Lambda

AWS Lambda monitors Lambda functions and reports metrics through which Amazon service?**A**Amazon CloudWatchAmazon CloudTrail**C**Amazon Kinesis**D**Amazon Elastic Compute Cloud

**Explanation**

AWS Lambda automatically monitors Lambda functions on your behalf, reporting metrics through Amazon CloudWatch. [http://docs.aws.amazon.com/lam...](http://docs.aws.amazon.com/lambda/latest/dg/monitoring-functions.html)

\#50AWS General

Your customers are concerned about the security of their sensitive data and their inquiry asks about what happens to old storage devices on AWS. What would be the best answer to this question? AWS uses a 3rd party security organization to destroy data as part of the decommissioning process.**B**AWS uses its proprietary software to destroy data as part of the decommissioning process.**C**AWS uses the techniques detailed in DoD 5220.22-M to destroy data as part of the decommissioning process.**D**AWS reformats the disks and uses them again.

**Explanation**

When a storage device has reached the end of its useful life, AWS procedures include a decommissioning process that is designed to prevent customer data from being exposed to unauthorized individuals.

**AWS uses the techniques detailed in DoD 5220.22-M \(“National Industrial Security Program Operating Manual “\) or NIST 800-88 \(“Guidelines for Media Sanitization”\) to destroy data as part of the decommissioning process.**

All decommissioned magnetic storage devices are degaussed and physically destroyed in accordance with industry-standard practices. [https://d0.awsstatic.com/white...](https://d0.awsstatic.com/whitepapers/aws-security-whitepaper.pdf)

\#52RDS

Can Amazon RDS manage synchronous data replication across Availability Zones?**A**YesYes, Amazon RDS can manage this but only for certain DB instance types.**C**No, Amazon RDS does so only for certain AZs.**D**No

**Explanation**

Yes, in the Multi-AZ Deployment option, Amazon RDS manages synchronous data replication across Availability Zones and automatic failover. [http://aws.amazon.com/rds/faqs...](http://aws.amazon.com/rds/faqs/)

\#54EC2

When does the billing process for an Amazon EC2 instance begin?**A**When the instance is in a 'pending' state.As soon as it launches for the first time.**C**When the AMI boot sequence is initiated.**D**When your distribution status changes to deployed.

**Explanation**

Billing commences when Amazon EC2 initiates the boot sequence of an AMI instance. Billing ends when the instance terminates, which could occur through a web services command, by running "shutdown -h", or through instance failure. When you stop an instance, Amazon shuts it down but doesn't charge per-second or per-hour usage for a stopped instance, or data transfer fees, but charges for the storage for any Amazon EBS volumes. [https://docs.aws.amazon.com/AW...](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-lifecycle.html)

\#57CloudWatch

You are implementing Amazon CloudWatch for monitoring of your AWS infrastructure. What can you use within CloudWatch to take actions such as sending a notification to an SNS topic or an Auto Scaling policy?**A**ActionEvent**C**Alarm**D**Dashboard

**Explanation**

You can use an alarm to automatically initiate actions on your behalf. An alarm watches a single metric over a specified time period, and performs one or more specified actions, based on the value of the metric relative to a threshold over time. Alarms invoke actions for sustained state changes only. CloudWatch alarms will not invoke actions simply because they are in a particular state. The state must have changed and been maintained for a specified number of periods. [http://docs.aws.amazon.com/Ama...](http://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html)







