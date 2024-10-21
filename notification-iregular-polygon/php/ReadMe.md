
# Task:

Compute geo-coordinates of an irregular polygon to locate when fans are within the boundaries and send notification alerts they have subscribed to on live event updates. 

## Solution Design:

This is  a PHP solution to compute whether fans are within the boundaries of an irregular polygon and send notification alerts if they have subscribed to live event updates.

This solution helps to determine if a fan is within an irregular polygon using the Ray-Casting algorithm and sends them notifications based on their location.

It can be extended by integrating third-party services for notifications, such as Firebase, Twilio, or email services like SendGrid. For a larger system, you can introduce a database to store fan subscriptions and preferences for live event updates.

### Steps

Step 1: Define the Polygon Coordinates
You will first define the irregular polygon as an array of geo-coordinates, which represents the event boundaries (stadium or location).

```
$polygon = [
    [51.5074, -0.1278], // Latitude, Longitude (Example Coordinates)
    [51.5080, -0.1285],
    [51.5090, -0.1270],
    [51.5085, -0.1260],
    [51.5078, -0.1268]
];


```

Step 2: Ray-Casting Algorithm in PHP
Next, we use the Ray-Casting algorithm to determine if a fan’s location is inside the polygon. This algorithm checks how many times a horizontal ray, starting from the point, crosses the polygon’s edges.

```
function isPointInPolygon($point, $polygon) {
    $x = $point[0];
    $y = $point[1];
    $inside = false;
    
    for ($i = 0, $j = count($polygon) - 1; $i < count($polygon); $j = $i++) {
        $xi = $polygon[$i][0];
        $yi = $polygon[$i][1];
        $xj = $polygon[$j][0];
        $yj = $polygon[$j][1];

        $intersect = (($yi > $y) != ($yj > $y)) && 
                     ($x < ($xj - $xi) * ($y - $yi) / ($yj - $yi) + $xi);
        if ($intersect) {
            $inside = !$inside;
        }
    }
    
    return $inside;
}


```


Step 3: Send Notification
Once you’ve determined that the fan is within the polygon, you can send a notification. For simplicity, the notification here is represented as an email using the PHP mail() function, but you can use services like Twilio, Firebase Cloud Messaging (FCM), or other notification systems.

```
function sendNotification($email, $message) {
    $to = $email;
    $subject = "Live Event Update";
    $headers = "From: notifications@example.com";
    
    mail($to, $subject, $message, $headers);
    echo "Notification sent to: " . $email;
}


```


Step 4: Putting It All Together
Now, combine the logic to check the location of the fan, and if they are within the polygon boundaries, send them a notification.

```
// Fan's current location (Latitude, Longitude)
$fanLocation = [51.5082, -0.1272]; // Example: Fan's geo-coordinates
$fanEmail = "fan123@example.com"; // Example: Fan's email

// Check if the fan is inside the polygon
if (isPointInPolygon($fanLocation, $polygon)) {
    // Send notification if the fan is within the event area
    sendNotification($fanEmail, "You are within the event area! Stay tuned for live updates.");
} else {
    echo "Fan is outside the event area.";
}


```



Step 5: Handle Multiple Fans
If you have multiple fans and need to check them all, you can loop through a list of fans with their locations and emails:


```
$fans = [
    ["location" => [51.5082, -0.1272], "email" => "fan123@example.com"],
    ["location" => [51.5100, -0.1300], "email" => "fan456@example.com"],
    // More fans...
];

foreach ($fans as $fan) {
    if (isPointInPolygon($fan['location'], $polygon)) {
        sendNotification($fan['email'], "You are within the event area! Stay tuned for live updates.");
    } else {
        echo "Fan " . $fan['email'] . " is outside the event area.\n";
    }
}


```

Step 6: Optional - Store and Track Subscriptions
You can enhance this system by adding a database to store fan subscriptions and notification preferences. Each fan could have a unique tenant ID and API key, as well as subscribe to notifications for specific events.

### TODO:
Extend the application  with a robust notification service, monitoring system, and error handling.
