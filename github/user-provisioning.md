# Purpose
This document explains the procedure to onboard user to GitHub and to a GitHub Team.

# Description
- Repositories are linked to GitHub Team.
- GitHub Team = Project in ADO
- Each GitHub Team is linked to Azure Active Directory Group (AD Group). So if you want to add or remove members from GitHub Team, you have to do it in Azure Active Directory Group (AD Group).
- Procedure to add/remove members to the AD Group is covered [here](../azure_devops/user_provisioning.md)

> **Note**: It usually takes an hour to sync the AD Group with GitHub. 

## New user to GitHub
- If the user is new to GitHub, adding users to the AD Group will trigger an email that sends a GitHub invitation to the user.
- The user must accept the invitation within 7 days and create a new GitHub account using Premier Email address. 
- If the user is unable to access Premier repositories after accepting the invitation, reach out to GitHub Admins and they will send a manual invitation.

## Existing User in GitHub
- If you are trying to add an existing user to a new project (GitHub Team), after adding the users to the AD Group, the user is automatically added to the GitHub Team and has access to all repositories in the GitHub Team. 

