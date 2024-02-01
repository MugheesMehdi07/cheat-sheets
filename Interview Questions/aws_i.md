## AWS Interview Questions & Answers

### Q1: What is AWS EC2 and what are its benefits?
- **A1:** AWS EC2 (Elastic Compute Cloud) is a web service that provides resizable compute capacity in the cloud. It is designed to make web-scale cloud computing easier for developers. Benefits include scalability, control over instances, various instance types for different needs, and integration with most AWS services.

### Q2: Explain what AWS S3 is and its use cases.
- **A2:** AWS S3 (Simple Storage Service) is an object storage service that offers industry-leading scalability, data availability, security, and performance. Use cases include storage for backup and recovery, web applications, archives, data lakes, and big data analytics.

### Q3: What is Amazon RDS and what databases does it support?
- **A3:** Amazon RDS (Relational Database Service) makes it easy to set up, operate, and scale a relational database in the cloud. It provides cost-efficient, resizable capacity and manages common database administration tasks. RDS supports several database instance types including Amazon Aurora, PostgreSQL, MySQL, MariaDB, Oracle Database, and SQL Server.

### Q4: Describe Auto Scaling in AWS.
- **A4:** Auto Scaling in AWS allows you to automatically scale your EC2 capacity up or down according to conditions you define. It helps ensure that you have the correct number of EC2 instances available to handle the load of your application, improving fault tolerance and reducing costs.

### Q5: What is AWS Lambda and how does it work?
- **A5:** AWS Lambda is a serverless compute service that lets you run code without provisioning or managing servers. It executes your code only when needed and scales automatically. You pay only for the compute time you consume - there's no charge when your code is not running.

### Q6: How does Amazon VPC work?
- **A6:** Amazon VPC (Virtual Private Cloud) lets you provision a logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define. You have complete control over your virtual networking environment, including selection of IP address range, creation of subnets, and configuration of route tables and network gateways.

### Q7: What are the different types of instances?
- **A7:** AWS provides a variety of instance types optimized to fit different use cases. Instance types comprise varying combinations of CPU, memory, storage, and networking capacity. Major types include General Purpose, Compute Optimized, Memory Optimized, Storage Optimized, and GPU instances.

### Q8: Explain the concept of a Security Group in AWS.
- **A8:** Security Groups in AWS act as a virtual firewall for your EC2 instances to control inbound and outbound traffic. They enable you to specify the protocols, ports, and source IP ranges that can reach your instances.

### Q9: What is Amazon S3 Glacier?
- **A9:** Amazon S3 Glacier is a secure, durable, and extremely low-cost storage service for data archiving and long-term backup. It is designed to deliver 99.999999999% durability and provides comprehensive security and compliance capabilities.

### Q10: How does AWS CloudFormation work?
- **A10:** AWS CloudFormation provides a way to create and manage a collection of related AWS resources, provisioning and updating them in an orderly and predictable fashion. You create a template that describes all the AWS resources you want (like EC2 instances or RDS DB instances), and AWS CloudFormation takes care of provisioning and configuring those resources for you.

## Advanced AWS Interview Questions & Answers

### Q11: What is AWS IAM and what are its main components?
- **A11:** AWS IAM (Identity and Access Management) is a web service that helps you securely control access to AWS resources. The main components are Users, Groups, Roles, and Policies. IAM enables you to manage users and their level of access to the AWS Console, create roles for different services, and manage permissions to dictate what actions are allowed on resources.

### Q12: Explain Elastic Load Balancing and its types in AWS.
- **A12:** Elastic Load Balancing automatically distributes incoming application traffic across multiple targets, such as EC2 instances. Types include Application Load Balancer (ALB) for HTTP/HTTPS traffic, Network Load Balancer (NLB) for TCP traffic, and Classic Load Balancer, which is a previous-generation balancer for EC2 instances.

### Q13: Describe the concept of Amazon EBS.
- **A13:** Amazon EBS (Elastic Block Store) provides persistent block storage volumes for use with EC2 instances. EBS volumes offer the consistent and low-latency performance needed to run your workloads. They are highly available and reliable storage volumes that can be attached to any running instance in the same Availability Zone.

### Q14: What is AWS CloudWatch and what are its uses?
- **A14:** AWS CloudWatch is a monitoring service for AWS cloud resources and the applications you run on AWS. It can be used to collect and track metrics, collect and monitor log files, set alarms, and automatically react to changes in your AWS resources.

### Q15: How does Amazon DynamoDB work?
- **A15:** Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability. It lets you offload the administrative burdens of operating and scaling a distributed database so that you don't have to worry about hardware provisioning, setup and configuration, replication, software patching, or cluster scaling.

### Q16: Explain the concept of a Snapshot in AWS.
- **A16:** In AWS, a snapshot is a backup of your volumes that are stored in Amazon S3. Snapshots are incremental backups, which means that only the blocks on the device that have changed after your last snapshot are saved. They can be used for backups, to create new EC2 volumes, or to move volumes across Availability Zones.

### Q17: What is AWS Direct Connect?
- **A17:** AWS Direct Connect is a cloud service solution that makes it easy to establish a dedicated network connection from your premises to AWS. This can reduce network costs, increase bandwidth throughput, and provide a more consistent network experience than internet-based connections.

### Q18: Describe the AWS Shared Responsibility Model.
- **A18:** The AWS Shared Responsibility Model is a concept that dictates which security controls are AWS’s responsibility and which are the user’s. AWS is responsible for the security "of" the cloud (infrastructure), while the user is responsible for security "in" the cloud (data, applications, and traffic).

### Q19: What is an AMI in AWS?
- **A19:** An AMI (Amazon Machine Image) provides the information required to launch an EC2 instance. You can launch instances from a public AMI, your own custom AMI, or an AMI that AWS provides. AMIs include the operating system, application server, applications, and any additional configurations.

### Q20: How do you secure data in transit in AWS?
- **A20:** To secure data in transit in AWS, you should use SSL/TLS for data transmission. AWS services like API Gateway, ELB, and CloudFront support SSL/TLS to encrypt data sent to and from your instances. Additionally, using client-side encryption or establishing a VPN (Virtual Private Network) are other methods to ensure data security during transit.

