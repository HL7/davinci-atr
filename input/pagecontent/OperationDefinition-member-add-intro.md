{:.stu-note}
This is new content for the STU 2 ballot.


### Introduction

This operation is used to remove a member along with the attributed provider from the Member Attribution List.
This allows the consumer (client) to remove members from the Group during the reconciliation process.


**Implementation Requirements**

Implementers are advised to read [Data Model Requirements](spec.html#member-attribution-list-data-model-requirements) to implement the Attribution list.

The following combinations of parameters SHALL be supported by the server implementing the operation.

* MemberId + ProviderNPI - (Adds the member and the attributed provider to the Attribution List).
* MemberId + ProviderNPI + attributionPeriod - (Adds the member, attributed provider and the attribution period to the Attribution List).
* patientReference + providerReference - (Adds the member and the attributed provider to the Attribution List).
* patientReference + providerReference + attributionPeriod - (Adds the member, attributed provider and the attribution period to the Attribution List). 


**APIs : Member Add :**

POST [Base FHIR Url]/Group/[id]/$member-add

