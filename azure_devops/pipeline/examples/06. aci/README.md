# Purpose
Follow this document if you want to run Docker container in Azure Container Instance (ACI).  Deploying to ACI is not straight forward as deploying to azure app service.  We can deploy only by using ARM Template.  In this example, we are deploying a container that mounts azure file share, uses log analytics and deploys to a private subnet. 

 > **Note: Blue/Green deployment Model not supported. It's always kill and create new container.**

# Pre-requisite
- Azure Resource Manager Service Connection for your subscription is needed. For example, if your subscription name is `SUB_LMS_PROD`, then create ARM service connection in the name as `SC_ARM_LMS_PROD`. 
  - Open snow ticket with cloud security team for this [here](https://premierprod.service-now.com/premiernow?id=dept_cat_item&sys_id=c64bdf091bdc2494be08975e034bcbbb)
  - Select "Azure" in Environment.

- Write ARM Template. Refer to [deploy](./deploy/) section.
  - `template.json`: ARM Template for deploying ACI.
  - `template.parameters-dev.json`: Parameters file for Dev environment. Similary create for other environments. 
  > **Note:** Naming convention is importation. For prod, create file as `template.parameters-prod.json`  

- Create Library Group: `cqdoc-filevalidation-dev-azure`.
    | Key | Value |
    | --- | --- | 
    | var_acr_name | acr_name | 
    | var_arm_parameter_file | template.parameters-dev.json |
    | var_az_location | East US | 
    | var_az_subscription | 807ab0e9-16d9-41e7-8f8d-123fdb12f6165 |
    | var_log_analytics_workspace_key | abc123xxxyyyzzz123 | 
    | var_storage_account_key | abc123disjoiisj123 |

# Explanation
- `pipeline/azure-pipeline.yaml` is the root pipeline file. 
- `pipeline/ci.yaml` contains the CI part that includes building Docker Image, and creating artifacts.
- `pipeline/deploy.yaml` is the template file that deploys to Azure ACI.
    - Downloads the docker image artifact file, convert to ACR image and push to ACR. 
    - Downloads the ARM templates from artifacts and deploy the ARM Template by overriding some parameters whose values are obtained from library groups (variable groups).