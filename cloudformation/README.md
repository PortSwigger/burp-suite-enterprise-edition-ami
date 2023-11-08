# CloudFormation Template

This CloudFormation template simplifies deployment of an EC2 instance runnning the Burp Suite Enterprise Edition AMI. It only creates the EC2 instance. You will need to create the network infrastructure needed (VPC, subnet, security groups etc.) and provide [an external database](https://portswigger.net/burp/documentation/enterprise/getting-started/setup-ext-db).

## Enterprise Version

The template requires that the AMI ID is supplied.  The choice of AMI ID has the effect of setting the version of Burp Suite Enterprise Edition.  Note that the AMI ID should be available in the same region as the template is being deployed in.

The current list of AMI IDs is available [here](/published_amis.md)

## Template Parameters

Parameters can be supplied as either plain values or as [vals references](https://github.com/helmfile/vals) to various parameter stores. This allows secrets to be passed to the instance without exposing them. For example:

DatabaseUrl: `jdbc:postgresql://burp-suite-enterprise-edition/burp_enterprise`

EnterpriseServerUsername: `ref+awssecrets:///burp-suite-enterprise-edition/database#/enterpriseServerUsername`

EnterpriseServerPassword: `ref+awssecrets:///burp-suite-enterprise-edition/database#/enterpriseServerPassword`