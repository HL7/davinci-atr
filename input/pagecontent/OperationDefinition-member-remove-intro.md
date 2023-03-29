{:.stu-note}
This is new content for the STU 2 ballot.


### Introduction

This operation is used to remove a member along with the attributed provider from the Member Attribution List.
This allows the consumer (client) to remove members from the Group during the reconciliation process.


**Implementation Requirements**

The following combinations of parameters SHALL be supported by the server implementing the operation.

* MemberId only - (Removes all attributions for the Member specified by the MemberId) 
* MemberId + ProviderNPI - (Removes all attributions for the combination of Member and Provider specified)
* patientReference - (Removes all attributions for the Member) 
* patientReference + providerReference - (Removes all attributions for the combination of Member and Provider specifeid)
* patientReference + providerReference + coverageReference - (Removes the attribution for the combination of Member and Provider and Coverage resources)


**APIs : Member Remove :**

POST [Base FHIR Url]/Group/[id]/$member-remove

