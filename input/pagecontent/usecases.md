### Business need

Providers need to access Member Attribution Lists to meet following business needs

* Close care gaps for members that 'count' in financial reconciliation

* Prospectively manage patients, meet quality metrics, and manage costs by closing care gaps.

* Track care costs of attributed patients, manage utilization and monitor referrals/specialist care.

* Perform end of year reconciliation to obtain 'credit' for the right patients based on plans/contracts. 

* Track monthly membership to view trends and confirm accountable care PMPM payments

* Determine project membership for the upcoming year based on prospective lists at end/start of year.

* Maintain historical data of patients for continuity of care as members fall off or get added to the list

* Performance reporting on specific targets and measures.

Using FHIR based APIs, providers and payers can exchange Member Attribution Lists which can then enable existing business processes and systems to meet the above business needs. The creation of a Member Attribution List typically starts with a need to identify the patients for a specific purpose such as Risk Based Contracts or Quality Reporting. Once the patients are identified other FHIR APIs and DaVinci specifications can be used to retrieve clinical, financial, and other relevant information as needed.

### Example Member Attribution List Exchange Scenarios 

#### Scenario 1

Provider Organization A enters a risk-based contract with Payer B. As part of establishing the contract, they document specific measures, targets, and financial incentives. Payer B uses historical claims and other information present about members to create a Member Attribution List for Provider Organization A. The Member Attribution List identifies the list of patients that Provider Organization A is responsible for, according to the contract. Payer B needs to exchange this list with Provider Organization A periodically to ensure that Provider Organization A remains aware of the list of patients they are contractually responsible for and any changes that may occur. Payer B could publish the list in a standard way and Provider Organization A would then retrieve the list. Alternatively Provider Organization A may request for the list and Payer B should provides the list once it is ready.

<div class="bg-success" markdown="1">

#### Scenario 2

Provider Organization A enters a contract with Payer B. As part of establishing the contract, they document specific measures, targets, and financial incentives. Provider Organization A assembles the list of members for whom they are responsible and creates an initial Member Attribution List to provide to Payer B. Payer B uses historical claims and other current information about members to update the provided Member Attribution List. The list is then published by Payer B to Provider Organization A. Provider Organization A retrieves the list and identifies changes that need to be made, then notifies the Payer B about the changes, in terms of additions and removals. Payer B either accepts or rejects the changes and may modify the existing Member Attribution List. If the list is modified, Payer B notifies Provider Organization A of the changes. Once Provider Organization A and Payer B finally agree upon a Member Attribution List they can start using the list for various business needs. 

</div>

#### Use of Member Attribution List as part of the Data Exchange for Quality Measures and Care Gaps

Member Attribution Lists are fundamental to closing care gaps and reporting quality measures. Providers have to report specific quality measures on certain patients to payers on specific quality measures and close any care gap requirements that may exist. Providers and Payers agree upon the list of patients for whom reporting needs to be performed on a regular basis. Similarly care gaps associated with these patients have to be closed to receive applicable financial incentives. In all these cases the agreement on what is the "list of patients" is critical. This function is served by the Member Attribution List. The Member Attribution List should be agreed upon by the Payers and Providers and exchanged on a regular cadence. Based on the patients in the Member Attribution List Payers can request for specific quality measure and care gaps data from Providers. Similarly, Providers can close care gaps for patients attributed to them via the Member Attribution List and can report quality data using the Data Exchange for Quality Measures DaVinci implementation guide.

<div class="bg-success" markdown="1">

#### Use of Member Attribution List for CMS Data at Point of Care (DPC) use case

The Centers for Medicare and Medicaid Services (CMS) Data at the Point of Care (DPC) API is currently in a pilot phase. As such,  only a limited number of users can access Medicare Fee-For-Service claims data through the API. This pilot program promotes the industry-standard HL7 Fast Healthcare Interoperability Resources (FHIR), specifically the Bulk FHIR specification. The mechanisms used by the DPC program have been outlined in this implementation guide which includes the creation of the Member Attribution List, requesting changes or updates to the Member Attribution List, and requesting claims data using the Bulk Data operations specifically the /Group/[id]/$davinci-data-export operation.

#### Use of Member Attribution List for CMS Beneficiary Claims Data API (BCDA) use case

The Beneficiary Claims Data API (BCDA) is an Application Programming Interface (API) that enables Accountable Care Organizations (ACOs) to retrieve Medicare claims data for their beneficiaries. BCDA serves as a direct pipeline from CMS to ACO systems to provide claims data at a more timely cadence. This includes Medicare claims data for instances in which beneficiaries receive care outside of the ACO, allowing a full picture of patient care. The BCDA initiative provides claims data, represented using Patient, Coverage and Explanation of Benefit FHIR resources, to the ACOs. CMS utilizes an attribution file to create the list of beneficiaries relevant to an ACO and then uses the Group resource to represent the beneficiary list. The Member Attribution List is represented using the data model present in this Implementation Guide. The claims data can be accessed using the same /Group/[id]/$davinci-data-export bulk data operation also specified in this Implementation Guide. 

#### Use of Member Attribution List for DaVinci Pdex use cases 

The DaVinci Pdex use cases for Payer to Payer exchange can utilize the DaVinci-data-export operation, as defined in the guide to exchange large amounts of data using the bulk data asynchronous pattern. The actual content to be exchanged will be defined in the Pdex IG in the future.

</div>


### Member Attribution List workflows and definitions

The following definitions are used in the Member Attribution List implementation guide.

1. __MemberId:__
A unique identifier for a member within a payers plan.

2. __Payer Identifier:__ 
A unique identifier for an organization that provides insurance plans and enters into contracts with health care providers.

3. __Contract Identifier:__
A unique identifier assigned by the Payer to their agreement with a specific healthcare provider.

4. __Plan Identifier:__
A unique identifier for an insurance plan that a payer provides. Members belong to specific plans.

**NOTE:** The combination of Member Identifier, Payer Identifier, Contract Identifier, and Plan Identifier is always unique.

5. __Attribution:__ 
Results of an Algorithmic or manual process that assigns patients to providers or payers. Alternatively a patient could declare to be part of a Group by providing or selecting their PCP information or ACO information.

6. __Member Attribution List:__
Enumeration of patients who are attributed to payers, providers, medical homes or groups. Patients may belong to multiple plans. 
The Attribution list contains the patients information along with other information such as Attributed Provider, Health Plan information, Validity Period for the list, Risk Information etc. A member may be present multiple times within a Member Attribution List, however the combination of Member Identifier, Payer Identifier, Contract Identifier and Plan Identifier is always unique. That  combination can be used to identify the member.

7. __Attributed Provider:__
The Provider responsible for managing the quality and costs of a patient’s health care, per the contract and who will receive the payments and credits based on performance.

8. __Attribution Period:__
The period over which the member is attributed to a specific provider. The period has a start and an end date.

8. __Producer:__
An Entity that creates the Member Attribution List and owns the master copy of the list. 
Producers allow changes to be made to the list. 
A Producer may receive an initial list from the Consumer, upon receiving they will own the list and publish the list for consumption.

9. __Consumer:__ 
An Entity that utlizes the Member Attribution List. 
Consumers may contribute to the creation of the list owned by the Producer.
Consumers may request changes be made to the list owned by the Producer.
Consumers may receive an initial list from the Producer and request changes before reaching final agreement on the list.

10. __Member Attribution List Data:__
Data contained within the Member Attribution List. This includes
* Patient Demographics Data 
* Attributed Provider Data (First Name, Last Name, Id, NPI, TIN, Address)
* Health Plan Data (Subscriber Id, Member Id, Medicare Id, Medicaid Id, Plan Name, Plan Type, Enrollment Start and End Dates)
* Attribution Data (Effective Start and End Date for Attribution, Attribution Method, Risk score)
* Miscellaneous Data (ACO Information, Conditions)

11. __Member Attribution List Changes:__ 
Changes in Member Attribution List Data, such as the addition or deletion of patients from the list.

### Member Attribution List Exchange for Scenario #1

{% include img.html img="workflow.png" caption="Figure 2: Member Attribution List Exchange Workflow for Scenario #1" %}

The following is a brief description of the workflow steps with a Payer representing the Producer and a Provider Organization representing the Consumer. 

**1. Payer (Producer) and Provider (Consumer) enter into a contract **<br/>
Provider and a Payer enter into a contract with specific terms and conditions and decide on the need for a Member Attribution List. Payer internally creates the Member Attribution List using internal processes and existing data about the patients. 

**2. Payer (Producer) Informs Provider (Consumer) and makes the List available to the Provider **<br/>
In this step the Payer informs the Provider about the list and makes it available to the Provider. The specific mechanism of how this exchange happens varies based on Payers and Providers. This implementation guide will specify standards for this interaction.

**3a. Provider (Consumer) informs Payer (Payer) about changes **<br/>
Once the Provider receives the list in Step 2, Provider reconciles the list with internal lists and data, if changes are needed, they notify the Payer about the specific changes. These changes could be to add additional patients, remove patients from the list etc. The specific mechanism of how this exchange happens varies based on Payers and Providers. 
If the Consumer has no changes, then Step 3a would not be executed and the Consumer has accepted the list for usage. 

Note: Steps 2 and 3a may be repeated as many times as needed until the Producer and Consumer agree upon the Member Attribution List.

**3b. Provider (Consumer) informs Payer (Producer) about no changes **<br/>
Once the Provider receives the list in Step 2, the Provider reconciles it with internal lists and data, in case where no changes are needed, they then notify the Payer about finalizing the list. The specific mechanism of how this exchange happens varies based on Payers and Providers. 

**4. Payer (Producer) makes list available to Provider (Consumer) **<br/>
Once the list is finalized, the Payer and Provider agree to exchange the list periodically as required. The specific mechanism of how this exchange happens varies based on Payers and Providers. This is accomplished by using the APIs specified by this implementation guide.

**NOTE:** The above workflow is the normal scenario. In addition to the above workflow the Producer may change the list periodically based on additional data. As this happens the Producer may decide to repeat Steps 2 through 4. The Producer and Consumer may use the notification capability using Subscriptions to keep track of changes to the Member Attribution List. Alternatively, the Producer and Consumer may agree upon a cadence to exchange the Member Attribution List based on business requirements.
Every change that is made to the list may be available to the Consumer via APIs in real-time or at specified intervals. For example, if it is a monthly list, then as changes get made the updated list will be exchanged on a monthly basis. The Producer may enable the Member Attribution List retrieval APIs continuously and allow Consumers to retrieve the [Member Attribution List data](usecases.html#member-attribution-list-workflows-and-definitions) at their convenience. 

#### Considerations

* The scenario above uses the term 'Producer'.  Typically, that would be a Payer organization, but in some cases, it could be a Provider Organization. This is true in [Data at Point of Care use cases](https://dpc.cms.gov/).

<div class="bg-success" markdown="1">

### Member Attribution List Exchange for Scenario #2 (STU2 Workflow)

{% include img.html img="workflow-scenario2.png" caption="Figure 3: Member Attribution List Exchange Workflow for Scenario #2" %}

The following is a brief description of the workflow steps with a Payer representing the Producer, and a Provider Organization representing the Consumer. This workflow differs from the previous workflow in that the Consumer is creating the Member Attribution List first and then providing the list to the Producer.

**1. Payer (Producer) and Provider (Consumer) enter into a contract **<br/>
Provider and a Payer enter into a contract with specific terms and conditions and decide on the need for a Member Attribution List. Payer supports the capabilities required to create a Member Attribution List.

**2. Provider (Consumer) creates the list in the Payer (Producer) system **<br/>
In this step the Provider creates the Member Attribution List in the payer system.

**3. Payer (Producer) reconciles the list internally and notifies Provider (Consumer) of changes **<br/>
Once the Payer receives the list in Step 2, the Payer may reconcile the list internally, modify it and then notify the Provider of the changes. 

**4. Provider (Consumer) reconciles the list and requests additional changes to the list by adding and removing members **<br/>
Providers reconcile the list internally and identify that there may be members who need to be added and members who need to be removed from the list. To do so, the Provider uses the member-add and member-remove APIs to add and remove members from the list.
Payers (Producrers) can decide if the members should be added or removed based on the request.

**NOTE** Steps 3 and 4 can be repeated as many times as needed until the Producer and the Consumer agree upon a final list.

**5. Payer (Producer) and Provider (Consumer) agree upon a Member Attribution List for a specific use case when the Consumer indicates there are no more changes to be made **<br/>
Consumer invokes the confirm-attribution-list operation to indicate there are no further changes to be made to the Member Attribution List. Providers and Payers agree upon the finalized Member Attribution List for various use cases.

</div>
