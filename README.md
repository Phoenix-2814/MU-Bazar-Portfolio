# MU Bazar

MU Bazar is a full-stack campus marketplace built for Marwadi University students. It gives students one place to list, find, and discuss appropriate products and hostel essentials.

## What the project does

- Browse listings by category, search text, and price range; sort results and load more listings as needed.
- Create an account with a university email address or use Google sign-in. Email registration includes verification and password reset flows.
- Create and manage listings with photos, categories, item condition, and price. Sellers can edit listings and mark them sold.
- Start private, real-time conversations between a buyer and seller, with unread counts and notifications.
- Report listings and provide administrators with tools to review reports, moderate listings, and manage accounts.
- Save a light or dark appearance preference.

## Project highlights

This project brings together a responsive React interface, a TypeScript API, persistent data models, and real-time messaging. It also includes practical product details such as paginated browsing, image validation and compression, rate limiting, session tracking, and automated checks in GitHub Actions.

## Technology

- **Frontend:** React, Vite, Axios, Socket.IO Client
- **Backend:** Node.js, TypeScript, Express, MongoDB/Mongoose, Socket.IO
- **Optional services:** Google Identity Services, ImageKit for image storage, Brevo or SMTP for email, and Redis for shared rate limits and multi-instance Socket.IO
- **Automation:** GitHub Actions, Vitest, Node test runner, Supertest, and an in-memory MongoDB test database

## Repository layout

```text
backend/     Express API, MongoDB models, authentication, chat, moderation, tests
frontend/    React client, UI components, static assets, frontend tests
.github/     CI workflow
```

## Run locally

Requirements: Node.js 20.19+ and npm. MongoDB is required to run the backend. The frontend can run without external credentials, but sign-in, email, and image hosting features need their respective providers configured.

1. In `backend/`, copy `.env.example` to `.env` and set at least `MONGO_URI` and a unique `JWT_SECRET` (32+ characters). For local email verification, configure SMTP or Brevo credentials.
2. In `frontend/`, copy `.env.example` to `.env` and set `VITE_API_URL=http://localhost:5000`. Set `VITE_GOOGLE_CLIENT_ID` only if configuring Google sign-in.
3. Install and start the API:

   ```sh
   cd backend
   npm ci
   npm run dev
   ```

4. In another terminal, install and start the web app:

   ```sh
   cd frontend
   npm ci
   npm start
   ```

The frontend runs at `http://localhost:3000`; the API runs at `http://localhost:5000`. The backend readiness endpoint is `/healthz`.

## Configuration

The sample files `backend/.env.example` and `frontend/.env.example` list the supported settings. The main backend settings are:

- `MONGO_URI` and `JWT_SECRET` for data and signed sessions
- `CLIENT_ORIGIN` and `PUBLIC_API_URL` for browser/API origins and uploaded image links
- `GOOGLE_CLIENT_ID` for Google sign-in
- `EMAIL_PROVIDER` plus SMTP or Brevo settings for verification and reset messages
- `IMAGEKIT_PRIVATE_KEY` for hosted listing/profile images
- `ADMIN_EMAILS` for the administrator allowlist
- `REDIS_URL` for shared rate limits and real-time events when running multiple API instances

The Vite variables are build-time browser settings. `VITE_API_URL` and `VITE_GOOGLE_CLIENT_ID` are visible to users in the built frontend; never place private credentials in a `VITE_` variable. Keep actual secrets in local `.env` files or the deployment platform's secret manager. `.env` files are excluded from Git.

## Checks

The GitHub Actions workflow audits dependencies, type-checks the API, runs backend tests, and builds the frontend. You can run the relevant commands locally:

```sh
cd backend
npm ci
npx tsc --noEmit
npm test

cd ../frontend
npm ci
npm run build
npm test
```

## Deployment notes

Deploy `backend/` as a Node service and `frontend/` as a Vite static site. Configure the production environment variables from the sample files, use HTTPS, set the exact frontend origin in `CLIENT_ORIGIN`, and ensure the OAuth client permits the deployed frontend origin. For multiple backend instances, configure Redis. Never use sample credentials in production.

## Project status

This repository contains the application source and local development setup. It does not include production credentials or a bundled live database. Integrations such as email delivery, Google sign-in, and hosted image uploads work only after their provider credentials are configured.


