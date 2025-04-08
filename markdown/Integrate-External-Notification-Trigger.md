---
stoplight-id: wiqclsdfoeau5
---

# How to trigger Notifications form external systems

Goal of this guide is to give you an overview of the different components used for sending a
notification, and how you can use the Shopgate Notification System to send out notifications via
an external system.

## Prerequisites
- You have read the [support article about notifications](https://support.shopgate.com/knowledge/push-nachrichten) and know how Campaigns & Templates work together.
- You have the swagger file of the [notification service](https://s3.eu-central-1.amazonaws.com/shopgatedevcloud-bigapi/swagger-docs/omni/static.html?url=https://s3.eu-central-1.amazonaws.com/shopgatedevcloud-bigapi/swagger-docs/omni/notification2-crud.yaml#/) available to check
- You have the swagger file of the [notification event receiver service](https://s3.eu-central-1.amazonaws.com/shopgatedevcloud-bigapi/swagger-docs/omni/static.html?url=https://s3.eu-central-1.amazonaws.com/shopgatedevcloud-bigapi/swagger-docs/omni/notification-event-receiver-crud.yaml) available to check

## Overview
To send a notification to your customers, you need to create a campaign. In the
Campaign you configure:
- When the notification should be send out (event based)
- The title & message of the notification
- What should happen in the app when the notification is opened  

Event based notifications will be sent automatically when the corresponding event is triggered. If you are using custom events, you need to trigger the custom event via the Notification Event
Receiver Service. 

A campaign with triggerType “event” can be dispatched multiple times. So you can use the same
campaign multiple times, to send notifications to multiple different users at different times.

As a summary, the following steps have to be done:
1. Create a campaign
3. Trigger the Event

## Creating a campaign
Campaigns can be created via Shopgate Admin or via API.
To create a campaign via the API use the route
```json
POST /merchants/{merchantCode}/campaigns
```
See swagger file for details about this call.
If you want to send the campaign based on a custom event, you have to create the campaign
with 
* “triggerType” = “event”
* “settings.eventType” = “custom”
* “settings.customEvent” = “yourEventName”

For custom event campaigns you can also use custom variables in the message & title. These
custom variables then have to be passed when triggering the event. Custom variables have to be
in the following format:    

**{{custom.myVariable}}**

## Triggering a custom event
To trigger a custom event, you have to call the Notification Event Receiver Service with the route
```json
POST /merchants/{merchantCode}/customNotificationEvent
```
When triggering a custom event, you can also further specify the recipients by passing
additionalFilter. For example if you want to send the notification only to a specific customer,
just pass an additionalFilter to filter for a specific email address.
If you used custom variables in the message, these also need to be passed along via
customVariables.
