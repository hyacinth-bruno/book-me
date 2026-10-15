# Testing Guide

## Client tests

The client uses Jest through Create React App and Testing Library. Tests and setup files live under `client/src`, including `App.test.tsx` and `setupTests.ts`.

Run the suite from `client/`:

```bash
npm test -- --watchAll=false
```

For a focused test during development, use Jest's name or path filters supported by the Create React App runner.

## Build validation

A production build catches TypeScript and bundling errors that may not appear during an isolated component test:

```bash
cd client
npm run build
```

## API validation

The API package does not currently define a test script. Validate API changes by starting MongoDB and the API, then exercising the affected endpoint with curl or the client. Check success, invalid input, missing records, and database failure behavior.

## Integration checklist

- Verify the route prefix and HTTP method match on both sides.
- Verify path parameter names and values.
- Verify request `Content-Type` and body shape.
- Verify empty results and non-2xx responses.
- Verify authentication assumptions explicitly; commented Passport middleware does not enforce access control.
