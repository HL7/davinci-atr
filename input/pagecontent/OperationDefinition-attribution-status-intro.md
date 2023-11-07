
### Introduction

This operation is used to retrieve the attribution status for a specific member. 
This allows the consumer (client) to retrieve member attribution status as part of work flows.


**Implementation Details**

The client (consumer) can pass a memberId or a patientReference which is a Reference to the patient resource in the Producer's system when querying for the attribution data. The Producer is supposed to return the attribution data for the individual member in a Bundle as part of the return value from the operation. If the member is not part of the Group or the client does not have appropriate privileges to query the Group, then an appropriate OperationOutcome would need to be returned. 
Similar to any FHIR operation, Consumers need to obtain authorization to successfully invoke the operation. 

**APIs : Attribution Status :**

POST [Base FHIR Url]/Group/[id]/$attribution-status

Producers **SHALL** return values from the operation as per the [FHIR Operation Response Specification](https://hl7.org/fhir/operations.html#response).

The returned resource from the above operation is a Bundle resource which contains [Member Attribution List Data](usecases.html#member-attribution-list-workflows-and-definitions) for a specific patient.

