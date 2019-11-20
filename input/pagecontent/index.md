{% raw %}
{% endraw %}
<!--ReleaseHeader-->
<p style="background-color: yellow; border: 1px solid maroon; padding: 5px;">
  This is the {{site.data.info.ballotstatus}} version of the {{site.data.fhir.igTitle}} Implementation Guide,  based on <a href="{{site.data.fhir.path}}">FHIR Version {{site.data.fhir.version}}</a>.  
  See the <a href="{{site.data.fhir.canonical}}/history.html">Directory of published versions</a> for other versions and for a change history.<br/>
  This specification was developed by <a href="{{site.data.fhir.ig.contact[0].telecom[0]}}">{{site.data.fhir.ig.publisher}}</a>
</p>
<!--EndReleaseHeader-->
<blockquote class="stu-note">
<p>
This specification is being prepared for balloting and connectathon testing.  It is expected to evolve, possibly significantly, as part of that process.
</p>
<p>
Feedback is welcome and may be submitted through the <a href="http://hl7.org/fhir-issues">FHIR change tracker</a> indicating "US Da Vinci ATR" as the specification.
</p>
<p>
This implementation guide is dependent on other specifications.  Please submit any comments you have on these base specifications as follows:
</p>
<ul>
  <li>Feedback on the FHIR core specification should be submitted to the <a href="http://hl7.org/fhir-issues">FHIR change tracker</a> with "FHIR Core" as the specification.</li>
  <li>Feedback on the US core profiles should be submitted to the <a href="http://hl7.org/fhir-issues">FHIR change tracker</a> with "US Core" as the specification.</li>
</ul>
<p>
Individuals interested in participating in the Risk Based Contracts Member Attribution List or  other HL7 Da Vinci projects can find information about Da Vinci [here](http://www.hl7.org/about/davinci).
</p>
</blockquote>


### Overview
The process of establishing and exchanging member lists for risk based contracts are complex and time consuming. Currently there are no standards in use for establishing and exchanging risk based contract member lists between payers and providers. The most common method in use today involves creation of files (CSVs, txt etc) and exchanging them using different methods such as Email and Secure Eile Transfer Protocol (SFTP).This implementation guide will use HL7 FHIR to specify standards for exchanging of Member Attribution Lists (MAL) between providers and payers. The list can be used by providers and payers to implement use cases for Value Based Contracts (VBC), Quality Reporting, Davinci Payer Data Exchange (PDex), Davinci Clinical Data Exchange (CDex) among others. 

The purpose of this implementation guide is to define the mechanisms (protocols), data structures and value sets to be used for exchanging the MAL. The MAL typically contains the following information:

* Plan/Contract information which is the basis for the Member Attribution list
* Patient Information
* Attributed Individual Provider Information
* Attributed Organization Information
* Member and Subscriber Coverage Information

The implementation guide is designed to allow for initial support of basic capabilities and to subsequently build new features over time. The initial capabilities include
 
* Exchange of a Full Member Attribution List.

The following features are in scope for future versions of the implementation guide 

* Notification of changes in Member Attribution Lists
* Exchange of Incremental Member Attribution Lists
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
* **[SMART on FHIR Backend Services Authorization](http://hl7.org/fhir/uv/bulkdata/authorization/index.html)** - Security protocols to be used for exchaning the MAL.

This implementation guide defines additional constraints and usage expectations above and beyond the information found in these base specifications.
