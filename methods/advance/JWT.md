A **JWT (JSON Web Token)** is an open standard (RFC 7519) used for securely transmitting information between parties as a JSON object. It is widely used in web applications for authentication and information exchange.

### Structure of a JWT
A JWT consists of three parts, separated by dots (`.`):
1. **Header**: Contains metadata about the token, such as the type of token (`JWT`) and the signing algorithm (e.g., `HS256`).
2. **Payload**: Contains the claims, which are statements about an entity (like user data) and additional data.
3. **Signature**: Verifies that the sender of the JWT is legitimate and ensures the token hasn't been tampered with.

A JWT looks like this:
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

### How JWT Works
1. **Authentication**: After a user logs in, the server generates a JWT containing claims (like user ID) and signs it using a secret or private key.
2. **Client Storage**: The token is sent to the client, which typically stores it in local storage, session storage, or cookies.
3. **Authorization**: For subsequent requests, the client sends the token in the `Authorization` header (e.g., `Bearer <token>`). The server verifies the token to allow access to protected resources.

### Benefits of JWT
1. **Compact**: It's small and can be easily transmitted via URL, HTTP headers, or cookies.
2. **Self-contained**: All the information needed for verification is included in the token, eliminating the need for server-side storage.
3. **Stateless**: Ideal for distributed systems since no session is stored on the server.

### Common Use Cases
1. **Authentication**: Ensures the user is who they claim to be.
2. **Information Exchange**: Securely shares information between different parties.

### Potential Drawbacks
1. **Token Revocation**: Since tokens are stateless, revoking a token can be challenging without implementing additional mechanisms like blacklists.
2. **Size**: JWTs can grow large if the payload contains excessive data, impacting performance when sent over networks.

### Example Claim in Payload
```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true,
  "iat": 1516239022
}
```
- `sub`: Subject (user ID)
- `name`: User's name
- `admin`: Whether the user is an admin
- `iat`: Issued at (timestamp)

