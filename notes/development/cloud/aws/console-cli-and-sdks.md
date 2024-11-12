### Interacting with AWS: Console, CLI, and SDKs

1. **Everything is an API Call**: Every action in AWS (creating, managing resources) is done through authenticated and authorized API calls.
    
2. **AWS Management Console**:
    
    - A web interface for managing AWS resources. It’s user-friendly, good for beginners, and services are grouped by categories (e.g., computing, storage).
    - Changing the region in the console updates the API requests to target a specific AWS region.
3. **AWS Command Line Interface (CLI)**:
    
    - A powerful tool for managing AWS resources via command line, useful for automation and scripting.
    - Example: `aws ec2 describe-instances` fetches data about EC2 instances. It’s ideal when you need to handle multiple tasks programmatically without manually using the console.
    - Available for Windows, Linux, and macOS.
4. **AWS SDKs**:
    
    - Allows developers to integrate AWS into applications using programming languages like Python, JavaScript, Java, etc.
    - Example (Python SDK): Using `boto3` to interact with EC2 in a Python app. Useful for embedding AWS services directly into app code. 
  
``` python
import boto3
ec2 = boto3.client('ec2')
response = ec2.describe_instances()
print(response)
```