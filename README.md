# GVM AV Systems (combined)

A single entry point that switches between two dashboards using a top-right
toggle. Both dashboards use the same Supabase project (`jkwakavosclpnbtyyltx`),
so one login works for both: logging in or out in either one applies to both.

- `index.html` — the shell/switcher. Deploy this whole folder as-is.
- `gvm-tracker.html` — GVM PM Tracker (default dashboard on load).
- `adhoc-token.html` — Adhoc / Token System.

## Accounts and roles

Each user has a separate role per app, both stored in `public.profiles`:

| App | Column | Roles |
|---|---|---|
| Adhoc / Token | `role` | `guest`, `admin`, `superadmin` |
| PM Tracker | `pm_role` | `guest` (view only), `user` (set PM dates), `admin` (manage contracts), `super_admin` |

New accounts start as guest in both. Registration and the password-reset screen
live on the Adhoc / Token page; the PM Tracker's "Forgot password?" link sends
people there.

## Data

- `kv_store` key `contracts` — PM Tracker contracts; `presence:<user id>` — who's online.
- `kv_store` keys `adhoc_token_*` — Adhoc / Token data.
- `activity_log` table — PM Tracker activity (visible to the PM super admin).

Row-level security limits writes per key: `contracts` needs PM `user` or above,
`presence:<id>` only its own user, `adhoc_token_*` any logged-in user.

## Deploy

Any static host works (GitHub Pages, Netlify, etc.) — just publish this folder.
`index.html` must stay in the same folder as the other two files since it
references them by relative filename.

## Notes

- Always opens on the PM Tracker; the last-viewed dashboard is not remembered.
- Editing either dashboard: edit `gvm-tracker.html` or `adhoc-token.html` directly.
- Editing the toggle/shell: edit `index.html`.
