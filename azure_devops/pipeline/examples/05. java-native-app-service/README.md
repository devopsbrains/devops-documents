# Purpose
Follow this document if you use maven to build java project and deploy to Azure App service without using Docker.

# Pre-requisite
- Azure Resource Manager Service Connection for your subscription is needed. For example, if your subscription name is `SUB_LMS_PROD`, then create ARM service connection in the name as `SC_ARM_LMS_PROD`. 
  - Open snow ticket with cloud security team for this [here](https://premierprod.service-now.com/premiernow?id=dept_cat_item&sys_id=c64bdf091bdc2494be08975e034bcbbb)
  - Select "Azure" in Environment.

- App service name, App Service Resource Group will be provided by cloud devops team. No need Service connection for this in ADO. 

- Library group is needed for deploy environments. For example: java-app-service-dev must have following key/values.

    | Key | Value | 
    | --- | --- |
    | var_az_app_service_rg | ResourceGroupName |
    | var_az_app_service | AppServiceName | 
    | var_spring_profiles_active | Optional_Used_in_AppSettings | 