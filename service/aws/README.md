# AWS
The AWS section can contain a single cloudformation template 'service.template', and a tokenisable Nginx configuration file, 'ec2-extension.conf', in order to provision the service.

This skeleton cloudformation template provided will provision a single EC2-instance using a set of AWS-specific parameters provided to Jenkins as environment variables, upon spinning your instance of ADOP. The parameters are as follows:

 * The VPC where you wish to spin up your instance (this will be set to the VPC where your ADOP instance is provisioned)
 * The subnet where you wish you to spin up your instance which can be either public or private (if a subnet is not set, the subnet where your ADOP instance is provisioned will be used)
 * An AWS keypair in order to gain SSH access to the box (if one is not provided, this will be set to the keypair used to access your ADOP instance)
 * An EC2 instance type (set to t2.large by default)

Additionally, the cloudformation template installs Apache HTTPD server on the host in order to act as a front-end validator when accessing your host. The HTTPD service is made to listen on port 8080.

You will need to add your AWS Access Key and Secret Access Key as global credentials in Jenkins so that it can be picked by the platform extension loader. You will then have to update the Load\_Platform\_Extension job to ensure the Username and Password binding uses your specified AWS credentials.

The Nginx config file is tokenised with the outputs of the cloudformation template and uploaded to the Nginx volume. We use the xip.io DNS resolver as a proxy configuration.

**Points to note:**

 * The instance is provided with a public IP in order to allow it outbound internet connectivity. In the case where you are spinning up your instance in a subnet which is connected to a NAT host, you may want to set the AssociatePublicIpAddress option to false (if it is not set to false, the traffic will be routed through the NAT anyway).
 * By default, ports 80, 22, 443 and 8080 have been opened up to VPC where you spin up your instance. The VPC CIDR block is provided to the cloudformation template as an input parameter and the security group rules use this parameter. In the case where you are accessing your instance through Nginx proxy, you will have to check the security groups for the host where Nginx resides.
 
It is recommended that you clone this repository and make additions and changes to the cloudformation template and Nginx config file as appropriate. *Do not remove any of the default parameters or outputs from the template as these are all used by the Load\_Platform\_Extension Jenkins job. Care needs to be taken when making significant changes to the template in order to ensure it is still compatible with the extension loader.*

# Chef
This platform extension spins up a blank Chef server with Chef 12 installed making use of the AWS-type platform extension. The EC2 instance makes use of an existing AMI which comes with all the configuration pre-baked.

The chef server is proxied over port 443 from Nginx and is accessible over HTTPS. The default access credentials for the chef server web UI (once you have loaded the platform extension) are as follows:

 * username: admin
 * password: admin@1
