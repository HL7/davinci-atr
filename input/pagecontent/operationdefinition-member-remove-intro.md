{:.stu-note}
This is new content for the STU 2 ballot. 

### Introduction

This operation is used to add a member along with the attributed provider to the Member Attribution List.
This allows the consumer (client) to add members to the Group during the reconciliation process.


**Implementation Requirements**

Implementers are advised to read [Data Model Requirements](spec.html#member-attribution-list-data-model-requirements) to implement the Attribution list.

The following combinations of parameters SHALL be supported by the server implementing the operation.

* MemberId only - (Removes all attributions for that Member) 
* MemberId + ProviderNPI - (Removes all attributions for the combination of Member and Provider)
* patientReference - (Removes all attributions for that Member) 
* patientReference + providerReference - (Removes all attributions for the combination of Member and Provider)
* patientReference + providerReference + coverageReference - (Removes the attribution for the combination of Member and Provider and Coverage resources)


**APIs : Member Add :**

POST [Base FHIR Url]/Group/[id]/$member-remove
