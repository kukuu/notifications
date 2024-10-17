```
// In the API Registration Page:
if(isset($_POST['submit'])){
    $email = $_POST['email'];
    
    // Check if user has an admin role
    $adminCheck = $db->prepare("SELECT role FROM users WHERE email = ? AND role = 'ADMIN'");
    $adminCheck->execute([$email]);
    if($adminCheck->rowCount() > 0){
        // Generate unique API key
        $apiKey = bin2hex(random_bytes(32));
        // Save API Key to the DB
        $saveKey = $db->prepare("UPDATE users SET api_key = ? WHERE email = ?");
        $saveKey->execute([$apiKey, $email]);
        
        echo "Your API Key: " . $apiKey;
    } else {
        echo "Error: Admin status not confirmed or email not found.";
    }
}


```

## Key Points:

i. Email Verification: Ensure the email exists and corresponds to an admin.

ii. Admin Role Confirmation: Use role-based access control (RBAC) to confirm the user has admin privileges.


iii. API Key Generation: Generate a secure API key (e.g., using random_bytes for strong encryption).

iv. Security Consideration: Ensure the API key is securely stored in the database and masked or sent securely to the user.

v. This method ensures only authorized admin users can generate API keys through the registration form, with proper validation and security.
