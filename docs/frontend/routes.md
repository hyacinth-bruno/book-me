# Frontend Routes

The React client uses React Router with `BrowserRouter`.

| Path | Page |
| --- | --- |
| `/` | Landing page |
| `/properties` | Property listing and search |
| `/properties/:id` | Property details |
| `/login` | Password login |
| `/signup` | User registration |
| `/profile` | User profile |
| `/favorites` | Saved properties |
| `/dashboard` | Dashboard |

The navigation bar and footer are rendered around every route.

Route parameters are strings supplied by React Router. `PropertyDetails` receives the property identifier from `/properties/:id`; API identifiers are MongoDB IDs and should be passed through without client-side coercion.

## API integration

The client currently calls the API at `http://localhost:8013`. Places are loaded on application mount through `fetchPlacesData`. User profile updates use `/users/:userId`.

The landing and properties experiences depend on place data being available at startup. The Redux store is initialized in `client/src/redux/store.ts`; asynchronous requests are implemented in `client/src/redux/thunk`.

Google sign-in is provided by `GoogleOAuthProvider` in `client/src/index.tsx`. The current client ID is embedded in source rather than loaded from a `REACT_APP_*` variable.

## Known integration issue

`client/src/redux/thunk/reservationsThunk.ts` currently uses `http://localhost:8013/reservations`, while the API exposes `/reservation` (singular). Reservation calls will need one side updated before that workflow can operate end to end.

## Navigation checklist

When adding a page:

1. Add the route in `client/src/App.tsx`.
2. Add a navigation entry if users should reach it from the shared navigation bar.
3. Confirm the page handles loading, empty, and API error states.
4. Add or update a client test when the route has user-visible behavior.
