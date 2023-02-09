[[_TOC_]]

## Overview

Azure DevOps continuous integration and continuos delivery is leveraged to manage the application and infrastructure lifecycle.

## DevOps Components

1. [Azure Boards](https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_boards/board/t/HIDEX%20Team/Stories) - Azure backlogs are used to manage work items - 
1. Azure [Repos](/DevOps/Branching-Strategy) - Each solution layer uses individual source control `Git`-based repositories. This includes the infrastructure and application components.
1. Azure [Pipelines](/Reports/Pipeline-Status) - Pipelines will be used for CI/CD for each solution layer.
1. Security
    - Azure DevOps [Service Connections](/DevOps/Service-Connections) - Provide access to external resources such as Azure for executing tasks in a job.
    - Azure Pipeline [Environments](/DevOps/Environments) - Pipeline environments are used to manage the logic deployment of the components and required security.

[
![components](/.attachments/ado-components.png)
