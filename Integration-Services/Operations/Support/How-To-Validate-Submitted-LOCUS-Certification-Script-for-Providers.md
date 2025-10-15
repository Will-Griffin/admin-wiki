Providers (Trading Partners) also known as Legal Entities who are in the process of onboarding for HIDEX LOCUS API will submit a LOCUS Certification Script. This script will contain a bunch of transactions for various test cases. Integration Team will validate the transactions identified in the script. 

Follow the steps below to validate/verify the LOCUS Script transactions:

Step # 1: 
Identify the LE number (Program ID), Client ID, Encounter ID, Practitioner ID from the submitted script.

Step # 2:
Use the following URL to open up the Monitoring Log. Make sure to use the right environment: DEV, TEST, or QA. Usually providers will perform LOCUS script transactions in QA environment.


- [DEV](https://portal.azure.com/#@lacounty.onmicrosoft.com/resource/subscriptions/14f73201-3f02-45e0-aa9f-2ccf4f7104d0/resourceGroups/rg-LAC-HIDEX-shared-dev/providers/Microsoft.Insights/components/appi-lac-hidex-dev-w2/overview))
- [TEST](https://portal.azure.com/#@lacounty.onmicrosoft.com/resource/subscriptions/965126b9-a5ce-4974-b238-7edaab03e70a/resourceGroups/rg-LAC-HIDEX-shared-t/providers/Microsoft.Insights/components/appi-lac-hidex-t-w2/overview))
- [QA](https://portal.azure.com/#@lacounty.onmicrosoft.com/resource/subscriptions/965126b9-a5ce-4974-b238-7edaab03e70a/resourceGroups/rg-LAC-HIDEX-shared-qa/providers/Microsoft.Insights/components/appi-lac-hidex-qa-w2/overview))


Step # 3:
After you click the link you'll be landed in the portal for Microsoft Azure. On the left menu, click "Monitoring" to expand the menu.

![image.png](/.attachments/image-05e4309b-4ef5-4c7d-abfd-2fba4328ef83.png)