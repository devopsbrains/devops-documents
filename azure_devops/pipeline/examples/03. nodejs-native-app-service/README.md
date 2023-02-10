# Purpose
Deployment of sample NodeJS app to app service without container.  For example, we used simple express framework and pm2 for starting the application.

# Pre-requisite
- Azure Resource Manager Service Connection for your subscription is needed. For example, if your subscription name is `SUB_LMS_PROD`, then create ARM service connection in the name as `SC_ARM_LMS_PROD`. 
  - Open snow ticket with cloud security team for this [here](https://premierprod.service-now.com/premiernow?id=dept_cat_item&sys_id=c64bdf091bdc2494be08975e034bcbbb)
  - Select "Azure" in Environment.


# Steps
- Templatized the pipeline build and deployment.
- In ci.yaml file, (build)
  - we install NPM dependencies and package the application as a zip file.
  - create artifact of the zip file.
- In deploy.yaml, (deploy)
  - we deploy to native apps.
  - You need to make changes to the `StartUpCommand` in the deploy.yaml file as it varies for each framework. 