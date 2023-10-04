### Business need

Providers need to access Member Attribution Lists for the following business needs

* Use the list to close care gaps for members that 'count' in financial reconciliation

* Use the list to prospectively manage patients and meet quality metrics and manage costs by closing care gaps.

* Use the list to track care costs of attributed patients, manage utilization, monitor referrals/specialist care.

* Use the list to perform end of year reconciliation to get 'credit' for the right patients based on plans/contracts. 

* Use the list for monthly membership tracking to see trends and confirm accountable care PMPM payments

* Use the list to determine project membership for upcoming year based on prospective lists at end/start of year.

* Use the list to keep historical data of patients for continuity of care as members fall off or get added to the list

* Use the list for performance reporting on specific targets and measures.

Using FHIR based APIs, providers and payers can exchange Member Attribution Lists which can enable existing business processes and systems to meet the above business needs. The creation of a Member Attribution List typically starts with a need to identify the patients for a specific purpose such as Risk Based Contracts or Quality Reporting. Once the patients are identified other FHIR APIs and Da Vinci specifications can be used to retrieve clinical, financial or other relevant information as needed.

### Example Member Attribution List Exchange Scenarios 

#### Scenario 1
Provider Organization A enters a risk-based contract with Payer B. As part of establishing the contract targets, specific measures and financial incentives are documented. Payer B uses historical claims and other information present about members to create a Member Attribution List for Provider Organization A. The Member Attribution List identifies the list of patients that Provider Organization A is responsible for as part of the contract. Payer B needs to exchange this list with Provider Organization A periodically to ensure that Provider Organization A is aware of the list of patients that it is responsible for as per the contract. Payer B could publish the list in standard way and Provider Organization A retrieves the list for use. Alternatively Provider Organization A may request for the list and Payer B provides the list once it is ready.

<div class="bg-success" markdown="1">

#### Scenario 2
Provider Organization A enters a contract with Payer B. As part of establishing the contract targets, specific measures, financial incentives are documented. Provider Organization A assembles the list of members for whom they are responsible and uses the information to create an initial member attribution list and provides it to Payer B.  Payer B uses historical claims and other information present about members to update the provided Member Attribution List for Provider Organization A. The list is published by Payer B to Provider Organization A. Provider Organization A retrieves the list and identifies a list of changes that need to be done to the list and notifies the Payer B about the changes in terms of additions and removals. Payer B either accepts or rejects the changes and may modify the existing Member Attribution List. If the list is modified, Payer B notifies Provider Organization A of the changes. Provider Organization A and Payer B finally agree upon a member attribution list and starts using the list for various business needs. 

</div>

#### Use of Member Attribution List as part of the Data Exchange for Quality Measures and Care Gaps
Member Attribution Lists are fundamental to closing care gaps and reporting on quality measures. Providers have to report on specific patients to payers on specific quality measures and close any care gap requirements that may exist. Providers and Payers agree upon the list of patients for whom reporting has to be performed on a regular basis. Similarly care gaps associated with these patients have to be closed to receive applicable financial incentives. In all these cases the agreement on what is the "list of patients" is critical. This function is served by the Member Attribution List. The Member Attribution List can be agreed upon between the Payers and Providers and exchanged on a regular cadence. Based on the patients attributed in the Member Attribution List Payers can request Providers for specific quality measure data, care gaps data. Similarly Providers can close care gaps for patients attributed to them via the Member Attribution List and can report quality data using the Data Exchange for Quality Measures Da Vinci implementation guide.

<div class="bg-success" markdown="1">

#### Use of Member Attribution List for CMS Data at Point of Care (DPC) use case
The Centers for Medicare and Medicaid Services (CMS) Data at the Point of Care (DPC) API is currently in a pilot phase in which a limited number of users can access Medicare Fee-For-Service claims data through the API. This pilot program promotes the industry-standard HL7 Fast Healthcare Interoperability Resources (FHIR), specifically the Bulk FHIR specification. The mechanisms used by DPC program have been outlined in this implementation guide which includes creation of the Member Attribution List, requesting changes or updates to the Member Attribution List, requesting claims data using the Bulk Data operations specifically /Group/[id]/$davinci-data-export operation.

#### Use of Member Attribution List for CMS Beneficiary Claims Data API (BCDA) use case
The Beneficiary Claims Data API (BCDA) is an Application Programming Interface (API) that enables Accountable Care Organizations (ACOs) to retrieve Medicare claims data for their beneficiaries. BCDA serves as direct pipeline from CMS to ACO systems to provide claims data on at a more timely cadence. This includes Medicare claims data for instances in which beneficiaries receive care outside of the ACO, allowing a full picture of patient care. The BCDA initiative provides claims data represented using Patient, Coverage and Explanation of Benefit FHIR resources to the ACOs. CMS ingests an attribution file to create the list of beneficiaries relevant to an ACO and uses the Group resource to represent the beneficiary list. The member attribution list is represented using the data model present in this Implementation Guide. The claims data can be accessed using the same /Group/[id]/$davinci-data-export bulk data operation also specified in this Implementation Guide. 

#### Use of Member Attribution List for DaVinci Pdex use cases 
The DaVinci Pdex use cases for Payer to Payer exchange have been identified as one of the use cases for using the DaVinci-data-export operation defined in the guide to exchange large amounts of data using the bulk data asynchronous pattern. The actual content to be exchanged will be defined in the Pdex IG in the future.

</div>


### Member Attribution List workflows and definitions

The following definitions are used for the Member Attribution List implementation guide.

1. __MemberId:__
A unique identifier for a member within a payers plan.

2. __Payer Identifier:__ 
A unique identifier for an organization that provides insurance plans and enters into contracts with health care providers.

3. __Contract Identifier:__
A unique identifier assigned by the Payer to the agreement with a specific healthcare provider.

4. __Plan Identifier:__
A unique identifier for an insurance plan that a payer provides. Members belong to specific plans.

**NOTE:** The combination of Member Identifier, Payer Identifier, Contract Identifier and Plan Identifier is always unique.

5. __Attribution:__ 
Results of Algorithmic or manual process that assigns patients to providers or payers. Alternatively a patient could declare to be part of a Group by providing or selecting their PCP information or ACO information.

6. __Member Attribution List:__
Enumeration of patients who are attributed to payers, providers, medical homes or groups. Patients may belong to multiple plans. 
The Attribution list contains the patient information along with information such as Attributed Provider, Health Plan information, Validity Period for the list, Risk Information etc. A member may be present multiple times within a member attribution list, however the combination of Member Identifier, Payer Identifier, Contract Identifier and Plan Identifier is always unique and can be used to identify the member.

7. __Attributed Provider:__
Provider responsible for managing the quality and costs of the patient’s health care per the contract and will receive the payments and credits based on performance.

8. __Attribution Period:__
The period over which the member is attributed to a specific provider. The period has a start and an end date.

8. __Producer:__
An Entity creating the attribution list.
Producer Owns the master copy of the list. 
Producers allow for changes to be made to the list. 
A Producer may receive an initial list from consumer and owns the list after that point in time and publishes the list for consumptionCons.

9. __Consumer:__ 
An Entity consuming the attribution list. 
Consumers may contribute to the creation of the list owned by the Producer.
Consumers may request changes to be made to the list owned by the Producer.
Consumers may receive an initial list from producer and may request changes to the list before reaching final agreement on the list.

10. __Attribution List Data:__
Data contained within the attribution list. Data includes
* Patient Demographics Data 
* Attributed Provider Data (First Name, Last Name, Id, NPI, TIN, Address)
* Health Plan Data (Subscriber Id, Member Id, Medicare Id, Medicaid Id, Plan Name, Plan Type, Enrollment Start and End Dates)
* Attribution Data (Effective Start and End Date for Attribution, Attribution Method, Risk score)
* Miscellaneous Data (ACO Information, Conditions)

11. __Attribution List Changes:__ 
Addition of patients to the attribution list. 
Deletion of patients to the attribution list. 
Changes in attribution list data. 

### Member Attribution List Exchange for Scenario #1

{% include img.html img="workflow.jpg" caption="Figure 2: Member Attribution List Exchange Workflow for Scenario #1" %}

The following is a brief description of the workflow steps with a Payer representing the Producer and a Provider Organization representing the Consumer. 

**1. Payer (Producer) and Provider (Consumer) enter into a contract **<br/>
Provider and a Payer enter into a contract with specific terms and conditions and decide on the need for a Member Attribution List. Payer internally creates the Member Attribution List using internal processes and existing data about the patients. 

**2. Payer (Producer) Informs Provider (Consumer) and makes the List available to the Provider **<br/>
In this step the Payer informs the Provider about the list and makes it available to the Provider. The specific mechanism of how this exchange happens varies based on Payers and Providers. This implementation guide will specify standards for this interaction.

**3a. Provider (Consumer) informs Payer (Payer) about changes **<br/>
Once the Provider receives the list in Step 2, Provider reconciles the list with internal lists and data and in case changes are needed, notifies the Payer about specific changes. These changes could be to add additional patients, remove patients from the list etc. The specific mechanism of how this exchange happens varies based on Payers and Providers. 
If the Consumer has no changes, then Step 3a would not be executed and the Consumer has accepted the list for usage. 

Note: Steps 2 and 3a may be repeated as many times as needed until the Producer and Consumer agree upon the member attribution list.

**3b. Provider (Consumer) informs Payer (Producer) about no changes **<br/>
Once the Provider receives the list in Step 2, Provider reconciles the list with internal lists and data and in case no changes are needed, notifies the Payer about finalizing the list. The specific mechanism of how this exchange happens varies based on Payers and Providers. 

**4. Payer (Producer) makes list available to Provider (Consumer) **<br/>
Once the list is finalized, the Payer and Provider agree to exchange the list periodically as required. The specific mechanism of how this exchange happens varies based on Payers and Providers. This implementation guide will specify standards for this interaction.

**NOTE:** The above workflow is the normal scenario. In addition to the above workflow the Producer may change the list periodically based on additional data. As this happens the Producer may decide to redo Steps 2 through 4. In this version of the IG, there are no notification mechanisms created for a Producer to notify a consumer when the list changes. However there could be an agreed upon cadence between the Producer and the Consumer on how often the list is exchanged. 
Every change that is made to the list may be available to the Consumer via APIs in real-time or at specified intervals. For example, if it is a monthly list, then as changes get made the updated list will be exchanged on a monthly basis. The change reconciliation process is out of scope for the current version of the IG as outlined in the above steps.

#### Considerations

* The scenario above uses the term 'Producer'.  Typically, that would be a Payer organization, but in some cases, it could be a Provider Organization. This is true in [Data at Point of Care use cases](https://dpc.cms.gov/).

<div class="bg-success" markdown="1">

### Member Attribution List Exchange for Scenario #2 (STU2 Workflow)

{% include img.html img="workflow-scenario2.png" caption="Figure 3: Member Attribution List Exchange Workflow for Scenario #2" %}

The following is a brief description of the workflow steps with a Payer representing the Producer and a Provider Organization representing the Consumer. This workflow differs from the previous workflow in that the consumer is creating the Member Attribution List first and then providing the list to the Producer.

**1. Payer (Producer) and Provider (Consumer) enter into a contract **<br/>
Provider and a Payer enter into a contract with specific terms and conditions and decide on the need for a Member Attribution List. Payer supports the capabilities required to create a Member Attribution List.

**2. Provider (Consumer) creates the list in the Payer (Producer) system **<br/>
In this step the Provider creates the member attribution list in the payer system.

**3. Payer (Producer) reconciles the list internally and notifies Provider (Consumer) of changes **<br/>
Once the Payer receives the list in Step 2, the Payer may reconcile the list internally and modify the list and notify the Provider of the changes in the list. 

**4. Provider (Consumer) reconciles the list and requests additional changes to the list by adding and removing members **<br/>
Providers reconcile the list internally and identify that there may be members who need to be added and members who need to be removed from the list. In order to do so, the Provider uses the member-add and member-remove APIs to add and remove members from the list.
Payers (Producrers) can decide if the members need to be added or removed based on the request.

**NOTE** Steps 3 and 4 can be repeated as many times as needed until the Producer and the Consumer agree upon a final list.

**5. Payer (Producer) and Provider (Consumer) agree upon a member attribution list for a specific use case when the Consumer indicates there are no more changes to be made **<br/>
Consumer invokes the confirm-attribution-list operation to indicate there are no further changes to be made to the attribution list. Providers and Payers agree upon the finalized member attribution list for various use cases.

</div>
