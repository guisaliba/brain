**everything in AWS is an API Call**: every action in AWS (creating, destroying, managing resources, etc.) is done through authenticated and authorized API calls.

there are three major ways to interact with AWS: CLI, SDKs or AWS Console:
1. **AWS  Console**:
    - A web interface for managing AWS resources. It’s user-friendly, good for beginners, and services are grouped by categories (e.g., computing, storage).
    - Changing the region in the console updates the API requests to target a specific AWS region.
2. **AWS Command Line Interface (CLI)**:
    - A powerful tool for managing AWS resources via command line, useful for automation and scripting.
    - Example: `aws ec2 describe-instances` fetches data about EC2 instances. It’s ideal when you need to handle multiple tasks programmatically without manually using the console.
    - Available for Windows, Linux, and macOS.
3. **AWS SDKs**:
    - Allows developers to integrate AWS into applications using programming languages like Python, JavaScript, Java, etc.
    - Example (Python SDK): Using `boto3` to interact with EC2 in a Python app. Useful for embedding AWS services directly into app code. 
  
``` python
import boto3
ec2 = boto3.client('ec2')
response = ec2.describe_instances()
print(response)
```