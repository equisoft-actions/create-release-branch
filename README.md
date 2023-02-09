# create-release-branch

Automatically create release/vX.X.x branch for vX.X.0 tags

This action should be used in a stand-alone workflow and triggered on `v*.*.0` tags.

The secret for the PAT used to create the branch should be in an environment only accessible to protected branches.

*Sample workflow*

```
name: Create release branch

on:
push:
  tags:
    - v*.*.0

jobs:
create-release-branch:
  runs-on: ubuntu-latest
  environment: release
  permissions:
    contents: write
  steps:
    - uses: actions/checkout@v3
      with:
        fetch-depth: 0

    - uses: equisoft-actions/create-release-branch@v1
      with:
        github-token: ${{ secrets.ADMIN_PAT }}
```
