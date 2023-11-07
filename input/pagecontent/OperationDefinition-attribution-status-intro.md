
### Introduction

This operation is used to retrieve the attribution status for a specific member. 
This allows the consumer (client) to retrieve member attribution status as part of work flows.


**Implementation Details**

The client (consumer) can pass a memberId or a patientReference which is a Reference to the patient resource in the Producer's system when querying for the attribution data. The Producer is supposed to return the attribution data for the individual member in a Bundle as part of the return value from the operation. If the member is not part of the Group or the client does not have appropriate privileges to query the Group, then an appropriate OperationOutcome would need to be returned. 

**APIs : Attribution Status :**

POST [Base FHIR Url]/Group/[id]/$attribution-status

