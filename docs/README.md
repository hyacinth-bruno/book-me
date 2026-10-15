# BookMe Documentation

BookMe is a property booking application with a TypeScript/Express API and a React client.

## Contents

- [Getting started](getting-started/setup.md)
- [Environment variables](getting-started/environment.md)
- [Troubleshooting](getting-started/troubleshooting.md)
- [Architecture](architecture/overview.md)
- [Data model](data-model.md)
- [API reference](api/endpoints.md)
- [Authentication](api/authentication.md)
- [API examples](api/examples.md)
- [Frontend routes](frontend/routes.md)
- [Frontend state](frontend/state.md)
- [Contributing](contributing/development.md)
- [Testing](contributing/testing.md)

## Quick reference

| Item | Value |
| --- | --- |
| API package | `api/` |
| Client package | `client/` |
| API local URL | `http://localhost:8013` |
| Client local URL | `http://localhost:3000` |
| Database | MongoDB, configured with `MONGODB_URL` |
| API start command | `cd api && npm start` |
| Client start command | `cd client && npm start` |

## Current limitations

- There is no root `package.json`; install and run each package independently.
- The API port and several client API URLs are hard-coded for local development.
- JWT route protection is configured but commented out in the route files.
- The client reservation thunk uses `/reservations`, while the API route prefix is `/reservation`.

## Repository layout

```text
api/       Express, TypeScript, and MongoDB service
client/    React, Redux Toolkit, and Material UI application
docs/      Project documentation
```
