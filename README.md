# splunk-github-wfa

Workflow actions for Splunk

## How to use

**reference**: <https://docs.github.com/en/actions/using-workflows/reusing-workflows>

### Appinspect

Required Input | Description
-------------- | -----------
`API_USER` | Action secret username for Splunk Appinspect API.
`API_PASS` | Action secret password for Splunk Appinspect API.

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
    uses: ZachChristensen28/splunk-github-wfa/.github/workflows/appinspect.yml@61f404792eba6f8c22465b8a6c96034ee20f2518
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

### Increment Build Number

#### Example Configuration

```yaml
name: Increment Build caller

on:
  push:
    branches:
      - devel
      - development
    paths:
        - "src/**"
        - "!app.conf"

jobs:
  call-packaging-workflow:
    uses: ZachChristensen28/splunk-github-wfa/.github/workflows/increment-build-number.yml@95c81c2bca6e0ad926e5c462ef003f6a6b30cbc0
```
