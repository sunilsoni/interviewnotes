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

- HTTP(S)
- Simple Queue Service (SQS)
- Lambda
- Mobile push notification
- Email
- Email-JSON
- Short Message Service (SMS) text messages

**Auto Scaling action** 
By specifying an EC2 Auto Scaling action, the EC2 Auto Scaling service can add or remove EC2 instances in response to changing demand. For example, if a metric indicates that instances are overburdened, you can have EC2 Auto Scaling respond by adding more instances.

**EC2 action**
If you’re monitoring a specific instance that’s having a problem, you can use an EC2 action to stop, terminate, or recover the instance. Recovering an instance migrates the instance to a new EC2 host, something you may need to do if there’s a physical hardware problem on the hardware hosting the instance.


## CloudWatch Dashboards

CloudWatch dashboards are your one-stop shop for keeping an eye on all of your important metrics. You can create multiple dashboards and add to them metric graphs, the latest values for a metric, and CloudWatch alarms. You can save your dashboards for future use and share them with others. Dashboards can also visualize metrics from multiple AWS Regions, so you can keep an eye on the global health of your infrastructure. 

Sample CloudWatch dashboard.

<img src="images/CloudWatch dashboard.png" width="900"/>

## CloudWatch Logs
CloudWatch Logs collects and stores log files from AWS and non-AWS sources and makes it easy to view, search, and extract custom metrics from them.

**Log Events, Streams, and Groups**

You configure your applications and AWS services to send log events to CloudWatch Logs.
A log event is analogous to a line in a log file and always contains a timestamp and an
event message. Many AWS services produce their own logs called vended logs that you can
stream to CloudWatch Logs. Such logs include Route 53 DNS query logs, VPC flow logs,
and CloudTrail logs. CloudWatch Logs can also receive custom logs from your applications,
such as web server access logs.

CloudWatch Logs organizes log events by log streams by storing log events from the
same source in a single log stream. For example, web server access logs from a specific
EC2 instance would be stored in one log stream, while Route 53 DNS query logs would be
stored in a separate log stream.

CloudWatch further organizes log streams into log groups. To organize related log
streams, you can place them into the same log group. For instance, if you have several log
streams that are collecting web server log events from multiple web servers, you can group
all of those log streams into a single log group.
   
CloudWatch Logs stores log events indefinitely by default, but you can configure a log
group’s retention settings to delete events automatically. Retention settings range from
1 day to 10 years. You can also archive your logs by exporting them to an S3 bucket.

## Metric Filters
A metric fi lter extracts data from log events in a log group and stores that data in a custom
CloudWatch metric. For example, suppose a log event from a database server contains the
time in milliseconds it takes to run a query. You may extract that value and store it as a
CloudWatch metric so you can graph it and create an alarm to send a notifi cation when it
exceeds a certain threshold.

You can also use metric fi lters to track the number of times a particular string occurs.
This is useful for counting the number of times a particular event occurs in a log, such as
an error code. For example, you might want to track how many times a 403 Forbidden
error appears in a web server log. You can confi gure a metric fi lter to count the number of
times the error occurs in a given timeframe—fi ve minutes, for example—and record that
value in a CloudWatch custom metric.

## CloudWatch Events
The CloudWatch Events feature lets you continuously monitor for specifi c events that represent
a change in your AWS resources—particularly write-only API operations—and take an
action when they occur. 

For example, an EC2 instance going from the running state to the stopped state would be an event. 
An IAM user logging into the AWS Management Console would also be an event. CloudWatch Events can then automatically and immediately take actions in response to those events.

You start by creating a rule to defi ne the events to monitor, as well as the actions you
want to take in response to those events. You defi ne the action to take by selecting a target,
which is an AWS resource. 

Some targets you can choose from include the following:

■✓ Lambda functions

■✓ EC2 instances

■✓ SQS queues

■✓ SNS topics

■✓ ECS tasks

CloudWatch responds to events as they occur, in real time. Unlike CloudWatch alarms,
which take action when a metric crosses and remains crossing a numeric threshold,
CloudWatch events trigger immediately. For example, you can create a CloudWatch event
to send an SNS notifi cation whenever an EC2 instance terminates. Or you could trigger a
Lambda function to process an image fi le as soon as it hits an S3 bucket.

Alternatively, you can create a schedule to automatically perform actions at regular
intervals. For example, to save money you might create a schedule to shut down development
instances every day at 7 p.m., after the developers have ideally stopped working!

# CloudTrail

CloudTrail keeps detailed event logs of every action that occurs against your AWS resources. Each event that CloudTrail logs includes the following parameters:
- The service. Specifically, this is the address of the service’s global endpoint, such as iam.amazonaws.com for IAM.
- The name of the API action performed, such as RunInstances, CreateUser, or PutObject.
- The region the resource is located in. For global services, this is always us-east-1.
- Response elements. In the case of an API operation that changes or creates a resource, this contains information about the results of the action. For example, the response elements for a RunInstances action to launch an EC2 instance would yield information such as the instance ID and private IP address.
- The principal that made the request. This may include the type of principal (IAM user or role), its Amazon resource name (ARN), and the name.
- The date and time of the request, given in coordinated universal time (UTC).
- The IP address of the requester.

## API and Non-API Events

The events CloudTrail logs consist of two different actions: API and non-API actions. API actions include things such as launching an instance, creating an S3 bucket, creating a new IAM user, or taking an EBS snapshot. Note that the term API action has nothing to do with how the action was performed. For example, terminating an EC2 instance is an API event whether you do it via the AWS Management Console, the AWS command-line interface, or an AWS software development kit. Non-API actions include everything else, such as logging into the management console.


## Management and Data Events
CloudTrail also classifies events along two other dimensions: management events and data events.

Management events—also known as control plane operations—are operations that a principal (such as a user or service) attempts to execute against an AWS resource.
Management events include write-only events—API operations that modify or might modify resources, and read-only events that read resource information but don’t make any changes. For example, the RunInstances API operation can create an EC2 instance, so it would be a write-only event. On the other hand, the DescribeInstances API operation returns a list of EC2 instances but doesn’t make any changes, so it’s a read-only operation. Data events consist of S3 object-level activity and Lambda function executions, both of which tend to be high volume. As such, CloudTrail treats data events as separate from management events. And when it comes to S3 object-level operations, CloudTrail draws a distinction between read-only events like GetObject and write-only events such as PutObject and DeleteObject .



## Event History
When you open an AWS account, CloudTrail begins logging all of your management events automatically. It stores 90 days of management events in the event history, which you can view, search, and download at any time. The event history log doesn’t record data events. For each region, CloudTrail maintains a separate event history log containing the events that occurred in that region. But events generated by global services including IAM and Route 53 are included in the event history for every region.


## Trails
If you want to customize the types of events CloudTrail logs—such as specifi c management or data events—or if you need to store more than 90 days of event history, you need to create a trail. A trail is a confi guration that directs CloudTrail to record specifi ed events in log fi les and deliver them to an S3 bucket. A trail can log events from either a single region or all regions. You can choose to log management events, data events, or both. You can also choose whether to log read-only or write-only events, or both. CloudTrail doesn’t provide a way to search trail logs, which are written in JavaScript Object Notation (JSON) format. But you can download the log fi les directly from S3. You can also confi gure CloudTrail to send a trail log to CloudWatch Logs, making them available for storage, searching, and metric fi ltering.


## Log File Integrity Validation
Log fi le integrity validation is an optional feature that provides assurance that no
CloudTrail log fi les are surreptitiously modifi ed or deleted. Here’s how it works: every time
CloudTrail writes a log fi le to the trail’s S3 bucket, it calculates and stores a cryptographic hash of the fi le, which is a unique value based on the contents of the log fi le itself. If anyone modifies the file, even by one bit, the hash of the modified file will be completely different than the original hash. This can tell you whether anyone has tampered with the log file, but it can’t tell you exactly how it’s been modified.

Log files can be encrypted using server-side encryption with Amazon S3-managed
encryption keys (SSE-S3) or server-side encryption with AWS KMS-managed keys
(SSE-KMS).

# Cost Explorer

AWS Cost Explorer is a feature of AWS Billing and Cost Management that offers configurable reports and graphs to help you understand how each of your AWS services impacts your monthly bill.

AWS Cost Explorer offers the following three categories of reports:
- Cost and usage reports
- Reservation reports
- Reserved instance recommendations

## Cost and Usage
You can generate cost and usage reports to give you a graphical view of your daily and monthly costs and usage over time. Cost Explorer can also show you the forecast for the current month, 3 months out, and 12 months out, helping you plan ahead. Figure 6.18 shows the monthly costs for the last 12 months and a forecast for the current month.

Figure: Cost and usage report showing monthly costs

<img src="images/Cost and usage.png" width="900"/>

You can go back as far as one year and filter or group by several parameters including but not limited to the following:

- Service
- Availability Zone
- Region
- Instance type
- Usage type
- Tag
- API operation
- Charge type
- Platform

This can help you quickly see which services are incurring the greatest costs and how those services costs are trending over time. Figure 6.19 shows the monthly costs for the last 12 months grouped by service.

Figure :  Cost and usage report showing monthly costs grouped by service

<img src="images/Cost and usage report showing monthly costs grouped by service.png" width="900"/>

In addition to letting you create your own custom reports, Cost Explorer offers the following five default cost and usage reports:

**Monthly costs by service** 
Displays your top five most expensive services over the past six months. The top five services are graphed individually, while other services are aggregated and graphed as a single bar.

**Monthly costs by linked account** 
Shows your costs for your top five linked accounts over the past six months. The top five linked accounts are grouped individually, and the rest are aggregated and graphed as one bar.

**Monthly EC2 running hours costs and usage**
Displays two monthly graphs showing the costs and running hours for your EC2 instances.

**Daily costs** 
Shows your monthly spend for the last six months and a forecast for the current month.

**AWS marketplace**:
The Core Compute Services, the AWS Marketplace allows vendors to make their products and services available to you via AWS. License, subscription, and usage costs are bundled together and billed through AWS. This report shows you how much you’ve spent on AWS Marketplace solutions.


## Reservation reports


## Reserved instance recommendations




# Amazon DynamoDB


# Amazon Simple Storage Service (Amazon S3)

# Amazon Virtual Private Cloud (Amazon VPC)

# AWS Elastic Beanstalk


# Elastic Load Balancing

# Amazon Kinesis

# AWS Lambda

# Amazon Simple Notification Service

# Amazon Simple Queue Service














