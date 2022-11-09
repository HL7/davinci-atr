### Da Vinci
Da Vinci is an HL7-sponsored project that brings together the U.S. payer ,providers, and technology suppliers (including EHR vendors)  to help payers and providers to positively impact clinical, quality, cost, and care management outcomes using FHIR-related technologies. The project organizes meetings (face-to-face and conference calls) as well as connectathons to find ways to leverage FHIR technologies to support and integrate value-based care (VBC) data exchange across communities. Da Vinci identifies value-based care use cases of interest to its member and the community as a whole.

The process that Da Vinci has adopted includes: 
1. identify business, clinical, technical and testing requirements, 
2. develop and ballot a FHIR based implementation guide (IG),
3. develop a reference implementation (RI) that is used to demonstrate that the concepts in the IG are possible to implement,
4. pilot the standard
5. support the production use of the IG to enable exchange of data to support interoperability for value-based care.

Additional information about Da Vinci, its members, the use cases and the implementation guides being developed can all be found on the [HL7 website](http://www.hl7.org/about/davinci). Meeting minutes and other materials can be found on the [Da Vinci Confluence page](https://confluence.hl7.org/display/DVP). The guiding principles for Da Vinci can be found [here](https://confluence.hl7.org/display/DVP/Da+Vinci+Clinical+Advisory+Council+Members?preview=/66940155/66942916/Guiding%20Principles%20for%20Da%20Vinci%20Implementation%20Guides.pdf).

### Systems
The implementation guide defines the responsibilities of the two types of systems involved in an ATR solution:

**Producer systems** are typically Payer systems but could theoretically be any system responsible for producing a Member Attribution List.These systems typically act as servers. 

**Consumer systems** are typically Provider systems that act on behalf of provider organizations who retrieve the attribution list from Producer. These systems typically act as clients.

### Underlying Specifications

This guide is based on the [HL7 FHIR]({{site.data.fhir.path}}index.html) standard, as well as the [Bulk Data IG]({{site.data.fhir.ver.bulkig}}/index.html) and [SMART on FHIR Backend Services Authorization]({{site.data.fhir.ver.smartapplaunch}}/index.html) specifications which build additional capabilities on top of FHIR.  This architecture is intended to maximize the number of clinical systems that conform to this guide as well as to allow for easy growth and extensibility of system capabilities in the future.

Implementers of this specification therefore need to understand some basic information about these specifications.


#### FHIR

This implementation guide uses terminology, notations and design principles that are
specific to FHIR.  Before reading this implementation guide, it's important to be familiar with some of the basic principles of FHIR as well
as general guidance on how to read FHIR specifications.  Readers who are unfamiliar with FHIR are encouraged to read (or at least skim) the following
prior to reading the rest of this implementation guide.

* [FHIR overview]({{site.data.fhir.path}}overview.html)
* [Developer's introduction]({{site.data.fhir.path}}overview-dev.html) (or [Clinical introduction]({{site.data.fhir.path}}overview-clinical.html))
* [FHIR data types]({{site.data.fhir.path}}datatypes.html)
* [Using codes]({{site.data.fhir.path}}terminologies.html)
* [References between resources]({{site.data.fhir.path}}references.html)
* [How to read resource & profile definitions]({{site.data.fhir.path}}formats.html)
* [Base resource]({{site.data.fhir.path}}resource.html)

This implementation guide supports [FHIR R4]({{site.data.fhir.path}}index.html) versions of the FHIR standard. FHIR R4 is just recently published and the goal is to ensure the implementation guide is aligned with the current direction of the FHIR standard. Initial implementations will focus on FHIR R4.

#### Data Model
This section maps the Member Attribution List data to FHIR resources to introduce resources that will be used in the implementation guide. 

{% include img.html img="maldata.svg" caption="Figure 1: Member Attribution List Data Model" %}

Implementers should familiarize themselves with the FHIR resources used within the guide based on the above data model.

<table>
  <thead>
    <tr>
      <th>FHIR R4</th>
    </tr>
  </thead>
  <tr>
    <td>
      <a href="{{site.data.fhir.path}}coverage.html">Coverage</a><br/>
      <a href="{{site.data.fhir.path}}group.html">Group</a><br/>
      <a href="{{site.data.fhir.path}}location.html">Location</a><br/>
      <a href="{{site.data.fhir.path}}organization.html">Organization</a><br/>
      <a href="{{site.data.fhir.path}}patient.html">Patient</a><br/>
      <a href="{{site.data.fhir.path}}relatedperson.html">RelatedPerson</a><br/>
      <a href="{{site.data.fhir.path}}practitioner.html">Practitioner</a><br/>
      <a href="{{site.data.fhir.path}}practitionerrole.html">PractitionerRole</a><br/>
    </td>
  </tr>
</table>

#### US Core IG

This implementation guide also builds on the US Core Implementation Guide where profiles exist for the resources identified in the data model above and implementers need to familiarize themselves with these profiles in those Implementation Guides.
<table>
  <tr>
    <td><a href="{{site.data.fhir.ver.uscoreR4}}/index.html">US Core 3.1.1 - FHIR R4 based IG</a></td>
  </tr>
</table>


#### Bulk Data IG
Bulk Data IG will be used to retrieve the Member Attribution List and related data. Bulk Data IG is used as the data could be large for some Member Attribution Lists. In addition, the requests and responses in existing workflows are asynchronous. Other Da Vinci implementation guides such as PDex, CDex are not used as part of this IG for Member Attribution List retrieval.

#### SMART on FHIR Backend Services Authorization
The SMART on FHIR Backend Services Authorization is used to secure all the system interactions between the Producers and the Consumers.
