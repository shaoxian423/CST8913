# Lab4 - Multi-Region Deployment with Load Balancing on Azure

## Student Information
**Student Name:** Shaoxian Duan  
**Student Number:** 041123100  

## 1. Solution Diagram
![diagram](lab4.png)

## 2. Target Architecture Description
The proposed architecture ensures high availability and minimal downtime by leveraging a multi-region deployment strategy with automatic failover and Azure Load Balancer:

### **Front End: WebServerVM**
- Hosted in multiple Azure regions using Azure Virtual Machines.
- Load-balanced across regions using an Azure Traffic Manager.
- If one region fails, traffic is redirected to another active region.

### **Back End: Azure SQLVM**
- Database replicated across regions using Azure SQL Database with Geo-Replication (configured during creation).
- Primary Azure SQLServer VM in Region A and Secondary Azure SQLServer VM in Region B.
- Automated failover uses Azure SQL Failover Group: Primary in Region A promotes Secondary in Region B if failure occurs.
- Synchronization uses Geo-Replication to minimize performance impact.

### **Load Balancing and Traffic Management**
- Azure Traffic Manager distributes incoming traffic between regional web servers.
- After the Azure Traffic Manager, load balancing directs the workflow to the appropriate route.
- If a WebServerVM in one region becomes unresponsive, requests are routed to the healthy region.

## 3. Migration Steps
1. **Migration Assessment (Pre-Migration)**
2. **Replication of Virtual Machines Across Azure Regions**
3. **Configuration of Load Balancers**
4. **Implementation of Database Replication and Failover**
5. **Migration Testing**

## Conclusion
This architecture ensures high availability by replicating web and database layers across Azure regions. Azure Traffic Manager handles traffic redirection, and Azure SQL Failover Group reduces downtime. Migration downtime will stay within the 6-hour limit.
