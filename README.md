# splunk-github-wfa

Workflow actions for Splunk

## How to use

### Appinspect

Required Input | Description
-------------- | -----------
`API_USER` | Action secret username for Splunk Appinspect API.
`API_PASS` | Action secret password for Aplunk Appinspect API.

#### Example Configuration

```yaml
name: Splunk Appinspect Caller
on:
  pull_request:
    branches:
      - main
      - master
    paths:
      - "src/**"
    types: [opened, ready_for_review]

jobs:
  call-packaging-workflow:
    uses: ZachChristensen28/splunk-github-wfa/.github/workflows/appinspect.yml@154fb6bd5201e90183c99b40661cb931d61781b4
    secrets:
      API_USER: ${{ secrets.API_USER }}
      API_PASS: ${{ secrets.API_PASS }}
```

### Package

#### Example configuration

```yaml
name: Package app caller
on:
  push:
    branches:
      - master
      - main
    paths:
      - "src/**"
jobs:
  call-packaging-workflow:
    uses: ZachChristensen28/splunk-github-wfa/.github/workflows/package-app.yml@154fb6bd5201e90183c99b40661cb931d61781b4
```

### Docs

Required Input | Description
-------------- | -----------
`config-path` | path to requirements.txt.

#### Example Configuration

```yaml
name: Documentation caller
on:
  push:
    branches:
      - master
      - main
    paths:
      - "docs/**"
      - "mkdocs.yml"

jobs:
    call-docs-workflow:
        uses: ZachChristensen28/splunk-github-wfa/.github/workflows/docs.yml@e96bdc58732819aa2a1f2a03cb8794c92cacd9f6
        with:
            config-path: docs/requirements.txt
```
