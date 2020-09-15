{% raw %}
{% endraw %}
<!--ReleaseHeader-->
<!--EndReleaseHeader-->


### Overview
Member Attribution (ATR) lists are used between Payers and Providers for implementing risk-based contracts, value based contracts, care gap closures and quality reporting. This version of the implementation guide has been developed with risk-based contracts. Future versions of the implementation guide will consider other use cases as identified by Da Vinci. A risk-based contract establishes responsibilities between an Payer and a Provider(individual or organization) where the providers have responsibility for health care costs incurred by a member(s) attributed to them by the Payer as part of the member attribution list. The processes of establishing and exchanging member lists for risk-based contracts are complex and time consuming. Currently there are no standards in use for establishing and exchanging risk-based contract member lists between payers and providers. The most common method in use today involves creation of files (CSVs, txt etc) and exchanging them using different methods such as Email and Secure File Transfer Protocol (SFTP).This implementation guide will use HL7 FHIR to specify standards for exchanging of Member Attribution Lists between providers and payers. The list can be used by providers and payers to implement use cases for Value Based Contracts (VBC), Quality Reporting, Da Vinci Payer Data Exchange (PDex), Da Vinci Clinical Data Exchange (CDex) among others. 

The purpose of this implementation guide is to define the mechanisms (protocols), data structures and value sets to be used for exchanging the Member Attribution List. The Member Attribution List typically contains the following information

* Plan/Contract information which is the basis for the Member Attribution list
* Patient Information
* Attributed Individual Provider Information
* Attributed Organization Information
* Member and Subscriber Coverage Information

The implementation guide is designed to allow for initial support of basic capabilities and to subsequently build new features over time. The initial capabilities include
 
* Exchange of a Full Member Attribution List.

The following features are in scope for future versions of the implementation guide 

* Notification of changes in Member Attribution Lists
* Exchange of partial Member Attribution Lists which contain information about changes and not the complete list.
* Requesting changes to existing Member Attribution Lists

The following aspects are not in-scope for the implementation guide

* Member Attribution List Creation and Reconciliation processes and workflows used by payers and providers


### Content and organization
The implementation guide is organized into the following sections:

* [Use Cases and Overview](usecases.html) describes the intent of the implementation guide, gives examples of its use and provides a high-level overview of expected process flow
* [Technical Background](background.html) describes the different specifications this implementation guide relies on and indicates what developers should read and understand prior to implementing this specification
* [Formal Specification](spec.html) covers the detailed implementation requirements and conformance expectation
* [Artifacts](artifacts.html) introduces and provides links to the [FHIR R4](artifacts.html) profiles, search parameters and other FHIR artifacts used in this implementation guide
* [Downloads](downloads.html) allows download of this and other specifications as well as other useful files
* [Credits](credits.html) identifies the individuals and organizations involved in developing this implementation guide

### Dependencies
This implementation guide relies on the following other specifications:
* **[FHIR R4]({{site.data.fhir.path}})** - The 'current' official version of FHIR as of the time this implementation guide was published.  See the [background page](background.html#fhir) for key pieces of this specification implementers should be familiar with.
* **[US Core STU3](http://hl7.org/fhir/us/core/index.html)** - The version of US Core based on FHIR R4.
* **[Bulk Data IG](http://hl7.org/fhir/uv/bulkdata/index.html)** - The Bulk Data Implementation Guide that will be leveraged as part of this IG.
* **[SMART on FHIR Backend Services Authorization](http://hl7.org/fhir/uv/bulkdata/authorization/index.html)** - Security protocols to be used for exchanging the Member Attribution List.

This implementation guide defines additional constraints and usage expectations above and beyond the information found in these base specifications.