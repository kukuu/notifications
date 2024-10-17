# Rich Media Notifications

Rich Interactive Customer Engagement for Gamification and Ecommerce.

This is a PHP implementation of Rich Interactive Notification to deliver Text and Video from a Cloud based SaaS platform. The system allows text messages and videos to be delivered from a PHP application. It requires a log-in access control for an Administrator and a Tennant. The application is  a multi-tenancy system and requires Tenant ID and API key:

## Components of the Solution:

1. Multi-Tenant Setup: Each client (tenant) will have a Tenant ID and API Key to access the notification platform.

2. User Roles (Access Control):

3. Administrator: Can manage users and notifications, view logs, and handle system settings.
User: Can log in, send notifications, and view their own activity logs.


4. Notification System: A simple mechanism to send text messages and videos via a web-based platform.
Logs every action performed by a user for audit purposes.

5. API Authentication: Authentication through Tenant ID and API Key to ensure secure access for each client.

## Implementation steps: 

1. Database Schema:
2. User Authentication (Login System)

   a. Login Form:

   b. Login Logic (login.php):
4. Dashboard and Access Control

   a. Dashboard (dashboard.php):
   
6. Sending Notifications (send_notification.php)

   a. Notification Form:

   b. Notification Logic (send_notification.php):
   
8. Viewing Logs (view_logs.php)
9. Registeration and API Key Generation
 
