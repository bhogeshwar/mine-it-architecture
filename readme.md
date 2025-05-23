# Mine-IT Predictive Maintenance Data Platform

## Project Overview

This repository contains the design and architecture for Mine-IT's Predictive Maintenance Data Platform built on AWS. The platform is designed to analyze data from IoT devices in mining equipment, inventory management systems, and field services systems to predict potential equipment failures before they occur, enabling proactive maintenance and minimizing operational disruptions.


## Business Challenge

Mine-IT, a company in the mining industry, needed a reliable data platform to support their unique Predictive Maintenance machine learning model. The platform needed to:

1. Ingest and process metrics from IoT devices deployed in mines
2. Integrate with inventory management systems and field services databases
3. Deploy the ML model in a scalable and reliable way
4. Distribute alerts to various subscribers
5. Generate daily reports on equipment status

The solution leverages AWS cloud services to achieve scalability, high availability, and operational efficiency.

## Architecture Components

### Data Ingestion Layer

- **IoT Device Data**: AWS IoT Core, IoT Rules, Kinesis Data Streams, and Kinesis Data Analytics process and aggregate IoT metrics in 10-minute windows
- **Inventory Management**: EventBridge schedules hourly data pulls from the inventory system's JSON API
- **Field Services**: AWS DMS with CDC continuously replicates data from the on-premises RDBMS

### Data Storage Layer

- **Amazon S3**: Central data lake for raw data storage with lifecycle policies for cost-effective retention
- **Amazon DynamoDB**: Low-latency access for processed IoT metrics
- **Amazon RDS**: Maintains relational structure for field services data

### Processing Layer

- **AWS Glue**: Serverless ETL capabilities with centralized Data Catalog
- **AWS Lambda**: Event-driven transformations and data enrichment
- **Amazon Athena**: SQL-based analytics on data stored in S3

### ML Model Layer

- **Amazon SageMaker**: Hosts the Predictive Maintenance ML model with automatic scaling
- **SageMaker Model Registry**: Manages model versions and enables controlled deployment
- **Amazon ECR**: Stores container images for consistent model deployment

### Alert and Notification Layer

- **Amazon EventBridge**: Processes events from the ML model and triggers alert workflows
- **Amazon SNS**: Distributes notifications to various subscribers
- **Amazon SQS**: Decouples alert producers from consumers for reliable delivery

### Reporting Layer

- **Amazon QuickSight**: Creates interactive dashboards and visualizations
- **Amazon Athena**: Provides SQL-based querying for generating daily reports

## Key Features

- **Real-time Data Processing**: Processes IoT data streams with 10-minute aggregation windows
- **Hourly Data Integration**: Ensures fresh data from inventory and field services systems
- **Scalable ML Deployment**: Hosts the Predictive Maintenance model with automatic scaling
- **Flexible Alert Distribution**: Easy addition of different subscribers to consume alerts
- **Automated Reporting**: Daily reports of hourly average alerts by location, vendor, and device model

## Key Concerns Addressed

### Data Freshness and Integrity

- Real-time IoT data processing with 10-minute aggregation windows
- Hourly updates from inventory and field services systems
- Change Data Capture (CDC) for efficient data replication
- Data validation at ingestion points to ensure quality

### Data Retention

- Tiered storage strategy with hot, warm, and cold tiers
- S3 Lifecycle policies for automated data management
- Raw data: 90 days in S3 Standard, 7 years in S3 Glacier
- Processed data: 365 days in S3 Standard, 7 years in S3 Glacier

### ML Model Lifecycle

- SageMaker for model training, hosting, and scaling
- Model Registry for version control and governance
- Container-based deployment with ECR for consistency
- CI/CD pipeline for model updates and deployment

### Security and Access Control

- Encryption at rest and in transit for all data
- IAM roles with least privilege principle
- VPC isolation for processing components
- Fine-grained access control with S3 Access Points

### Reliability/Availability

- Multi-AZ deployment for high availability
- Serverless architecture where possible
- Automatic scaling based on demand
- Fault-tolerant data processing with retry mechanisms

### Operational Best Practices

- Infrastructure as Code using AWS CDK
- Comprehensive monitoring with CloudWatch
- Automated alerting for operational issues
- CI/CD pipeline for infrastructure updates

## Implementation Details

This repository contains the design documentation and architecture diagrams for the Mine-IT Data Platform. The implementation would involve:

1. Setting up the AWS infrastructure using Infrastructure as Code (AWS CDK or CloudFormation)
2. Configuring data ingestion pipelines for IoT, inventory, and field services data
3. Implementing data processing and storage components
4. Deploying the ML model using SageMaker
5. Setting up alert distribution and reporting mechanisms

## Getting Started

To explore this architecture:

1. Review the architecture diagrams in the `assets/images` directory
2. Examine the detailed component descriptions in the website
3. For implementation, follow AWS best practices for each service

## Future Enhancements

Potential enhancements to the platform could include:

- Integration with additional data sources
- Advanced analytics capabilities using Amazon EMR or SageMaker
- Enhanced visualization and reporting using QuickSight
- Edge computing capabilities using AWS Greengrass
- Multi-region deployment for global operations






