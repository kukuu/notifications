
# Task:

Compute geo-coordinates of an irregular polygon to locate when fans are within the boundaries and send notification alerts they have subscribed to on live event updates. 

## Solution Design:

This is  a JS solution to compute whether fans are within the boundaries of an irregular polygon and send notification alerts if they have subscribed to live event updates.

This solution helps to determine if a fan is within an irregular polygon using the Ray-Casting algorithm and sends them notifications based on their location.

It can be extended by integrating third-party services for notifications, such as Firebase, Twilio, or email services like SendGrid. For a larger system, you can introduce a database to store fan subscriptions and preferences for live event updates.

### Steps

Follow the following steps for this implementation:

i. Define the polygon boundaries (stadium/event area).

ii. Use the Ray-Casting algorithm to determine if a fan's location is inside the polygon.

iii. Send notifications (for simplicity, we'll just log a message to the console).

#### Step 1: Define Polygon Boundaries

The event area is defined by an array of geo-coordinates (latitude, longitude) representing the polygon.

```
// Define polygon (stadium boundaries) as an array of [latitude, longitude] pairs
const polygon = [
  [51.5074, -0.1278], // Example coordinates
  [51.5080, -0.1285],
  [51.5090, -0.1270],
  [51.5085, -0.1260],
  [51.5078, -0.1268]
];

```

#### Step 2: Ray-Casting Algorithm

To check if a fan is within the polygon, use the Ray-Casting algorithm. This function checks if a given point (fan's coordinates) is inside the polygon.

```
function isPointInPolygon(point, polygon) {
  let x = point[0], y = point[1];

  let inside = false;
  for (let i = 0, j = polygon.length - 1; i < polygon.length; j = i++) {
    let xi = polygon[i][0], yi = polygon[i][1];
    let xj = polygon[j][0], yj = polygon[j][1];

    let intersect = ((yi > y) !== (yj > y)) &&
      (x < (xj - xi) * (y - yi) / (yj - yi) + xi);
    if (intersect) inside = !inside;
  }

  return inside;
}

```

#### Step 3: Send Notifications

When a fan's location is detected inside the polygon, send them a notification. For simplicity, we'll just log to the console, but in a real-world app, you'd integrate a service like Twilio for SMS or Firebase for mobile notifications.

``` 
function sendNotification(fanId, message) {
  console.log(`Notification sent to Fan ${fanId}: ${message}`);
}

```

#### Step 4: Full Implementation

This function checks a fan's location and sends them a notification if they are within the polygon.

```
// Fan's current location
const fanLocation = [51.5082, -0.1272]; // Example: Fan's current geo-coordinates
const fanId = 123; // Example: Fan's unique ID

// Check if the fan is within the polygon (stadium/event area)
if (isPointInPolygon(fanLocation, polygon)) {
  sendNotification(fanId, "You're within the event area! Stay tuned for live updates.");
} else {
  console.log("Fan is outside the event area.");
}

```

#### Step 5: Integrating with a Real Notification System (Optional)


To actually send a notification to fans' devices, you can integrate a real notification service like Firebase Cloud Messaging (for mobile) or Twilio (for SMS).

For example, using Twilio:

```
const accountSid = 'your_account_sid';
const authToken = 'your_auth_token';
const client = require('twilio')(accountSid, authToken);

function sendNotification(fanPhoneNumber, message) {
  client.messages
    .create({
      body: message,
      from: 'your_twilio_number',
      to: fanPhoneNumber
    })
    .then(message => console.log(`Message sent: ${message.sid}`))
    .catch(error => console.error(error));
}

```
