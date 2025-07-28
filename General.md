# General Infrastructure

- **CI/CD Pipelines**: GitHub Actions
- **Cloud Service Provider**: AWS
- **Provisioning Tool**: Terraform via HCP Terraform

`enpicie` Organization is used to leverage GitHub Organizations' secret and variable sharing features for the purpose of implementing reusable infrastructure for projects by enpicie (user chzylee).

AWS CloudFormation is used to deploy some of the initial architecture needed to setup fluid Terraform deployments, but the stack above comprises what is primarily used.
