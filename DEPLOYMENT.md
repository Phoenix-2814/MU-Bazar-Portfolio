# Deployment

Deploy the `backend/` directory as a Node.js service and `frontend/` as a Vite static site. Keep credentials in your hosting provider's secret manager; do not commit `.env` files or put private values in frontend `VITE_` variables.

## Backend

- Build: `npm ci && npm run build`
- Start: `npm start`
- Health/readiness endpoint: `/healthz`
- Configure `NODE_ENV=production`, `MONGO_URI`, `JWT_SECRET`, `CLIENT_ORIGIN`, and `PUBLIC_API_URL`.
- Configure Google OAuth, email, ImageKit, and the administrator allowlist only when those features are needed. See `.env.example` for setting names.
- Set `TRUST_PROXY_HOPS` to the number of trusted proxies used by the host. Add `REDIS_URL` when using multiple API instances.

## Frontend

- Build from the `frontend/` directory with `npm ci && npm run build`.
- Set `VITE_API_URL` to the public API origin and optionally `VITE_GOOGLE_CLIENT_ID` before building.
- Configure the frontend host's security headers and Content Security Policy for the deployed API, Socket.IO, Google Identity Services, and image host origins.

Use HTTPS for both services, restrict CORS to the deployed frontend origin, and configure database access and backups before serving real users. Review the current hosting provider's documentation for platform-specific settings.
