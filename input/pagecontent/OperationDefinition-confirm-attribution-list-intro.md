{:.stu-note}
This is new content for the STU 2.


### Introduction

This operation is used to indicate to a Producer that the Consumer does not have any more changes to be made to the Attribution List using the reconciliation APIs member-add and member-remove.

**Implementation Requirements**

When the method is invoked by the Consumer, the Producer acknowledges the operation with a HTTP status code of 201 Accepted.
The Producer may change the status of the Attribution List to "final" indicating that no more changes will be made via the member-add and member-remove APIs. The Producer may make additional changes to the Attribution List before changing the status to final.
Similar to any FHIR operation, Consumers need to obtain authorization to successfully invoke the operation. 

**APIs : Confirm Attribution List :**

POST [Base FHIR Url]/Group/[id]/$confirm-attribution-list

Producers **SHALL** return values from the operation as per the [FHIR Operation Response Specification](https://hl7.org/fhir/operations.html#response)
