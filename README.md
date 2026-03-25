# Reclaim Frontend

Reclaim is the main user-facing experience for a lost-and-found platform. This Next.js app lets users report lost or found items, search with location-aware filters, submit claims, manage recovery workflows, chat in real time, and access admin tooling when authorized.

## What The App Does

- Browse all reported lost and found items from a unified home feed
- Filter items by type, category, keyword, and location
- Post new lost or found reports with images and map-based location input
- Sign up with email/password or Google OAuth
- View item details and submit claims or retrieval requests
- Manage personal items and claims from a dashboard
- Chat with matched users in real time
- Use AI-assisted search to refine discovery
- Access admin controls for users, items, and platform stats

## Frontend Stack

- Next.js 15 with the App Router
- React 18 and TypeScript
- Tailwind CSS 4
- Axios for API requests
- Google OAuth via `@react-oauth/google`
- Socket.IO client for chat
- Leaflet and React Leaflet for map/location flows
- `react-hot-toast` for notifications

## Main Routes

### Public

- `/` home feed with search and filters
- `/items/[id]` item detail page
- `/auth/login` login
- `/auth/register` registration and Google sign-in
- `/profile/[id]` public profile view

### Authenticated

- `/post` create a new item
- `/dashboard` manage posted items, claims, and retrievals
- `/chat` real-time chat interface
- `/settings` account settings
- `/items/[id]/claim` submit a claim/request

### Admin

- `/admin` admin dashboard for stats, users, and items

## Key UI Areas

### Home Feed

- Debounced search against the backend
- Desktop sidebar and mobile modal filters
- Search autocomplete
- Lost/found type switching
- Location filtering with country, state, city, and bounds support

### Item Lifecycle

1. A user creates a lost or found post.
2. Other users discover it through search or filters.
3. A claimant submits a claim or retrieval request.
4. The owner reviews claims and approves or rejects them.
5. Approved users can open chat and coordinate recovery.
6. The owner can mark the flow as resolved/retrieved.

### Dashboard

- View items created by the current user
- See pending claim counts
- Manage incoming claims
- Edit or delete pending outgoing claims
- Track retrieval activity separately from claims

### Chat

- Connects to the backend Socket.IO server
- Joins item-specific rooms
- Sends and receives messages in real time

## Project Structure

```text
reclaim-frontend/
├── app/                 # App Router pages
├── components/          # Reusable UI and domain components
├── context/             # Auth state
├── lib/                 # API client
├── public/              # Static assets
└── src/                 # Legacy/generated app files
```

Notes:

- The active app code is primarily in `app/`, `components/`, `context/`, and `lib/`.
- There is also a `src/app` folder in the repo. The current product-facing app uses the top-level `app/` routes.

## Local Setup

1. Install dependencies.

```bash
npm install
```

2. Create the local env file.

```bash
cp .env.example .env.local
```

3. Start the frontend.

```bash
npm run dev
```

Open `http://localhost:3000`.

## Environment Variables

Create `reclaim-frontend/.env.local`:

```env
NEXT_PUBLIC_API_URL=http://localhost:5001/api
NEXT_PUBLIC_GOOGLE_CLIENT_ID=
```

### Variable Notes

- `NEXT_PUBLIC_API_URL`: Base URL for all REST calls. The app defaults to `http://localhost:5001/api` if unset.
- `NEXT_PUBLIC_GOOGLE_CLIENT_ID`: Required for the Google OAuth provider used in login and registration flows.

## Scripts

- `npm run dev` starts the Next.js development server
- `npm run build` builds the production bundle
- `npm run start` runs the production server
- `npm run lint` runs ESLint

## Backend Expectations

This frontend depends on the backend for:

- auth and session bootstrapping
- item CRUD and search
- claims workflow
- admin data
- image upload endpoints
- AI search
- chat history and Socket.IO events

The backend should be running on `http://localhost:5001` in local development unless `NEXT_PUBLIC_API_URL` points elsewhere.

## Integration Notes

- The shared API client attaches the JWT from `localStorage` on each request.
- Socket chat derives its host from `NEXT_PUBLIC_API_URL`.
- Google OAuth should use the same client ID configured in the backend.
- Leaflet CSS is loaded globally in the app layout.

## Related Docs

- Backend setup: [`../reclaim-backend/README.md`](../reclaim-backend/README.md)
- Repo overview: [`../README.md`](../README.md)
