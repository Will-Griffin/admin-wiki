Integration Services Project prioritization

1. HIDEX/FHIR - The Healthcare Information Data Exchange (HIDEX) provides a common platform for DPH and DMH to exchange Fast Healthcare Interoperability Resources (FHIR) compliant messages/services and Electronic Data Interchange (EDI) files with mutual contract providers. 
 – dependency for Modernization project (stand up baseline functionality)
   - Netsmart FHIR Implementation - custom mapping for service gaps and data mapping
     - Dictionary service api updates to add additional fhir/netsmart mappings
   - GoAnywhereMFT - Replace Globalscape Electronic File Transfer (EFT)
   - Onboarding Pilot and Provider data load
   - Soap Proxy (Replacement for legacy apis CS, SRL, EPSDT, etc.)
   - Fhir proxy (Custom validation and routing)

2. CalAIM BHQIP - The CalAIM Behavioral Health Quality Improvement Program (BHQIP) is an incentive payment program designed to support Mental Health Plans (MHP), Drug Medi-Cal State Plans (DMC), and Drug Medi-Cal Organized Delivery Systems (DMC-ODS) as they prepare for changes under the California Advancing and Innovating Medi-Cal (CalAIM) initiative. BHQIP allows counties to earn incentive payments by achieving certain milestones related to CalAIM.
   - BHQIP milestone 3B deliverables:
     - Provider Directory api, documentation, survey and reporting metrics
     - Patient Access api, documentation, survey and reporting metrics
   - ECM SFTP support - facilitate data exchange using the Secure File Transger Protocol (SFTP)
3. SOGI - Add Sexual Orientation and Gender Identity related fields to comply with Board mandate.
   - updates to FHIR and soap proxy apis
   - updates to legacy CS (new wsdl) api
   - updates to Master Data Management (MDM) web service
4. Access Center Modernization FHIR customization & Support - Modernize business processes, workflows and technology for the 24/7 ACCESS Call Center in order to improve client care delivery, reducing time‐to‐care and streamline call agent
experience.
   - Azure Cloud Infrastructure changes
   - MDM changes - Update service logic to send messages to D365
   - Update FHIR Proxy logic to handle scheduling-related resources 
   - Sync data between IBHIS and FHIR data stores
   - PMRT case api - customize FHIR resources to allow collection of data
5. Client Services Information (CSI) Assessment Record web service updates:
   - SR#753909_Capture initial medication evaluation data & Apply logic for business rule
   - SR#748178_Connect SRTS data with CSI Assessment webservice data elements
   - Requires update to base library used by all apis (BizTalk Infrastructure changes).
6. SRL - Service Request Log
7. CalHHS Interoperability

Not ranked:
- NACT EDI274 Integration support - Assist with processing Provider Directory data into EDI X12 274-file to DHCS.
- ReadyAPI Transition to Postman (Ongoing) - convert test suites from ReadyAPI testing tool to use Postman api testing to reduce licensing costs
- MPKI Replacement - Replace current MPKI solution with new vendor/platform.
- Service Bus - Implement Service Bus technology

- Support for EDI Claiming - Process EDI X12 837, 277, TA1 and 835-files to support claiming.
- Support for Prescriber Benefits Management (PBM) services - Process prescriber data and EDI X12834-file between DMH and PBM vendor, Magellan (now Prime Therapeutics)
- Support for legacy BizTalk apis: Client Services (CS), EPSDT, CS
- Security SQL scan/remediation
- Security ISD remediation - Address and remediate vulnerabilities found during ISD security scan.
- Imprivata - SFTP support with vendor to send and receive Fairwarning audit log data for compliance.
- Health Access and Integration Support - SFTP and automation services.
- Treasurry Tax Collector Department/DMH Central Business Office (CBO) support - Encrypt/Decrypt Bank of America ACH files and support SFTP.
- DMH Enterprise Assessment - Standardize Integration business processes.
- NOAD
- School based exchange