# CaseStudy-MigrationPlan.md

---

### 1. Discovery and Tooling Setup 

**Tools for Discovery:**

- **Azure Migrate: Discovery and Assessment Tool**  
  Use the **Azure Migrate Appliance**  deployed on-premises to automatically discover all VMs and workloads.
- **Azure Migrate Application Discovery**  
  For deeper insights, enable agent-based discovery selectively on critical systems.

**Data to Collect:**

- Operating system details (Ubuntu)
- VM performance metrics (CPU, RAM, disk I/O, network)
- NGINX, Node.js, PostgreSQL, Redis, HAProxy and other Software and application inventory 
- Application dependencies and interconnections
- storage usage and etc.

**Credential and Permission Management:**

- Use **Azure Key Vault** to store sensitive credentials securely.
- Apply **Azure RBAC (Role-Based Access Control)** to enforce least-privilege access.
- Create a **service principal credentials** with minimum necessary permissions to support the discovery process securely.

---

### 2. Assessment Planning

**Assessment Parameters:**

- Performance history: 60 days
- Sizing strategy: Performance-based (right-sizing recommendations)
- Assessment scope: Azure readiness and cost estimates

**Target Azure Environment:**

- **Region:** Canada Central
- **Compute:**  
  - D-series VMs for NGINX/API servers  
  - E-series for PostgreSQL 
- **Storage:**  
  - Premium SSD (for PostgreSQL, Redis)  
  - SSD (for API and web application)  
  - HDD (for backups)

**Assessment Validation:**

- Review assessment results with DevOps and stakeholders
- Compare recommended sizing and costs with current usage
- Validate application compatibility using Azure readiness reports

---

### 3. Dependency Analysis and Optimization

**Dependency Mapping Approach:**

- Use **Azure Migrate’s agentless dependency mapping** for general overview
- Enable **agent-based mapping** on key nodes (PostgreSQL, Redis) for deeper insights

**Cleaning Dependency Data:**

- Filter out system dependencies (SSH, DNS, etc.)
- Use logs to focus on business-critical service interactions

**Key Metrics to Capture:**

- **Criticality:** High for PostgreSQL and Redis
- **User base:** High concurrent usage on API servers
- **SLA:** Max 2-hour downtime
- **Backup:**  
  - Daily PostgreSQL backups  
  - Optional Redis snapshots  
  - Azure Backup for VM backups

---

### 4. Server Grouping and Migration Waves 

**Logical Groupings:**

- **Frontend:** 2 NGINX web servers
- **Backend:** 2 Node.js API servers
- **Data Layer:** 1 PostgreSQL DB + 1 Redis instance
- **Other:** HAProxy load balancer, backup system

**Migration Waves:**

1. **Wave 1:** Redis + PostgreSQL (replicate data to Azure)
2. **Wave 2:** Backend (Node.js) servers
3. **Wave 3:** Frontend (NGINX) servers
4. **Wave 4:** Load balancer (HAProxy) and switch-over

**Precautions:**

- Update **NSG firewall rules** in Azure
- Configure Azure Load Balancer with health probes
- Plan for **static internal IPs** for service discovery
- Update DNS or use **Azure DNS** for IP re-pointing

---

### 5. Migration Plan Documentation 

#### Pre-Migration

- Set up Azure Migrate appliance and perform discovery
- Complete assessment and validate with stakeholders
- Enable replication for PostgreSQL via **Azure Database Migration Service**

#### Azure Resource Setup

- Provision Azure VMs using Migrate-recommended sizing
- Configure networking: VNETs, subnets, NSGs, private IPs
- Deploy **Azure Load Balancer** with frontend/backend pools
- Create **Azure Database for PostgreSQL (Flexible Server)**
- Set up **Azure Cache for Redis** (Premium tier for HA)

#### DNS and Backup

- Update internal and external DNS to reflect new IPs
- Use **Azure Backup** and **Blob Storage** for backup replication

#### Testing and Validation

- Run pre-migration test cases with application owners
- Validate full functionality: API, frontend, Redis, DB
- Perform simulated failover and rollback tests

#### Final Cutover

- Schedule migration in agreed 2-hour downtime window
- using **Azure Monitor** and **Application Insights** Monitor system 

#### Post-Migration

- Decommission on-prem VMs in phases
- Enable cost optimization tools (Azure Advisor, Cost Management)
- Conduct post-mortem with stakeholders

**Application Owner Role:**

- Approve test plans and data validation results
- Support DNS changes and session-related reconfigurations
- Validate post-migration application behavior and performance

---