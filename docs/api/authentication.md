# Authentication

BookMe contains two authentication paths: password login with JWTs and Google ID-token login with Passport.

## Password flow

1. Register with `POST /users`.
2. Log in with `POST /users/login` and an email/password body.
3. On success, the API returns `userData` and a JWT.
4. The token is signed with `JWT_SECRET` and expires after one hour.
5. A protected request would conventionally send `Authorization: Bearer <token>`.

The JWT strategy extracts the token from the `Authorization` header and looks up the user by the email in the token payload.

## Google flow

1. The client obtains a Google ID token through the Google OAuth provider.
2. The client sends that token to `POST /users/login-google`.
3. Passport validates the token with `CLIENT_ID`.
4. The API finds or creates a user from the Google name and email.
5. The current Google controller returns `userData` but does not issue the same application JWT as password login.

## Current security status

Passport is initialized in the application, but JWT authentication calls are commented out in the route files. As a result, current routes should be treated as unauthenticated. Before enabling production access:

- Add route-level authentication where ownership or administration is required.
- Enforce that path IDs belong to the authenticated user.
- Validate and whitelist update fields.
- Return deliberate status codes for invalid credentials, missing users, and forbidden operations.
- Avoid logging tokens, credentials, or full request objects.
