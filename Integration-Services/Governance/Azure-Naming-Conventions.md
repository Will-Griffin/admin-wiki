[[_TOC_]]

## Overview

An effective naming convention composes resource names from important information about each resource.

## Naming scope

All resources have a scope defining the level that the resource names must be unique.

Some resources require to be globally scoped because of DNS entries that are generated. Others can be unique inside a resource group.

> Consider using the company abbreviation for globally unique resource names.

![resource-naming-scope.png](/.attachments/resource-naming-scope-88272246-5cd3-4071-a290-8fb5db5590b3.png)

## Naming components

```
{resource-type}-{department}-{purpose|workload|application|project}-{environment}-{location}
```

## Naming abbreviations

Consider abbreviating Azure resource types following the Microsoft [recommended abbreviations for Azure resource types](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations)

### Location abbreviations

Consider the following abbreviations when naming resources in order to save on character length.

| Location  | Abbreviation |
| :--       | :--          |
| West US   | w1           |
| West US 2 | w2           |
| West US 2 | w3           |
| East US   | e1           |
| East US 2 | e2           |

## Naming restrictions

Some resources have length and character restrictions. Storage accounts for example requires a 24 character max limit on the name of its resource. It also excludes the use of dashes in its name.