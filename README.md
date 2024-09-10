# documentation
Creating an Application Load Balancer (ALB) and configuring it with multiple target groups can significantly enhance application scalability and reliability.

Instance Setup: Launch four EC2 instances with private subnets, placing two instances in subnet 1A and the remaining two in subnets 1B and 1C. Ensure proper userdata configuration for each instance.

Target Group Creation: Create three target groups: Home Page: HTTP 80, health check /homepage/, add all instances. Movies: HTTP 80, health check /movies/, add movies server only. Shows: HTTP 80, health check /shows/, add shows server only.

Load Balancer Configuration: Create an ALB (Internet-facing) in the VPC, selecting the public subnets and appropriate security group. Configure two listeners: HTTP (80) and HTTPS (443). Selecting the SSL certificate for domain.

Route 53 Setup: Create a Route 53 record pointing to the ALB.

HTTP to HTTPS Redirection: Configure HTTP to HTTPS redirection: Create a rule to redirect HTTP (80) traffic to HTTPS (443). Ensure proper HTTPS redirection for all incoming traffic.

Path-Based Routing: Implement path-based routing for different content: Create rules to direct traffic based on paths (e.g., /movies/, /shows/). Ensure each rule forwards traffic to the corresponding target group.


Auto Scaling Group AWS:  involves setting up a group of EC2 instances that can automatically scale in or out based on demand. This ensures that you have the right number of instances running to handle the load for your application. An ASG is typically created using a Launch Template which defines the instance settings.

Configure the Auto Scaling Group : Name ,Launch Template, Configure the Network Settings: VPC and Subnet, Target groups, Route53, SNS, alarm,



Launch template
Creating a Launch Template specifying the configuration settings for the EC2 instances, such as the AMI, instance type, key pair, security groups, and other parameters. Launch Templates are more flexible and powerful than Launch Configurations.

EC2 Dashboard Log in to your AWS Management Console. In the AWS Management Console, go to the EC2 Dashboard. Open Launch temple Configure Launch Template Details : name, Amazon Machine Image, Instance Type, Key pair (login), VPC and Subnet, Security Groups.

Using the Launch Template to Launch an Instance or Auto Scaling Group

Launch an EC2 Instance: On the Launch Templates page, select the launch template. Click on "Actions" and then "Launch instance from template". Choose the version of the template (if applicable) and review the instance details. Click "Launch instance" to create a new EC2 instance using this template.

Create an Auto Scaling Group: Use the Launch Template to create an Auto Scaling Group for automatic scaling of instances. Navigate to Auto Scaling Groups on the left-hand menu. Click on "Create Auto Scaling group" selecting the launch template you created.


Network load balancer
In AWS, load balancers play a major role in distributing incoming traffic across multiple targets to ensure high availability, fault tolerance, and scalability of applications.

NLB operates at Layer 4 (Transport Layer) handling TCP and UDP traffic. It provides ultra-high performance and low-latency load balancing, making it suitable for use cases that require extreme performance and scalability.

NLB operates at the transport layer, allowing it to efficiently distribute traffic based on IP protocol data (TCP or UDP).

High Performance: NLB offers high throughput and low latency, making it suitable for latency-sensitive and high-traffic applications.

Cross-Zone Load Balancing: NLB supports cross-zone load balancing, enabling it to distribute traffic evenly across instances in different availability zones within the same region.

Target Groups: NLB forwards incoming traffic to a target group, which can include EC2 instances, IP addresses, or Lambda functions. Practical Implementation:

Setting Up NLB: Create a Network Load Balancer in the AWS Management Console, specifying the listeners, target group, and other configuration details.

Testing Load Balancing: Use tools like curl to send requests to the NLB's DNS name and observe the distribution of traffic across the registered targets.

Monitoring and Optimization: Utilize AWS CloudWatch metrics to monitor the performance of the NLB and optimize its configuration based on traffic patterns and application requirements.

Advantages and Use Cases:

Highly Scalable Applications: NLB is well-suited for applications that require high scalability and handle a large volume of traffic, such as gaming platforms, media streaming services.

UDP-Based Applications: NLB is ideal for UDP-based applications like DNS servers and online gaming platforms that require efficient load balancing of UDP traffic.

AWS CI/CD
AWS CodePipeline In this step, we can create an AWS CodePipeline to automate the continuous integration process of application. AWS CodePipeline will orchestrate the flow of changes from our GitHub repository to the deployment of our application.

Go to the AWS Management Console and navigate to the AWS CodePipeline service. Click on the "Create pipeline" button. Provide a name for your pipeline and click on the "Next" button. For the source stage, select "GitHub" as the source provider. Connect your GitHub account to AWS CodePipeline and select your repository. Choose the branch you want to use for your pipeline. In the build stage, select "AWS CodeBuild" as the build provider. Create a new CodeBuild project by clicking on the "Create project" button. Configure the CodeBuild project with the necessary settings for your Python application, such as the build environment, build commands, and artifacts. Save the CodeBuild project and go back to CodePipeline. Continue configuring the pipeline stages, such as deploying your application using AWS Elastic Beanstalk or any other suitable deployment option. Review the pipeline configuration and click on the "Create pipeline" button to create your AWS CodePipeline.

AWS CodeBuild In this step, we can configure AWS CodeBuild to build an application. CodeBuild will take care of building and packaging our application for deployment.

In the AWS Management Console, navigate to the AWS CodeBuild service. Click on the "Create build project" button. Provide a name for your build project. For the source provider, choose "AWS CodePipeline." Select the pipeline you created in the previous step. Configure the build environment, such as the operating system, runtime, and compute resources required for your Python application. Specify the build commands, such as installing dependencies and running tests. Customize this based on your application's requirements. Set up the artifacts configuration to generate the build output required for deployment. Review the build project settings and click on the "Create build project" button to create your AWS CodeBuild project.

AWS CodeDeploy AWS CodeDeploy automates code deployments to any instance.

Go to your GitHub repository and make a change to an application source code. Commit and push your changes to the branch configured in your AWS CodePipeline. Head over to the AWS CodePipeline console and navigate to your pipeline. we can see the pipeline automatically kick off as soon as it detects the changes in the repository. It will fetch the latest code, trigger the build process with AWS CodeBuild, and deploy the application if we configured the deployment.

