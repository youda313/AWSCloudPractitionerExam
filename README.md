---
description: Preparation for AWS Cloud Practitioner Exam
---

# Initial page

### 1\) Around the World with AWS

#### Region

* Geographic area consisting of 2 or more availability zones

#### Availability Zone

* A data center

#### Edge Location

* CDN Endpoints for CloudFront
* Many more edge locations than regions

### 2\) Elastic Container Registry 

To begin the authorisation process to communicate your docker client with your default registry :  
`aws ecr get-login --region <region> --no-include-email`

docker login command will produce an authorisation token used within the registry for 12 hours`docker login -u AWS -p <password> https://<aws_account_ID>.dkr.ecr.region.amazonaws.com`

\`\`



