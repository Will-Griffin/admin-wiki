[[_TOC_]]

## Overview

The EDI X12 837 Patient Claim Flow is documented below.

![x12overview](/.attachments/workstream-x12-overview.png)

## Technology Stack

1. Azure Blob Storage
    - SFTP server. Manages SFTP connectivity, user permissions, storage containers for x12 artifacts.
    - Cold storage. Used to store archived RAW files
2. Azure Integration Account - Scalable cloud-based container that manages B2B artifacts such as:
    - Trading Partners
    - Agreements - Used to specify how aprtners exchange messages securely and expected acknowledgement and processing requirements.
    - Schemas - Used to check the validity of the x12 EDI files and transform them to JSON and XML.
3. Azure Logic Apps - Used to orchestrate the x12 workflow for the various files.
4. Azure Log Analytics Workspace - Used to monitor the x12 workflow and view logs.

## SFTP Server

Azure Blob Storage will be leveraged to provide SFTP support allowing providers to connect securely and manage the X12 artifacts.

Requirements:

1. Storage account must use general-purpose v2 or premium block blob SKU
2. Storage account must enable Azure Data Lake Storage Gen2 capabilities
3. Outgoing communication through port 22 is required

### Container Management

Containers are the logical and security boundary for providers to manage their own x12 EDI files.

- Each provider is assigned a container
- DMH and DPH EDI documents will be stored in the same containers, identified only by the interchange identifier in the file
- The name of the container will be the name of the trading partner with their interchange identifier - `test-hospital-026508070`
    - Consider using `-` vs spaces between the words in the provider's name.
- A separate container called `backup` will be used to store processed files.

### Folder Structure for Provider Container

A folder structure will be leveraged inside each container allowing for separation of input and output files.

- in - Contains 837 input files
- out - Contains all outbound files such as TA1, 277, 999, 835
- error - Contains any custom error files generated while processing the 837    

### Folder Structure for Processed Files

A folder for each trading partner will exist with the processed RAW files.

- {Trading-Partner-Name}
    - 837
    - 277
    - 999
    - 835

### Authentication

Users will be able to authenticate using SSH password. This password can be regenerated via the Azure Portal for the specified user.

> NOTE: Azure Blob Storage also supports SSH Private/Public key but only 1 method of authentication is supported at a time.

### User Management

A local user account will be created for each provider granting them access to their specific container or home directory. The account will include the following permissions:

- Read
- Write
- List

### Connecting via SFTP Client

Any SFTP compliant utility can be leveraged to SFTP files. The user will need the connection string, username, and password.

#### Connecting via PowerShell and Open SSH

1. Connect using connection string
2. Change directory to the `Upload` folder
3. Run the `put` command and specify the file to upload

```powershell
sftp stlachidexx12devwestus2.testhospital@stlachidexx12devwestus2.blob.core.windows.net
stlachidexx12devwestus2.testhospital@stlachidexx12devwestus2.blob.core.windows.net's password:
Connected to stlachidexx12devwestus2.blob.core.windows.net.
sftp> cd in
sftp> put 837.edi
```

## Integration Account Configuration

An Azure Integration Account will manage all B2B artifacts required for the EDI X12 process.

### x12 Schemas

The following schemas are to be stored in the integration account

1. X12_00501_837
1. X12_00501_837_I
1. X12_00501_837_P
1. X12_00501_277_A
1. X12_00501_999
1. X12_00501_835

### Trading Partners

A record for each provider and each LA County department will be added under trading partners. This will be used to represent each participant in the business relationship.

- `Qualifier` - Set to 14 - D-U-N-S Plus Suffix / EAN (European Article Numbering Association)
- `Value` - Set to the provider or department's interchange identifier. This value should be numeric.

### x12 Agreements

An agreement between each LA County department will be added defining how partners exchange messages.

Further documentation on the settings can be found here - [https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-enterprise-integration-x12#receive-settings](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-enterprise-integration-x12#receive-settings).

#### Agreement Header

| Property       	| Description                                                          	| Value                              	|
|----------------	|----------------------------------------------------------------------	|------------------------------------	|
| Host Partner   	| Select name of an existing partner receiving 837 such as DMH or DPH. 	|                                    	|
| Host Identity  	| The DUNS 14 identifier for the receiving partner.                    	| Identifier currently uses type `14`. 	|
| Guest Partner  	| Select name of an existing partner sending 837.                      	|                                    	|
| Guest Identity 	| The DUNS 14 identifier for the sending partner.                      	| Identifier currently uses type `14`. 	|

#### Agreement Receive Settings

For specific HIPAA schema and message type configuration see the following document for futher details [https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-enterprise-integration-x12#hipaa-schemas-and-message-types](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-enterprise-integration-x12#hipaa-schemas-and-message-types)

| Property                                       	| Description                                        	| Value                                     	|
|------------------------------------------------	|----------------------------------------------------	|-------------------------------------------	|
| ISA1                                           	| Authorization Qualifier                            	| 00 - No Authorization Information Present 	|
| ISA2                                           	|                                                    	| N/A                                       	|
| ISA3                                           	| Security Qualifier                                 	| 00 - No Security Information Present      	|
| TA1 Expected                                   	| Acknowledgement                                    	| Enabled                                   	|
| FA Expected                                    	| Acknowledgement                                    	| Disabled                                  	|
| ISA11 Usage                                    	| Envelope setting                                   	| Repetition separator = `^`                	|
| Interchange control number duplicate check     	| Disallow Interchange control number duplicates     	| Enabled                                   	|
| Interchange control number duplicate threshold 	| Check for duplicate ISA12 every (days)             	| 30                                        	|
| Group control number duplicate check           	| Disallow Group control number duplicates           	| Enabled                                   	|
| Transaction set control number duplicate check 	| Disallow Transaction set control number duplicates 	| Enabled                                   	|
| Validation Message Type                        	| The EDI message type such as 837_P or 837_I        	| The expected schema validation            	|
| Validation EDI Validation                      	|                                                    	| false                                     	|
| Validation Extended Validation                 	|                                                    	| false                                     	|
| Validation Allow Leading/Trailing Zeros        	|                                                    	| false                                     	|
| Validation Trim Leading/Trailing Zeros         	|                                                    	| false                                     	|
| Validation Trailing Separator Policy           	|                                                    	| NotAllowed                                	|
| Internal Settings - Convert implied decimal format Nn to base 10 numeric value              	|                                                    	| Disabled                                  	|
| Internal Settings - Create empty XML tags if trailing separators are allowed                                             	|                                                    	| Enabled                                   	|
|                                                	|                                                    	|                                           	|

## Processing Flow

Various Azure Logic App instances will be used to manage the end-to-end EDI processing.

1. Inbound - Manages all inbound processing of 837 and TA1 submittal. Handles the following tasks:
    1. Agreement resolution
    2. 837 schema validation
    3. TA1 submittal
    4. NetSmart submittal
2. Outbound - Manages all outbound processing of files received from NetSmart. Handles the following files:
    1. 277
    2. 999
    3. 835

### 837 Decoding and TA1 Submittal

The following diagram outlines the detailed steps taken by the workflow to ingest and process the 837 file.

1. Poll for new or modified files
2. Resolve agreement
3. Handle resolve errors if found
4. Decode message
5. Handle decoding errors if found
6. In Parallel
    1. Process ACKs
        - Send TA1 to provider
    2. Process Bad Messages
        - Log errors
        - Send failed message to provider
    3. Process Good Messages
        - TBD
7. Archive the input files        

![837flow](/.attachments/workstream-x12-837-flow.png)

#### Retrieving 837 Files

An Azure Function will be used to aggregate all new files across all provider folders in the SFTP server. For each file, an event will be published to Azure Event Grid. The Inbound Logic App will be triggered by the Azure Event Grid.

> NOTE: At this time an Azure Blob Storage with SFTP enabled does not sent events to Azure Event Grid which can trigger Azure Logic Apps. In the future this should be revisited.

### 277 Processing

1. Poll for new files from NetSmart
1. Log process start
1. Resolve agreement
1. Extract `Loop2200B_TRN2` field and add to log entry
1. Handle resolve errors if found
1. Send file to provider
1. Archive the input file
1. Delete the input fule
1. Move the input file to NetSmart `Processed` folder.

### 999 Processing

1. Poll for new files from NetSmart
1. Log process start
1. Resolve agreement
1. Handle resolve errors if found
1. Send file to provider
1. Archive the input file
1. Delete the input fule
1. Move the input file to NetSmart `Processed` folder.

### 835 Processing

1. Poll for new files from NetSmart
1. Log process start
1. Resolve agreement
1. Extract `CLP01` field and add to log entry
1. Handle resolve errors if found
1. Send file to provider
1. Archive the input file
1. Delete the input fule
1. Move the input file to NetSmart `Processed` folder.

### x12 Retention Policy

Once the 837 file has been processed it will be stored in a separate Azure Blob storage account with cold sku under the `x12-backup` directory. A subfolder with the trading partner's name will be created under this folder where provider specific files will be stored.

## NetSmart SFTP Server

NetSmart SFTP server uses SSH username/password. They include a pre-production and production environment.

Each server has a root level folder that specifies the environment.

| LAC Environment 	| NetSmart Environment 	|
|-----------	|--------------	|
| DEV | dev |
| QA | qa |
| Production | live |

### NetSmart's Inbound Folder Structure

- Environment {dev, qa, live} - Environment specific folder
  - Message Type {837P | 837I) - Location where all provider files go

### NetSmart's Outbound Folder Structure
NetSmart's outbound folder structure 
- Environment {dev, qa, live} - Environment specific folder
  - Message Type {277CA | 835 | 999) - Location where all provider files go
    - PROCESSED - Location to write files after the LAC process has picked the up.

## Logging and Error Handling

All logs and diagnostics will be sent to Azure Log Analytics Workspace. Various approaches can be leverage to view logs depending on the user's role and access to the system.

1. Logic App Run History
2. Log Analytics Workspace
    - Logic App B2B Solution
    - Custom log entries

### Required Logging X12 Codes

These sections should be included in the logging.

| Direction 	| Message Type 	| Name                    	| Code           	| Code Sequence 	|
|-----------	|--------------	|-------------------------	|----------------	|---------------	|
| Both      	| All          	| Interchange Sender ID   	| ISA - I06      	| 06            	|
| Both      	| All          	| Interchange Receiver ID 	| ISA - I07      	| 08            	|
| Both      	| All          	| Control Number          	| ISA - I12      	| 13            	|
| Inbound   	| 837          	| Group Control Number    	| GS06           	| 06            	|
| Inbound   	| 837          	| Claim Submitter's Identifier  | CLM01          	| 01            	|
| Inbound   	| 837          	| Reference Identification	| BHT03          	|               	|
| Outbound  	| 835          	| Claim Submitter's Identifier  | CLP01          	| 01            	|
| Outbound  	| 277          	|                         	| Loop2200B_TRN2 	|               	|
| Outbound  	|              	| Group Control Number	    | AK102          	|               	|

### Correlating codes with message types

This table provides a mapping between the messages.

| Message Type 	| Code  	| Maps to Message Type 	| Maps to Code   	|
|--------------	|-------	|----------------------	|----------------	|
| 837          	| CLM01 	| 835                  	| CLP01          	|
| 837          	| BHT03 	| 277                  	| Loop2200B_TRN2 	|
| 837          	| GS06  	| 277                  	| AK102          	|
| 837          	| GS06  	| 999                  	| AK102          	|
| 837          	| GS06  	| 835                  	| AK102          	|
| 837          	|       	|                      	|                	|

### Generating Custom Logs

Custom log entries can be generated as needed in the workflow via the [Azure Log ANalytics Data Collector](https://docs.microsoft.com/en-us/connectors/azureloganalyticsdatacollector/#send-data) connector. These logs are to be written to Azure Log Analytics Workspace. The table to add logs to is `edi_x12`.

Configuration:
- Configure run after - Enable the step to run after the previous step when it has timed out or has failed.
- Custom Log Name - Use the parameter `LogName`
- JSON Request Body - Use the json body from below.

> NOTE: When configuring steps that come after an error logging step, those should run when the log step has been skipped.

Log Schema:

| Property      	| Description                                        	| Default Value 	                                |
|---------------	|----------------------------------------------------	|---------------------------------------------      |
| FileProcessed 	| The base64 encoded full path of the file processed 	| @{triggerBody()?['Id']}             	            |
| Message       	| A custom message                                     	|               	                                |
| Exception         | Optional. A custom error or generated by a step       | @{body('Resolve_X12_agreement')['ErrorMessage']}  |
| LogicAppName  	| The fully qualified resource id of the logic app   	| @{workflow().name}             	                |
| RunId         	| The unique run identifier                          	| @{workflow().run.name}             	            |
| Severity      	| The type of message. Information, Warning, Error   	|               	                                |

```json
{
"FileProcessed": "@{triggerBody()?['Id']}",
"Message": "",
"Exception": "@{body('Resolve_X12_agreement')['ErrorMessage']}",
"LogicAppName": "@{workflow().name}",
"RunId": "@{workflow().run.name}",
"Severity": "Error"
}
```

The following severity levels should be used:
- Information
- Warning
- Error

### Viewing Run History via Azure Portal

- Access Azure Portal
- Open the instance of Logic Apps
- View the history in the Overview pane
- Click on an individual run to view each step and drill into the output of each step

Run History:

![runHistory](/.attachments/workstream-x12-run-history.png)

Step Output:

![runError](/.attachments/workstream-x12-run-history-error.png)


### Viewing EDI Logs

TBD

### Correlating processed file with run logs

TBD

## Testing

TBD

## References

- [EDI Data Segments](https://www.stedi.com/edi/x12-005010/segment)
- [ISA Interchange Control Header](https://www.stedi.com/edi/x12-005010/segment/ISA)
- [GS Functional Group Header](https://www.stedi.com/edi/x12-005010/segment/GS)
- [CLP Claim Level Data](https://www.stedi.com/edi/x12-005010/segment/CLP)