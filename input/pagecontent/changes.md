### STU2 Changes

The following is a list of all the changes from STU1 to STU2.

#### New Additions

1. [Addition of new scenario#2 (STU2 Workflow) user story for providers to create attribution lists in payers systems](usecases.html#member-attribution-list-exchange-for-scenario-2-stu2-workflow)
2. [Added additional usage scenarios for Member Attribution List and Bulk Data Export in DPC, BCDA and Pdex initiatives](usecases.html#use-of-member-attribution-list-for-cms-data-at-point-of-care-dpc-use-case) 
3. [Addition of a generalized DaVinci Data Export operation for enabling bulk data export across multiple use cases](OperationDefinition-davinci-data-export.html)
4. [Addition of member-add operation](OperationDefinition-member-add.html)
5. [Addition of member-remove operation](OperationDefinition-member-remove.html)
6. [Added usage APIs for member-add and member-remove operations](spec.html#member-attribution-list-reconciliation-apis)
7. [Addition of capability to create Groups, Patients, Practitioners by Consumer in the Producer system](CapabilityStatement-atr-producer.html#resource-summary)
8. [Ability to provide provenance via X-Provenance-Header during POST and PUT operations for creation of data](CapabilityStatement-atr-producer.html#rest-behavior)
9. Add CodeSystem and ValueSets for Characteristics.code for Davinci Patient List [Ticket #28806](ValueSet-davinci-group-characteristic.html)
11. [Created Change Log.](changes.html)

#### Changes to existing requirements

1. [Use DaVinci Data Export instead of Bulk Data $export operation.](spec.html#requirements-for-implementation-of-the-davinci-data-export-operation)
2. Add clarifications on APIs for DaVinci Data Export operation. [Ticket #36717](spec.html#requirements-for-implementation-of-the-davinci-data-export-operation)
3. [Add clarifications on handling large groups.](StructureDefinition-atr-group.html#introduction)
4. Change Patient Profile SSN Identifier from SS to SB [Ticket #37835](StructureDefinition-atr-patient.html)
5. Modified the capability statements for Producer to add of-type modifier search parameter. [Ticket #30894](CapabilityStatement-atr-producer.html#search)
6. Updated the dependencies to fix US Core to 3.1.1 and Bulk Data IG to 1.0.1 [Ticket #38804]
7. Updated Coverage profile to add Member Identifier [Ticket #37836](StructureDefinition-atr-coverage.html)
8. Updated Examples to use proper code system for NPI [Ticket #34297]
9. [Updated SMART on FHIR Guidance for authorization.](spec.html#smart-on-fhir-backend-services-authorization)
10. [Updated Producer and Consumer capability statements to add X-Provenance Header support.](CapabilityStatement-atr-producer.html#rest-behavior)



