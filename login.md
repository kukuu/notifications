```
session_start();
include 'db.php';  // Include DB connection

if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $tenant_id = $_POST['tenant_id'];
    $api_key = $_POST['api_key'];
    $username = $_POST['username'];
    $password = $_POST['password'];

    // Authenticate Tenant by Tenant ID and API Key
    $stmt = $db->prepare("SELECT * FROM tenants WHERE tenant_id = ? AND api_key = ?");
    $stmt->execute([$tenant_id, $api_key]);
    $tenant = $stmt->fetch(PDO::FETCH_ASSOC);

    if ($tenant) {
        // Authenticate User
        $stmt = $db->prepare("SELECT * FROM users WHERE username = ? AND tenant_id = ?");
        $stmt->execute([$username, $tenant['tenant_id']]);
        $user = $stmt->fetch(PDO::FETCH_ASSOC);

        if ($user && password_verify($password, $user['password'])) {
            // Store session variables
            $_SESSION['user_id'] = $user['user_id'];
            $_SESSION['tenant_id'] = $tenant['tenant_id'];
            $_SESSION['role'] = $user['role'];
            header("Location: dashboard.php");
        } else {
            echo "Invalid username or password.";
        }
    } else {
        echo "Invalid Tenant ID or API Key.";
    }
}

```
