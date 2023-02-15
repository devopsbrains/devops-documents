# Azure DevOps Linux Pipeline
This document contains various pipeline steps that can be followed in Azure DevOps Pipeline for different use cases when you are using **Premier Self Hosted Windows Agents**.

# Table of Contents

- [Pre-requisite](#pre-requisite)
- [Pipeline Steps](#pipeline-steps)
  - [DotNet](#dotnet)
  - [NuGet](#nuget)
- [Appendix](#appendix)

# Pre-requisite
Premier Agents are hosted within the Premier network that provides access to other applications that are hosted within Premier. For example, **[Nexus](https://nexus.premierinc.com/artifacts)** application.  In order to use Premier Agents in your pipeline, specify the Pool name in the pipeline YAML code.  

## Pipeline level
If you want your entire pipeline to be executed in Premier agents, then specify
```YAML
pool:
  name: "Premier Windows Agents"
```

## Stage level
If you want to run a specific stage in Premier agents, then specify
```YAML
stages:
- stage: Build
  pool: "Premier Windows Agents"
  jobs:
  - job: ...
```

## Job Level
If you want to run a specific job in Premier agents, then specify
```YAML
jobs:
- job: ABC
  pool: "Premier Windows Agents"
```

# Pipeline Steps

## DotNet

**Option 1:**: Recommended
```YAML
- powershell: dotnet restore
```

**Option 2:** Use this option only if you have `NuGet.Config` file in your project and that has NuGet feed pointing to Nexus. Check [appendix](#appendix) section.
```YAML
- task: DotNetCoreCLI@2
  displayName: 'dotnet restore'
  inputs:
    command: 'restore'
    feedsToUse: 'config'
    nugetConfigPath: NuGet.Config
    projects: '**/*.csproj'
    includeNuGetOrg: false 
```

## NuGet

**Option 1:**: Recommended
```YAML
- task: NuGetToolInstaller@1
  displayName: Install NuGet

- powershell: nuget restore abc.sln
  displayName: NuGet Restore
```
**Option 2:** Use this option only if you have `NuGet.Config` file in your project and that has NuGet feed pointing to Nexus.  Check [appendix](#appendix) section.
```YAML
- task: NuGetToolInstaller@1
  displayName: Install NuGet

- task: NuGetCommand@2
  inputs:
    command: 'restore'
    restoreSolution: '**/*.sln'
    includeNuGetOrg: false
    feedsToUse: 'config'
    nugetConfigPath: NuGet.Config
```


# Appendix
- To upload packages to Nexus, please check [this document](./upload_nexus_artifacts.md)
- Sample `NuGet.Config` file pointing to Nexus can be found [here](../../nexus/repository_manager/nexus_in_local.md#nuget)