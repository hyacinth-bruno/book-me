# Getting Started

## Prerequisites

- Node.js with npm
- A running MongoDB instance
- Google OAuth client credentials if Google sign-in is used
- A terminal for each long-running process

MongoDB may run locally or remotely. The connection string must be reachable from the API process; the API does not start its HTTP listener until the connection succeeds.

## Install dependencies

Install each package separately because the repository does not define a root `package.json`:

```bash
cd api
npm install

cd ../client
npm install

cd ..
```

## Configure the API

Create `api/.env` with the values described in [Environment variables](environment.md). The API cannot start until it can connect to MongoDB.

## Run the services

Start the API in one terminal:

```bash
cd api
npm start
```

The API listens on `http://localhost:8013` after the MongoDB connection succeeds.

Start the client in a second terminal:

```bash
cd client
npm start
```

Create React App normally serves the client at `http://localhost:3000`.

## Recommended startup order

1. Start MongoDB.
2. Start the API and wait for `The server is running on port 8013`.
3. Start the client.
4. Open the client and exercise the landing page before testing authenticated workflows.

The API uses `nodemon` and watches TypeScript files under `api/src`. The client uses Create React App's development server and reloads when source files change.

## Smoke check

Open `http://localhost:3000`. The client loads places from `GET http://localhost:8013/places`. If the page has no properties, verify that the API is running and that the database contains place records.

Check the API directly with:

```bash
curl http://localhost:8013/places
```

An API connection error usually means the server did not start, while an empty JSON response usually means the database has no matching records.
