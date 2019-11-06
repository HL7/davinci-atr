This section of the implementation guide defines the specific conformance requirements for systems wishing to conform to this Risk Based Contracts Member Attribution List Exchange implementation guide.  The bulk of it focuses on the implementation of  the [Bulk Data IG](http://hl7.org/fhir/uv/bulkdata/index.html) to meet attribution list use-cases.  It also describes the use of [SMART on FHIR Backend Services Authorization](http://hl7.org/fhir/uv/bulkdata/authorization/index.html) and provides guidance on privacy, security and other implementation requirements.


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


#### Profiles
This specification makes significant use of [FHIR profiles]({{site.data.fhir.path}}profiling.html), search parameter definitions and terminology artifacts to describe the content to be shared as part of Memeber Attribution List interactions. The implementation guide supports two versions of FHIR: [STU3](http://hl7.org/fhir/STU3) and [R4]({{site.data.fhir.path}}) and profiles for both are listed for each interaction.  This version of the specification does not (yet) provide guidance for DSTU2 resources.

The full set of profiles defined in this implementation guide can be found by following the links on the [Artifacts](allartifacts.html) page.


#### US Core
This implementation guide also leverages the [US Core](http://hl7.org/fhir/us/core) set of profiles defined by HL7 for sharing non-veterinary EMR individual health data in the U.S.  Where US Core profiles exist, this Guide either leverages them directly or uses them as a base for any additional constraints needed to support the member attribution list use cases.  If no constraints are needed, this IG doesn't define any profiles.

Where US Core profiles do not yet exist (e.g. for Coverage, Group), profiles have been created that try to align with existing US Core profiles in terms of elements exposed and terminologies used.


#### Bulk Data IG 
This section outlines how the Bulk Data IG will be leveraged by this implementation guide. 



#### SMART on FHIR Backend Services Authorization
This section outlines how the SMART on FHIR Backend Services Authorization guide will be used by this implementation guide. 


#### Capability Statements
This section lists the capability statements for Producer and Consumer systems.

##### Producer Systems

* List operations , profiles, search parameters

##### Consumer Systems

* List operations , profiles, search parameters



### Member Attribution List Exchange Interactions Details

#### Consumer identifies relevant Member Attribution List in Producer's system (Discovery of Group Resource)

Add Example Requests and Responses.

#### Consumer requests Member Attribution List from Producer's system (Bulk Data Request)

Add Example Requests and Responses.

#### Producer makes Member Attribution List available to Consumer (Bulk Data Response)

Add Example Requests and Responses.

#### Consumer retrieves Member Attribution List from Producer (FHIR Request)

Add Example Requests and Responses.





