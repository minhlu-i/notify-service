# Notify Service

## Planning the integration

1. Anything that happened in the system from the business point, can trigger notification(s).
2. Notifications to send can be targeted to one or more recipients or a group of recipients.
3. We need to support different channels of notifications: Email, SMS, Push for Android/iOS devices, in-app.
4. Notifications should be localized, with means to support different languages and time zones at least.
5. Users should have access to their previous/old notifications (AKA notifications or notification center).
6. Some push or email notifications shouldn’t be recorded/visible in the user’s notification center (such as a marketing alert about a discount, or another short-living alert), and vice versa, some notifications that are visible in the user’s notification center, shouldn’t have produced an alert such as a push notification (or an email have been sent).
7. Users should be able to customize the notifications consumption (frequency, categories, channels ..), for example, set a preferred channel for some type of notifications, or even turn that off.

## Technical requirements

1. The setup code should be easy to understand/maintain.
2. Integration of new notifications is simple, fast and straightforward, without modifying any existing code, but only by extending it by a pattern/convention that is used for the previous notifications.
3. Easy to change existing notifications without affecting other parts (e.g. remove the push channel for a specific type without touching any setup code, without affecting other notifications).
4. Easy to add new channels/providers (e.g. browser notifications, WhatsApp messages).
5. A very straightforward way of adding/editing new translations (localization) for specific notifications. And quick or even immediate reflection of new translations to the working system.
6. Adding new settings for users to customize notifications is not a headache.
7. Overall service is highly testable, so covering with integration/backend e2e tests is not time-consuming
8. Easy to debug specific cases.

## What we will need to have

1. Trigger. We will need to have triggers that will produce notifications.

   E.g. in an e-commerce business “order-created” event where we need to send notifications to the order owners, means buyer and seller, and maybe another notification to finance or whatever company department. Let’s consider we already have triggers from other services, in the form of events mentioned above.

2. Template service(s) for building email messages based on templates, similar but maybe less complicated generators for other channels (Push, SMS ..). There are lots of open-source solutions for that in almost all the popular languages.

3. Localization service for translations.

    For example, we don’t want to persist a bunch of text in DB for showing notification history in the client app, but we want the app to build the text depending on the language and other parameters after the history is fetched to the client app. Same for the backend, for sending localized push we need to build localized push notifications using our translations. As we want to have localized notifications I assume our infrastructure already supports localization, and we already should be using some custom build or 3rd party service. In my case, our company already had localization service.

4. Service that handles the trigger, does the core logic and is capable of sending and/or persisting notifications.

5. Provider integrations. Email, APNS for ios, FCM for Android, etc. depending on what providers we need.

## System design

![System design](assets/images/system.png)

## Service Architecture

### Database design

![database design](assets/images/database_design.png)
