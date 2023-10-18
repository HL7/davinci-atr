This section defines the specific requirements related to Subscriptions and Notifications Attribution List changes. The specification focuses on the creation of SubscriptionTopics in the Producer's systems, and notifications from the Producer to the Consumer (subscriber to the topic) when the list changes.
 

### Usage of FHIR Subscriptions Backport IG to implement Subscriptions

The Member Attribution List IG leverages the Subscriptions Backport IG to implement Subscriptions and associated notifications. The following are the Subscription Topic URLs that need to be used in the creation of the Subscription. 

#### SubsciptionTopic (Notification Events) and Canonical Url

This section identifies the topic and the Canonical URL for the topic. These URLs **SHALL** be used to create Subscription. 


|Notification/Named Event/Subscription Topic	| Canonical Url 	| ResourceId/ResourceType expected as part of notification	|
| :---										| :---			| :--- 														|
| atr-list-change							|http://hl7.org/fhir/us/davinci-atr/SubscriptionTopic/atr-list-change|Group|

   
The following is an example of the atr-list-chagne SubscriptionTopic.

* [atr-list-change Subscription](StructureDefinition-atr-list-change-subscription.html)


#### Consumer Requirements for Subscription Creation

* The Consumer **SHOULD** support the creation of a SubscriptionTopic by a Consumer.

* When the Consumer creates subscription resources in the Producer system, the Consumer **SHALL** represent the Canonical URL for the atr-list-change topic from the above table as part of the Subscription.criteria element.

* When the Consumer creates subscription resources in the Producer system, the Consumer **SHALL** identify the specific Member Attribution List for change notification as part of the Subscription.criteria.extension element.

* When the Consumer creates subscription resources in the Producer system, the Consumer **SHALL** identify the Subscription to be active using the Subscription.status field.

* Consumers intending to receive notifications via Subscriptions **SHALL** implement a rest-hook channel to receive notifications from the Producer.   

* Consumers **SHALL** update previously created Subscriptions in the Producer system and turn them off using the Subscription.status field, when the specific attribution list is not used anymore.

#### Producer Requirements for Subscriptions

* Producer **SHOULD** support creation of Subscriptions for atr-list-change topic identified in the above table.

* Producer **SHOULD** support updating of Subscriptions for atr-list-change topic identified in the above table.

* When supporting subscriptions, Producers **SHALL** verify that the Consumer has the necessary authorization to subscribe to the Member Attribution List specified using the Group/id as part of the Subscription.criteria.extension element.

* When Consumers do not have the right authorization for the Member Attribution List, Producers **SHALL** reject the create or update of the Subscription with a status code of 401. 

* Producer **SHOULD** support the channel of type rest-hook to notify the subscribers of changes.

* Producer **SHOULD** support a notification payload type of id-only where the id of the changed resource is included.

* When supporting subscriptions, Producers **SHALL** notify the subscribers of attribution list changes when the Subscription.status is active and the 


### Implementing Notifications without using FHIR Subscriptions 

There are situations where the Producers have not implemented the Subscriptions capability. To enable implementation of the Member Attribution List use cases in these situations, the Producer and Consumer may use alternative mechanisms to receive notifications.

Example of alternative mechanisms include email notifications between contact persons representing Producer and Consumer, regular periodic download of the attribution list by Consumers.

