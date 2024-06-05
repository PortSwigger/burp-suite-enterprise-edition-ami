# Setup guide: using an AMI

You can use the Burp Suite Enterprise Edition AMI to create an EC2 instance that contains Burp Suite Enterprise Edition. The AMI includes both the server and scanning machine components required for an installation capable of scanning.

Before you choose to deploy Burp Suite Enterprise Edition using an AMI, be aware of the following key points:

- Easy to install if your organization already uses AWS.
- You'll need experience with EC2 and managing your own external relational database instance, such as AWS RDS.
- All scans run on a single EC2 instance. The number of scans you can run concurrently depends on the size of your instance. We don't currently support external scanning machines.
- Doesn't support automatic updates. We recommend that you deploy a new AMI that contains the updated version of Burp Suite Enterprise Edition to a replacement instance.

## Prerequisites

Before you use an AMI to deploy an instance, make sure you meet these prerequisites:

- You must have prior experience with AWS using AMIs or CloudFormation to deploy instances.
- Make sure that you understand the [system requirements for the instance](#system-requirements-for-ami-instances).
- You have set up a VPC and VPC subnet for the instance.
- You have set up an [external database](https://portswigger.net/burp/documentation/enterprise/setup/self-hosted/kubernetes/setup-external-database.html).
- We recommend you use [Vals](https://github.com/helmfile/vals) to avoid storing passwords in plain text.

For information on what we're able to support you with, see [Support scope for AMIs](#support-scope-for-ami-instances).

## System requirements for AMI instances

### Instance types

The following table shows the number of concurrent scans each instance type supports in the CloudFormation template, using the default values for container resource allocations.

| Instance Type | CPU cores | RAM (GB) | Concurrent Scans |
|---------------|-----------|----------|------------------|
| m7i.2xlarge   | 8         | 32       | 1                |
| r7i.2xlarge*  | 8         | 64       | 2                |
| m7i.4xlarge   | 16        | 64       | 3                |
| r7i.4xlarge   | 16        | 128      | 6                |
| m7i.8xlarge   | 32        | 128      | 8                |
| r7i.8xlarge   | 32        | 236      | 14               |
| r7i.12xlarge  | 48        | 384      | 22               |
| r7i.16xlarge  | 64        | 512      | 30               |
| r7i.24xlarge  | 96        | 768      | 46               |
| r7i.48xlarge  | 192       | 1,536    | 94               |

*Default instance size in the CloudFormation template

### Default values for container resource allocations

These settings are suitable for most deployments and typical scan targets. If you change the container resource allocations, it alters the number of concurrent scans each instance type can handle. You may need to tune these settings if you are scanning very large or complex targets.

| **Setting**                     | **Value** |
|---------------------------------|-----------|
| maxCpuPerContainer          | 4000m     |
| maxMemoryPerContainer       | 8Gi       |
| webServerContainerCpu       | 1400m     |
| webServerContainerMemory    | 4Gi       |
| enterpriseServerContainerCpu| 1400m     |
| enterpriseServerContainerMemory | 4Gi   |
| connectionCheckContainerCpu | 1400m     |
| connectionCheckContainerMemory | 2Gi   |
| scanContainerCpu            | 1400m     |
| scanContainerMemory         | 8Gi       |


## System requirements for the external database

The external database stores the accumulated data from your scans. The required size depends on the number of scans that you perform and the number of issues found.

The requirements for the external database are the same as for a Kubernetes instance. For more information, see:

- [Database system requirements](https://portswigger.net/burp/documentation/enterprise/setup/self-hosted/kubernetes/external-database-requirements)
- [Setting up your external database](https://portswigger.net/burp/documentation/enterprise/setup/self-hosted/kubernetes/setup-external-database)

## Support scope for AMI instances

The following is within our support scope for AMI instances:

- Creation of an EC2 instance that contains Burp Suite Enterprise Edition and its components using an AMI.
- Supporting the application running state post-deployment.
- Updating to later versions of Burp Suite Enterprise Edition.

### Not supported

We are unable to support the following:

- Creating your external database.
- Creating your VPC, VPC subnet and related infrastructure.
- Customization of the AMI.

## AMI customer responsibilities

When you use an AMI to deploy and run Burp Suite Enterprise Edition, it is your responsibility to do the following:

- Make sure that your instance is appropriately sized.
- Keep Burp Suite Enterprise Edition up to date with our latest releases.
- Manage your infrastructure and security settings, such as your subnets, security groups, and TLS certificates.

### Supported regions

Our GitHub AMI repository contains a list of supported regions.

- [Published AMIs](https://github.com/PortSwigger/burp-suite-enterprise-edition-ami/blob/main/published_amis.md)
