[[_TOC_]]

## FHIR terminology
see FHIR [Terminology module](http://hl7.org/fhir/terminology-module.html).

## Design considerations

- Map LA County concepts and values to Netsmart.
- Augment LA County FHIR resources with custom terminology.

## Design recommendations

- Consider using FHIR `ValueSets` to define your own custom terminology.
- Consider using FHIR `ConceptMap` resource to map your terminology to Netsmart.
- Currently the Azure Health Data Service does not support a terminology service. Consider implementing your own [`$translate`](https://hl7.org/fhir/conceptmap-operation-translate.html) endpoint as another Azure Function in the FHIR Proxy and add your custom business logic.
    - Consider following the specification for the query and response signatures.