# Poly Haven Public API — agent rules

Express (Node, CommonJS) API behind api.polyhaven.com. Data from Firestore (`firestore.js`, `utils/cachedFirestore.js`). License AGPL-3.0.

## Layout
- `app.js` — server entry, mounts every route.
- `routes/*.js` — one file per endpoint; `routes/v2/` for v2.
- `utils/` — search (`assetSearch.js`, `keywordIndex.js`, `embeddingIndex.js`, `rankFusion.js`), rate limiting, key validation.
- `swagger.yml` — public API docs; **update it whenever an endpoint's request or response shape changes**.
- `*.json` at the root (`taxonomy.json`, `asset_types.json`, …) are served data, not config.

## Commands
- `npm ci` then `npm run dev` (nodemon). Needs Firestore credentials in `.env` — never commit them.
- No test suite. Verify by running the server and calling the endpoint with curl.
- Format with the bundled prettier: `npx prettier --write <file>`.

## Rules
- Pushing to `master` deploys to production via `.github/workflows/main.yml`. Never push there.
- Keep responses backward compatible; third-party apps depend on them.
