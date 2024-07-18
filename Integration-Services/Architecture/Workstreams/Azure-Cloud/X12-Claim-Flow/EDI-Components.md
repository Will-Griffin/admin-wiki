[[_TOC_]]

## Overview

Various Azure resources are used to support the EDI process:
- Hosting
- Monitoring
- Configuration
- Workflows
- SFTP

## Azure Resources

1. API Connections - These are used by LogicApp workflows to connect to external components such as Integration Accounts, Netsmart SFTP, Provider SFTP, and custom log sink.

    > NOTE: these names are auto generated but could potentially be setup beforehand and manually wired up in a workflow.
    > These names match the last segment in the `connection.id` in `connections.json`. These names currently *do not* align with the connection reference used in the workflows.

    - azureblob - Connects to the Provider SFTP service `salachidexx12sftp{env}w2`.
    - azureblob-2 - Backup storage for all messages `salachidexx12ifunc{env}w2`.
    - azureblob-3 - Connects to the Provider SFTP service `salachidexx12sftp{env}w2`. (_potentially the `azureblob` connection can be used in place of this_)
    - azureeventgrid - Connects to `evgt-lac-hidex-x12-{env}-w2` for triggering the `837` workflow.
    - azureloganalyticsdatacollector - Connects to `log-lac-hidex-{env}-w2` for logging custom logs.
    - sftpwithssh - Connects to the NetSmart SFTP server. In development, this connects to `salachidexx12nssftp{env}w2`.
    - x12 - Connects to the Integration Account `ia-lac-hidex-x12-{env}-w2`.

1. App Service Plan:
    - Event Publisher - `plan-lac-hidex-x12-inbound-{env}-w2` - Compute resource
    - Workflows - `plan-lac-hidex-x12-logic-{env}-w2` - Compute resource
1. Application Insights - Monitoring tool for custom EDI applications such as event publisher and logic app workflows. This does _NOT_ include integration account logs. Those will go to Log Analytics.
1. Event Grid Topic - `evgt-lac-hidex-x12-{env}-w2` - Reliable event delivery system used to trigger the `837` inbound LogicApp workflow.
1. Function App:
    - App - `func-lac-hidex-x12-inbound-{env}-w2` - Hosts the 837 inbound [event publisher](/Architecture/Workstreams/X12-Claim-Flow/Aggregating-inbound-messages).
    - Slot - `func-lac-hidex-x12-inbound-{env}-w2/staging` - Hosts the blue/green slot used for deploying the 837 inbound event publisher.
1. Integration Account - `ia-lac-hidex-x12-{env}-w2` - Azure B2B solution used to configure trading partners, schemas, and agreements.
1. Log Analytics - `log-lac-hidex-{env}-w2` - Used to store all system logs across all components and also provides native Azure B2B monitoring for EDI x12. This is part of the shared DMH\DPH infrastructure in another subscription.
1. Logic App (Standard) - `logic-lac-hidex-x12-logic-{env}-w2` - Hosts all workflows used to process the x12 message types. This is hosted in an Azure App Service.
1. Storage Accounts:
    - `salachidexx12bak{env}w2` - The long-term backup storage for all messages.
    - `salachidexx12ifunc{env}w2` - Used by the event publisher for hosting the application.
    - `salachidexx12logic{env}w2` - Used by the LogicApp (Standard) for hosting the workflows.
    - `salachidexx12sftp{env}w2` - Used as the SFTP server for providers to connect to.
    - `salachidexx12nssftp{env}w2` - Used as an SFTP server to mock NetSmart. This should only be used for development purposes.