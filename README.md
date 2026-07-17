# operations-static

The real production host for Atrium (nav-portal's AtriumX Preact app),
published via GitHub Pages at `operate.legacyvpartners.com`. Started life as
a launcher hub, a Google-Sign-In-gated tile grid linking OUT to other tools.
The Phase 3 cutover (2026-07-13) replaced that. `index.html` IS the app now,
not a link to it. Never hand-edit anything here. Everything is build output
from `legacy-tools-mono/apps/nav-portal/scripts/deploy-atrium.mjs` (canonical
source moved there 2026-07-16; see the disarmed
`~/Desktop/legacy-tools/nav-portal/`'s DISARMED.md).

`index.html` and `atrium.html` are deliberately byte-identical duplicates,
not accidental drift. `atrium.html` exists so `/atrium.html` keeps working
as an explicit direct link (bookmarks, docs) even though `/` (index.html) is
the real entry point. `deploy-atrium.mjs` asserts they match on every deploy
and fails closed if they diverge (see `build-atrium.mjs`'s own comment at the
`atrium.html`/`index.html` emit calls). Don't "clean up" by collapsing them
into one file. That breaks the direct-link contract.

`assets/` holds content-hashed `AtriumX.<hash>.js`/`.css`, same file, same
shape as `atrium-static`'s (that repo is the asset-only rollback host; this
one also carries the HTML shell). `deploy-atrium.mjs` prunes old hash pairs
on every deploy (keeps 6 + the live pair).

Google Sign-In on the client is a UX nicety, not the security boundary. The
real boundary is `RpcGate.ts`'s server-side idToken verification (domain
allowlist), since anyone can read this repo's static files regardless of
sign-in state.
