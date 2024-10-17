```
session_start();
include 'db.php';

if ($_SESSION['role'] != 'admin') {
    echo "Access denied.";
    exit();
}

$stmt = $db->prepare("SELECT * FROM logs");
$stmt->execute();
$logs = $stmt->fetchAll(PDO::FETCH_ASSOC);

echo "<h1>Logs</h1>";
foreach ($logs as $log) {
    echo "User ID: " . $log['user_id'] . " Action: " . $log['action'] . " at " . $log['created_at'] . "<br>";
}


```
