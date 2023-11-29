{% raw %}
{% endraw %}
<!--ReleaseHeader-->
<!--EndReleaseHeader-->
 

### Overview
Member Attribution (ATR) lists are used between Payers and Providers for implementing risk-based contracts, value based contracts, care gap closures and quality reporting. The processes of establishing and exchanging Member Attribution Lists are complex and time consuming. Currently there are no standards in use for establishing and exchanging risk-based contract member lists between payers and providers. The most common method in use today involves the creation of files (CSVs, txt etc) and exchanging them using various methods such as Email and Secure File Transfer Protocol (SFTP).This implementation guide will use HL7 FHIR to specify standards for the exchange of Member Attribution Lists between providers and payers. The list can be used by providers and payers to implement use cases for Value Based Contracts (VBC), Quality Reporting, Da Vinci Payer Data Exchange (PDex) and Da Vinci Clinical Data Exchange (CDex) among others. 

The purpose of this implementation guide is to define the mechanisms (APIs, protocols), data structures and value sets to be used for exchanging the Member Attribution List. The Member Attribution List typically contains the following information:

* Plan/Contract Information which is the basis for the Member Attribution list
* Patient Information
* Attributed Individual Provider Information
* Attributed Organization Information
* Member and Subscriber Coverage Information

This implementation guide is designed to allow 

* Exchange of a Full Member Attribution Lists.
* Requesting changes to existing Member Attribution Lists.
* Request and receive notifications of changes to Member Attribution Lists.


### Content and organization
The implementation guide is organized into the following sections:

* [Use Cases and Overview](usecases.html) describes the intent of the implementation guide, gives examples of its use and provides a high-level overview of expected process flow
* [Technical Background](background.html) describes the other specifications this implementation guide relies on. It also indicates what developers should read and understand prior to implementing this specification
* [Formal Specification](spec.html) covers the detailed implementation requirements and conformance expectations
* [Artifacts](artifacts.html) introduces and provides links to the [FHIR R4](artifacts.html) profiles, search parameters and other FHIR artifacts used in this implementation guide
* [Downloads](downloads.html) - provides downloadable versions of this and other specifications as well as other useful files
* [Credits](credits.html) identifies the individuals and organizations involved in developing this implementation guide

### Dependencies
This implementation guide relies on the following other specifications:
* **[FHIR R4]({{site.data.fhir.path}})** - The 'current' official version of FHIR as of the time this implementation guide was published.  See the [background page](background.html#fhir) for key pieces of this specification that implementers should be familiar with.
* **[US Core STU3.1.1]({{site.data.fhir.ver.uscoreR4}}/index.html)** - The US Core version based on FHIR R4.
* **[Bulk Data IG]({{site.data.fhir.ver.bulkig}}/index.html)** - The Bulk Data Implementation Guide that will be leveraged as part of this IG.
* **[SMART on FHIR Backend Services Authorization]({{site.data.fhir.ver.smartapplaunch}}/backend-services.html)** - Security protocols to be used when exchanging the Member Attribution List.

This implementation guide defines additional constraints and usage expectations beyond the information found in these base specifications.