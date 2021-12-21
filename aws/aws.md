# Amazon Web Services (AWS)

AWS stands for Amazon Web Service; it is a collection of remote computing services also known as a cloud computing
platform. This new realm of cloud computing is also known as IaaS or Infrastructure as a Service.

## Key components of AWS:

1. **Route 53:** A DNS web service
2. **Simple E-mail Service**: It allows sending e-mail using RESTFUL API call or via regular SMTP
3. **Identity and Access Management:** It provides enhanced security and identity management for your AWS account
4. **Simple Storage Device or (S3)**: It is a storage device and the most widely used AWS service
5. **Elastic Compute Cloud (EC2)**: It provides on-demand computing resources for hosting applications. It is handy in
   case of unpredictable workloads
6. **Elastic Block Store (EBS)**: It offers persistent storage volumes that attach to EC2 to allow you to persist data
   past the lifespan of a single Amazon EC2 instance
7. **CloudWatch**: To monitor AWS resources, It allows administrators to view and collect key Also, one can set a
   notification alarm in case of trouble.

   
# Elastic Cloud Compute (EC2)

Elastic Cloud Compute (EC2) is one of the first web service interfaces when AWS was released, allowing users to create and configure compute machines within the cloud. EC2 allows users to create VM (virtual machine) on the Amazon cloud for running applications that can be accessed via the Internet. The software can be configured on cloud servers based on your specifications. You select the operating system (i.e., Microsoft Windows or Linux) best suited to your requirements or applications, and you get the operating system pre-installed. EC2 provides the actual host server and operating system.

If you want any additional software, you must manually install it on top of the OS as a developer. So, if you want JDK (Java Development Kit), you can install Java. You can also install Tomcat, a database, and so on. It’s almost like getting a brand-new laptop that only has the operating system, and you need to install your tools on top of it.

# Relational Database Service (RDS)

AWS Relational Database Service (RDS) is your relational database in the cloud. This allows you to quickly deploy a relational database in the cloud. It has support for a wide range of databases to choose from, including MySQL, Oracle, Microsoft SQL Server, and so on. You can manage these tools using your normal admin tools. If you are using MySQL, you can use MySQL Workbench. If you are using the Oracle Database, you can use Oracle SQL Developer, and the list goes on. AWS also has support for NoSQL databases such as MongoDB. So, all major database feature’s that you need can be found in AWS with the support of the relational Database Service.


# Route 53

Amazon Route 53 is a Domain Name System (DNS), which allows you to route your custom domain names to your actual application on AWS. So, you configure Route 53 to send requests from the browser to your AWS application. The AWS DNS sets up your custom domain name.

# CloudWatch

Amazon CloudWatch is a key service that helps you plan, monitor, and fine-tune your AWS infrastructure and applications. It lets you collect, search, and visualize data from your applications and AWS resources in the form of logs, metrics, and events. 

Common CloudWatch use cases include the following:

**Infrastructure monitoring and troubleshooting** 
Visualize performance metrics to discover trends over time and spot outliers that might indicate a problem. Correlate metrics and logs across your application and infrastructure stacks to understand the root cause of failures and performance issues.

**Resource optimization** 
Save money and help with resource planning by identifying overused or underused resources. Ensure performance and availability by using AWS Auto Scaling to automatically provision new EC2 instances to meet demand.

**Application monitoring** 
Create CloudWatch alarms to alert you and take corrective action when a resource’s utilization, performance, or health falls outside of a threshold that you define.

**Log analytics** 
Search, visualize, and correlate logs from multiple sources to help with troubleshooting and identify areas for improvement.


## CloudWatch Metrics

CloudWatch Metrics is a feature that collects numeric performance metrics from both AWS and non-AWS resources such as on-premises servers. A metric is a variable that contains a timeordered set of data points. Each data point contains a timestamp, a value, and optionally a unit of measure. For example, a data point for the CPU Utilization metric for an EC2 instance may contain a timestamp of December 25, 2018 13:37, a value of 75, and Percent as the unit of measure. All AWS resources automatically send their metrics to CloudWatch. These metrics include things such as EC2 instance CPU utilization, S3 bucket sizes, and DynamoDB consumed read and write capacity units. CloudWatch stores metrics for up to 15 months. You can graph metrics to view trends and how they change over time.

**Figure:** Using CloudWatch to graph the CPU Utilization metric for an EC2 Instance

<img src="images/CloudWatch-Metrics.png" width="900"/>

## CloudWatch Alarms

A CloudWatch alarm watches over the value of a single metric. If the metric crosses a threshold that you specify (and stays there), the alarm will take an action. For example, you might configure an alarm to take an action when the average CPU utilization for an instance exceeds 80% for five minutes. The action can be one of the following:

**Notification using Simple Notification Service**
The Simple Notification Service (SNS)allows applications, users, and devices to send and receive notifications from AWS. SNS uses a publisher-subscriber model, wherein a publisher such as an AWS service generates a notification and a subscriber such as an end user receives it. The communication channel that SNS uses to map publishers and subscribers is called a topic. 
SNS can send notifications to subscribers via a variety of protocols including the following:

■■ HTTP(S)
■■ Simple Queue Service (SQS)
■■ Lambda
■■ Mobile push notification
■■ Email
■■ Email-JSON
■■ Short Message Service (SMS) text messages

**Auto Scaling action** 
By specifying an EC2 Auto Scaling action, the EC2 Auto Scaling service can add or remove EC2 instances in response to changing demand. For example, if a metric indicates that instances are overburdened, you can have EC2 Auto Scaling respond by adding more instances.

**EC2 action**
If you’re monitoring a specific instance that’s having a problem, you can use an EC2 action to stop, terminate, or recover the instance. Recovering an instance migrates the instance to a new EC2 host, something you may need to do if there’s a physical hardware problem on the hardware hosting the instance.





## CloudWatch Dashboards


## CloudWatch Logs








# Amazon DynamoDB


# Amazon Simple Storage Service (Amazon S3)

# Amazon Virtual Private Cloud (Amazon VPC)

# AWS Elastic Beanstalk


# Elastic Load Balancing

# Amazon Kinesis

# AWS Lambda

# Amazon Simple Notification Service

# Amazon Simple Queue Service














