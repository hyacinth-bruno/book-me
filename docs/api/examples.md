# API Examples

These examples use the local API at `http://localhost:8013`.

## List places

```bash
curl http://localhost:8013/places
```

## Register a user

The controller accepts fields including `name`, `email`, `password`, `avatar`, `phoneNumber`, `isAdmin`, and `isBanned`. Public registration should normally allow only safe user-owned fields.

```bash
curl -X POST http://localhost:8013/users \
  -H 'Content-Type: application/json' \
  -d '{"name":"Ada Lovelace","email":"ada@example.com","password":"change-me"}'
```

## Log in

```bash
curl -X POST http://localhost:8013/users/login \
  -H 'Content-Type: application/json' \
  -d '{"email":"ada@example.com","password":"change-me"}'
```

A successful password login returns a JSON object containing `userData` and `token`.

## Create a reservation

The API route is singular: `/reservation/:userId`.

```bash
curl -X POST http://localhost:8013/reservation/USER_ID \
  -H 'Content-Type: application/json' \
  -d '{"placeId":"PLACE_ID"}'
```

The complete reservation body is defined by `api/src/models/Reservation.ts` and its controller; keep the example identifiers as placeholders.

## Send a bearer token

JWT enforcement is not currently enabled on the route files, but this is the expected header format for a protected endpoint:

```bash
curl http://localhost:8013/users/USER_ID \
  -H 'Authorization: Bearer JWT_TOKEN'
```
