```
session_start();
if (!isset($_SESSION['user_id'])) {
    header("Location: login.php");
    exit();
}

// Check if the user is admin
if ($_SESSION['role'] == 'admin') {
    echo "<h1>Admin Dashboard</h1>";
    echo "<a href='manage_users.php'>Manage Users</a><br>";
    echo "<a href='view_logs.php'>View Logs</a><br>";
} else {
    echo "<h1>User Dashboard</h1>";
}

echo "<a href='send_notification.php'>Send Notification</a>";


```
