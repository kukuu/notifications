# Notifications

This is a PHP implementation of a rich interactive customer engagement Cloud based  SaaS Notification  platform for E-commerce and Gamification. 

The application delivers Text and Video from a Cloud based SaaS platform. The system allows text messages and videos to be delivered to Internet connectivity devices and requires a log-in access control for an Administrator and a Tennant. The application is  a multi-tenancy system and requires Tenant ID and API key to access and create a Notification.

Each notification and log is tied to the tenant_id so that data is isolated by tenant. Only users from the same tenant can view or send notifications for their respective tenants.

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
   
8. Viewing Logs (view_logs.php): The admin can view logs of actions performed by users: https://github.com/kukuu/notifications/blob/main/view-logs.md
9. Registeration and API Key Generation : API keys for tenants can be generated using bin2hex() or a similar function in PHP when a new tenant registers:

To extend an API generation key functionality in a registration form accessible via a link from the login page that requires email verification and confirmation of admin status, you can follow this approach:

Steps for Implementation:

1. Login Page Link:

a. Provide a link on the login page for "Generate API Key".

b. The link redirects to a separate API Key Registration form.


2. Registration Form:

The form should have fields for:

a. Email (required to verify the user's identity)

b. Confirmation of Admin Role (this can be a hidden field checked against the database or a checkbox for simplicity).

c. Generate Key button, which calls the function to generate an API key.


3. API Key Generation:

On submitting the form, check:

a. The email exists and is associated with a valid admin account.

b. If the user has an Admin role, proceed with generating an API key.

c. Generate a unique API key for the user.

d. Save the key in the database linked to the tenant ID.


4. Send API Key:

a. Upon successful generation, the key should be displayed or sent via email.


https://github.com/kukuu/notifications/blob/main/registration-and-apiKeyGeneration.md 


## Conclusion:

This implementation provides a basic structure for a notification system where users and administrators from different tenants can log in, send notifications (text messages and videos), and view their own logs. Each tenant has its own API key, and access control is based on user roles (admin and user). You can extend this by integrating with SMS APIs or video delivery platforms if required.
 
