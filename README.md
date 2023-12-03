# Notify Service

## Planning the integration

1. Anything that happened in the system from the business point, can trigger notification(s).
2. Notifications to send can be targeted to one or more recipients or a group of recipients.
3. The system should be able to prioritize notifications. OTPs are high-priority messages while news feed updates may be a lower priority.
4. We need to support different channels of notifications: Email, Push for Android/iOS devices, in-app.
5. Notifications should be localized, with means to support different languages and time zones at least.
6. Users should have access to their previous/old notifications (AKA notifications or notification center).
7. Some push or email notifications shouldn’t be recorded/visible in the user’s notification center (such as a marketing alert about a discount, or another short-living alert), and vice versa, some notifications that are visible in the user’s notification center, shouldn’t have produced an alert such as a push notification (or an email have been sent).
8. Users should be able to customize the notifications consumption (frequency, categories, channels ..), for example, set a preferred channel for some type of notifications, or even turn that off.
9. User can access to their service APIs with JWT token.

## Technique

1. Messaging systems: Kafka. Recive request create notification.
2. Storage: Cassandra. For Schema Flexibility, Write-heavy System, Highly available System.
3. APIs: Rust.
4. Notification delivery.
   - Email.
   - Push Notification (FCM).
   - In-app notification.
   - Webhook.

## System design

![System design](assets/images/system.png)

## Service Architecture

### Database design

![database design](assets/images/database_design.png)

## Reference:

- [Designing a Scalable Notification System in a System Design Interview](https://www.linkedin.com/pulse/design-notification-system-omar-ismail/)
- [Design a Notification System!](https://blog.devgenius.io/a-notification-system-is-a-critical-part-of-many-applications-and-platforms-enabling-users-to-stay-49540ac45a89)
