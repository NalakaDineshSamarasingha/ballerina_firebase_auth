# Package Overview

This Ballerina package provides functionality for generating Firebase authentication tokens using a service account JSON file. It implements JWT-based authentication and token generation, enabling secure communication with Firebase services. The package is designed to simplify integrating Firebase Authentication in Ballerina applications.

---

## Key Features

- **Service Account Management**: Reads and processes the Firebase service account credentials from a JSON file.
- **JWT Token Generation**: Creates a signed JWT token required for accessing Firebase services.
- **OAuth2 Token Retrieval**: Uses the generated JWT to obtain an access token from Firebase's OAuth2 server.
- **Token Expiry Handling**: Automatically detects and regenerates tokens if expired.

---

## Usage

Here's how you can use this package to authenticate and obtain an access token for Firebase:

### 1. Import the Package

```ballerina
import lakpahana.firebase_auth;
```

### 2. Define the `AuthConfig`

Configure the authentication settings, including the scope, expiration time, and the path to the Firebase service account JSON file.

```ballerina
AuthConfig authConfig = {
    jwtConfig: {scope: "https://www.googleapis.com/auth/firebase.messaging", expTime: 3600},
    serviceAccountPath: "service.json"
};
```

### 3. Create a `Client` Instance

Create an instance of the `Client` class using the configuration defined above.

```ballerina
final Client firebase = check new(authConfig);
```

### 4. Generate an Access Token

Call the `generateToken` method to retrieve an OAuth2 access token.

```ballerina
string|error token = firebase.generateToken();
io:println("Access Token: ", token);
``


## Implementation Details

1. **Service Account Parsing**: Reads the JSON credentials file and extracts the required fields.
2. **JWT Creation**: Constructs and signs a JWT using the service account's private key.
3. **OAuth2 Token Exchange**: Exchanges the JWT for an OAuth2 access token.
4. **Thread-Safe Operations**: Ensures thread safety during token creation and validation using `lock`.
