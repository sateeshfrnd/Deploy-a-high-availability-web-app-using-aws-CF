# Deploy-a-high-availability-web-app-using-aws-CF
Deploy a high-availability web app using AWS CloudFormation

In this project, automate the process to setup high availabile infrastructure for deploying application using AWS CloudFormation.

## Requirements
### Server specs

- Create a Launch Configuration for your application servers in order to deploy four servers, two located in each of your private subnets. The launch configuration will be used by an auto-scaling group.

- 2 vCPUs and at least 4GB of RAM. The Operating System to be used is Ubuntu 18. So, choose an Instance size and Machine Image (AMI) that best fits this spec.

- Allocate at least 10GB of disk space so that you don't run into issues. 

### Security Groups and Roles

- Since will be downloading the application archive from an **S3 Bucket**, so need to create an **IAM Role** that allows your instances to use the S3 Service.

- Application communicates on the default *HTTP Port: 80*, so your servers will need this inbound port open since you will use it with the **Load Balancer** and the **Load Balancer Health Check**. As for outbound, the servers will need unrestricted internet access to be able to download and update their software.

- The load balancer should allow all public traffic *(0.0.0.0/0)* on *port 80* inbound, which is the default *HTTP port*. Outbound, it will only be using *port 80* to reach the internal servers.

- The application needs to be deployed into private subnets with a **Load Balancer** located in a public subnet.

- One of the output exports of the **CloudFormation** script should be the public URL of the **LoadBalancer**. if you add http:// in front of the load balancer **DNS Name** in the output, for convenience.


## Files 
The files included are: 
| File      | Description |
| ----------- | ----------- |
| scripts/setup_high_available_infra.yml| CloudFormation YAML script|
| scripts/setup_high_available_infra.json| CloudFormation script parameters|
| scripts/create.sh            | Cloudformation create stack script       |
| scripts/update.sh            | Cloudformation update stack script       |
| scripts/destroy.sh           | Cloudformation delete stack script       |
| index.html      | Index document for the website.      |
| /images            | Screenshots of the deployment        |

## Infrastructure Diagram
![](https://github.com/sateeshfrnd/Deploy-a-high-availability-web-app-using-aws-CF/blob/main/images/deploy-high-availability-web-app.jpeg)

## Dependencies
- AWS Account
- Any Editor (VS Code, notepad++)
- [lucidchart](www.lucidchart.com) to draw architecture diagrams for AWS infra.
- Configure AWS CLI to execute Cloudformation script.

## How to run 
```
./create.sh deploy-ha-infra setup_high_available_infra.yml setup_high_available_infra.json
```

