# Cost Estimate for 2-Tier Application in Azure

## Overview
This document estimates the initial monthly cost of a 2-tier application deployed in Microsoft Azure using the Azure Pricing Calculator.

## Configuration
- **Region**: East US (Resources), East Asia (Networking Destination)
- **Frontend**:
  - VM: Standard B2s (2 vCPUs, 4 GiB RAM)
  - Storage: 64 GiB (Premium SSD, P6) - Adjusted from 50 GiB (closest available size)
- **Backend**:
  - VM: Standard D2s v3 (2 vCPUs, 8 GiB RAM)
  - Storage: 128 GiB (Premium SSD, P10) - Adjusted from 100 GiB (closest available size)
  - SQL Database: Basic Tier (5 DTUs)
- **Networking**: 200 GB outbound data transfer (East US to East Asia)

## Cost Breakdown
| Component            | Description               | Monthly Cost (USD) |
|----------------------|---------------------------|--------------------|
| Frontend VM          | Standard B2s              | $30.37            |
| Frontend Storage     | 64 GiB Premium SSD (P6)   | $10.21            |
| Backend VM           | Standard D2s v3           | $79.83            |
| Backend Storage      | 128 GiB Premium SSD (P10) | $19.71            |
| SQL Database         | Basic Tier (5 DTUs)       | $4.90             |
| Networking           | 200 GB Outbound (East US to East Asia) | $9.75            |
| **Total**            |                           | **$145.01**       |

*Note*: Costs are approximate and based on East US pricing as of March 2025. Disk sizes adjusted to nearest available Premium SSD options (64 GiB and 128 GiB) due to fixed capacity constraints. Backend VM cost ($79.83) reflects current Pay as you go pricing; adjust if discounts apply. Networking cost reflects inter-region transfer from East US to East Asia.

## Source
- Generated using [Azure Pricing Calculator](https://azure.microsoft.com/en-us/pricing/calculator/)
- PDF saved as `cost-estimate.pdf`.