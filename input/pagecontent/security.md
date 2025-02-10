{% raw %}
{% endraw %}
<!--ReleaseHeader-->
<!--EndReleaseHeader-->

### Generic Privacy, Safety, and Security guidance across all Da Vinci IGs 

This implementation guide uses terminology, notations and design principles that are specific to FHIR. Implementers **SHALL** adhere to any security and privacy rules defined by:

FHIR Core: All Da Vinci Implementation guides including Member Attribution Implementation Guide **SHALL** follow the FHIR [Security & Privacy Module](http://hl7.org/fhir/R4/secpriv-module.html), [Security Principles](http://hl7.org/fhir/R4/security.html) and [Implementer's Checklist](http://hl7.org/fhir/R4/safety.html)
HRex: [Privacy & Security]({{site.data.fhir.ver.hrex}}/security.html)


### Member Attribution IG Specific Security Requirements 

* Implementers of Member Attribution IG **MUST** refer to the [Capability Statements](artifacts.html) to implement the desired Member Attribution security capabilities. 
* Implementers **MUST** implement the [Member Attribution Security requirements](spec.html#smart-on-fhir-backend-services-authorization) to ensure the implementation meets the necessary security requirements. 