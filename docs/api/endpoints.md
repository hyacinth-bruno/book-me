# API Endpoints

Base URL: `http://localhost:8013`

The API returns JSON. Request and response shapes are defined by the controllers and Mongoose models; validate them against source before building a separate client.

## Conventions

- JSON request bodies require `Content-Type: application/json`.
- Path identifiers are MongoDB document IDs unless the endpoint says otherwise.
- The API currently has no documented health endpoint; use a read endpoint such as `GET /places` for a basic connectivity check.
- Error status codes are not uniform across controllers. Clients should handle non-2xx responses and unexpected response bodies defensively.

## Users

| Method | Path | Purpose |
| --- | --- | --- |
| `POST` | `/users` | Register a user |
| `POST` | `/users/login` | Log in with email and password; returns user data and a JWT on success |
| `POST` | `/users/login-google` | Authenticate with a Google ID token |
| `GET` | `/users` | List all users |
| `GET` | `/users/:userId` | Get one user |
| `PUT` | `/users/:userId` | Update a user |
| `DELETE` | `/users/:userId` | Delete a user |

## Places

| Method | Path | Purpose |
| --- | --- | --- |
| `GET` | `/places` | List all places |
| `POST` | `/places` | Create a place |
| `PUT` | `/places/:placeId` | Update a place |
| `GET` | `/places/placeId` | Get a place by ID |

> The final place route is registered literally as `/places/placeId`; it does not currently use a `:placeId` parameter.

## Reservations

| Method | Path | Purpose |
| --- | --- | --- |
| `POST` | `/reservation/:userId` | Create a reservation for a user |
| `GET` | `/reservation/:userId` | List reservations for a user |
| `DELETE` | `/reservation/:id` | Delete a reservation |

## Wishlists and reviews

| Method | Path | Purpose |
| --- | --- | --- |
| `POST` | `/wishlist` | Create a wishlist entry |
| `GET` | `/wishlist/:userId` | Get a user's wishlist |
| `DELETE` | `/wishlist` | Delete a wishlist entry |
| `POST` | `/review` | Create a review |
| `GET` | `/review` | List reviews |
| `GET` | `/review/:placeId` | List reviews for one place |

## Authentication status

Passport initialization is enabled, but the JWT middleware is commented out in the current route files. Do not assume these endpoints enforce ownership or administrator permissions yet.

See [Authentication](authentication.md) for token and Google sign-in details, and [API examples](examples.md) for request examples.
