# Rich Media Notifications

This is a rich interactive customer engagement for Gamification, Ecommerce and a PHP implementation.

The application delivers Text and Video from a Cloud based SaaS platform. The system allows text messages and videos to be delivered to Internet connectivity devices and requires a log-in access control for an Administrator and a Tennant. The application is  a multi-tenancy system and requires Tenant ID and API key to access and create a Notification.

## Components of the Solution:

1. Multi-Tenant Setup: Each client (tenant) will have a Tenant ID and API Key to access the notification platform: 

2. User Roles (Access Control):

3. Administrator: Can manage users and notifications, view logs, and handle system settings.
User: Can log in, send notifications, and view their own activity logs.


4. Notification System: A simple mechanism to send text messages and videos via a web-based platform.
Logs every action performed by a user for audit purposes.

5. API Authentication: Authentication through Tenant ID and API Key to ensure secure access for each client.

## Implementation steps: 

1. Database Schema: Create tables for Users, Roles, Permissions, and the many-to-many relationships between them (User-Roles and Role-Permissions): https://github.com/kukuu/notifications/blob/main/database-schema.md
2. User Authentication (Login System): First, we need an authentication mechanism where users and admins log in using a username, password, Tenant ID, and API key.

   a. Login Form: https://github.com/kukuu/notifications/blob/main/login-form.md

   b. Login Logic (login.php): https://github.com/kukuu/notifications/blob/main/login.md
4. Dashboard and Access Control : This is a sample code for an access control system that restricts access to different pages based on user roles.

   a. Dashboard (dashboard.php): https://github.com/kukuu/notifications/blob/main/dashboard.md
   
6. Sending Notifications (send_notification.php): Both text messages and video URLs can be sent through the system.

   a. Notification Form: https://github.com/kukuu/notifications/blob/main/notification-form.md

   b. Notification Logic (send_notification.php): https://github.com/kukuu/notifications/blob/main/notification-logic.md
   
8. Viewing Logs (view_logs.php): The admin can view logs of actions performed by users.
9. Registeration and API Key Generation
 
