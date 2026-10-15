# Frontend State and Data Flow

The client uses Redux Toolkit with React Redux. The store is configured in `client/src/redux/store.ts`.

## State areas

| Slice | Responsibility |
| --- | --- |
| `placesSlice` | Property data used by landing, listing, and detail views |
| `reservationSlice` | Reservation data and reservation actions |
| `userSlice` | Current user and user-list/profile updates |
| `filterSlice` | Property filtering state |

## Async work

Thunks under `client/src/redux/thunk` make HTTP requests and dispatch slice actions. Places are fetched from `App.tsx` on mount through `fetchPlacesData`. User profile edits use Axios requests to `/users/:userId`.

## Adding a request

1. Define or confirm the TypeScript type in `client/src/types/types.ts`.
2. Add the request to the relevant thunk module.
3. Dispatch a slice action for the success state.
4. Decide how loading and failure states will be represented before wiring the component.
5. Keep the API path aligned with the route registered in `api/src/app.ts`.

## Known behavior

Many existing thunks log responses but do not expose a shared loading or error state. New work should avoid silently swallowing request failures and should keep components usable while data is loading.

The reservation thunk currently uses `/reservations`, which does not match the API's `/reservation` prefix. See [Troubleshooting](../getting-started/troubleshooting.md).
