### Introduction

This profile is used to associate a specific coverage instance to a specific member who is on the Member Attribution List.
Since patients can have multiple coverages, it is important to identify the specific coverage instance that led to the patient being on the Member Attribution List. The Coverage instance will contain the member information, payer information and the plan information.


**Implementation Requirements**

Implementers are advised to read [Data Model Requirements](spec.html#member-attribution-list-data-model-requirements) to implement the Coverage profile.


**APIs : Retrieval of Coverage Resource Instance:**

The Coverage instance is retrieved as part of the Bulk API request on the Group resource representing the Member Attribution List. 

