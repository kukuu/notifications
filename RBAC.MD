# RBAC

A Role-Based Access Control (RBAC) implementation in PHP consists of multiple components that enforce security by assigning permissions to roles, and roles to users. In a typical RBAC system, roles are defined with specific permissions, and users are assigned to one or more roles. Below is an example of a basic yet thorough PHP RBAC implementation:

## Components:
i. Users Table: Stores the user information.

ii. Roles Table: Stores the roles (e.g., Admin, Editor, Viewer).

iii. Permissions Table: Stores different permissions (e.g., Create, Edit, Delete).

iv. Role-Permissions Table: Maps roles to their respective permissions.

v. User-Roles Table: Maps users to their respective roles.


## Step-by-step Implementation:
1. Database Schema
Create tables for Users, Roles, Permissions, and the many-to-many relationships between them (User-Roles and Role-Permissions).
