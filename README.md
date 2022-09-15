# helm-upgrade-test

This is a reusable GitHub workflow to test Helm chart upgrades.

It'll deploy a kind cluster, install the chart, upgrade it, wait in-between, and finally run tests.

## Usage

Create a workflow file in your repository, e.g. `.github/workflows/helm-upgrade-test.yaml` :

```yaml
name: Helm upgrade test
on:
  pull_request:

jobs:
  helm-upgrade-test:
    runs-on: ubuntu-latest
    steps:
      - uses: metal-toolbox/helm-upgrade-test/.github/workflows/upgrade-test@main
        with:
          install-strategy: helm
```

The workflow will be triggered on every pull request. It will install the chart in the `charts` directory and upgrade it to the version in the pull request. No tests will be ran.

### Configuration

The workflow can be configured using the following inputs:

| Input | Description | Default |
| --- | --- | --- |
| `helm-version` | Helm version to use | `latest` |
| `install-strategy` | Strategy to use for installing the chart. Can be `helm` or `argocd` | `helm` |
| `wait-cmd` | Command to run to wait for the chart to be ready | `sleep 10` |
| `wait-cmd-afterupgrade` | Command to run to wait for the chart to be ready after the upgrade | `sleep 10` |
| `test-cmd` | Command to run to test the chart | `echo "No tests defined"` |
