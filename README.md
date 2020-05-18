---
description: Preparation for AWS Cloud Practitioner Exam
---

# Initial page

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

### 2\) Elastic Container Registry 

To begin the authorisation process to communicate your docker client with your default registry :  
`aws ecr get-login --region <region> --no-include-email`

docker login command will produce an authorisation token used within the registry for 12 hours`docker login -u AWS -p <password> https://<aws_account_ID>.dkr.ecr.region.amazonaws.com`

\`\`



