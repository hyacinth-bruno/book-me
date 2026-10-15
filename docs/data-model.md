# Data Model

BookMe persists its domain objects in MongoDB through Mongoose models in `api/src/models`.

## Core entities

| Entity | Model | Main relationships and fields |
| --- | --- | --- |
| User | `User` | Identity, email, hashed password, name, avatar, phone number, admin and banned flags |
| Place | `Place` | Property information used by listings and property details |
| Reservation | `Reservation` | Booking information associated with a user and a place |
| Review | `Review` | User feedback associated with a place |
| Wish list | `WishList` | A saved place associated with a user |

## Relationship direction

- A user can own reservations, reviews, and wish-list entries.
- A place can have reservations, reviews, and wish-list entries.
- The API commonly receives the relationship identifier in the URL, such as `/reservation/:userId` or `/review/:placeId`.
- The exact field names and required values remain defined by the TypeScript model files; update this page when a schema changes.

## Persistence notes

Services are the preferred location for database access. Controllers should coordinate request and response handling rather than duplicating Mongoose queries. New models should be accompanied by a route or service test where practical, plus endpoint documentation if the model becomes externally visible.

## Data quality risks

- Passwords are hashed during normal password registration with bcrypt; existing records should not be populated with plaintext passwords.
- Several update endpoints accept request body fields directly. Validate and whitelist fields before exposing these endpoints to untrusted clients.
- Authentication middleware is currently commented out, so identifiers in request paths are not reliably tied to the authenticated user.
