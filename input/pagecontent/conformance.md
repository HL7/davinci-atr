{% raw %}
{% endraw %}
<!--ReleaseHeader-->
<!--EndReleaseHeader-->

This implementation guide uses terminology, notations and design principles that are specific to FHIR.
This implementation guide uses specific terminology such as SHALL, SHOULD, MAY to flag statements that have relevance for the evaluation of conformance with the guide. As well, profiles in this implementation guide make use of the mustSupport element. Base expectations for the intepretations of these terms are set in the [FHIR core specification](http://hl7.org/fhir/R4/conformance-rules.html#conflang).

### Generic Conformance Expectations across Da Vinci Implementation Guides 

All Da Vinci Implementation guides including Member Attribution Implementation Guide **SHOULD** follow the conformance expectations as outlined in the [Da Vinci HRex IG Conformance Expectations]({{site.data.fhir.ver.hrex}}/conformance.html).

### MustSupport

Profiles in this implementation guide make use of the [mustSupport](http://hl7.org/fhir/R4/profiling.html#mustsupport) element.

* Producers **SHALL** be capable of populating all data elements as specified by the profiles and are returned using the specified APIs in the capability statement.
* Consumers **SHALL** be capable of processing resource instances containing the MUST SUPPPORT data elements without generating an error or causing the application to fail. In other words Consumers **SHOULD** be capable of displaying the data elements for human use or storing it for other purposes.
* In situations where information on a particular data element is not present and the reason for absence is unknown, Producers **SHALL NOT** include the data elements in the resource instance returned from executing the API requests.
* When accessing Member Attribution Lists, Consumers **SHALL** interpret missing data elements within resource instances as data not present in the Producer's system.

In addition to the above implementers are advised to review the **MustSupport** definition from [HREX]({{site.data.fhir.ver.hrex}}/conformance.html#mustsupport) and [US Core]({{site.data.fhir.ver.uscore7}}/must-support.html)


### Member Attribution IG Specific Conformance Expectations 

Implementers of Member Attribution IG **MUST** refer to the [Capability Statements](artifacts.html) to implement the desired Member Attribution capabilities. Implementers also **MUST** review the Member Attribution **MustSupport** definition above to ensure the implementation meets conformance expectations. 

The Producer specific requirements for REST interactions, operations, profiles and search parameters to be supported are outlined in the [Producer Capability Statement](CapabilityStatement-atr-producer.html). 

The Consumer specific requirements for REST interactions, operations, profiles and search parameters to be supported are outlined in the [Consumer Capability Statement](CapabilityStatement-atr-consumer.html).


### US Core
This implementation guide also leverages the US Core 3.1, US Core 6.1, and US Core 7.0 set of profiles defined by HL7 for sharing non-veterinary EHR individual health data in the United States. Where US Core profiles exist, this guide either leverages them directly or uses them as a base for any additional constraints needed to support the member attribution use case. Where no constraints are needed, this IG does not define additional profiles, as all US Core profiles are deemed to be part of this IG and available for use in member attribution data exchange communications.

Where US Core profiles do not yet exist profiles have been created that try to align with existing US Core profiles in terms of elements exposed and terminologies used.

Note that, in some cases, the US Core profiles require support for data elements that are not necessarily relevant to the member attribution use case. The authors of this IG believe that leveraging existing standard interfaces will promote greater (and quicker) interoperability than would a more finely-tuned custom interface. 