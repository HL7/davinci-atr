### STU2 Changes

The following is a list of all the changes from STU1 to STU2.

#### New Additions for STU2

1. [Addition of new scenario#2 (STU2 Workflow) user story for providers to create attribution lists in payers systems](usecases.html#member-attribution-list-exchange-for-scenario-2-stu2-workflow)
2. Added additional usage scenarios for Member Attribution List and Bulk Data Export in DPC, BCDA and Pdex initiatives[Ticket #37764](usecases.html#use-of-member-attribution-list-for-cms-data-at-point-of-care-dpc-use-case) 
3. Addition of a generalized DaVinci Data Export operation for enabling bulk data export across multiple use cases[Ticket #37764](OperationDefinition-davinci-data-export.html)
4. [Addition of member-add operation](OperationDefinition-member-add.html)
5. [Addition of member-remove operation](OperationDefinition-member-remove.html)
6. [Added usage APIs for member-add and member-remove operations](spec.html#member-attribution-list-reconciliation-apis)
7. [Addition of capability to create Groups, Patients, Practitioners by Consumer in the Producer system](CapabilityStatement-atr-producer.html#resource-summary)
8. [Ability to provide provenance via X-Provenance-Header during POST and PUT operations for creation of data](CapabilityStatement-atr-producer.html#rest-behavior)
9. Added CodeSystem and ValueSets for Characteristics.code for Davinci Patient List [Ticket #28806](ValueSet-davinci-group-characteristic.html)
10. Added [Subscription Requirements](subscription.html) to enable subscriptions and notifications for Member Attribution List.
11. Added generic [DaVinci Patient List capability](StructureDefinition-davinci-patient-list.html) that can be used for a generic patient list. 
12. Modified [Member Attribution List](StructureDefinition-atr-group.html) to inherit from genreric [DaVinci Patient List](StructureDefinition-davinci-patient-list.html) 
11. [Created Change Log](changes.html) and Publication Request for STU2.

#### Changes to existing IG

1. [Use DaVinci Data Export instead of Bulk Data $export operation.](spec.html#requirements-for-implementation-of-the-davinci-data-export-operation)
2. Add clarifications on APIs for DaVinci Data Export operation. [Ticket #36717](spec.html#requirements-for-implementation-of-the-davinci-data-export-operation)
3. [Add clarifications on handling large groups.](StructureDefinition-atr-group.html#introduction)
6. Updated the dependencies to fix US Core to 3.1.1 and Bulk Data IG to 1.0.1 [Ticket #38804]
7. Updated Coverage profile to add Member Identifier [Ticket #37836](StructureDefinition-atr-coverage.html)
8. Updated Examples to use proper code system for NPI [Ticket #34297]
9. [Updated SMART on FHIR Guidance for authorization.](spec.html#smart-on-fhir-backend-services-authorization)
10. [Updated Producer and Consumer capability statements to add X-Provenance Header support.](CapabilityStatement-atr-producer.html#rest-behavior)
11. Updated FHIR Build template to use DaVinci template.

#### Tickets implemented in STU2


* [FHIR-39898](https://jira.hl7.org/browse/FHIR-39898) - Correct Workflow Diagram for Scenario 2 (Step 5 unclear)
* [FHIR-40127](https://jira.hl7.org/browse/FHIR-40127) - Ability to query a Payer about attribution of a particular patient(s)
* [FHIR-40128](https://jira.hl7.org/browse/FHIR-40128) - Add Subscription functionality
* [FHIR-42799](https://jira.hl7.org/browse/FHIR-42799) - Clarify STU2 workflow
* [FHIR-42860](https://jira.hl7.org/browse/FHIR-42860) - $davinci-data-export operation not defined for Attribution List import
* [FHIR-41855](https://jira.hl7.org/browse/FHIR-41855) - Typo in slice name einIdentifier
* [FHIR-39664](https://jira.hl7.org/browse/FHIR-39664) - API for change request in scenario #1
* [FHIR-40209](https://jira.hl7.org/browse/FHIR-40209) - Narrative Content needs Technical Editing
* [FHIR-39955](https://jira.hl7.org/browse/FHIR-39935) - Data Model shows RelatedTo but it is not present in the profile
* [FHIR-39740](https://jira.hl7.org/browse/FHIR-39740) - Wrong Action for Member Remove profile
* [FHIR-39927](https://jira.hl7.org/browse/FHIR-39927) - Update DaVinci-data-export to be a profile of Bulk Export
* [FHIR-39667](https://jira.hl7.org/browse/FHIR-39667) - Clarify how to remove a member
* [FHIR-39666](https://jira.hl7.org/browse/FHIR-39666) - Clarify source of truth for scenario#1 and #2
* [FHIR-40129](https://jira.hl7.org/browse/FHIR-40129) - Spell out PTO Acronym
* [FHIR-40670](https://jira.hl7.org/browse/FHIR-40670) - Clarify PTO
* [FHIR-41377](https://jira.hl7.org/browse/FHIR-41377) - Add purpose of use in Group.member as extension
* [FHIR-40206](https://jira.hl7.org/browse/FHIR-40206) - Large number of technical corrections
* [FHIR-39669](https://jira.hl7.org/browse/FHIR-39669) - Wrong description in add operation
* [FHIR-39670](https://jira.hl7.org/browse/FHIR-39670) - Wrong description in remove operation
* [FHIR-42147](https://jira.hl7.org/browse/FHIR-42147) - Remove requirement to reject requests without minimal resource types
* [FHIR-40213](https://jira.hl7.org/browse/FHIR-40213) - Representation of NPI and TIN
* [FHIR-39921](https://jira.hl7.org/browse/FHIR-39921) - davinic-data-export requirements
* [FHIR-39663](https://jira.hl7.org/browse/FHIR-39663) - List push vs pull
* [FHIR-41858](https://jira.hl7.org/browse/FHIR-41858) - TIN Identifier and NPI Identifier should have a type on slice
* [FHIR-42861](https://jira.hl7.org/browse/FHIR-42861) - Should EMRs be able to create Group resource in payer
* [FHIR-39739](https://jira.hl7.org/browse/FHIR-39739) - Clarify responsibility for adding and removing members
* [FHIR-39665](https://jira.hl7.org/browse/FHIR-39665) - Specify what remove operation actually does
* [FHIR-39668](https://jira.hl7.org/browse/FHIR-39668) - Optional params in remove operation
* [FHIR-39934](https://jira.hl7.org/browse/FHIR-39934) - Change text box in Figure 3
* [FHIR-39896](https://jira.hl7.org/browse/FHIR-39896) - US Core depeendency is 3.0.0 but should be 3.1.1
* [FHIR-39741](https://jira.hl7.org/browse/FHIR-39741) - Text updates














