# Burp Suite Enterprise Edition AMI

The Burp Suite Enterprise Edition AMI includes both the server and scanning machine components required for an installation capable of scanning. You must provide the configuration for an external database connection in the user data when you launch an EC2 instance. There is [a CloudFormation template](cloudformation) you can use/adapt. It has an example of how the user data must be specified.

See https://portswigger.net/burp/documentation/enterprise/getting-started/ami for more information.