# AWSLambda_EC2Availability [![Build Status](https://travis-ci.org/chriselsen/AWSLambda_EC2Availability.svg?branch=master)](https://travis-ci.org/chriselsen/AWSLambda_EC2Availability)
AWS Lambda Function to calculate availability of EC2 instances based on [System Status Checks (StatusCheckFailed_System)](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/monitoring-system-instance-status-check.html#types-of-instance-status-checks) metrics.

![Screenshot](https://github.com/chriselsen/AWSLambda_EC2Availability/raw/master/EC2Availability.PNG)

**Pre-Requisites:**
* Role for Lambda that allows put-metric access to Amazon CloudWatch and DescribeInstances for EC2

**How-To:**
* Create AWS Lambda function
  * Name: EC2Availability
  * Description: Calculate availability of EC2 instances
  * Runtime: Node.js 6.10
  * Handler: index.handler
  * Timeout : 30 sec
  * Source: In file EC2Availability.nodejs
* Configure AWS CloudWatch event rule as trigger
  * Schedule: Fixed rate of 1 minute
  * Function: EC2Availability
  * Input: Constant (JSON text)
  * JSON: { "instanceType": "t2.micro", "daysAggregate": "30", "region": "us-west-2" }
 
**Defaul Settings for JSON:**
* instanceType: All
* daysAggregate: 30  <-- Calculate availability over last 30 days
* region: us-west-2  <-- Oregon
 
