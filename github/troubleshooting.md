# Troubleshooting
This document covers common issues that can be resolved by application teams on their own.

## SSL Clone issue in Intellij 
- **Problem**: I am having SSL certificate issue (unable to get Local issuer certificate). I am unable to clone the code from git to IntelliJ.
- **Solution**:
  1. Open Intellij, Go to: File -> Settings -> Advanced Settings
  2. Check  the "Use Windows Certificate Store" option

## SSL Clone Issue in Visual Studio
**Solution**: Within Visual Studio, click the Git→Settings menu item, then change the Credential Helper Select Element to Secure Channel

## User has not received GitHub invitation
- **Solution 1**: Request the owner of the Azure AD group to Remove the member and wait for one hour and add him again which will trigger a new GitHub invite automatically.
- **Solution 2**: Request the application delivery team to Send the GitHub invite manually again.

## User unable to access Premier repositories after GitHub invite
- Login to https://github.com/premierinc using premier email address
- Now try to accept the invitation
- Now they can access the premier repository.

## User unable to see repositories of one project
- **Problem**: The user may not be part of the project AD group. For example, if the user unable to view repositories of WFM project, then the user may not be part of "devops_wfm" AD group.
- **Solution**: So the solution is to add the user to the project AD group in Azure Active Directory. Only owners of the AD group can add the users to the AD group in Azure Active Directory. 
