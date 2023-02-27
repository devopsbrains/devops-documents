# Purpose
This document contains information about build agents in Azure DevOps. 

# Agents in on-premises Premier DataCenter

The below table provides the subnet allocated for ADO agents in on premises Premier DC.  

|  | Charlotte (NP) | Culpeper (Prod)  |
|--|--|--|
| Subnet | 10.95.36.0/24 | 10.185.70.0/24 |

Following pools in ADO has agents deployed to these subnets.
```yaml
pool: Premier Linux Agents
```
```yaml
pool: Premier Windows Agents
```

# Firewall Request
If your pipeline fails due to connectivity issue, you have to raise a Firewall request to the Network Team.  When you place any firewall requests, mention the above two subnets as source. Use [Firewall Rules Changes](https://premierprod.service-now.com/premiernow?id=dept_cat_item&sys_id=ce0029b34f644a00f9c58b8d0210c7dc) catalog to open a Firewall Request 

The below table provides the format to place in firewall rule change request everytime when a new request is created.

- Production or Non-Production: Select any environment

|  | Source IP/Subnet | Source Hostname | Destination IP/Subnet | Destination Hostname | Destination Port | Description |
|--|--|--|--|--|--|--|
| Subnet | 10.95.36.0/24 | Azure DevOps Non Prod Agents | Target Server Host IP Address | Target Server Host Name | Destination Port | Allow Non Prod Agents |
| Subnet | 10.185.70.0/24 | Azure DevOps Prod Agents | Target Server Host IP Address | Target Server Host Name | Destination Port | Allow Prod Agents |
