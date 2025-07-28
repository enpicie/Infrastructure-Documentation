# HCP Terraform Directory

This document is here to help navigate the `enpicie` HCP Terraform org in one place without being in HCP Terraform UI.

## Projects

- AWS-API-startgg - AWS API services for serving start.gg data
- AWS-FGC - AWS resources used for projects to serve the greater FGC
- AWS-Infrastructure - General AWS Infrastructure config

## Workspaces

Each Workspace corresponds to one set of deployments.

Each application should have **1 workspace per environment** as prod and dev deployments will be independent deployments.

Exceptions are configuration deployments which are independent of an environment.

### Workspace Setup

[action-workflow-hcp-terraform-workspace-setup](https://github.com/enpicie/action-workflow-hcp-terraform-workspace-setup) is used in GitHub Actions to provision workspaces for projects.

_It does not take an input for environment_ as applications are responsible for managing this naming themselves to enable custom configurations in each application's code as needed.
