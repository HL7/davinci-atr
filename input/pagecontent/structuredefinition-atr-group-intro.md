### Introduction

This profile represents an instance of Member Attribution List. The resource instance contain information related to members who are attributed to a specific individual provider or a provider organization. The instance may also contains information about the contract, settlement entity details. In addition, NPI and TIN of the consumer (provider) organization may be contained within the instance. Attribution information such as the attributed period, attributed provider is also contained within the group resource. Members may be added or removed from the member attribution list. Group.member has a cardinality of 0..* because  Groups may have zero members when they are initially created and members get added at a later point in time. The Group.member.inactive flag is used to indicate that the patient is no longer part of the Member Attribution List.


**Implementation Requirements**

Implementers are advised to read [Data Model Requirements](spec.html#member-attribution-list-data-model-requirements) to implement the Group profile and create a Member Attribution List.


**APIs : Retrieval of Group Resource Instance:**

The Group instance is retrieved using search parameters outlined in the [Group discovery APIs](spec.html#consumer-identifies-relevant-member-attribution-list-in-producers-system-discovery-of-group-resource). 

The retrieved Group resource instance which represents the Member Attribution List has member and other related resource references. In order to retrieve the complete Member Attribution List information including member, coverage, attributed provider information a Bulk API request is initiated on the retrieved Group resource. 

**Handling Large Groups** 

Groups which have large number of members (for e.g > 100,000) end up consuming a large number of resources on server, client and the network to retrieve the Group either using search mechanisms or read mechanisms. In order to limit the amount of data being returned by the server the following requirements are being levied.

	* All Group search operations or read operations should use the _summary=true parameter. This parameter will only return teh summary of the Group resource and does not include any members. This makes the operation light weight for clients and severs. 
	
	* Once the Group is received, the client can perform the atr-export operation on the Group resource which will create a NDJSON file for the Group itself. In this case the NDJSON file will only contain a single line with a large number of data based on the number of members present in the Group.
	
	* NOTE: There is discussion on creating a new operation to page the Group resource based on the number of data elements. When this is made available, the IG will be revised to use the method for Group searches and reads without the _summary parameter. 

