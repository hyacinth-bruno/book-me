# Development Guide

## Project conventions

- Keep API code under `api/src` and client code under `client/src`.
- Keep route registration in `api/src/routes`, request handling in controllers, and database access in services/models.
- Keep reusable client state in Redux slices and asynchronous requests in thunks.
- Use TypeScript for new API and client code.
- Prefer the existing controller/service and Redux slice/thunk boundaries over putting database or request logic directly in UI components.
- Keep route paths and API base URLs synchronized between `api/src/routes` and client thunks.

## Useful commands

API:

```bash
cd api
npm start
```

Client:

```bash
cd client
npm start
npm test
npm run build
```

The client test command is interactive by default. Use the test runner's non-watch option in automation when needed, for example `npm test -- --watchAll=false`.

## Before opening a change

1. Run the client build for client changes.
2. Run the client tests when behavior changes.
3. Start MongoDB and the API when validating API or integration changes.
4. Check that endpoint names, request bodies, and identifiers match on both sides.
5. Never commit credentials, local `.env` files, or generated build output.

## Change checklist

For a new API endpoint, update the route, controller, service/model behavior, endpoint documentation, and a client thunk or test when applicable. For a new client page, update routing, navigation, loading/error states, and the frontend route documentation.

## Documentation standard

Document externally visible behavior, setup requirements, and known limitations. Prefer short tables and runnable command examples. Update the relevant page when an endpoint, environment variable, route, or startup command changes.
