# CloudFormation Template

This CloudFormation template simplifies deployment of an EC2 instance runnning the Burp Suite Enterprise Edition AMI. It only creates the EC2 instance. You will need to create the network infrastructure needed (VPC, subnet, security groups etc.) and provide [an external database](https://portswigger.net/burp/documentation/enterprise/getting-started/setup-ext-db).

## Enterprise Version

By default, the template will launch the latest release of Burp Suite Enterprise Edition. If you want to "pin" the version to a specific release, replace the "latest" tag with the required version number e.g. `/portswigger/burp-suite-enterprise-edition/2023.9.1/enterprise-ami`.

## Template Parameters

Parameters can be supplied as either plain values or as [vals references](https://github.com/helmfile/vals) to various parameter stores. This allows secrets to be passed to the instance without exposing them. For example:

DatabaseUrl: `jdbc:postgresql://burp-suite-enterprise-edition/burp_enterprise`

EnterpriseServerUsername: `ref+awssecrets:///burp-suite-enterprise-edition/database#/enterpriseServerUsername`

EnterpriseServerPassword: `ref+awssecrets:///burp-suite-enterprise-edition/database#/enterpriseServerPassword`