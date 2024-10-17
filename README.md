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

   b. Login Logic (login.php):
4. Dashboard and Access Control

   a. Dashboard (dashboard.php):
   
6. Sending Notifications (send_notification.php)

   a. Notification Form:

   b. Notification Logic (send_notification.php):
   
8. Viewing Logs (view_logs.php)
9. Registeration and API Key Generation
 
