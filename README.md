# record-deployment Github Action

This action records a deployment happening on GitHub Actions to Prodvana.


# Requirements
- [pvnctl](https://github.com/prodvana/pvnctl) present in the CI environment
  - We recommend using [init-pvnctl-action](https://github.com/prodvana/init-pvnctl-action) to handle installation and authentication initialization

# Usage

## Inputs

| Input             | Default        | Description                                                                                                                                              |
| ----------------- | -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| app               | (required)     | A unique name for the application being deployed. An application is a collection of related services with the same set of deployment channels. e.g. infra, product, <company name>     |
| service           | (required)     | A unique name for the service being deployed, e.g. api, web                                                                                              |
| release_channel   | (required)     | A unique name for the release channel of the service being deployed, e.g. staging, prod                                                                  |
| deployment_system | github-actions | The deployment system doing the deployment                                                                                                                  |
| pending           | false          | Record the deployment in pending state instead of succeeded state, meant to be used with update-deployment-status action                                       |
| auth_context      | default        | pvnctl auth context to use. If you're using this action with init-pvnctl, leave as the default                                                           |


## Basic Usage

```yaml
steps:
  # pvnctl must be installed in your Action environment for configs-apply
  - uses: prodvana/init-pvnctl-action@v0.1.0
    with:
      org: my-org
      api_token: ${{ secrets.YOUR_PRODVANA_API_TOKEN }}
  - uses: prodvana/record-deployment-action@v0.1.2
    with:
      app: product-name
      service: web
      release_channel: prod
```
