# Purpose
This document covers steps to email the test results & reports after pipeline execution.

# Pre-requisite
A Generic Service Connection must be created that must contain the SMTP details. To do so, follow the steps:
- Go to **Project Settings**.
- Go to **Service Connections**
- Create a new Service Connection and search for **Generic Service Connection**.

- Create Generic Service Connection
  | Field | Value |
  | -- | -- |
  | Server URL | https://premierinc.mail.protection.outlook.com:25 | 
  | Username (optional) | Your Premier Email Address |
  | Password/Token Key (optional) | Your Premier Password |
  | Service Connection Name | email_automation_sc |
  | Description (optional) | automation email | 
  | Security | Select `Enable - Grant access permission to all pipelines` | 
- Click Create. 

> **Note: Once the service connection is created and if you want to modify any values, do not edit it. Please delete the service connection and create a new one.**


# Add Email Task To Pipeline
Create a new job like `Email Automation` and add below configuration to pipeline.

> **Note: EmailReport@1 task works only from windows agents. Hence specify the pool name.**

```YAML
  - job: EmailAutomation
    pool:
      name: 'Premier Windows Agents'
    displayName: Email Automation
    dependsOn: ['job1'] # provide the job name which produces the test results
    steps:
      - task: EmailReport@1
        inputs:
          sendMailConditionConfig: 'Always'
          subject: '[{environmentStatus}] {passPercentage} tests passed in for $(Build.BuildNumber)'
          toAddress: 'email1@premierinc.com;email2@premierinc.com'
          defaultDomain: 'premierinc.com'
          groupTestResultsBy: 'run'
          includeCommits: true
          maxTestFailuresToShow: '15'
          includeOthersInTotal: false
          usePreviousEnvironment: false
          enableTLS: true
          smtpConnectionEndpoint: 'email_automation_sc' # service connection name you created in pre-requisite step
```

# Reference
- [Email Report Extension](https://marketplace.visualstudio.com/items?itemName=epsteam.EmailReportExtension) official document.
