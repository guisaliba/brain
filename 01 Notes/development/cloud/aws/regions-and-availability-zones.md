### AWS Global Infrastructure: Regions and Availability Zones (AZs)

1. **Regions**: Physical locations where AWS hosts datacenters worldwide. Each region has a specific code (e.g., `us-east-1` for Northern Virginia, `ap-northeast-1` for Tokyo).
    
    - **Key point**: Regions are independent—data isn't shared between regions without explicit permission.
      
2. **Choosing a Region**:
    
    - Consider **latency** (closer to users = faster), **price**, **service availability**, and **compliance**.
    - Latency-sensitive apps (like gaming) need regions close to users.
      
3. **Availability Zones (AZs)**: Clusters of datacenters within a region, each with redundant power, networking, and connectivity.
    
    - Identified by codes like `us-east-1a` (AZ in Northern Virginia).
      
4. **Scope of AWS Services**:
    
    - Some services work at the **region level** (e.g., automatic data replication across AZs).
    - Others require you to pick an **AZ** (you manage durability and availability).
      
5. **Resilience**:
    
    - Best practice: Use services with region-level scope for built-in availability.
    - If not possible, ensure workloads are spread across at least two AZs for failover in case one fails.

**Summary**: AWS operates globally through regions and AZs. Choose the right region based on latency and cost, and design resilient applications by leveraging multiple AZs for failover.