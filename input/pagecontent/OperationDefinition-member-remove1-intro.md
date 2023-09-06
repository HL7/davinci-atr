{:.stu-note}
This is new content for the STU 2 ballot. 

### Introduction

This operation is used to add a member along with the attributed provider to the Member Attribution List.
This allows the consumer (client) to add members to the Group during the reconciliation process.


**Implementation Requirements**

The following combinations of parameters SHALL be supported by the server implementing the operation.

* MemberId + ProviderNPI - (Adds the member and the attributed provider to the Attribution List).
* MemberId + ProviderNPI + attributionPeriod - (Adds the member, attributed provider and the attribution period to the Attribution List).
* patientReference + providerReference - (Adds the member and the attributed provider to the Attribution List).
* patientReference + providerReference + attributionPeriod - (Adds the member, attributed provider and the attribution period to the Attribution List). 


**APIs : Member Add :**

POST [Base FHIR Url]/Group/[id]/$member-add

