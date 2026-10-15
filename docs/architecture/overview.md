# Architecture Overview

## Services

BookMe is split into two independently started applications:

- **API:** Express routes call controllers, which use service modules and Mongoose models.
- **Client:** React Router renders pages, while Redux Toolkit stores places, reservations, and user state.

The packages have separate dependency manifests and lifecycle commands. A deployment must build or run them independently unless a higher-level orchestration layer is added.

```text
React client (:3000)
        |
        | HTTP / JSON
        v
Express API (:8013)
        |
        v
MongoDB
```

## API request flow

1. `api/src/server.ts` loads dotenv and connects to MongoDB.
2. Once connected, it starts the Express app.
3. `api/src/app.ts` enables JSON parsing, CORS, Passport initialization, and route prefixes.
4. Route handlers delegate to controllers.
5. Controllers use service modules and Mongoose models to read or write data.

## Domain areas

The API currently has route groups for users, places, reservations, wishlists, and reviews. Corresponding models live in `api/src/models` and business access modules live in `api/src/services`.

The main API layers are:

| Layer | Location | Responsibility |
| --- | --- | --- |
| Bootstrap | `api/src/server.ts` | Load configuration, connect MongoDB, start HTTP listener |
| App wiring | `api/src/app.ts` | Middleware, Passport initialization, route mounting |
| Routes | `api/src/routes` | HTTP verbs, path parameters, controller selection |
| Controllers | `api/src/controllers` | Parse requests and produce responses |
| Services | `api/src/services` | Reusable database operations and domain access |
| Models | `api/src/models` | Mongoose schemas and document types |

## Authentication

Password login creates a JWT that expires after one hour. Passport is configured with JWT and Google strategies, but the route-level JWT authentication calls are currently commented out. Treat the mutating endpoints as unauthenticated until those middleware calls are enabled and tested.

## Client data flow

`client/src/App.tsx` fetches places when the application mounts. Redux thunks use `fetch` or Axios to call the API and dispatch slice actions. API URLs are currently hard-coded to `http://localhost:8013` in several client modules.

The client entry point wraps the application with `GoogleOAuthProvider`, Redux `Provider`, and `BrowserRouter`. `NavBar` and `Footer` surround the route content, so changes to those components affect every page.

## Failure boundaries

- MongoDB connection failure prevents the API from listening.
- API request failures are handled inconsistently; several controllers log errors without returning a consistent error response.
- Client thunks generally assume a successful JSON response and do not share a centralized API error handler.
