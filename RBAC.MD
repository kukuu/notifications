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

3. PHP Classes: Now, let's create the PHP classes to manage users, roles, and permissions.

a. DB Connection

```
class DB {
    private static $instance = null;

    public static function getInstance() {
        if (self::$instance == null) {
            self::$instance = new PDO('mysql:host=localhost;dbname=rbac_db', 'username', 'password');
            self::$instance->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
        }
        return self::$instance;
    }
}

```

b. RBAC Class: This class contains methods to check user roles and permissions.

``` 
class RBAC {

    // Get all roles for a user
    public static function getUserRoles($userId) {
        $db = DB::getInstance();
        $query = $db->prepare("SELECT r.role_name FROM roles r 
                               JOIN user_roles ur ON r.id = ur.role_id
                               WHERE ur.user_id = :userId");
        $query->execute(['userId' => $userId]);
        return $query->fetchAll(PDO::FETCH_COLUMN);
    }

    // Get all permissions for a user
    public static function getUserPermissions($userId) {
        $db = DB::getInstance();
        $query = $db->prepare("SELECT p.permission_name FROM permissions p
                               JOIN role_permissions rp ON p.id = rp.permission_id
                               JOIN user_roles ur ON ur.role_id = rp.role_id
                               WHERE ur.user_id = :userId");
        $query->execute(['userId' => $userId]);
        return $query->fetchAll(PDO::FETCH_COLUMN);
    }

    // Check if a user has a specific permission
    public static function hasPermission($userId, $permission) {
        $permissions = self::getUserPermissions($userId);
        return in_array($permission, $permissions);
    }

    // Check if a user has a specific role
    public static function hasRole($userId, $role) {
        $roles = self::getUserRoles($userId);
        return in_array($role, $roles);
    }
}


```

c. Authentication (Login Example)

``` 
session_start();

class Auth {
    public static function login($username, $password) {
        $db = DB::getInstance();
        $query = $db->prepare("SELECT * FROM users WHERE username = :username");
        $query->execute(['username' => $username]);
        $user = $query->fetch(PDO::FETCH_ASSOC);

        if ($user && password_verify($password, $user['password'])) {
            $_SESSION['user_id'] = $user['id'];
            return true;
        }
        return false;
    }

    public static function logout() {
        session_destroy();
    }

    public static function isLoggedIn() {
        return isset($_SESSION['user_id']);
    }

    public static function getUserId() {
        return $_SESSION['user_id'];
    }
}


```

4. Usage Example
Check if a logged-in user has a particular permission before accessing a resource.

``` 
session_start();

if (Auth::isLoggedIn()) {
    $userId = Auth::getUserId();

    // Example of role check
    if (RBAC::hasRole($userId, 'Admin')) {
        echo "You are an Admin";
    }

    // Example of permission check
    if (RBAC::hasPermission($userId, 'Edit')) {
        echo "You have permission to edit";
    } else {
        echo "Access Denied: You do not have permission to edit.";
    }
} else {
    echo "Please log in first.";
}

``` 

5. Customisation and Integration

The above RBAC system can be further customized to fit the needs of different applications:

Granular permissions: You can create more fine-grained permissions (like Edit_Post, Delete_Post) depending on your business requirements.
Audit trail: Track when users perform actions based on their roles and permissions by adding logs to record significant actions or changes.
Scalability: This solution can scale by handling role-based permissions across multiple modules and integrating into complex systems.
6. Testing and Maintenance
Regularly test the role-permission mappings and ensure that any new roles or permissions are correctly reflected in the database. Automate permission assignment and audits as part of the deployment process to maintain consistency.


Conclusion:
This RBAC implementation is modular, scalable, and highly customizable, providing a robust security mechanism for managing users' access levels in a PHP application. You can extend this to include APIs, multi-level roles, and more complex permission rules as needed.
