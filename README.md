# Blue-Green Deployment on AWS
This project demonstrates the implementation of a blue-green deployment strategy utilizing AWS services.Blue-green deployments enable zero-downtime releases, ensuring smooth application updates and rollbacks with minimal service disruption. The project seamlessly integrates various AWS services including EC2, AMI, Auto Scaling Groups, Load Balancer, CodeDeploy, CodePipeline, and S3, streamlining the automation of build, deployment, and traffic switching processes.

## setup apache server
create a ec2 instance and allow all trafic in security-group (for testing purpose) and run below command to setup httpd server.
```
sudo su -
yum install httpd -y
cd /var/www/html/
echo "welcome to my website-1" > index.html

systemctl start httpd
systemctl enable httpd
```
now copy the public ipaddress and check in browser url, website is working or not.
## setup code-deploy agent
install code-deploy agent on ec2 server to connect with aws code deploy service for automatic deployment.
### install prerequities
```
yum update
yum install ruby -y
yum install wget -y
```
installing of the code-deploy agent on ec2 instance, its vary on the region. means we need to install the agent as per the region where our ec2 is running.
### Install code-deploy agent
```
cd ~
wget https://<bucket-name>.s3.<region-identifier>.amazonaws.com/latest/install
chmod +x ./install
sudo ./install auto

systemctl start codedeploy-agent
systemctl status codedeploy-agent
```
change the `bucket-name` is the name of the Amazon S3 bucket that contains the [CodeDeploy resource kit](https://docs.aws.amazon.com/codedeploy/latest/userguide/resource-kit.html#resource-kit-bucket-names) files for your region, and `region-identifier` is the region code for your region.

### create AMI of that instance
### create IAM roles
create role for EC2
1. `AdministratorAccess`
2. `AmazonS3FullAccess`
3. `AWSCodeDeployFullAccess`
4. `AWSCodePipeline_FullAccess`
5. `AutoScalingFullAccess`
6. `ElasticLoadBalancingFullAccess`

create role for code-deploy
1. `AWSCodeDeployRole`
2. `AmazonS3FullAccess`
3. `AdministratorAccess`

#### create launch template
#### create autoscaling group
#### create targer group
#### create laodbalancer
#### create code deploy and code deploy group
#### create code pipeline
