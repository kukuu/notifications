# Notifications

Rich Interactive Customer Engagement for Gamification and Ecommerce.

This is a PHP implementation of Rich Interactive Notification to deliver Text and Video from a Cloud SaaS platform.

## Implementation steps: 
To implement a simple notification system that allows text messages and videos to be delivered using PHP, with log-in access control for an Administrator and a user, and with SaaS (Software as a Service) multi-tenancy features (Tenant ID and API key), you need to address the following key components:

### Components of the Solution:

1. Multi-Tenant Setup:

Each client (tenant) will have a Tenant ID and API Key to access the notification platform.

2. User Roles (Access Control):

3. Administrator: Can manage users and notifications, view logs, and handle system settings.
User: Can log in, send notifications, and view their own activity logs.


4. Notification System:

A simple mechanism to send text messages and videos via a web-based platform.
Logs every action performed by a user for audit purposes.

5. API Authentication:

Authentication through Tenant ID and API Key to ensure secure access for each client.
