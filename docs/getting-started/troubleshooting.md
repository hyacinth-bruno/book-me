# Troubleshooting

## API does not start

Check the following in order:

1. Confirm `api/.env` exists and contains a valid `MONGODB_URL`.
2. Confirm MongoDB is running and reachable.
3. Run `npm start` from `api/`, not the repository root.
4. Look for `MongoDB connecting error` in the terminal output.
5. Check whether port `8013` is already in use.

The server calls `app.listen` only after `mongoose.connect` succeeds, so a database failure looks like an unavailable API.

## Client cannot load places

- Open `http://localhost:8013/places` directly.
- Confirm the client is using the same API port documented in [Environment variables](environment.md).
- Inspect the browser Network panel for CORS, connection, or JSON parsing errors.
- Confirm the database contains place documents.

## Login problems

For password login, verify the email exists, the password matches the bcrypt hash, and `JWT_SECRET` is set. For Google login, verify `CLIENT_ID` matches the token's audience and that the client is using the expected Google OAuth configuration.

The API currently returns inconsistent error bodies and some controllers only log caught errors. Inspect both the HTTP status and response body rather than relying on one fixed error shape.

## Reservations do not work

The API exposes `/reservation` but the current client thunk calls `/reservations`. This route mismatch must be corrected before client reservation requests can reach the API. Also verify that the request includes the user identifier expected by the API route.

## Client build or test failures

Run commands from `client/` and reinstall dependencies if `node_modules` is missing:

```bash
npm install
npm run build
npm test -- --watchAll=false
```
