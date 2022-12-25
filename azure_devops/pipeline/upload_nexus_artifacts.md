# Purpose
This section covers steps to be followed for uploading artifacts to Nexus. 

# Table of Contents
- [Python PYPI](#python-pypi)

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
