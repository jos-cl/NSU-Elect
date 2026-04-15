# NSUElect

NSUElect is a Firebase-powered election platform for the Nortec Student Union and class representative elections. This scaffold uses Firebase Hosting, Cloud Functions, Firestore, Authentication, Storage, and the Local Emulator Suite.

## Stack

- Firebase Hosting for the frontend
- Firebase Cloud Functions for the HTTP API and scheduled jobs
- Firestore for elections, candidates, votes, nominations, and analytics
- Firebase Authentication with custom tokens for student login
- Local emulators for Hosting, Firestore, Functions, and Auth

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

Deploy everything:

```bash
npm run deploy
```

Deploy app and backend only:

```bash
npm run deploy:app
```

Deploy rules and indexes only:

```bash
npm run deploy:rules
```

## Notes

- The student login flow uses a Cloud Function that issues Firebase custom tokens after the student number is verified.
- Voting is submitted through a Cloud Function and written transactionally to prevent double voting.
- Election scheduling enforces the constitutional rule that elections must end at least five weeks before the end of term three.
- Frontend pages are emulator-aware and can target local Functions, Firestore, and Auth automatically when opened from local hosting.
