# General Organization Infrastructure

- **CI/CD Pipelines**: GitHub Actions
- **Cloud Service Provider**: AWS
- **Provisioning Tool**: Terraform via HCP Terraform

`enpicie` Organization is used to leverage GitHub Organizations' secret and variable sharing features for the purpose of implementing reusable infrastructure for projects by enpicie (user chzylee).

AWS CloudFormation is used to deploy some of the initial architecture needed to setup fluid Terraform deployments, but the stack above comprises what is primarily used.

## GitHub Organization Secrets and Variables

`enpicie` organization uses _org-level_ secrets and variables to share core information. Secrets contain data that should not be committed. Variables contain data that may often be reused and should be visible to possible users.

### Secrets

- `TF_API_TOKEN` - Service Account API Token to authenticate to HCP Terraform
- `GH_ACTIONS_PAT` - Personal Access Token for use in GitHub Actions with permissions to update Org Variables

### Variables

- `AWS_TF_ROLE_VARSET_*`
  - Naming pattern of variables that contain the Name of an HCP Terraform Variable Set
  - Variable Set has reference to a Role for Terraform to use for authenticating to AWS
  - Part of name denoted by wildcard `*` here describes permissions granted by the role (e.g. `AWS_TF_ROLE_VARSET_LAMB_APIGW` has Lambda and API Gateway permissions)
