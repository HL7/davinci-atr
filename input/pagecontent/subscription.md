This section defines the specific requirements related to Subscriptions for notifications of Member Attribution List changes. The specification focuses on the creation of SubscriptionTopics in the Producer's systems, and notifications from the Producer to the Consumer (subscriber to the topic) when the Member Attribution List changes.
 

### Usage of FHIR Subscriptions Backport IG to implement Subscriptions

The Member Attribution List IG leverages the [Subscriptions R5 Backport IG](({{site.data.fhir.ver.subscriptionsIg}}/index.html) to implement Subscriptions and associated notifications. The following is the SubscriptionTopic URL that has to be used in the creation of the Subscription. 

#### SubsciptionTopic and Canonical URL

This section identifies the topic and the Canonical URL for the topic.This URL **SHALL** be used by the Consumer to create a Subscription for notification. 


|Notification/Named Event/SubscriptionTopic	| Canonical Url 	| ResourceId/ResourceType expected as part of notification	|
| :---										| :---			| :--- 														|
| atr-list-change							|http://hl7.org/fhir/us/davinci-atr/SubscriptionTopic/atr-list-change|Group|

   
The following is an example of the Member Attribution List change SubscriptionTopic.

* [atr-list-change Subscription](StructureDefinition-atr-list-change-subscription.html)


#### Consumer Requirements for Subscription Creation

* The Consumer **SHOULD** support the creation of a SubscriptionTopic by a Consumer.

* When the Consumer creates Subscription resources in the Producer system, the Consumer **SHALL** represent the canonical URL for the atr-list-change topic from the above table as part of the Subscription.criteria element.

* When the Consumer creates Subscription resources in the Producer system, the Consumer **SHALL** identify the specific Member Attribution List for change notification using the Group/id as the value of the Subscription.criteria.extension element.

* When the Consumer creates Subscription resources in the Producer system, the Consumer **SHALL** identify the Subscription to be active using the Subscription.status field.

* When the Consumer creates Subscription resources in the Producer system, the Consumer **SHALL** identify the Subscription payload to be fhir+json using the Subscription.payload field.

* When the Consumer creates Subscription resources in the Producer system, the Consumer **SHALL** identify that the notification must include only the id using the Subscription.payload.extension.

* Consumers intending to receive notifications via Subscriptions **SHALL** implement a rest-hook channel to receive notifications from the Producer.   

* Consumers **SHALL** update previously created Subscriptions in the Producer system and turn them off using the Subscription.status field, when the specific Member Attribution List is not used anymore.

#### Producer Requirements for Subscriptions

* Producer **SHOULD** support creation of Subscriptions for atr-list-change topic.

* Producer **SHOULD** support updating of Subscriptions for atr-list-change topic.

* When supporting Subscriptions, Producers **SHALL** verify that the Consumer has the necessary authorization to subscribe to the Member Attribution List specified using the Group/id as part of the Subscription.criteria.extension element.

* When Consumers do not have the right authorization for the Member Attribution List, Producers **SHALL** reject the create or update of the Subscription for the specific Member Attribution List with a status code of 401. 

* When supporting Subscriptions, the Producer **SHALL** support the channel of type rest-hook to notify the subscribers of changes.

* When supporting Subscriptions, the Producer **SHALL** support a notification payload type of id-only where the id of the changed resource is included.

* When supporting Subscriptions, Producers **SHALL** notify the subscribers of Member Attribution List changes when the Subscription.status is active.


### Implementing Notifications without using FHIR Subscriptions 

There are situations where the Producers have not implemented the FHIR Subscriptions capability. To enable implementation of the Member Attribution List use cases in these situations, the Producer and Consumer may use alternative mechanisms to receive notifications.

Example of alternative mechanisms include email notifications between contact persons representing Producer and Consumer, regular periodic download of the attribution list by Consumers.

