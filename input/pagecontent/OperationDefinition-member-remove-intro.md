


### Introduction

This operation is used to remove a member along with the attributed provider from the Member Attribution List.
This allows the consumer (client) to remove members from the Group during the reconciliation process.


**Implementation Requirements**

The following combinations of parameters SHALL be supported by the server implementing the operation.

* memberId only: Removes all attributions for the Member specified by the MemberId 
* memberId + providerNpi: Removes all attributions for the combination of Member and Provider specified
* patientReference: Removes all attributions for the Member 
* patientReference + providerReference: Removes all attributions for the combination of Member and Provider specified
* patientReference + providerReference + coverageReference: Removes the attribution for the combination of Member and Provider and Coverage resources

#### Effect of Attribution List Status on the member-remove operation

* The Producer **SHALL** allow the member-remove operation only when the attribution list status is "draft" or "open".

* When the attribution list status is in a "draft" status, member-remove operations will change the member's active flag to false, indicating the the member is going to be removed from the list, however as part of the data exchange the member **SHALL** be included in the list as long as the status is draft.

* Once the list has a status of final, the producer **SHOULD** remove the inactive members from the list and may only retain the active members. 

* When the attribution list status is "open", the Producer **SHOULD** remove the member from the list when a member-remove operation is invoked.

* When the attribution list status is "final" the Producer **SHALL** reject the operation with appropriate OperationOutcome.


**APIs : Member Remove :**

POST [Base FHIR Url]/Group/[id]/$member-remove

Producers **SHALL** return values from the operation as per the [FHIR Operation Response Specification](https://hl7.org/fhir/operations.html#response).

