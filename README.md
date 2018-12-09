# Skeleton of a Policy

## Rule Description
* This section gives you a general idea of the aforementioned rule and tells you why it should be adhered to.

### Results Tab 
* This consists of all the Failed Resources, Ignored Resources, and the possible fixes available.
            
### Filter Tab
* This consists of a set of options that can be used to filter out the resources for which the rule should apply. If the options           are not set, by default, all resources which fail to comply to the rule will appear. 
            
### Action Tab
* Once marked, you can choose to undertake a specific action such as 'Stop', 'Delete', etc, after a resource repeatedly fails a           rule over a user specified period of time.

Consider the following illustration of the Public S3 Bucket rule,

## Rule Description 

An S3 Bucket when made public is automatically vulnerable to security breaches. Apart from this, you will be billed by AWS for           every download from a bucket. If there is an unprecedented amount of traffic due to some malicious attack it will quickly become         expensive. Hence, a bucket with public permissions should be made private. 

## Results Tab 

![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")

* Here, the Failed Resources section contains a list of all the Public S3 Buckets present. 
* The Ignore Resources section gives you the option of bypassing the rule for few or all resources. 
* This can be done by selecting the resource(s), and then clicking on Ignore All/ Ignore Selected. 
* On doing this, you can see that the selected resource(s) are now present in the Ignore Resources section.
* If you want to revert this action you can select the Revoke/ Revoke All option. (ask)
* If an automated fix is not available, you can follow the steps provided in 'how to fix'. 

## Filter Tab

![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")

* Filters can be used to apply the rule to S3 Buckets over only specfic regions.
* This can be done by specifying the Region.
* You can go one step further by specifying the tag(s) of the resource(s) in the 'Inlcude resources with tags' option.
* Once this is done, only the tagged resource(s) will be picked up.
* The same goes for explicitly excluding a resource by specifying the tag(s) of the resource(s) in the 'Exclude resources with             tags' option.
* Once this is done the tagged resource(s) will not be picked up.

## Action Tab

![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")

* On marking the Action tab you can choose to automate an action such as Delete, Stop, etc, for the failing resources after a             user specified period of time. 


# List of Cost Policies

## Old AMIs

  ### Description

  EBS backed AMIs are charged for the EBS volumes along with the EBS Snapahots. S3 backed AMIs are charged for the S3 storage.
  Hence, old AMIs should ideally be deregistered to avoid these costs.

  ### Action

  * DEREGISTER : Deregisters the old AMI(s).
        
## Old Snapahots

  ### Description

  It is advisible to not keep Snapshots older than 10 days due to the incurred cost that comes along with it.

  ### Action

   * DELETE : Deletes Snapahots older than 10 days.

## Idle EC2 for 3 days

  ### Description

  EC2 instances that are running but have a CPU utilization of less than 2% over a period of 72 hours are considered to be                 idle EC2 instances.
        
  ### Action

  * STOP : Stops the idle EC2 instances.
  * TERMINATE : Terminates the idle EC2 instances.  

## Detached Elastic IPs

  ### Description

  AWS enforces an hourly charge if an Elastic IP (EIP) address within your account is not associated with a running EC2                   instance or an Elastic Network Interface (ENI).

  ### Action

  * No action available yet.

## EC2 with No Network Activity

  ### Description

  EC2 instances where the data being sent or recieved is less than 128Kbs over a period of 5 days is considered to have no                 network activity.

  ### Action

  * STOP : Stops the idle EC2 instances. 
  * TERMINATE : Terminates the idle EC2 instances.  

## EMR across Multiple AZs

  ### Description

  There are costs incurred when data is being sent from one availablity zone to another, hence it is advisible to not have EMR             clusters that span over multiple AZs.

  ### Action

  * No action available yet.
          
## Public S3 Bucket

  ### Description

  An S3 Bucket when made public is automatically vulnerable to security breaches. Apart from this, you will be billed by AWS               for every download from a bucket. If there is an unprecedented amount of traffic due to some malicious attack it will                   quickly become expensive. Hence, a bucket with public permissions should be made private. 

            
  ### Action

  * DELETE : Deletes the public S3 Buckets.

## S3 VPC EndPoint

  ### Description

  A VPC endpoint enables you to privately connect your VPC to your S3 Bucket without requiring an internet gateway, NAT                   device, VPN connection, or AWS Direct Connect connection. Instances in your VPC do not require public IP addresses to                   communicate with resources in the service. Traffic between your VPC and the other service does not leave the Amazon network.             As there are charges associated with internet gateways etc, this is a better and safer option.

  ### Action

  * No action available yet.

## UnderUtilized EC2 Instance

  ### Description

  When an EC2 Instance has a CPU utlilization of less than 10% it is considered to be underutilized.

  ### Action

  * STOP : Stops the underutilized EC2 instances. 
  * TERMINATE : Terminates the underutilized EC2 instances.  

## Unused EBS

  ### Description

  Elastic Block Stores that are provisioned but unattached to any instances or are underutilized incur some cost and hence                 should be deleted when unused.

  ### Action

  * DELETE : Deletes the unused EBS.

## Unused Load Balancers

  ### Description

  Load Balancers with zero connections(unused) but in active state are still billed for by AWS. 

  ### Action

  * DELETE : Deletes the unused Load Balancers.

## Unused PIOPS Disks

  ### Description

  Provisioned IOPS disks that are not attached to any resources such as EC2, RDS, etc or are underutilized are still billed               for by AWS.

  ### Action

  * TERMINATE : Terminates the unused Provisioned IOPS Disks


# List of Secuity Policies 

## IAM POLICIES

  ### AWS Resource Access  

  Ensure IAM instance roles are used for AWS resource access from instances.

  ### AWS Support Role

  A support role should be created so as to manage incidents with the AWS support.

### Access Keys 90 day Rotation 

Changing access keys (which consist of an access key ID and a secret access key) on a regular schedule is a well-known                   security best practice because it shortens the period an access key is active and therefore reduces the business impact if               they are compromised.

### Access Keys for Console Access Users

Do not set up access keys during inital user setup for all IAM users that have console password.

### Active IAM Master/Manager 

IAM Master/Manager roles should be active in order to effectively manage user permissions for all levels of your                         organisation.

### Avoid Root account 

We strongly recommend that you do not use the root user for your everyday tasks, even the administrative ones. Instead,                 adhere to the best practice of using the root user only to create your first IAM user. Then securely lock away the root user             credentials and use them to perform only a few account and service management tasks.

### Current Contact Info 

Ensure your contact information is current.

### Disable Unused Credentials 

Ensure that credentials unused for more than 90 days are disabled.

### Enable Detailed Billing

To have a better idea about the breakup details of your spend ensure detailed billing is activated.

### Hardware MFA Enabled 

Ensure hardware mutlifactor authorisation is enabled. Without multi-factor authentication (MFA), antivirus software,                     firewalls, encryption technology, and vulnerability tests can be bypassed.

### IAM Group Policy

Ensure IAM policies are attached only to groups or roles and not directly to individual users.

### IAM Password Policy 90 days

Ensure that the IAM password policy expires within 90 days or less.

### IAM Policy groups/roles

Ensures that security questions are registered in the AWS account.

### MFA Enabled

Ensure mutlifactor authorisation is enabled for all IAM users that have a console password. Without multi-factor                         authentication (MFA), antivirus software, firewalls, encryption technology, and vulnerability tests can be bypassed.

### Minimum 1 LowerCase letter in password

To make your password stronger ensure that it contains a minimun of one lowercase letter.

### Minimum 1 Number

To make your password stronger ensure that it contains a minimun of one number.

### Minimum 1 Symbol 

To make your password stronger ensure that it contains a minimun of one symbol.

### Minimum 1 UpperCase letter in password 

To make your password stronger ensure that it contains a minimun of one uppercase letter.

### Minimum Password Length 

To make your password stronger ensure that it contains a minimun of one lowercase letter.

### Password Reuse

Ensures IAM policy password prevents password reuse.

### Root MFA Enabled

Ensures that mutlifactor authentication is enabled for root user access.

### Root access key 

Ensures no root account access key exists.

### SNS Topic Subscribers

A topic is a communication channel to send messages and subscribe to notifications. Ensure that the SNS topic Subscribers               are matched appropriately. 

### Security Contact Info 

Ensures security contact information is registered.


## MONITORING POLICIES


### AWS Auth Failure 

Ensures that a log metric filter and alarm exists for AWS management console authentication failures.

### AWS Config Change

Ensures that a log metric filter and alarm exists for AWS Config configuration changes.


### Alarm for UnAuthorized API calls 

Ensures that a log metric filter and alarm exists for unauthorized API calls.

### CMKs Deletion/Disable

Ensures that a log metric filter and alarm exists for disabling or scheduled deletion of customer created CMKs.

### CloudTrail Config Change

Ensures that a log metric filter and alarm exists for CloudTrail Config Changes.

### IAM Policy Change

Ensures that a log metric filter and alarm exists for IAM Policy changes.

### MFA Console SignIn

Ensures that a log metric filter and alarm exists for management console sign-in without mutlifactor authentication.

### NACL Change

Ensures that a log metric filter and alarm exists for changes in Network Access Control List.

### Network Gateway Change

Ensures that a log metric filter and alarm exists for changes to Network Gateways.

### Root Account Alarm

Ensures that a log metric filter and alarm exists for when there root access occurs.

### Route Table Change 

Ensures that a log metric filter and alarm exists for when there are changes in the route table.

### S3 Policy Change

Ensures that a log metric filter and alarm exists for when there are changes in S3 Bucket policies.

### Security Group Change

Ensures that a log metric filter and alarm exists for when there are changes in security groups.

### VPC Change

Ensures that a log metric filter and alarm exists for when there are VPC changes.


## AUDIT POLICIES


### AWS Config Enabled

AWS Config provides a detailed view of the configuration of AWS resources in your AWS account. This includes how the                     resources are related to one another and how they were configured in the past so that you can see how the configurations and             relationships change over time. By having the AWS Config enabled for all regions it helps in keeping track of growing                   resources present in all regions. 

### Cloud Trail integration of CloudWatch Logs 

Cloud Trail tracks user activity and API usage. After you configure CloudTrail integration with CloudWatch Logs, which you               can do from the CloudTrail console or using the AWS SDKs or AWS CLI, CloudTrail begins to continuously and automatically                 deliver all the CloudTrail events associated with API activity to a CloudWatch Logs log group you specify. 

### CloudTrail Enabled

CloudTrail trails should be active for all regions so that it is able to pick up the user activity and the API usage in all             regions for that specfifc trial.

### CloudTrail Encrypted

CloudTrail logs should be encrypted at rest so that it stays protected even if it falls into the wrong hands.

### CloudTrail Log File Validation

Ensures that CloudTrail log file validation has been enabled.

### CloudTrail Public Access

Ensures that S3 bucket cloudtrail logs are not publically accessible.

### No SSE/KMS Encryption for S3 

Reports S3 Buckets without SSE/KMS encryption. 

  #### Actions 

  * DELETE : Deletes the reported S3 Buckets.


### Public EC2 Instance 

Reports EC2 instances with public ip addresses.

  #### Actions

  * STOP : Stops the EC2 instance.
  * TERMINATE : Terminates the EC2 instance.

### Rotation of customer CMKs Enabled

When you enable automatic key rotation for a customer managed CMK, AWS KMS generates new cryptographic material for the CMK             every year. AWS KMS also saves the CMK's older cryptographic material so it can be used to decrypt data that it encrypted.

### S3 Bucket Access 

Ensures S3 Bucket access logging is enabled on the cloudtrail S3 bucket.


## NETWORKING POLICIES


### RDP not Allowed from Everywhere

Ensures that no security group has the TCP/UDP port (3389) open to the world.

### SSH not Allowed from Everywhere

Ensures that no security group has the SSh port (22) open to the world.

### VPC Flow Logging Enabled

Ensures VPC flow logging is enabled for all VPCs.

### VPC Peering with Least Access

Ensures that when VPC peering takes place they have least access while connecting to each other.

### VPC Traffic Restriction of Security Group 

Ensures that the default security group of every VPC restricts all traffic.

# EC2 SCHEDULER 

## DESCRIPTION 

The EC2 scheduler once activated, can be used to stop and restart EC2 instances. For the scheduler to work the following should be specifed :

    1. The stop and restart time (default being 10pm and 6am) along with the timezone (default being IST).
    2. The regions across which the scheduler should be active.

Apart from the above two mandatory requirements, there is an option of including or excluding resources with specific tags available.

There are three types of schedulers :

Daily scheduler : The daily scheduler is used to stop and restart EC2 instances on a daily basis according to a stipulated time specifed by the user.

Weekend scheduler : Similar to the daily scheduler, this scheduler is used to stop and restart EC2 instances during the weekend.

Customisable scheduler : The customisable scheduler is similar to the above two and n-number of them can be created with varying parameters.


# RDS SCHEDULER 

## DESCRIPTION 

The RDS scheduler once activated, can be used to stop and restart RDS instances. For the scheduler to work the following should be specifed :

1. The stop and restart time (default being 10pm and 6am) along with the timezone (default being IST).
2. The regions across which the scheduler should be active.

Apart from the above two mandatory requirements, there is an option of including or excluding resources with specific tags available.

There are three types of schedulers :

Daily scheduler : The daily scheduler is used to stop and restart RDS instances on a daily basis according to a stipulated time specifed by the user.

Weekend scheduler : Similar to the daily scheduler, this scheduler is used to stop and restart RDS instances during the weekend.

Customisable scheduler : The customisable scheduler is similar to the above two and n-number of them can be created with varying parameters.
