# Azure DevOps Linux Pipeline
This document contains various pipeline steps that can be followed in Azure DevOps Pipeline for different use cases when you are using **Premier Self Hosted Windows Agents**.

# Table of Contents

- [Pre-requisite](#pre-requisite)
- [Pipeline Steps](#pipeline-steps)
- [Reference](#reference)

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


# Reference
- To upload packages to Nexus, please check [this document](./upload_nexus_artifacts.md)