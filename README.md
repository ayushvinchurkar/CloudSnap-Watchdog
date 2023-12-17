# CloudSnap-Watchdog

# Objective:
The project aims to automate the cleanup of Amazon Elastic Block Store (EBS) snapshots in an AWS environment. EBS snapshots are used for backup and recovery purposes, but over time, unused or orphaned snapshots can accumulate, leading to increased storage costs. The goal of this project was fortified with robust error-handling mechanisms to gracefully manage scenarios where associated volumes or snapshots were not found, ensuring the overall reliability of the automation process. The project showcased technical proficiency in serverless architecture, AWS Lambda, CloudWatch, EB and SNS resulting in significant cost savings through the removal of redundant EBS snapshots which are no longer needed and contributing to enhanced resource management within AWS cloud environments.







# Components:

**AWS Lambda Function (lambda_handler):**

**Trigger:** Scheduled execution, using AWS CloudWatch Events.

**Runtime:** Python.

Execution Role: The Lambda function assumes a role with the necessary permissions to interact with EC2 and delete EBS snapshots.
# Boto3 Library:

The official AWS SDK for Python is used to interact with AWS services programmatically.
# Functionality:

**Snapshot Retrieval:** Utilizes the describe_snapshots API to retrieve information about EBS snapshots owned by the AWS account (OwnerIds=['self']).

**Active Instance Retrieval:** Uses the describe_instances API to identify running EC2 instances and extracts their instance IDs.

**Snapshot Cleanup Logic:**
Iterates through each retrieved snapshot.
Checks if the snapshot is associated with a volume.
If not, deletes the snapshot as it is not attached to any volume.
If associated with a volume, checks if the volume still exists.
If the volume has no attachments (not attached to any running instance), deletes the snapshot.
If the volume is not found (possibly deleted), deletes the snapshot.

**Error Handling:** Utilizes try and except blocks to handle exceptions, such as when attempting to describe volumes that may no longer exist (InvalidVolume.NotFound).

**Logging:** Prints messages to log the actions taken, providing visibility into the cleanup process.
# Deployment:

The Lambda function is deployed in the AWS environment.
It is scheduled to run at defined intervals (e.g., daily or weekly) using AWS CloudWatch Events.
# Considerations:

**Permissions:** Ensure that the Lambda execution role has the necessary IAM policies attached for EC2 and EBS actions.

**Testing:** Thoroughly test the Lambda function in a controlled environment before deploying it in a production setting.

**Monitoring:** Implement monitoring and logging mechanisms (e.g., AWS CloudWatch Logs) for better visibility into the Lambda function's execution.
# Benefits:

**Cost Optimization:** Regularly cleaning up unused EBS snapshots helps reduce storage costs.

**Resource Efficiency:** Ensures that storage resources are used efficiently by removing unnecessary snapshots.

**Automation:** Automates a manual and potentially error-prone task, improving operational efficiency.
