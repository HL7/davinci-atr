### Da Vinci
Da Vinci is an HL7-sponsored project that brings together the U.S. payer ,providers, and technology suppliers (including EHR vendors)  to help payers and providers to positively impact clinical, quality, cost, and care management outcomes using FHIR-related technologies. The project organizes meetings (face-to-face and conference calls) as well as connectathons to find ways to leverage FHIR technologies to support and integrate value-based care (VBC) data exchange across communities. Da Vinci identifies value-based care use cases of interest to its member and the community as a whole.

The process that Da Vinci has adopted includes: 
1. identify business, clinical, technical and testing requirements, 
2. develop and ballot a FHIR based implementation guide (IG),
3. develop a reference implementation (RI) that is used to demonstrate that the concepts in the IG are possible to implement,
4. pilot the standard
5. support the production use of the IG to enable exchange of data to support interoperability for value-based care.

Additional information about Da Vinci, its members, the use cases and the implementation guides being developed can all be found on the [HL7 website](http://www.hl7.org/about/davinci). Meeting minutes and other materials can be found on the [Da Vinci Confluence page](https://confluence.hl7.org/display/DVP).

### Systems
The implementation guide defines the responsibilities of the two types of systems involved in a ATR solution:

**Producer systems** are typically Payer systems but could theoretically be any system responsible for producing a Member Attribution List. These systems typically act as servers. 

**Consumer systems** are typically Provider systems that act on behalf of provider organizations who retrieve the attribution list from Producer. These systems typically act as clients.

### Underlying technologies

This guide is based on the [HL7 FHIR]({{site.data.fhir.path}}index.html) standard, as well as the [Bulk Data IG](http://hl7.org/fhir/uv/bulkdata/index.html) and [SMART on FHIR Backend Services Authorization](http://hl7.org/fhir/uv/bulkdata/authorization/index.html) specifications, which build additional capabilities on top of FHIR.  This architecture is intended to maximize the number of clinical systems that conform to this guide as well as to allow for easy growth and extensibility of system capabilities in the future.

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

This implementation guide supports the [STU3](http://hl7.org/fhir/STU3) and [R4]({{site.data.fhir.path}}index.html) versions of the FHIR standard. FHIR services based on STU3 are being moved into production by EMR vendors. R4 is just recently published and the goal is to ensure the implementation guide is aligned with the current direction of the FHIR standard. Initial implementations will focus on STU3.

#### Data Model
This section maps the Member Attribution List data to FHIR resources to give an introduction to the resources that will be used in the guide. 

{::options parse_block_html="false" /}
<figure>
  <img height="300px" src="mal-data.png" alt="Member Attribution List Data mapped to FHIR resources"/>
</figure>
{::options parse_block_html="true" /}

<br/>

Implementers should familiarize themselves with the FHIR resources used within the guide based on the above data model.

<table>
  <thead>
    <tr>
      <th>STU3</th>
      <th>R4</th>
    </tr>
  </thead>
  <tr>
    <td>
      <a href="http://hl7.org/fhir/STU3/coverage.html">Coverage</a><br/>
      <a href="http://hl7.org/fhir/STU3/group.html">Group</a><br/>
      <a href="http://hl7.org/fhir/STU3/location.html">Location</a><br/>
      <a href="http://hl7.org/fhir/STU3/organization.html">Organization</a><br/>
      <a href="http://hl7.org/fhir/STU3/patient.html">Patient</a><br/>
      <a href="http://hl7.org/fhir/STU3/person.html">Person</a><br/>
      <a href="http://hl7.org/fhir/STU3/practitioner.html">Practitioner</a><br/>
      <a href="http://hl7.org/fhir/STU3/practitionerrole.html">PractitionerRole</a><br/>  
    </td>
    <td>
      <a href="{{site.data.fhir.path}}coverage.html">Coverage</a><br/>
      <a href="{{site.data.fhir.path}}group.html">Group</a><br/>
      <a href="{{site.data.fhir.path}}insuranceplan.html">InsurancePlan</a><br/>
      <a href="{{site.data.fhir.path}}location.html">Location</a><br/>
      <a href="{{site.data.fhir.path}}organization.html">Organization</a><br/>
      <a href="{{site.data.fhir.path}}patient.html">Patient</a><br/>
      <a href="{{site.data.fhir.path}}person.html">Person</a><br/>
      <a href="{{site.data.fhir.path}}practitioner.html">Practitioner</a><br/>
      <a href="{{site.data.fhir.path}}practitionerrole.html">PractitionerRole</a><br/>
    </td>
  </tr>
</table>

#### US Core IG

This implementation guide also builds on the US Core Implementation Guide where profiles exist for the resources identified in the data model above and implementers need to familiarize themselves with these profiles in those Implementation Guides.
<table>
  <tr>
    <td><a href="http://hl7.org/fhir/us/core/STU3">US Core (3.0.0 - R4 based)</a></td>
  </tr>
  <tr>
    <td><a href="http://hl7.org/fhir/us/core/STU2">US Core (2.0.0 - STU3 based)</a></td>
  </tr>
</table>


#### Bulk Data IG
Bulk Data IG will be used to retrieve the Member Attribution List. Once the Member Attribution List is retrieved, the Bulk Data IG will be further used to retrieve clinical and financial information about the members using other DaVinci implementation guides. 

#### SMART on FHIR Backend Services Authorization
The SMART on FHIR Backend Services Authorization is used to secure all the system interactions between the Producers and the Consumers.
