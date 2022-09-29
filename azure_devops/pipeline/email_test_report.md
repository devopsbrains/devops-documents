Table of contents
=================

<!--ts-->
   * [Scope of document](#Scope-of-document)
   * [Outlook Extension added in ADO Premier Organization](#Outlook-Extension-added-in-ADO-Premier-Organization)
   * [Outlook Extension if not added in ADO Organization](#Outlook-Extension-if-not-added-in-ADO-Organization)
   * [Create Generic Service Connection](#Create-Generic-Service-Connection)
   * [Add Email Task To Pipeline](#Add-Email-Task-To-Pipeline)
   * [Reference](#Reference)
<!--te-->

**Scope of document**
=====================
- To receive Test Case Results from ADO once pipeline completed and published output results.

**Outlook Extension added in ADO Premier Organization**
=======================================================

- Extension Name `Email Report Extension` **by Microsoft DevLabs** (installed Already on PremierInc Azure DevOps & Tested)

**Outlook Extension if not added in ADO Organization**
=======================================================

- Login to [DevOps Premier](https://dev.azure.com/premierinc/)
- Go to `Organization Settings`
- Select `Extensions`
- Select `Browse marketplace`
- Search for **Email Report Extension**
- Choose **Email Report Extension by Microsoft DevLabs**
- Click on Get it free
- Select an `Azure DevOps Organization`, choose `premierinc`
- Click on `Download`
- After Installing it will ask `Proceed to organization`
- Now, we will have an extension installed on our organization.

**Create Generic Service Connection**
=====================================

- Parameters required to create a `Generic Service Connection` for automation email
  - [ ]   Server URL
          `https://premierinc.mail.protection.outlook.com:25`
  - [ ]   Username (optional)
          `Your Premier Email Address`
  - [ ]   Password/Token Key (optional) 
          `Your Premier Password`
  - [ ]   Service Connection Name
          `automation`
  - [ ]   Description (optional)
          `automation email`
  - [ ]   Security
          `Enable - Grant access permission to all pipelines`

**Add Email Task To Pipeline**
==============================

- Create a new job like `Email Automation` and add below configuration to pipeline.
```YAML
  - job: EmailAutomation
    pool:
      name: 'Premier Windows Agents'
    displayName: Email Automation
    dependsOn: ['BuildStageName']
    steps:
      - task: EmailReport@1
        inputs:
          sendMailConditionConfig: 'Always'
          subject: '[{environmentStatus}] {passPercentage} tests passed in for $(Build.BuildNumber)'
          toAddress: 'email@premierinc.com'
          defaultDomain: 'premierinc.com'
          groupTestResultsBy: 'run'
          includeCommits: true
          maxTestFailuresToShow: '15'
          includeOthersInTotal: false
          usePreviousEnvironment: false
          enableTLS: true
          smtpConnectionEndpoint: 'automation'
```

**Reference**
=============

Please find more details available from below link

[Email Report Extension](https://marketplace.visualstudio.com/items?itemName=epsteam.EmailReportExtension)
