# Using an AMI to launch an instance

Burp Suite DAST is preinstalled in the Burp Suite DAST AMI. To see a full list of AMI IDs and the regions we support, see [Published AMIs](https://github.com/PortSwigger/burp-suite-enterprise-edition-ami/blob/main/published_amis.md).

We recommend using CloudFormation to deploy the Burp Suite DAST AMI:

## Create a stack

1. Download the [CloudFormation Template yaml file](https://github.com/PortSwigger/burp-suite-enterprise-edition-ami/tree/main/cloudformation).
2. Log in to your AWS account and go to the CloudFormation console.
3. Create a stack with new resources.
4. Upload the CloudFormation template.
5. Enter the **Stack name** and **ImageID** of the Burp Suite DAST AMI for your region.

## Configure your instance

1. Set an **InstanceType** that meets the [system requirements](https://github.com/darren-portswigger/wayland-smithy/blob/main/README.md#system-requirements-for-ami-instances). If the **InstanceType** you require isn't listed, edit the **AllowedValues** for the **InstanceType** in the **CloudFormation** template.
2. In the **KeyName** field, enter the name of the **KeyPair** that will be used to access the instance.
3. If you are storing credentials or settings in SSM or Secrets Manager, enter the name of your IAM instance profile in the **IaminstanceProfile** field.
4. Under **Network Configuration**, enter the **SubnetID** and **SecurityGroups** values for the instance.
5. Enter the values for the **Database Configuration**. For more information, see [Setting up your external database (Kubernetes)](https://portswigger.net/burp/documentation/enterprise/setup/self-hosted/kubernetes/setup-external-database). We recommend you use [Vals](https://github.com/helmfile/vals) to avoid storing passwords in plain text.
6. For the **Web Server Configuration**, select whether the webserver is using TLS (HTTPS). If you set **UseHttps** to **true**, enter the **HttpsCertificate** and **HttpsPassphrase**.
8. We recommend that you leave the **Resource Allocation Configuration** settings blank, to use the default values. If you need to increase the resource values, see [Kubernetes container system requirements](https://portswigger.net/burp/documentation/enterprise/setup/self-hosted/kubernetes/k8-system-requirements#container-system-requirements).
9. If you are storing the images used by the AMI in a private container registry, enter the **ContainerRegistry** value.
10. Click **Next**.
11. Enter the **Configure stack options** values as required, and click **Next**.

## Create your instance

1. In the **Review and create** window, check the configuration and then click **Submit**.
2. Wait for the stack to be created.
3. To navigate to your newly created EC2 instance, go to the **Resources** tab of your stack and click the link in the **Physical ID** column.
4. In the **Instances** window, select the instance and copy and paste the IP address or DNS name into a browser. The Burp Suite DAST console will open.

If this is the first time that you have used the database with Burp Suite DAST, you will be prompted to create the administrator user credentials. For more information, see [Creating the admin user](https://portswigger.net/burp/documentation/enterprise/setup/self-hosted/kubernetes/create-admin).
