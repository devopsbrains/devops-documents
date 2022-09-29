**What is GIT LFS:**

Git Large File Storage (LFS) replaces large files such as audio samples, videos, datasets, and graphics with text pointers inside Git, while storing the file contents on a remote server like GitHub.com or GitHub Enterprise.

Table of contents
=================

<!--ts-->
   * [Prerequisites](#Prerequisites)
   * [Scope of document](#Scope-of-document)
   * [Migrate a branch using LFS without history to GitHub](#Migrate-a-branch-using-LFS-without-history-to-GitHub)
   * [Reference](#Reference)
<!--te-->

**Prerequisites**
=================
- Download and install the Git Bash

**Scope of document**
=====================
- How can we migrate a source repository branch with LFS(Large File Size) to GitHub.

**Migrate a branch using LFS without history to GitHub**
=======================================================
- Once we came to know like the source repository consists of **LFS(Large File Size)** files. We can use LFS to push our large files to GitHub as noramlly GitHub blocks the files > 100 MB with normal push process.

Now lets try to push a LFS repo to GitHub
```
 1. Clone a repository
    `git clone remote url`
   
 2. cd to repo root level

 3. Create a new empty branch with expected name by using below command
    git checkout --orphan branchname
    It will create a new empty branch
 
 4. Initialize Git LFS by running below command
    git lfs install
   
 5. In each Git repository where you want to use Git LFS, select the file types you'd like Git LFS to manage (or directly edit your .gitattributes). 
    You can configure additional file extensions at anytime.
    git lfs track "*.fileextension"
    EX: git lfs track "*.avi"

 6. Now make sure .gitattributes is tracked
    git add .gitattributes

 7. Let's check whether LFS tracking under attributes files or not by running below command
    git lfs track

 8. Now let's commit LFS files first with attributes to track LFS Files using below command
    git commit -m 'added attributes file'
   
 9. Now Add all files
    git add --all
   
10. Let's do final commit with all pending files
    git commit -m 'added all files'
   
11. Now push all files to target repository in GitHub including LFS files
    git push origin --all
```

- Now, got to GitHub target repository and check a new branch with latest code with LFS files pushed or not.

**Reference**
=============

Please find below links to know more on LFS

GIt Large File Storage [LFS](https://git-lfs.github.com) Official Documentation

[Moving Git large files to Git LFS](https://confluence.atlassian.com/bitbucketserverkb/moving-git-large-files-to-git-lfs-in-bitbucket-server-1072486368.html)
