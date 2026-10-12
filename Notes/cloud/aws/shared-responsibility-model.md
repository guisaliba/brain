### Shared Responsibility Model in AWS

1. **AWS’s Responsibility: Security _OF_ the Cloud**  
    AWS secures the underlying infrastructure that runs its services (data centers, hardware, network).
    
    - They handle the security of **regions**, **availability zones**, **physical datacenters**, and manage server hardware, virtualization, and core networking.
      
2. **Customer’s Responsibility: Security _IN_ the Cloud**  
    You, the customer, are responsible for securing how you use AWS services. This includes:
    
    - Configuring services properly, encrypting data, managing access controls, and ensuring compliance with data protection laws.
      
3. **Categories of AWS Services**:
    
    - **Infrastructure Services** (e.g., EC2): AWS manages base infrastructure; customers manage OS, application platforms, and data.
    - **Container Services** (e.g., RDS): AWS handles the OS and platforms; you handle securing your data and access.
    - **Abstract Services** (e.g., S3): AWS takes care of most aspects (including encryption), while you manage your data and access.
      
4. **Key Takeaways**:
    
    - Always secure your data: encrypt it, schedule backups, and control access.
    - Choose regions wisely based on compliance needs (e.g., data sovereignty laws).
    - AWS manages the infrastructure; you manage what’s running on it and the security around your data.

**Summary**: AWS secures the cloud infrastructure, while you secure the data and resources you use on it. Make sure to configure everything properly and protect your data with encryption and access controls.

https://aws.amazon.com/compliance/shared-responsibility-model/