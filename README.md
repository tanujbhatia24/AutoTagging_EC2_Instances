# Auto-Tagging EC2 Instances on Launch (AWS Lambda + Boto3 + Cloudwatch)
## Objective
Automatically tag newly launched EC2 instances with the **current date** and the **IAM user or role** who launched them, using AWS Lambda and Boto3.
---

## Project Structure
- `LambdaAutoTagEC2Role_tanuj.py` – Python code for tagging EC2 instances
- `README.md` – Project instructions and documentation
---

## Requirements
- AWS Account with permissions to:
  - Launch EC2 instances
  - Create Lambda functions
  - Create IAM roles
  - Configure CloudWatch Event rules
- Python 3.x (for Lambda)
---

## Setup Instructions
### 1. EC2 Preparation
You just need EC2 launch permissions. No special configuration required for instances.
---

### 2. Create IAM Role for Lambda
1. Go to **IAM > Roles > Create role**
2. Select **Trusted entity: Lambda**
3. Attach the policy: `AmazonEC2FullAccess`
4. Name the role: `tanuj_LambdaAutoTagEC2Role`
---

### 3. Create the Lambda Function
1. Go to **Lambda > Create function**
2. Runtime: `Python 3.x`
3. Choose **Use existing role** → `tanuj_LambdaAutoTagEC2Role`
4. Lambda Code<br>
   You can use the below file for reference.<br>
   [LambdaAutoTagEC2Role_tanuj.py](https://github.com/tanujbhatia24/AutoTagging_EC2_Instances/blob/main/LambdaAutoTagEC2Role_tanuj.py)
---

### 4. Setup CloudWatch Event Rule
1. Go to Amazon CloudWatch > Events > Rules > Create rule
2. Name the rule: AutoTagEC2Launch_tanuj
3. Select Event Source: AWS event pattern
   - Use this JSON pattern:
     ```bash
      {
      "source": ["aws.ec2"],
      "detail-type": ["EC2 Instance State-change Notification"],
      "detail": {
      "state": ["running"]
        }
      }
     ```
   3. Add Target → Lambda Function you created
  ---

## Testing
1. Launch a new EC2 instance.
2. Wait ~30–60 seconds.
3. Go to EC2 → Instances → Tags tab.
4. Confirm that the following tags are present:
5. LaunchDate: <Today's date>
6. LaunchedBy: <IAM User or Role name>
---

## Snapshots (Attach for validation)<br>
1. Lambda function code and execution log<br>
2. IAM Role with policy<br>
3. CloudWatch Event rule<br>
4. EC2 instance with auto-applied tags<br>
---

## Summary
This solution uses AWS Lambda, Boto3, and CloudWatch Events to fully automate the tagging of EC2 resources at the moment of launch. This improves traceability and cost/resource management within AWS.
---

## License
This project is intended for educational and demonstration purposes. You are welcome to use and adapt it as a reference; however, please ensure that your work represents your own understanding and is not reproduced verbatim.
