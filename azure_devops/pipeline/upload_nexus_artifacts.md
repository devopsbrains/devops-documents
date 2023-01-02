# Purpose
This section covers steps to be followed for uploading artifacts to Nexus. 

# Table of Contents
- [Python PYPI](#python-pypi)
- [DotNet NuGet](#dotnet-nuget)

# Python PYPI
| index | url | description | 
| -- | -- | -- |
| premier-pypi | https://nexus.premierinc.com/artifacts/repository/premier-pypi/ | Can be pushed only once |
| premier-pypi-snapshots | https://nexus.premierinc.com/artifacts/repository/premier-pypi-snapshots/ | Can be pushed multiple times and overwrite packages |

```bash
# To upload release versions
twine upload -r premier-pypi <filename>

# To upload snapshots or development versions
twine upload -r premier-pypi-snapshots <filename>
```

# DotNet NuGet
In order to upload Nuget Package to Nexus, use the below Pipeline Task:

```YAML
  - task: NuGetCommand@2
    inputs:
      command: 'push'
      packagesToPush: '$(Build.ArtifactStagingDirectory)/**/*.nupkg;!$(Build.ArtifactStagingDirectory)/**/*.symbols.nupkg'
      nuGetFeedType: 'external'
      publishFeedCredentials: 'Nexus_Nuget-Inflow'
```

`Nexus_Nuget-Inflow` is the name of the service connection of type "NuGet" configured in the Azure DevOps Project.  If not configured, please ask our team to configure it for you.  We created one service connection in CODE ADO project and then shared the same connection across other projects in Azure DevOps. 