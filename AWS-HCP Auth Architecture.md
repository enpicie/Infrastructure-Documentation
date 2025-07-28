# AWS-HCP Auth Architecture

Here is the documentation of the setup to authenticate HCP Terraform runs to AWS with the necessary permissions.

## Goals

- Automate deployments and consume reusable pipeline stages for repeated work
- Minimize manual steps to obtain proper authorization for each new project
- Minimize manual steps to update permissions or alter any infrastructure config
- Avoid committing and exposing sensitive data/credentials

## Diagram

This diagram explains the general infrastructure architecture using the service [startgg-bracket-helper-bot](https://github.com/enpicie/startgg-bracket-helper-bot) as an example.

![Architecture Diagram](./diagrams/enpicie%20Terraform%20Architecture.drawio.png)

## GitHub Actions

GitHub Actions pipelines consume reusable composite actions for basic tasks needed for all HCP Terraform runs.

Repos named with pattern `action-workflow-hcp-terraform-*` are Composite Actions for GitHub Actions pipelines with pipeline steps that will be reused across projects. Documentation for each action can be found in its repo's README.

- [action-workflow-hcp-terraform-workspace-setup](https://github.com/enpicie/action-workflow-hcp-terraform-workspace-setup) - Sets up HCP Terraform Workspace
- [action-workflow-hcp-terraform-var-set-attach](https://github.com/enpicie/action-workflow-hcp-terraform-var-set-attach) - Attach Variable Set to HCP Terraform Workspace
  - Primarily used to attach variable sets for corresponding AWS Permissions
- [action-workflow-hcp-terraform-run](https://github.com/enpicie/action-workflow-hcp-terraform-run) - Executes Terraform run in HCP Terraform

[GitHub Organization Secrets and Variables](General.md#github-organization-secrets-and-variables) have common parameters used with these actions.

## OIDC Setup

All authentication is done using an OIDC Provider in AWS with associated IAM Roles granting relevant permissions to Terraform. This is to minimize need to commit long-term credentials anywhere. The OIDC Provider was configured manually in AWS and can be reused for all HCP Terraform authentication from the `enpicie` organization.

## AWS Auth Injection

AWS Roles assumable via OIDC are injected into workspaces via HCP Terraform Variable Sets [as recommended by Hashicorp docs](https://www.hashicorp.com/en/blog/access-aws-from-hcp-terraform-with-oidc-federation#Using-OIDC-federation).

Repos can consume these roles to authenticate with necessary permissions to AWS by attaching the Variable Set to their corresponding HCP Terraform Workspace. Use [action-workflow-hcp-terraform-var-set-attach](https://github.com/enpicie/action-workflow-hcp-terraform-var-set-attach) for this and see the usage docs in the repo's README for more details.
