# Troubleshooting

## 400 Bad Request while uploading package to Nexus
  - `Problem`: It looks like the version you are trying to upload is already present in Nexus.
  - `Solution`: Change the version or add `-SNAPSHOT` to the version. You can push `-SNAPSHOT` versions multiple times whereas you can push non-snapshot versions only once to Nexus when it comes to Maven.

## 404 Not Found or Quarantine
  - `Problem`: The package is blocked by Nexus Firewall as it has vulnerabilities. 
  - `Solution`: Use a non-vulnerable version of the package or use a different package. 

## Pipeline fails due to Connectivity Issue or Network not found.
  - `Problem`: Firewall issue
  - `Solution`: Follow [this document](./agents.md) to raise a Firewall request. 