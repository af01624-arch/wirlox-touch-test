# WIRLOX Touch Test 4.3 (separate Worker)

This package is **not** a replacement for the live WIRLOX repo.

Create a separate GitHub repository, e.g. `wirlox-touch`, and upload `wrangler.json` and the entire `public/` folder to that repository. The main `af01624-arch/wirlox` repository MUST stay untouched.

Connect the separate repo to a new Cloudflare Worker named `wirlox-touch` (the Worker name must equal the `name` in `wrangler.json`). Branch: `main`. Build command: leave blank (no build). Deploy command: `npx wrangler deploy`. Root directory: `/`.

For phone testing, connect the new Worker to `touch.wirlox.com`. Because `*.wirlox.com/*` already points to the production Worker, **do not assume adding only a Custom Domain overrides that wildcard route**. Explicitly route `touch.wirlox.com/*` to `wirlox-touch` (and ensure the `touch` DNS hostname exists, or use the Cloudflare Custom Domain feature to create it). This is a follow-up step after the new Worker deploys; verify carefully to avoid changing production routes.

## What changed
- Only the touch test: pointer drag, directional axis-lock, no inertia/acceleration, no multi-step skips, no accidental two-axis changes.
- Drag left/right over the wheel to spin the horizontal wheel. Drag up/down in its central alphabet area to change paired letters.
- First move at 26 px, subsequent moves at 34 px of additional travel; minimum 65ms between moves; max one move per pointer event.
- Arrow keys/touch arrow buttons work as before.
- User-provided `FL_Click.wav` is used via Web Audio at 28% gain on each real wheel move, including button and keyboard input.
- Touch test starts on the same seven puzzle layouts. No changes to target words, mathematical minimums, or scoring logic. Local storage on touch.wirlox.com is separate from the main site's.

Stop and test after every stage. Do not update the production Worker, routes or `wrangler.json` of the main repo.
