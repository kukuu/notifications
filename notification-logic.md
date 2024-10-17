```
session_start();
include 'db.php';

if ($_SERVER['REQUEST_METHOD'] == 'POST') {
    $message = $_POST['message'];
    $video_url = $_POST['video_url'];
    $user_id = $_SESSION['user_id'];
    $tenant_id = $_SESSION['tenant_id'];

    // Insert notification into the database
    $stmt = $db->prepare("INSERT INTO notifications (user_id, tenant_id, message, video_url) VALUES (?, ?, ?, ?)");
    $stmt->execute([$user_id, $tenant_id, $message, $video_url]);

    // Log the action
    $stmt = $db->prepare("INSERT INTO logs (user_id, action) VALUES (?, 'Sent a notification')");
    $stmt->execute([$user_id]);

    echo "Notification sent!";
}


```
