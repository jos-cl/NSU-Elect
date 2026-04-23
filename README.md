# NSUElect

NSUElect is a Firebase-powered election platform for the Nortec Student Union and class representative elections. The default deployment flow is configured for Firebase Spark (no-cost) tier using Hosting and Firestore resources.

## Stack

- Firebase Hosting for the frontend
- Firestore for elections, candidates, votes, nominations, and analytics
- Local emulators for Hosting, Firestore, Functions, and Auth
- Optional Blaze-only services: Cloud Functions and Storage (not included in default deploy)

## Project Structure

- `functions/` backend HTTP functions and scheduled jobs
- `public/` static frontend pages, styles, and client-side JavaScript
- `firestore.rules` access rules
- `firestore.indexes.json` query indexes
- `storage.rules` storage access control

## Setup

1. Install root dependencies.
   - `npm install`
2. Install functions dependencies.
   - `npm --prefix functions install`
3. Set your Firebase project alias.
   - Update `.firebaserc` with your real project ID, or run `firebase use --add`
4. Add your Firebase web config in `public/js/firebase-init.js`.
5. Seed Firestore collections such as `students`, `academic_terms`, and `electoral_commission`.

## Local Development

Start the full emulator suite:

```bash
npm run emulators
```

Default local URLs:

- Hosting: `http://127.0.0.1:5000`
- Functions: `http://127.0.0.1:5001`
- Firestore: `127.0.0.1:8080`
- Auth: `127.0.0.1:9099`
- Emulator UI: `http://127.0.0.1:4000`

## Deploy

Deploy Spark-safe targets (default):

```bash
npm run deploy
```

Deploy hosting only:

```bash
npm run deploy:app
```

Deploy rules and indexes only:

```bash
npm run deploy:rules
```

Deploy all services (requires Blaze plan and Storage setup):

```bash
npm run deploy:blaze
```

## Notes

- Cloud Functions and Storage deployments are excluded from default scripts so you can stay on Spark tier.
- If you later move to Blaze, run `npm run deploy:blaze` after enabling required APIs and Storage in Firebase Console.
- Election scheduling enforces the constitutional rule that elections must end at least five weeks before the end of term three.
- Frontend pages are emulator-aware and can target local Functions, Firestore, and Auth automatically when opened from local hosting.
