# Schedule_EC2HealthChecks--Lambda

This project automates the monitoring and management of an EC2 instance using an AWS Lambda function. The Lambda function checks the availability of the EC2 instance every 15 minutes and performs actions to ensure it remains operational without manual intervention.

## Table of Contents

- [Objective](#objective)
- [Architecture](#architecture)
- [Setup Instructions](#setup-instructions)
- [Lambda Function](#lambda-function)
- [Error Handling](#error-handling)
- [Testing Phase](#testing-phase)

## Objective

The main goals of this automation are to:
- Monitor the EC2 instance's availability.
- Restart the instance if it becomes unreachable.
- Automatically pull the latest code from GitHub for the Discord bot receiver.
- Send alerts via SQS and SMS in case of issues.

## Architecture

- **AWS Lambda**: A serverless function that runs every 15 minutes.
- **EventBridge**: Triggers the Lambda function on a schedule.
- **SQS**: Sends notifications if the instance encounters issues.
- **EC2**: The instance being monitored.

## Setup Instructions

### Prerequisites

- AWS Account
- AWS CLI installed and configured
- Node.js installed
- AWS SAM CLI installed

### Steps

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/SneakerManager/Schedule_EC2HealthChecks--Lambda.git
   cd Schedule_EC2HealthChecks--Lambda
   ```

2. **Configure Environment Variables**:
   Update the `template.yaml` file with your EC2 instance ID and SQS queue URL.

3. **Create the SQS Queue**:
   Use the AWS Management Console or AWS CLI to create an SQS queue for sending alerts.

4. **Deploy the SAM Application**:
   Build and deploy your SAM application:
   ```bash
   npm run build
   sam build
   sam deploy --guided
   ```

   Follow the prompts to set up the stack name, region, and other parameters.

5. **Set Up IAM Roles**:
   Ensure that the Lambda function has the necessary permissions to interact with EC2 and SQS.

6. **Testing**:
   - Use the cheapest EC2 instance available during testing.
   - Make sure to associate an Elastic IP with the instance for consistent communication.

## Lambda Function

The Lambda function is defined in `src/index.ts`. It performs the following tasks:

- Checks the status of the EC2 instance.
- Restarts the instance if it's not running.
- Sends alerts to SQS if there are issues.

## Error Handling

The Lambda function is designed to handle errors gracefully. If the instance is down or if an error occurs, an alert is sent to the SQS queue. You can integrate Amazon SNS to send SMS notifications based on these alerts.

## Testing Phase

For the testing phase:

- Use the cheapest EC2 instance available.
- Ensure a fixed IP address by associating an Elastic IP with the instance.


## Contact

For any questions or clarifications, feel free to reach out to me at [your_email@example.com].
```