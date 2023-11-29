

### Introduction

This operation is used to add a member along with the attributed provider to the Member Attribution List.
This allows the consumer (client) to add members to the Group during the reconciliation process.


**Implementation Requirements**

The following combinations of parameters SHALL be supported by the server implementing the operation.

* memberId + providerNpi: Adds the member and the attributed provider to the Attribution List
* memberId + ProviderNpi + attributionPeriod: Adds the member, attributed provider and the attribution period to the Attribution List
* patientReference + providerReference: Adds the member and the attributed provider to the Attribution List
* patientReference + providerReference + attributionPeriod: Adds the member, attributed provider and the attribution period to the Attribution List

Similar to any FHIR operation, Consumers need to obtain authorization to successfully invoke the operation. 

#### Effect of Attribution List Status on the member-add operation

* The Producer **SHALL** allow the member-add operation only when the attribution list status is "draft". 

* When the attribution list status is "final" the Producer **SHALL** reject the operation with appropriate OperationOutcome.


**APIs : Member Add :**

POST [Base FHIR Url]/Group/[id]/$member-add

Producers **SHALL** return values from the operation as per the [FHIR Operation Response Specification](https://hl7.org/fhir/operations.html#response).

