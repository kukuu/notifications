# RBAC

A Role-Based Access Control (RBAC) implementation in PHP consists of multiple components that enforce security by assigning permissions to roles, and roles to users. In a typical RBAC system, roles are defined with specific permissions, and users are assigned to one or more roles. Below is an example of a basic yet thorough PHP RBAC implementation:

## Components:
i. Users Table: Stores the user information.

ii. Roles Table: Stores the roles (e.g., Admin, Editor, Viewer).

iii. Permissions Table: Stores different permissions (e.g., Create, Edit, Delete).

iv. Role-Permissions Table: Maps roles to their respective permissions.

v. User-Roles Table: Maps users to their respective roles.


## Step-by-step Implementation:
1. Database Schema: 
Create tables for Users, Roles, Permissions, and the many-to-many relationships between them (User-Roles and Role-Permissions).

``` 
-- Users Table
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    password VARCHAR(255) NOT NULL
);

-- Roles Table
CREATE TABLE roles (
    id INT AUTO_INCREMENT PRIMARY KEY,
    role_name VARCHAR(50) NOT NULL
);

-- Permissions Table
CREATE TABLE permissions (
    id INT AUTO_INCREMENT PRIMARY KEY,
    permission_name VARCHAR(50) NOT NULL
);

-- User Roles Table (Mapping users to roles)
CREATE TABLE user_roles (
    user_id INT NOT NULL,
    role_id INT NOT NULL,
    PRIMARY KEY (user_id, role_id),
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE,
    FOREIGN KEY (role_id) REFERENCES roles(id) ON DELETE CASCADE
);

-- Role Permissions Table (Mapping roles to permissions)
CREATE TABLE role_permissions (
    role_id INT NOT NULL,
    permission_id INT NOT NULL,
    PRIMARY KEY (role_id, permission_id),
    FOREIGN KEY (role_id) REFERENCES roles(id) ON DELETE CASCADE,
    FOREIGN KEY (permission_id) REFERENCES permissions(id) ON DELETE CASCADE
);

```

2. Data Example: Inserting data into the roles, permissions, and role_permissions tables.

```
-- Insert Roles
INSERT INTO roles (role_name) VALUES ('Admin'), ('Editor'), ('Viewer');

-- Insert Permissions
INSERT INTO permissions (permission_name) VALUES ('Create'), ('Edit'), ('Delete'), ('View');

-- Assign Permissions to Roles
INSERT INTO role_permissions (role_id, permission_id) VALUES
(1, 1), -- Admin can Create
(1, 2), -- Admin can Edit
(1, 3), -- Admin can Delete
(1, 4), -- Admin can View
(2, 2), -- Editor can Edit
(2, 4), -- Editor can View
(3, 4); -- Viewer can only View


```
