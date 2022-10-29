# Purpose
Follow this document if you use maven to build your docker image and push to ACR and deploy to Azure App service

# Pre-requisite
- Azure Resource Manager Service Connection is needed. For example, if your subscription name is `SUB_LMS_PROD`, then create ARM service connection in the name as `SC_ARM_LMS_PROD`. Open snow ticket with cloud security team for this.
- Docker Registry service connection for ACR is needed. For example, if your acr name is `lmsprod1acr.azurecr.io`, then create docker registry service connection of type ACR with name `lmsprod1acr`. Create snow ticket with cloud security team for this.
- App service name will be provided by cloud devops team. No need Service connection for this in ADO. 

# Steps
- In the `pom.xml` file, make sure the image name and alias is ${project.artifactId}
- In the pipeline, previously we used `mvn deploy` goal, but going forward use `mvn install` goal as it just creates the docker image but not push anywhere. Refer the `pipeline/ci.yaml` file.
- We push the image to ACR during the deploy step and then deploy to Azure app service. Refer to `pipeline/deploy.yaml` file.
- We have templatized the pipeline files. 

