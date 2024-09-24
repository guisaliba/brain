### Authentication vs Authorization

1. **Authentication**: Verifies **who you are**.
    
    - Example: Logging into AWS with your email and password. It ensures you’re the legitimate user.
2. **Authorization**: Determines **what you can do**.
    
    - Example: After logging in, authorization decides if you can view, edit, or delete resources.

### Root User in AWS

- The **root user** has full access to everything in your AWS account.
- It’s created with your email and password and should be protected.
- Additionally, the root user has **access keys** for making API/CLI requests.

### Best Practices for Root User

- Use a **strong password** and **don’t share** the root credentials.
- Avoid using the root account for daily tasks; instead, create other users with limited permissions.
- **Disable** or **delete** access keys for the root user to prevent security risks.

**Summary**: Authentication is about confirming identity, while authorization is about assigning permissions. The AWS root user has unlimited power, so secure it tightly and only use it for critical actions.