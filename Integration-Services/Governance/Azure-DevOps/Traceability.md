## Overview

End-to-end traceability is required from user story to deployment. To accomplish this the following settings are configured.

1. Each pull request should be linked to the following items:
    - User Story
    - Task 

    > NOTE: The pull request may close the story or leave it open.

1. Each `CI` pipeline will set `Automatically link work items included in this run` under [pipeline settings](https://docs.microsoft.com/en-us/azure/devops/pipelines/customize-pipeline?view=azure-devops#pipeline-settings).