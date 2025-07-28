# AWS-HCP Auth Architecture

Here is the documentation of the setup to authenticate HCP Terraform runs to AWS with the necessary permissions.

## Goals

- Minimize manual steps to obtain proper authorization for each new project
- Minimize manual steps to update permissions or alter any infrastructure config
- Avoid committing and exposing sensitive data/credentials
- Automate deployments and consume reusable pipeline stages for repeated work

## GitHub Actions

Repos named with pattern `action-workflow-hcp-terraform-*` are Composite Actions for GitHub Actions pipelines with pipeline steps that will be reused across projects. Documentation for each action can be found in its repo's README.

- [action-workflow-hcp-terraform-workspace-setup](https://github.com/enpicie/action-workflow-hcp-terraform-workspace-setup) - Sets up HCP Terraform Workspace
- [action-workflow-hcp-terraform-var-set-attach](https://github.com/enpicie/action-workflow-hcp-terraform-var-set-attach) - Attach Variable Set to HCP Terraform Workspace
  - Primarily used to attach variable sets for corresponding AWS Permissions
- [action-workflow-hcp-terraform-run](https://github.com/enpicie/action-workflow-hcp-terraform-run) - Executes Terraform run in HCP Terraform

[GitHub Organization Secrets and Variables](General.md#github-organization-secrets-and-variables) have common parameters used with these actions.
