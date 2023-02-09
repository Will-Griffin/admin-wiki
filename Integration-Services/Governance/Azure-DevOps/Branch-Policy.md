[[_TOC_]]

## Overview

Azure DevOps [branch policies](https://docs.microsoft.com/en-us/azure/devops/repos/git/branch-policies?view=azure-devops&tabs=browser) are required on every repository on the `main` branch. This will force all changes made to `main` branch go through

## Security

The following features are enabled one each branch:

1. Require a minimum of `1` reviewer
    - Reset all code reviewer votes when new changes are pushed.
1. Require work items are linked.
1. Require that all comments are resolved.
1. Support only basic merge (no fast-forward)
1. Enable build validation
1. Enable code coverage for .NET code
1. Associate required reviewers

## Enable Pull Request

![policy](/Integration-Services/.attachments/ado-branch-policies.png)

## Enable Build Validation

This will enable the Pull Request to run a build and validate the code.

![policy-build](/Integration-Services/.attachments/ado-branch-policies-build.png)