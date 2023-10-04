This section of the implementation guide defines the specific conformance requirements for systems wishing to conform to this Member Attribution List  implementation guide.  The bulk of it focuses on the implementation of  the [Bulk Data IG]({{site.data.fhir.ver.bulkig}}/index.html) to meet attribution list use-cases.  It also describes the use of [SMART on FHIR Backend Services Authorization]({{site.data.fhir.ver.smartapplaunch}}/index.html) and provides guidance on privacy, security and other implementation requirements.


### Context

#### Pre-reading
Before reading this formal specification, implementers should first familiarize themselves with two other key portions of the specification:

* The [Use Cases & Overview](usecases.html) page provides context for what this formal specification is trying to accomplish and will give a sense of both the business context and general process flow enabled by the formal specification below.

* The [Technical Background](background.html) page provides information about the underlying specifications and indicates what portions of them should be read and understood to have necessary foundation to understand the constraints and usage guidance described here.


#### Conventions
This implementation guide uses specific terminology to flag statements that have relevance for the evaluation of conformance with the guide:

* **SHALL** indicates requirements that must be met to be conformant with the specification.

* **SHOULD** indicates behaviors that are strongly recommended (and which may result in interoperability issues or sub-optimal behavior if not adhered to), but which do not, for this version of the specification, affect the determination of specification conformance.

* **MAY** describes optional behaviors that are free to consider but where the is no recommendation for or against adoption.


#### Systems

This implementation guide sets expectations for two types of systems:

* **Producer systems** are typically Payer systems but could theoretically be any system responsible for producing a Member Attribution List. These systems typically act as servers. 

* **Consumer systems** are typically Provider systems that act on behalf of provider organizations who retrieve the attribution list from Producer. These systems typically act as clients.

The requirements and expectations described here are not intended to be exhaustive. Producers and Consumers could potentially support additional resources and extensions, etc.  The purpose of this implementation guide is to establish a baseline of expected behavior and data elements that communication partners can rely on and then build from.  Future versions of this specification will evolve based on implementer feedback.

#### Claiming Conformance 

Producers and Consumers asserting conformance to this implementation guide have to implement the requirements outlined in [Producer Capability Statement](CapabilityStatement-atr-producer.html) and [Consumer Capability Statement](CapabilityStatement-atr-consumer.html) respectively. The following definition of MUST SUPPORT is to be used in the implementation of the requirements.

##### MUST SUPPORT Definition

* Producers SHALL be capable of populating all data elements as specified by the profiles and are returned using the specified APIs in the capability statement.
* Consumers SHALL be capable of processing resource instances containing the MUST SUPPPORT data elements without generating an error or causing the application to fail. In other words Consumers SHOULD be capable of displaying the data elements for human use or storing it for other purposes.
* In situations where information on a particular data element is not present and the reason for absence is unknown, Producers SHALL NOT include the data elements in the resource instance returned from executing the API requests.
* When accessing Member Attribution Lists, Consumers SHALL interpret missing data elements within resource instances as data not present in the Producer's system.


#### Profiles
This specification makes significant use of [FHIR profiles]({{site.data.fhir.path}}profiling.html), search parameter definitions and terminology artifacts to describe the content to be shared as part of Member Attribution List interactions. The implementation guide is based on FHIR [R4]({{site.data.fhir.path}}) and profiles are listed for each interaction. 

The full set of profiles defined in this implementation guide can be found by following the links on the [FHIR Artifacts](artifacts.html) page.


#### US Core
This implementation guide also leverages the [US Core]({{site.data.fhir.ver.uscoreR4}}/index.html) set of profiles defined by HL7 for sharing non-veterinary EMR individual health data in the U.S.  Where US Core profiles exist, this Guide either leverages them directly or uses them as a base for any additional constraints needed to support the member attribution list use cases.  If no constraints are needed, this IG doesn't define any profiles.

Where US Core profiles do not yet exist (e.g. for Coverage, Group), profiles have been created that try to align with existing US Core profiles in terms of elements exposed and terminologies used.

<div class="bg-success" markdown="1">

#### Requirements for Implementation of the $davinci-data-export operation
 
The Bulk Data Export async pattern is used by this IG for the implementation of the davinci-data-export operation. The actual Bulk Data export operation is not directly used in this IG.

Producer systems SHALL support the [$davinci-data-export operation](OperationDefinition-davinci-data-export.html) operation for member attribution list implementation. 

Producer systems SHALL support the exportType of ```hl7.fhir.us.davinci-atr``` for implementing Member Attribution List IG.

Producer systems SHALL export only the patients contained in the identified group if a list of member references are supplied as part of the [$davinci-data-export operation](OperationDefinition-davinci-data-export.html) operation.

When member references are not supplied, the Producer systems SHALL export data for all members contained in the Member Attribution List. 

Producer systems SHALL support the reading and searching of Group resources per the capability statement expectations outlined below.

Producer systems SHALL support ```Group,Patient,Coverage,Practitioner,Organization``` as resource types for the ```[base]/Group/[id]/$davinci-data-export?resourceTypes``` parameter for the exportType of ```hl7.fhir.us.davinci-atr```. 

Producer systems SHOULD support ```Related Person, PractitionerRole, Location``` resource types for the ```[base]/Group/[id]/$davinci-data-export?resourceTypes``` parameter for the exportType of ```hl7.fhir.us.davinci-atr```. 

Producer systems SHALL reject requests that do not contain the minimum resource types of ```Group,Patient,Coverage,Practitioner,Organization``` as resource types for the ```[base]/Group/[id]/$davinci-data-export?resourceTypes``` parameter for the exportType of ```hl7.fhir.us.davinci-atr```.

* The producer SHALL create NDJSON files for each of the resources that are linked to the member to create an attribution list as outlined below 

The resource list includes
 
	The Patient who is the member.
	The Coverage which resulted in the Patient being a member of the Group
	The Organization to which the Patient is attributed to as part of the attribution list.
	The Practitioner or PractititonerRole that the patient is attributed to as part of the attribution list
	The RelatedPerson who may be the Subscriber of the Coverage. 
	The Group itself which contains the list of members and their relationship to the other members.  

Producer systems SHALL support the Bulk Data Kick-off Request for the [$davinci-data-export operation](OperationDefinition-davinci-data-export.html) as defined in the [Bulk Data IG]({{site.data.fhir.ver.bulkig}}/index.html) export operation specification.

Producer systems MAY support the Bulk Data Delete Request for the [$davinci-data-export operation](OperationDefinition-davinci-data-export.html) as defined in the [Bulk Data IG]({{site.data.fhir.ver.bulkig}}/index.html) export operation specification.

Producer systems SHALL support the Bulk Data Status Request for the [$davinci-data-export operation](OperationDefinition-davinci-data-export.html) as defined in the [Bulk Data IG]({{site.data.fhir.ver.bulkig}}/index.html) export operation specification.

Producer systems SHALL set the requireAccessToken to ```true``` within the Bulk Data Status Request response body as defined in the [Bulk Data IG]({{site.data.fhir.ver.bulkig}}/index.html) export operation specification.

Producer systems SHALL require Consumer systems to provide valid ```access token``` to access the member attribution list files. 

Producer systems SHALL support the Bulk Data File Request for the [$davinci-data-export operation](OperationDefinition-davinci-data-export.html) as defined in the [Bulk Data IG]({{site.data.fhir.ver.bulkig}}/index.html) export operation specification.

When the Consumer systems do not have appropriate authorization to the data requested, the Producer systems SHALL return OperationOutcome with appropriate error message.

When the Consumer systems do not have appropriate access token to access the data requested, the Producer systems SHALL return OperationOutcome with appropriate error message.




#### SMART on FHIR Backend Services Authorization

This section outlines how the SMART on FHIR Backend Services Authorization will be used by this implementation guide. 

Producer systems SHALL advertise conformance to SMART Backend Services by hosting a Well-Known Uniform Resource Identifiers (URIs) as defined in the [SMART on FHIR Backend Services Authorization]({{site.data.fhir.ver.smartapplaunch}}/backend-services.html) specification.

Producer systems SHALL include token_endpoint, scopes_supported, token_endpoint_auth_methods_supported and token_endpoint_auth_signing_alg_values_supported as defined in the [SMART on FHIR Backend Services Authorization]({{site.data.fhir.ver.smartapplaunch}}/backend-services.html) specification.

Consumer systems SHALL share their JWKS with the Producer systems using URLs as defined in the [SMART on FHIR Backend Services Authorization]({{site.data.fhir.ver.smartapplaunch}}/backend-services.html) specification.

Consumer systems SHALL obtain the access token as defined in the [SMART on FHIR Backend Services Authorization]({{site.data.fhir.ver.smartapplaunch}}/backend-services.html) specification.

Producer systems SHALL support ```system/*.read`` scopes for Member Attribution List exchange.

Producer systems supporting the creation and reconciliation of a Member Attribution List by Consumer systems SHOULD also support the ``system/*.write`` scope for Member Attribution List exchange.

During Consumer registration, the Producer system  MAY collect the NPI and Tax Identification Numbers applicable for a specific contract along with the specific contract information. This information MAY be used by the Producer to create the necessary Member Attribution List and provide an API that will allow the Consumer to retrieve the Member Attribution List. Producers MAY follow other OAuth best practices for Consumer registration.

When the Consumer is trying to discover the specific Group resource that represents the Member Attribution List for a specific use case, the Producer SHALL verify that the Consumer credentials provided allow the Consumer to access the requested specific Group Resource. 

**NOTE:** This verification is for a specific Group instance and not just the Group Resource type which is controlled by the scopes.


</div>


#### Capability Statements
This section lists the capability statements for Producer and Consumer systems.

##### Producer Systems

The Producer specific requirements for REST interactions, operations, profiles and search parameters to be supported are outlined in the [Producer Capability Statement](CapabilityStatement-atr-producer.html). 



##### Consumer Systems

The Consumer specific requirements for REST interactions, operations, profiles and search parameters to be supported are outlined in the [Consumer Capability Statement](CapabilityStatement-atr-consumer.html).


### Member Attribution List Data Model requirements

The section outlines specific requirements that need to be followed in creating the Member Attribution List.

#### Representing Contracts

* Producers SHALL create one Member Attribution List represented by an instance of Group Resource. There will be exactly one Group Resource instance per Contract between a Payer and a Provider.

* Producers SHALL ensure the combination of Member Identifier, Payer Identifier, Contract Identifier and Plan Identifier are unique. 
 
* Producers SHALL include the Contract Identifier within the Group.identifier element during the creation of the Member Attribution List.

* Producers SHALL make available the Group resource for Consumers for at least the duration of the contract in compliance with applicable regulations and policies. 

* Producers SHALL create new versions of Group resource instances as data in the Group (Members, Attributed periods, coverage references, attributed providers) change. Producers may or may not retain older versions of the Group based on their instance version scheme. In some instances Producers may choose a version scheme based on agreements with Consumers. When queried by the Consumers, Producers SHALL return the latest version of the Group resource instance unless a specific version is queried.

* Producers SHALL represent the validity period of the contract in the Group.contractValidityPeriod extension.


#### Representing Plans and Coverage

* Producers SHALL include the Plan Identifier in Coverage.class data element during the creation of the Member Attribution List.

* Producers SHALL include the Coverage that is associated with the member in the Member Attribution List as part of the Group.member.anyReference data element.

#### Handling Identifiers

* Producers SHALL include settlement entity names, ACO identifiers in Group.identifier during the creation of the Member Attribution List. This is helpful for Consumers to discover the Group using a single settlement entity name and/or an ACO identifier. 

* Producers SHALL include the provider NPI and/or TIN in Group.identifier field during the creation of the Member Attribution List. These identifiers are used by Consumers to discover the Group Resource using their own NPI and/or TIN.

* When Member Identifiers are present, Producers SHALL include the Member Identifier in the Coverage.identifier.


#### Handling Attribution Period and Attributed Providers

* Producers SHALL include the attribution period in the Group.member.period data element. This indicates the period over which the member is attributed to the provider.

* When members get attributed to different providers during the same contract for different providers, Producers SHALL include the member multiple times in the Member Attribution List, once for each provider with whom the member is attributed including their attribution period. 

* When members are not attributed to a provider or an organization, Producers MAY attribute the member to the Settlement Entity organization which is responsible for the contract. Producers SHALL include the attribution period in the Group.member.period element. 

* Producers SHALL include the contract validity period in Group.extension (membershipValidityPeriod) data element.

* Producers SHALL set ```Group.member.inactive = true``` when the member is no longer attributed.

* Producers SHALL set ```Group.member.extension.ext-changeType = dropped``` when the member is no longer attributed.

* Producers SHALL set  ``Group.member.extension.ext-changeType = new``` when a member is added to the attribution list for the first time.

* Producers SHOULD set  ``Group.member.extension.ext-changeType = changed``` when a members information has changed.

* Producers SHOULD set  ``Group.member.extension.ext-changeType = nochange``` when a members information has not changed from the previous version of the attribution list.


#### Security and Privacy considerations on Identifiers

* Producers SHOULD exchange Provider NPI and TIN only as needed and when the NPIs and TINs belong to providers associated with the receiving organization.

* Consumers SHOULD NOT be sharing the NPI and TIN information amongst providers unless required for transactions related to Payments, Treatment and Operations (PTO).


### Member Attribution List Exchange Interactions Details and APIs

#### Consumer identifies relevant Member Attribution List in Producer's system (Discovery of Group Resource)

This interaction outlines the APIs for a Consumer (for example, Provider organization) to discover the Group Resource in a Producer's system ( for example, Payer organization).This Group resource represents the Member Attribution List that has been created by the Producer based on a contract between the Producer and the Consumer.
For example, Multicare a Provider Organization would like to identify the Member Attribution List that a Payer organization (e.g Cambia Health Systems) has created based on a contract between Cambia and Multicare.

**Precondition:**

In order to discover the appropriate Group Resource (Member Attribution List) the Consumer is expected to know its own NPI and/or Tax Identification Number or Contract Identifier or Settlement Entity Identifiers. Producers and Consumers may exchange this information during the contract establishment. Similarly Producers may provide the name of the Group resource representing the Member Attribution List that can be retrieved by the Consumer. 
Note: Producers and Consumers MAY have a predetermined cadence on exchanging member attribution lists and this API could be invoked based on the cadence.

**API: Discover Group using NPI and TIN**

```

GET <Server Base URL>/Group?identifier:of-type=http://terminology.hl7.org/CodeSystem/v2-0203|NPI|<ExampleNPI>&identifier:of-type=http://terminology.hl7.org/CodeSystem/v2-0203|TAX|<ExampleTIN>&_summary=true

```

In the above API, notice the use of "of-type" modifier on the search to allow searching based on type which includes a CodeSystem and a Value. In addition the “<ExampleNPI>" and "<ExampleTIN>” will be substituted with the values that represent the Consumer organization.

The Producer verifies the client credentials according to the SMART Backend Services Authorization protocols and in addition verifies that the Consumer is allowed to access the specific Member Attribution List and returns one or more Group Resources representing the Member Attribution Lists for each contract between the Producer and the Consumer.

NOTE: In order to avoid issues with servers, clients and networks when Group resources are large, Consumers **SHOULD** include the _summary=true parameter in all Group search and read operations. Servers **SHOULD** support the _summary parameter and provide only the Group summary without the member data as per the resource definition.  

**API: Discover Group using NPI or TIN**


```

GET <Server Base URL>/Group?identifier=http://terminology.hl7.org/CodeSystem/v2-0203|<NPI or TAX>|<ExampleNPI or ExampleTIN>&_summary=true

```


**API: Discover Group using Identifiers (Contract Identifier or Settlement Entity Identifier)**


```

GET <Server Base URL>/Group?identifier=http://example.org|<Identifier Value>&_summary=true

```


**API: Discover Group using Name**


```

GET <Server Base URL>/Group?name=myorg&_summary=true

```


**Expected Result:**

Consumer receives one or more Group Resources from the above API call(s). Each Group Resource represents a specific Member Attribution List between the Producer and the Consumer. To narrow down the specific Member Attribution List for a specific contract the Consumer has to examine the ```Group.identifier``` and ```Group.contractValidityPeriod``` element and compare the contract information. An example resource retrieved by the above discovery APIs can be found at [Group Example](Group-fullexample.html).


#### Consumer requests Member Attribution List from Producer's system (Member Attribution List Export Request - Bulk Data Request)

This interaction outlines the APIs for a Consumer (Provider) organization to request the full Member Attribution List that is applicable to their specific organization for a specific contract.
**Note:** The request has to be accepted by the Payer and eventually a Member Attribution List would be made available. This is an asynchronous request following Bulk Data IG specifications.

For example, Multicare would like to request the Member Attribution List details from Cambia Health Systems for a specific contract. 

**Precondition:** 

Provider Organization knows the specific Group Resource for the specific contract that represents the Member Attribution List from executing the discovery of group resource API outlined previously.


**API:**

```

GET or POST <Server Base URL>/Group/[Group id]/$davinci-data-export?resourceTypes=GRoup,Patient,Practitioner,PractitionerRole,Organization,Location,Coverage,RelatedPerson&exportType=hl7.fhir.us.davinci-atr 

OR 

GET or POST <Server Base URL>/Group/[Group id]/$davinci-data-export?resourceTypes=GRoup,Patient,Practitioner,Organization,Coverage&exportType=hl7.fhir.us.davinci-atr


```

NOTE: Any other combination of resourceTypes are not valid for the exportType of hl7.fhir.us.davinci-atr.

**Expected Results:**
Request is accepted by the Producer and a Content Location is received as part of the Response. Detailed examples for Bulk Data Request can be found in the Bulk Data IG.

#### Consumer polls the Content Location for Request Completion and Member Attribution List data location (Member Attribution List Export Request Polling - Bulk Data Poll Request)

This interaction outlines the APIs for a Consumer (Provider) organization to poll the Content Location received as part of Member Attribution List Export Request outlined previously. This polling is required to determine completion status of the export request. This would be repeated until the request is complete or cancelled following the Bulk Data IG specifications.

For example, Multicare would poll the content location received from Cambia as part of the Member Attribution List Export Request. 

**Preconditions:** 

* Consumer has requested the Member Attribution List export which has been accepted by the Producer.
* Consumer organization has the URL for the Content Location where the request status can be polled.

**API**

```

GET <Content Location from Member Attribution List Export Request>

```

**Expected Results:**

* The completion status of the Member Attribution List Export Request.
* Once the request is completed, a 200 HTTP code is returned along with the Response Body containing the URLs for the files representing the Member Attribution List.
* At least one URL is returned for each of the resource types specified using the resourceTypes parameter in the Member Attribution List Export Request which are Patient,Practitioner,PractitionerRole,Organization,Location,Coverage and RelatedPerson resources.
* Detailed examples for content polling can be found in the Bulk Data IG.

#### Consumer retrieves Member Attribution List from Producer (FHIR Request)

AThis interaction outlines the APIs for a Consumer (Provider) organization to retrieve each of the files that represent the Member Attribution List.

For example, Multicare retrieves each of the NDJSON files representing the Member Attribution List. 

**Precondition:**

Consumer has the URLs to retrieve the files representing the Member Attribution List from a successfully completed Member Attribution List Export Request. These URLs are obtained by executing the Member Attribution List Export Request Polling interaction until the request is completed.

**API:**

```

GET <File URL for each Resource identified in Member Attribution List Export Request completion response>

```

**Expected Results:**

* Retrieve the NDJSON files for each of the following resources.
* One or more NDJSON files for Group, Patient,Practitioner,PractitionerRole,Organization,Location,Coverage and RelatedPerson
* Detailed examples for NDJSON file retrieval can be found in the Bulk Data IG.


<div class="bg-success" markdown="1">

### Member Attribution List Reconciliation APIs

The following are the Member Attribution List Reconciliation APIs and their purpose

* [member-add](OperationDefinition-member-add.html) - Used to request addition a member and their attributed provider to an Attribution List.
* [member-remove](OperationDefinition-member-remove.html) - Used to request the removal of a member and their attributions from an Attribution List.
* [confirm-attribution-list](OperationDefinition-confirm-attribution-list.html) - Used to confirm that the reconciliation process is complete and there are no pending changes from the Consumer.
* [attribution-status](OperationDefinition-attribution-status.html) - Used to request attribution status for a specific member.

#### Example Scenarios demonstrating the use of reconciliation APIs

**Scenario 1** : A Consumer wants to add a specific patient to the Attribution List. 

The Consumer determines the patient's memberId and the NPI of the attributed provider and uses the [member-add](OperationDefinition-member-add.html) operation on the specific Group instance to add the member.

**Scenario 2** : A Consumer wants to remove a specific patient and their attributions from the Attribution List. 

The Consumer determines the patient's memberId and uses the [member-remove](OperationDefinition-member-remove.html) operation on the specific Group instance to remove the member.

**Scenario 3** : A Consumer wants to update the attribution associated with a specific patient 

Step 1: The Consumer determines the patient's memberId and uses the [member-remove](OperationDefinition-member-remove.html) operation on the specific Group instance to remove the member.

Step 2: Once the attributions are removed in Step 1, The Consumer determines the patient's memberId and the NPI of the attributed provider and uses the [member-add](OperationDefinition-member-add.html) operation on the specific Group instance to add the member.


**Scenario 4** : A Consumer wants to confirm that the Attribution List is final

The Consumer uses the [confirm-attribution-list](OperationDefinition-confirm-attribution-list.html) operation on the specific Group instance to indicate to the Producer that the list is final and no more changes will be requested by the Consumer.

**Scenario 5** : A Consumer wants to determine the status of attribution for a specific member

The Consumer determines the patient's memberId and uses the [attribution-status](OperationDefinition-attribution-status.html) operation on the specific Group instance to retrieve the attribution status of the patient.


#### Consumer requests addition of a member to the Member Attribution List 

This interaction outlines the APIs for a Consumer (for example, Provider organization) to add a member to the Member Attribution List.

**Precondition:**

In order to add a member to the Member Attribution List, the Consumer should have successfully discovered the attribution list.
The Consumer knows the MemberId and the AttributedProvider NPI or the references to the Member and the Attributed Provider in the Producer system. 
The attribution list status has to be "draft" for the reconciliation API of member-add to be allowed. 

**API: Add a member to the Member Attribution List**

The following combinations of parameters **SHALL** be supported by the server implementing the operation.

* MemberId + ProviderNPI - (Adds the member and the attributed provider to the Attribution List).
* MemberId + ProviderNPI + attributionPeriod - (Adds the member, attributed provider and the attribution period to the Attribution List).
* * patientReference + providerReference - (Adds the member and the attributed provider to the Attribution List).
* patientReference + providerReference + attributionPeriod - (Adds the member, attributed provider and the attribution period to the Attribution List).


* The Producers **MAY** decide to add the member based on the information provided and any additional information that is present in the Producer system. 
* If the Producer's adjudication process results in the member not being added, the Producer **SHALL** return an OperationOutcome with a message indicating the reason why the addition was not performed.


```

POST [Base FHIR URL]/Group/[id]/$member-add

The body will contain the parameters resources with combinations specified above.


```


**Expected Results:**

* Successful addition of the Patient to the Member Attribution List if the member and the provider is found in the system. 
* An OperationOutcome if the Patient to be added is not found in the system.
* An OperationOutcome if the Producer does not add the member to the attribution list.
* An OperationOutcome if the Attribution List is in a status of final.


#### Consumer requests removal of a member to the Member Attribution List 

This interaction outlines the APIs for a Consumer (for example, Provider organization) to remove a member from the Member Attribution List. The semantics of the member-remove operation based on the attribution list status is outlined at [Member Remove semantics.](OperationDefinition-member-remove.html)

**Precondition:**

In order to remove a member to the Member Attribution List, the Consumer should have successfully discovered the attribution list.
The Consumer knows the MemberId and the AttributedProvider NPI or the references to the Member and the Attributed Provider in the Producer system. 
The attribution list status has to be "draft" for the reconciliation API to be allowed.

**API: Remove a member to the Member Attribution List**

The following combinations of parameters **SHALL** be supported by the server implementing the operation.

* MemberId only - (Removes all attributions for the Member specified by the MemberId)
* MemberId + ProviderNPI - (Removes all attributions for the combination of Member and Provider specified)
* patientReference - (Removes all attributions for the Member)
* patientReference + providerReference - (Removes all attributions for the combination of Member and Provider specifeid)
* patientReference + providerReference + coverageReference - (Removes the attribution for the combination of Member and Provider and Coverage resources)

* The Producers **MAY** decide to remove the member based on the information provided and any additional information that is present in the Producer system. 
* If the Producer's adjudication process results in the member not being removed, the Producer **SHALL** return an OperationOutcome with a message indicating the reason the removal was not performed.



```

POST [Base FHIR URL]/Group/[id]/$member-remove

The body will contain the parameters resources with combinations specified above.
 

```


**Expected Results:**

* Successful removal of the Patient from the Member Attribution List if the member and the provider is found in the system. 
* An OperationOutcome if the Patient to be removed is not found in the system or the member attribution list. 
* An OperationOutcome is returned if the Producer decides not to remove the member.
* An OperationOutcome if the Attribution List is in a status of final.


#### Consumer indicates to the Producer that the Consumer is done with the reconciliation  

This interaction outlines the APIs for a Consumer to indicate to the Producer that the Consumer has finished the reconciliation process and has no pending changes. 

**Precondition:**

The Consumer and the Producer are already exchanging a specific Member Attribution List in draft form.

**API: Confirm Attribution List**

The operation does not require any parameters.

* The Producer **SHALL** return a status of 201 Accepted when the API is invoked. 

* The Producers **SHOULD** change the attribution list status to final from draft.

* Prior to changing the attribution list status to final, the Producer **MAY** make changes to the attribution list based on internal business processes and information.


```

POST [Base FHIR URL]/Group/[id]/$confirm-attribution-list

There are no parameters for the operation.
 

```


**Expected Results:**

* Successful acceptance of the operation with a HTTP status code of 201 Accepted. 
* Change the list status to final eventually by the Producer. 


</div>
