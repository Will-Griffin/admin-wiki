[[_TOC_]]

## Overview

Azure resource groups are used as the container for related resources as part of this solution. Azure resources that require similar deployment, user access, and lifecycle should stay together.

## Resource Groups

This solution uses 9 resource groups to separate resources across lifecycles and access. These resource groups will be duplicated across other environment subscriptions.


| Name | Desc |
|--|--|
| `rg-LAC-HIDEX-shared-{env}` | Contains cross departmental API processing services |
| `rg-LAC-HIDEX-edi-{env}` | Contains cross departmental EDI specific services |
| `rg-LAC-DMHDPH-HIDEX-Keyvaults-{env}` | Contains cross departmental Keyvault resources |
| `rg-LAC-DPH-HIDEX-{env}`  | Contains DPH specific services |
| `rg-LAC-DPH-HIDEX-Keyvaults-{env}` | Contains Keyvault resources specific to DPH |
| `rg-LAC-DPH-HIDEX-ANALYTICS-{env}` | Contains Analytic services specific to DPH |
| `rg-LAC-DMH-HIDEX-{env}` | Contains DMH specific services |
| `rg-LAC-DMH-HIDEX-Keyvaults-{env}` | Contains Keyvault resources specific to DMH |
| `rg-LAC-DMH-HIDEX-ANALYTICS-{env}` | Contains Analytic services specific to DMH |

![azrg](/Integration-Services/.attachments/az-resource-groups.png)
