# Environment Variables

The API loads environment variables with `dotenv` from `api/.env`.

The file belongs in `api/`, not in the repository root. `dotenv.config()` is called by the server and authentication modules before their values are used.

| Variable | Used for | Required |
| --- | --- | --- |
| `MONGODB_URL` | MongoDB connection string | Yes |
| `JWT_SECRET` | Signing password-login JWTs | Yes for password login |
| `CLIENT_ID` | Google token validation in the API | Yes for Google login |

Example:

```dotenv
MONGODB_URL=mongodb://127.0.0.1:27017/book-me
JWT_SECRET=replace-with-a-long-random-value
CLIENT_ID=your-google-oauth-client-id
```

Do not commit `.env` files or real credentials. The client currently contains a Google OAuth client ID in `client/src/index.tsx`; client IDs are public identifiers, but they should still be managed consistently with the deployment configuration.

Use a different `JWT_SECRET` for every deployed environment. A missing secret can cause token generation or Passport JWT configuration to fail; it should never fall back to a shared example value.

## Configuration notes

- The API port is currently hard-coded to `8013` in `api/src/server.ts`.
- CORS is enabled for all origins by the Express app.
- The API exits when the MongoDB connection fails.
- The API does not currently read a configurable port variable.
- The client does not currently read an API base URL from an environment variable.
