Monitoring
- find data sources to query
  - messagebox, suspends, ports
    - update ports (onboarded EDI provider ports)
- 

Troubleshooting
- Party properties
  - Check parties (thumbprint)
- MessageBox queries
  - suspended messages
  - Active messages


# work items 
Develop sql query to see:
- suspends
- active
- parties (thumbprint)
- views should be in 1 place instead of needing to login to every server
  - sqlp6.support(?)

monitoringConfigure BHM 
- daily 6am health check (mbvoutput)
- live monitoring
  - check for when receive/send ports + host instances go down based on rules (some ports should stay down)
- adjust ntst smoke pipelines (direct calls to netsmart/clientservices) to hourly runs

regular tasks
- onboarding
  - add ps1(?) sql query to verify record is in db
    - https://dev.azure.com/lacdmh-integrationservices/EDI/_releaseDefinition?definitionId=12&_a=definition-tasks&environmentId=55

source
- https://dev.azure.com/lacdmh-integrationservices/Support/_git/Support?path=/queries&version=GBadd-biztalk-support-resources

360 cleanup
- decommission app server
- archive db