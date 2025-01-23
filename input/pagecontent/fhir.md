This implementation guide uses terminology, notations and design principles that are specific to FHIR.  Before reading this implementation guide, it is important to be familiar with some of the basic principles of FHIR as well as general guidance on how to read FHIR specifications.  Readers who are unfamiliar with FHIR are encouraged to read (or at least skim) the following prior to reading the rest of this implementation guide.

* [FHIR overview]({{site.data.fhir.path}}overview.html)
* [Developer's introduction]({{site.data.fhir.path}}overview-dev.html) (or [Clinical introduction]({{site.data.fhir.path}}overview-clinical.html))
* [FHIR data types]({{site.data.fhir.path}}datatypes.html)
* [Using codes]({{site.data.fhir.path}}terminologies.html)
* [References between resources]({{site.data.fhir.path}}references.html)
* [How to read resource & profile definitions]({{site.data.fhir.path}}formats.html) and additional [IG reading guidance](https://build.fhir.org/ig/FHIR/ig-guidance/readingIgs.html)

* [Base resource]({{site.data.fhir.path}}resource.html)

This implementation guide supports the [R4]({{site.data.fhir.path}}index.html) version of the FHIR standard and builds on the [US Core 3.1 (FHIR R4)]({{site.data.fhir.ver.uscore3}}), [US Core 6.1 (FHIR R4)]({{site.data.fhir.ver.uscore6}}), and [US Core 7.0 (FHIR R4)]({{site.data.fhir.ver.uscore7}}) implementation guides.  Implementers therefore need to familiarize themselves with the profiles in that guide as well as with the FHIR resources used within the implementation guide(s) they will be implementing.  The general implementation notes and guidance on the resource pages of these guides will apply to Da Vinci implementations as they would in any other.  A complete list of the FHIR resources in the core specification can be found [here]({{site.data.fhir.path}}resourcelist.html)

The resources profiled or otherwise used in this specification include:

<table class="grid">
  <thead>
    <tr>
      <th>Resource</th>
      <th>Usage</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a href="{{site.data.fhir.path}}coverage.html">Coverage</a></td>
      <td>Used to convey coverage information to a provider</td>
    </tr>
    <tr>
      <td><a href="{{site.data.fhir.path}}group.html">Group</a></td>
      <td>Used as a container for representing an Attribution List in FHIR</td>
    </tr>
    <tr>
      <td><a href="{{site.data.fhir.path}}patient.html">Patient</a></td>
      <td>Identifies the member in a Member Attribution List, referenced in Group.member</td>
    </tr>
    <tr>
      <td><a href="{{site.data.fhir.path}}practitioner.html">Practitioner</a></td>
      <td>Used to represent the Attributed Provider for a Patient</td>
    </tr>
    <tr>
      <td><a href="{{site.data.fhir.path}}practitionerrole.html">PractitionerRole</a></td>
      <td>Used to represent the Attributed Provider for a Patient associated with a location or facility</td>
    </tr>
    <tr>
      <td><a href="{{site.data.fhir.path}}location.html">Location</a></td>
      <td>Used to represent Provider's facility</td>
    </tr>
    <tr>
      <td><a href="{{site.data.fhir.path}}operationdefinition.html">OperationDefinition</a></td>
      <td>Used when defining operations namely davinci-data-export, member-add, member-remove etc.</td>
    </tr>
    <tr>
      <td><a href="{{site.data.fhir.path}}organization.html">Organization</a></td>
      <td>Used to represent Payer, Attributed Provider Organization in a Member Attribution List/td>
    </tr>
    <tr>
      <td><a href="{{site.data.fhir.path}}subscription.html">Subscription</a></td>
      <td>Used to represent subscription topics which can be used for notification of Member Attribution List changes to Providers</td>
    </tr>
    <tr>
      <td><a href="{{site.data.fhir.path}}structuredefinition.html">StructureDefinition</a></td>
      <td>Used when defining profiles, logical models, and extensions in this guide</td>
    </tr>
    <tr>
      <td><a href="{{site.data.fhir.path}}capabilitystatement.html">CapabilityStatement</a></td>
      <td>Used to define requirements for consumer and producer actors participating in a Member Attribution List data exchange</td>
    </tr>
    <tr>
      <td><a href="{{site.data.fhir.path}}relatedperson.html">RelatedPerson</a></td>
      <td>Used to represent subscribers in Coverage</td>
    </tr>
    <tr>
      <td><a href="{{site.data.fhir.path}}codesystem.html">CodeSystem</a></td>
      <td>Used to represent code systems used in the IG</td>
    </tr>
    <tr>
      <td><a href="{{site.data.fhir.path}}valueset.html">ValueSet</a></td>
      <td>Used to represent value sets used in the IG</td>
    </tr>
  </tbody>
</table>

Implementers should review the general descriptions and usage notes for these resources for additional implementation guidance