[[_TOC_]]

## Overview

The initial phase of the x12 process is to aggregate and process inbound messages. A custom Azure Function is used to aggregate all new 837 messages sent by the provider to LACO via SFTP. This component reads from the same Azure Storage Account and for each file will publish an event to Azure Event Grid.

![2022-07-26_11-22-43.png](/Integration-Services/.attachments/2022-07-26_11-22-43-40fd9a0f-a0c5-4213-9e0f-e15b286abc23.png)

> NOTE: Currently data lake and SFTP enabled storage accounts do not publish events to Event Grid. Once this is natively supported, then this custom component could be removed.

## Components

- Azure Function - Used to connect to the SFTP blob storage and read all new 837 messages and publish an event.
- Provider SFTP - The SFTP service where provider's login and upload 837 files.
- Event Grid - Used as the event messaging layer which will trigger the logic app 837 processing.
- Resource Group - https://portal.azure.com/#@lacounty.onmicrosoft.com/resource/subscriptions/14f73201-3f02-45e0-aa9f-2ccf4f7104d0/resourceGroups/rg-LAC-HIDEX-edi-DEV/overview

## Source Control and Pipelines

- Git: https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_git/hidex-edi-x12
- CI: https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_build?definitionId=14
- PR: https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_build?definitionId=9

## Setup

- Review the application [readme](https://dev.azure.com/LACDMH-DPH-Integration/HIDEX/_git/hidex-edi-x12?path=/README.md&_a=preview) and required configuration.
- The managed identity is used to connect to the event grid, so configuration around credentials can be left blank.
- Currently the blob connection string is used so this is required.
- Set the function schedule via the `Inbound837FunctionSchedule` property using CRON syntax.

## Process

1. List all containers in the SFTP storage account.
2. For each container find all new blobs
3. For each blob, plush an event.