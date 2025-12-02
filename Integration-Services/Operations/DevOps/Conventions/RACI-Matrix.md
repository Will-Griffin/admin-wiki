## Overview
RACIs clearly lay out roles and responsibilities for activities bringing clarity to who is doing what. This document outlines standards for RACIs existing in ADO DevOps since there is a broad range of stakeholders making updates. Standards are intended to ensure the RACI is updated using criteria that is harmonized across all roles and delivery methodologies. 

|Activities |[Scrum Master](Role-Definitions.md#Scrum-master) |[Product Owner](/DevOps/Conventions/Role-Definitions.md#Product-Owner) |[Dev Lead](Role-Definitions.md#Dev-Lead) |[Dev Team](Role-Definitions.md#Dev-Team-Member) |[Business Analysts](Role-Definitions.md#Business-Analyst) | MCS Dev Team |MCS PjM |MCS Architect |
|--|--|--|--|--|--|--|--|--|
|Daily Scrum | R | A | A | C | I | C | C | C |
|Sprint Planning | C | R | A | C | C | C | C | C |
|User Stories - Prioritization             | C | R | C |
|User Stories - Create Description         | C | R | A |
|User Stories - Define Acceptance Criteria | C | R | A |
|Tasks Creation                            | I | R | A |
|Task Execution                            | I | I | C | R
|Define Business Logic                     | I | 
|Map Business domain to FHIR               | I | 
|Map SOAP to FHIR                          | I |
|Map LACO FHIR to NetSmart FHIR            | I | 


## RACI Attributes
### Responsible (R)
	1. Responsible role(s) execute the activity.
	2. Every RACI should have at least 1 role that is Responsible.
	3. This role should be limited to no more than 2 roles to add clarity and avoid confusion.
	4. If a role is listed as Responsible, it should not have Consulted or Informed since the role is actively involved.
### Accountable (A)
	1. The Accountable role ensures the activity gets done.
	2. Only one role should be Accountable.
	3. Every activity should have an Accountable role.
### Consulted (C)
	1. Consulted role(s) should be engaged for input before or while the activity is being worked on or a decision is being made.
	2. These role(s) will provide helpful and meaningful inputs to the activity and may need to execute a set of tasks to this end.
	3. It is a two-way communication between the role(s) doing the activity and the role(s) consulted.
	4. If a role is listed as Consulted, it should not have Responsible or Informed.
### Informed (I)
	1. Informed role(s) have no active participation in the activity but need to be aware when the activity is complete and/or decisions made.
	2. It is a one-way communication from the role Responsible to those Informed.
	3. If a role is listed as Informed, it should not be Accountable or Responsible.