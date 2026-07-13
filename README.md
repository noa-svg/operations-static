# operations-static

Static launcher hub for LVP operations tooling, published via GitHub Pages at
`operations.legacyvpartners.com`. Same shape as `atrium-static`/`cayman-form-static`:
plain HTML/CSS/JS, no build step, no server.

Google Sign-In (domain-restricted to legacyvpartners.com) gates the tile grid.
It is a UX gate only — the real security boundary for each linked tool is that
tool's own Google auth (App Center's `access: DOMAIN`, or the Google Sheet's own
sharing permissions).

Never hand-edit `GOOGLE_CLIENT_ID` in index.html without checking with Noa first
(it's an OAuth Client ID scoped to this exact origin).
