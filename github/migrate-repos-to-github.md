# Purpose
This document covers steps on how to migrate repositories to GitHub from any SCM (Bitbucket/GitLab).

# Scenarios
- Scenario 1: A simple repository with no large files. 
- Scenario 2: The repository have large files but those files are not needed in GitHub anymore. 
- Scenario 3: The repository have large files (>100 MB) and you need them in GitHub.

> Note:  After migrating to GitHub, make sure you change the linked repository in Bamboo to point GitHub if you are going to use Bamboo. Refer the [reference](#reference) section. 

## Scenario 1: Migrate Repository to GitHub with Histories
### Pre-Requisite
- Make sure you create a empty github repository and that is tied to a GitHub Team you have access to. Use Self Service.
- Make sure you have the access to both old SCM and new GitHub repository.

### Steps

- Git mirror clone the repository 
```bash
git clone --mirror https://code.premierinc.com/source/scm/dmm/scs_db.git
```
- Remove remote origin pointing to old SCM
```bash 
cd scs_db.git 
git remote remove origin 
```

- Rename the master branch to main branch and point origin to GitHub
```bash
git branch  # shows current branch name 
git branch -m main # this will rename current branch (master) to main branch 
git remote add origin https://github.com/PremierInc/example-temp.git # provide the github origin URL
```

- Verify Origin change to the Github Repository and push to GitHub
```bash
git remote -v
git push --mirror 
```

## Scenario 2: Migrate Repository (LFS) with Histories 
You have large files in your repository but you no longer need them in GitHub or in Histories. Then follow the below steps:
### Pre-Requisite
- Make sure you create a empty github repository and that is tied to a GitHub Team you have access to. Use Self Service.
- Make sure you have the access to both old SCM and new GitHub repository.
- Make sure you installed "Git-LFS" from internet. 
- Make sure you downloaded [BFG Cleaner](https://rtyley.github.io/bfg-repo-cleaner/#usage) Executable from internet. 

### Steps

- Clone the repository using mirror clone
```bash
git clone --mirror https://code.premierinc.com/source/scm/dmm/some-big-repo.git
```
- Use bfg.jar to remove files greater than 100 MB.
```
java -jar bfg.jar --strip-blobs-bigger-than 100M some-big-repo.git
```
- Do Garbage Pruning and push to GitHub
```bash
cd some-big-repo.git
git remote remove origin
git reflog expire --expire=now --all && git gc --prune=now --aggressive
git branch -m main # this will rename current branch (master) to main branch 
git remote add origin https://github.com/PremierInc/example-temp.git # provide GitHub Origin URL
git push --mirror
```

# Reference
- [BFG Repo Cleaner](https://rtyley.github.io/bfg-repo-cleaner/)
- [Link GitHub in Bamboo](https://github.com/PremierInc/code-devops-documents/wiki/Integrate-GitHub-with-Bamboo)
- Configure [Github in Bamboo](https://confluence.atlassian.com/bamboo/github-289277001.html)

<!-- ## Scenario 2: Migrate Repository (LFS) without Histories
If your repository has large file, then we cannot migrate them to GitHub with histories.  
### Pre-Requisite
- Make sure you create a empty github repository and that is tied to a GitHub Team you have access to. Use Self Service.
- Make sure you have the access to both old SCM and new GitHub repository.
- Make sure you installed "Git-LFS" from internet. 

### Steps
- Clone a repository and change directory
```bash
git clone <url>
cd repo
```
- Create a new empty branch with expected name and Initialize Git LFS by running below command
```bash
git checkout --orphan branchname
git lfs install
```
- In each Git repository where you want to use Git LFS, select the file types you'd like Git LFS to manage (or directly edit your .gitattributes). You can configure additional file extensions at anytime.
```bash
git lfs track "*.fileextension"

# example
git lfs track "*.avi"
```
- Now make sure .gitattributes is tracked
```
git add .gitattributes
```
- Let's check whether LFS tracking under attributes files or not by running below command
```
git lfs track
```
- Now let's commit LFS files first with attributes to track LFS Files using below command:
```
git commit -m 'added attributes file'
```
- Now Add all files and commit and push
```
git add --all
git commit -m 'added all files'
```
- Now push all files to target repository in GitHub including LFS files
```
git push origin --all
```
- Now, got to GitHub target repository and check a new branch with latest code with LFS files pushed or not. -->
